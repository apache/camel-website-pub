# ![google pubsub source](_images/kamelets/google-pubsub-source.svg) Google Pubsub Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the messages of a Google Cloud Pub/Sub subscription, one message per Pub/Sub message, and acknowledges each one once it has been processed.

Use it to react to events that other applications publish to a Pub/Sub topic, such as orders, uploads or alerts. To publish messages, use `google-pubsub-sink`. To react to new files in a Cloud Storage bucket through Pub/Sub notifications, use `google-storage-event-based-source`.

Output: the body is the data of the Pub/Sub message, as bytes, and the `Content-Type` header is `application/octet-stream`. The `CamelGooglePubsubMessageId` and `CamelGooglePubsubPublishTime` headers give the ID and the publish time of the message, `CamelGooglePubsubAttributes` gives its attributes as a Map, and each attribute is also set as a header of its own, except a `Content-Type` attribute, which is only in `CamelGooglePubsubAttributes`.

Good to know: the subscription must already exist; for one that does not, it logs an error and receives nothing. A message whose processing fails is not acknowledged, so Pub/Sub delivers it again. With `ackMode` `NONE`, the route acknowledges each message itself, through the `CamelGooglePubsubAcknowledge` header. On a subscription with a dead-letter topic, `maxDeliveryAttempts` stops a message that keeps failing from being processed again. Without `serviceAccountKey`, it logs in with the Application Default Credentials of the environment where it runs.

## Configuration Options

The following table summarizes the configuration options available for the `google-pubsub-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **projectId** | Project ID | **Required** The ID of the Google Cloud project that holds the subscription, as shown in the Google Cloud console. It is the project ID, not the project name or number. | string |  | my-project-123 |
| **subscriptionName** | Subscription Name | **Required** The name of the subscription to read from, without the `projects/…​/subscriptions/` part. Create it on the topic first, in the Google Cloud console or with `gcloud pubsub subscriptions create`. | string |  | orders-sub |
| **ackMode** | Acknowledge Mode | When a message is acknowledged. `AUTO`: once it has been processed; a message whose processing fails is given back (nack), so that Pub/Sub delivers it again. `NONE`: never by the Kamelet; the route acknowledges each message itself, for example with the Simple expression `$\{header.CamelGooglePubsubAcknowledge.ack($\{exchange})}`, or gives it back with `nack`. A message that is not acknowledged is delivered again: with `synchronousPull`, once the acknowledgement deadline of the subscription has passed; otherwise once `maxAckExtensionPeriod` has passed. When it is not set, it is `AUTO`. Enum values: \* AUTO \* NONE | string |  |  |
| **concurrentConsumers** | Concurrent Consumers | How many messages to receive and process in parallel, each in its own stream from the subscription. | integer | 1 |  |
| **maxAckExtensionPeriod** | Max Ack Extension Period | How long, in seconds, a message that has not been acknowledged yet is kept, by extending its acknowledgement deadline. After that time, Pub/Sub delivers it again. Only used when `synchronousPull` is false. When it is not set, it is 3600, one hour. | integer |  | 600 |
| **maxDeliveryAttempts** | Max Delivery Attempts | A message that Pub/Sub has delivered this many times is given back (nack) without being processed. Pub/Sub delivers it again until the maximum of delivery attempts of the subscription is reached, and then moves it to the dead-letter topic. Pub/Sub only counts the deliveries on a subscription with a dead-letter topic; on another subscription, this option does nothing. When it is not set, the maximum of the dead-letter policy of the subscription is read when the Kamelet starts, which needs the permission `pubsub.subscriptions.get`; when it cannot be read, a warning is logged and there is no limit. Set it to 0 for no limit. | integer |  | 5 |
| **maxMessagesPerPoll** | Max Messages Per Poll | The most messages to ask Pub/Sub for at once. Only used when `synchronousPull` is true. | integer | 1 |  |
| **serviceAccountKey** | Service Account Key | The JSON key of a service account that may read the subscription, encoded in Base64: create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys, then encode the downloaded file, for example with `base64 -w0 key.json`. When it is not set, the Application Default Credentials are used: the key file named in the `GOOGLE_APPLICATION_CREDENTIALS` environment variable, or the service account of the Google Cloud machine it runs on. | binary |  |  |
| **synchronousPull** | Synchronous Pull | If true, it asks Pub/Sub for messages in batches of up to `maxMessagesPerPoll`, instead of keeping a stream open that Pub/Sub pushes the messages through. | boolean | false |  |

## Dependencies

At runtime, the `google-pubsub-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:google-pubsub
    
