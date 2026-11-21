# ![google storage event based source](_images/kamelets/google-storage-event-based-source.svg) Google Storage Event-based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives the change notifications of a Google Cloud Storage bucket from a Pub/Sub subscription, one message per change, and can download each new file.

Use it to react as soon as a file is uploaded to, changed in or deleted from a bucket, without reading the whole bucket over and over. It needs a Pub/Sub notification on the bucket, created for example with `gcloud storage buckets notifications create gs://my-bucket --topic=my-topic`, and a subscription on that topic. To read and delete the files of a bucket instead, use `google-storage-source`.

Output: by default, the body is the notification as JSON text (bytes): the metadata of the file, such as its name, size and content type. The `eventType` header says what happened (`OBJECT_FINALIZE` for a new or replaced file, `OBJECT_DELETE` for a deleted one), and the `objectId` and `bucketId` headers give the name of the file and of its bucket. With `getObject` set to true, the body of a new file in `bucketNameOrArn` is the content of the file, as bytes, with the `CamelGoogleCloudStorage…​` headers of the file, such as `CamelGoogleCloudStorageContentType`; its name and its bucket are only in the `objectId` and `bucketId` headers. In both cases, the `google-storage-event-id` header identifies the change.

Good to know: every notification of the subscription comes out, also for other events and other buckets; `bucketNameOrArn` is only used to choose which new files to download. Downloading does not delete the file. A notification whose processing fails is not acknowledged, so Pub/Sub delivers it again. Cloud Storage also sends its notifications at least once, so the same change can come twice, in two Pub/Sub messages with different IDs; `google-storage-event-id` is the same in both. To process each change once, put the steps after the Kamelet in an `idempotentConsumer` step on `${header[google-storage-event-id]}`. A `MemoryIdempotentRepository` remembers the changes of one process, until it restarts; with more than one replica, use a shared repository, such as the ones of `camel-infinispan` or `camel-sql`. With `ackMode` `NONE`, the route acknowledges each notification itself, through the `CamelGooglePubsubAcknowledge` header. On a subscription with a dead-letter topic, `maxDeliveryAttempts` stops a notification that keeps failing from being processed again.

## Configuration Options

The following table summarizes the configuration options available for the `google-storage-event-based-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name | **Required** The name of the bucket whose new files are downloaded when `getObject` is true, without `gs://`. Notifications of other buckets come out unchanged. | string |  | my-bucket |
| **projectId** | Project ID | **Required** The ID of the Google Cloud project that holds the subscription, as shown in the Google Cloud console. It is the project ID, not the project name or number. | string |  | my-project-123 |
| **serviceAccountKey** | Service Account Key | **Required** The JSON key of a service account that may read the subscription (and, with `getObject`, the files of the bucket), encoded in Base64: create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys, then encode the downloaded file, for example with `base64 -w0 key.json`. | binary |  |  |
| **subscriptionName** | Subscription Name | **Required** The name of the Pub/Sub subscription that receives the notifications of the bucket, without the `projects/…​/subscriptions/` part. | string |  | bucket-events-sub |
| **ackMode** | Acknowledge Mode | When a notification is acknowledged. `AUTO`: once it has been processed; a notification whose processing fails is given back (nack), so that Pub/Sub delivers it again. `NONE`: never by the Kamelet; the route acknowledges each notification itself, for example with the Simple expression `$\{header.CamelGooglePubsubAcknowledge.ack($\{exchange})}`, or gives it back with `nack`. A notification that is not acknowledged is delivered again: with `synchronousPull`, once the acknowledgement deadline of the subscription has passed; otherwise only after an hour, for which its deadline is extended. When it is not set, it is `AUTO`. Enum values: \* AUTO \* NONE | string |  |  |
| **concurrentConsumers** | Concurrent Consumers | How many notifications to receive and process in parallel, each in its own stream from the subscription. | integer | 1 |  |
| **getObject** | Get Object in Bucket | If true, the body of a notification for a new or replaced file (`OBJECT_FINALIZE`) in `bucketNameOrArn` is replaced by the content of the file. If false, the body is the notification itself. | boolean | false |  |
| **maxDeliveryAttempts** | Max Delivery Attempts | A notification that Pub/Sub has delivered this many times is given back (nack) without being processed. Pub/Sub delivers it again until the maximum of delivery attempts of the subscription is reached, and then moves it to the dead-letter topic. Pub/Sub only counts the deliveries on a subscription with a dead-letter topic; on another subscription, this option does nothing. When it is not set, the maximum of the dead-letter policy of the subscription is read when the Kamelet starts, which needs the permission `pubsub.subscriptions.get`; when it cannot be read, a warning is logged and there is no limit. Set it to 0 for no limit. | integer |  | 5 |
| **maxMessagesPerPoll** | Max Messages Per Poll | The most notifications to ask Pub/Sub for at once. Only used when `synchronousPull` is true. | integer | 1 |  |
| **synchronousPull** | Synchronous Pull | If true, it asks Pub/Sub for notifications in batches of up to `maxMessagesPerPoll`, instead of keeping a stream open that Pub/Sub pushes them through. | boolean | false |  |

