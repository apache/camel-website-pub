# ![google storage event based source](_images/kamelets/google-storage-event-based-source.svg) Google Storage Event-based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from Google Pubsub reporting events related to a Google Storage bucket.

## Configuration Options

The following table summarizes the configuration options available for the `google-storage-event-based-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name Or ARN | **Required** The Google Cloud Storage bucket name or Bucket Amazon Resource Name (ARN). | string |  |  |
| **projectId** | Project Id | **Required** The Google Cloud Pub/Sub Project ID. | string |  |  |
| **serviceAccountKey** | Service Account Key | **Required** The service account key to use as credentials for the Pub/Sub publisher/subscriber. You must encode this value in base64. | binary |  |  |
| **subscriptionName** | Subscription Name | **Required** The subscription name. | string |  |  |
| **concurrentConsumers** | Concurrent Consumers | The number of parallel streams to consume from the subscription. | integer | 1 |  |
| **getObject** | Get Object in Bucket | If `getObject` is enabled, then the file created in the Bucket is retreived and returned as body, if not only the event is returned as body. | boolean | false |  |
| **maxMessagesPerPoll** | Max Messages Per Poll | The maximum number of messages to receive from the server in a single API call. | integer | 1 |  |
| **synchronousPull** | Synchronous Pull | Specifies to synchronously pull batches of messages. | boolean | false |  |

## Dependencies

At runtime, the `google-storage-event-based-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:google-pubsub
    
-   camel:google-storage
    
-   camel:jackson
    
-   camel:core
    

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
    

Optional parameters: - `synchronousPull`: Specifies to synchronously pull batches of messages (default: false) - `maxMessagesPerPoll`: The maximum number of messages to receive from the server in a single API call - `concurrentConsumers`: The number of parallel streams to consume from the subscription

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-event-based-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-event-based-source.kamelet.yaml)