-   camel:jackson3
    

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
      uri: "kamelet:google-pubsub-source"
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

## Google Pubsub Source Kamelet Description

### Authentication methods

This Kamelet uses Service Account Key authentication to connect to Google Cloud Pub/Sub. You need to provide:

-   A service account key encoded in base64 format
    
-   The Google Cloud Project ID
    
-   The subscription name from which to consume messages
    

### Output format

The Kamelet consumes messages from Google Cloud Pub/Sub. The body is the data of each message, as bytes, and the attributes of the message are set as headers.

### Configuration

The Kamelet requires the following parameters:

-   `projectId`: The Google Cloud Pub/Sub Project ID
    
-   `subscriptionName`: The subscription name
    

Optional parameters: - `serviceAccountKey`: The service account key to use as credentials (must be base64 encoded) - `synchronousPull`: Specifies to synchronously pull batches of messages (default: false) - `maxMessagesPerPoll`: The maximum number of messages to receive from the server in a single API call (default: 1) - `concurrentConsumers`: The number of parallel streams to consume from the subscription (default: 1) - `ackMode`: `AUTO` (when not set) or `NONE`, see below - `maxDeliveryAttempts`: How many deliveries of a message to process at most, on a subscription with a dead-letter topic - `maxAckExtensionPeriod`: How long, in seconds, a message that is not acknowledged yet is kept (when not set: 3600)

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: google-pubsub-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: google-pubsub-source
    properties:
      projectId: "my-gcp-project"
      subscriptionName: "my-subscription"
      serviceAccountKey: "{{service-account-key-base64}}"
      synchronousPull: true
      maxMessagesPerPoll: 10
      concurrentConsumers: 2
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

### Acknowledging Messages

With `ackMode` not set, or `AUTO`, a message is acknowledged once it has been processed. A message whose processing fails is given back to Pub/Sub, which delivers it again.

With `ackMode: NONE`, the Kamelet does not acknowledge the messages. The route does it, with the object in the `CamelGooglePubsubAcknowledge` header, for example once the message has been stored:

```yaml
- route:
    from:
      uri: "kamelet:google-pubsub-source"
      parameters:
        projectId: "my-project-123"
        subscriptionName: "orders-sub"
        ackMode: NONE
        synchronousPull: true
      steps:
        - to:
            uri: "kamelet:log-sink"
        - script:
            groovy: "request.headers.CamelGooglePubsubAcknowledge.ack(exchange)"
```

Call `nack` instead of `ack` to have Pub/Sub deliver the message again right away. A message that is neither acknowledged nor given back is delivered again: with `synchronousPull`, once the acknowledgement deadline of the subscription has passed; otherwise once `maxAckExtensionPeriod` has passed, which is one hour when it is not set.

### Dead-Letter Topic

On a subscription with a dead-letter topic, Pub/Sub counts the deliveries of each message, and moves a message to the dead-letter topic once it has been delivered as many times as the dead-letter policy allows. The count is in the `CamelGooglePubsubDeliveryAttempt` header.

A message that has been delivered `maxDeliveryAttempts` times is given back without being processed, until Pub/Sub moves it. When `maxDeliveryAttempts` is not set, the Kamelet reads the maximum of the dead-letter policy when it starts, so the last delivery is not processed. That needs the permission `pubsub.subscriptions.get`; when the policy cannot be read, a warning is logged, and every delivery is processed. With `maxDeliveryAttempts: 0`, every delivery is processed.

```yaml
- route:
    from:
      uri: "kamelet:google-pubsub-source"
      parameters:
        projectId: "my-project-123"
        subscriptionName: "orders-sub"
        maxDeliveryAttempts: 3
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-pubsub-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-pubsub-source.kamelet.yaml)