## Dependencies

At runtime, the `google-storage-event-based-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:google-pubsub
    
-   camel:google-storage
    
-   camel:jackson3
    
-   camel:jsonpath
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:google-storage-event-based-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Google Storage Event-based Source Kamelet Description

### Authentication methods

This Kamelet uses Service Account Key authentication to connect to Google Cloud Pub/Sub for receiving Google Storage bucket events. You need to provide:

-   A service account key encoded in base64 format
    
-   The Google Cloud Project ID
    
-   The subscription name configured to receive storage events
    
-   The bucket name or ARN for which events are monitored
    

### Output format

The Kamelet receives data from Google Pub/Sub reporting events related to a Google Storage bucket and produces the event data in JSON format.

### Configuration

The Kamelet requires the following parameters:

-   `projectId`: The Google Cloud Pub/Sub Project ID
    
-   `subscriptionName`: The subscription name
    
-   `serviceAccountKey`: The service account key to use as credentials (must be base64 encoded)
    
-   `bucketNameOrArn`: The bucket name or ARN for which events are monitored
    

Optional parameters: - `synchronousPull`: Specifies to synchronously pull batches of messages (default: false) - `maxMessagesPerPoll`: The maximum number of messages to receive from the server in a single API call - `concurrentConsumers`: The number of parallel streams to consume from the subscription - `ackMode`: `AUTO` (when not set) or `NONE`, see below - `maxDeliveryAttempts`: How many deliveries of a notification to process at most, on a subscription with a dead-letter topic

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: google-storage-event-based-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: google-storage-event-based-source
    properties:
      projectId: "my-gcp-project"
      subscriptionName: "storage-events-subscription"
      serviceAccountKey: "{{service-account-key-base64}}"
      bucketNameOrArn: "my-storage-bucket"
      synchronousPull: true
      maxMessagesPerPoll: 10
      concurrentConsumers: 2
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

### Acknowledging Notifications

With `ackMode` not set, or `AUTO`, a notification is acknowledged once it has been processed, and given back to Pub/Sub when its processing fails, so that Pub/Sub delivers it again.

With `ackMode: NONE`, the route acknowledges each notification itself, with the object in the `CamelGooglePubsubAcknowledge` header, as described for the Google Pubsub Source Kamelet. A notification that is not acknowledged is delivered again: with `synchronousPull`, once the acknowledgement deadline of the subscription has passed; otherwise after an hour.

On a subscription with a dead-letter topic, a notification that has been delivered `maxDeliveryAttempts` times is given back without being processed, until Pub/Sub moves it to the dead-letter topic. When `maxDeliveryAttempts` is not set, the maximum of the dead-letter policy of the subscription is used.

```yaml
- route:
    from:
      uri: "kamelet:google-storage-event-based-source"
      parameters:
        projectId: "my-project-123"
        subscriptionName: "bucket-events-sub"
        serviceAccountKey: "{{gcp.serviceAccountKey}}"
        bucketNameOrArn: "my-bucket"
        maxDeliveryAttempts: 3
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-event-based-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-event-based-source.kamelet.yaml)