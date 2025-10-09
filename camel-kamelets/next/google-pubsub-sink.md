# ![google pubsub sink](_images/kamelets/google-pubsub-sink.svg) Google Pubsub Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send messages to Google Cloud Pub/Sub.

## Configuration Options

The following table summarizes the configuration options available for the `google-pubsub-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Destination Name | **Required** The destination name. | string |  |  |
| **projectId** | Project Id | **Required** The Google Cloud Pub/Sub Project ID. | string |  |  |
| **serviceAccountKey** | Service Account Key | The service account key to use as credentials for the Pub/Sub publisher/subscriber. You must encode this value in base64. | binary |  |  |

## Dependencies

At runtime, the `google-pubsub-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:google-pubsub
    
-   camel:jackson
    

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:google-pubsub-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Google Pubsub Sink Kamelet Description

### Authentication

This Kamelet supports Google Cloud authentication through service account keys. The service account key is optional - if not provided, the Kamelet will use default credentials.

### Required Configuration

-   **Project ID**: The Google Cloud Pub/Sub Project ID
    
-   **Destination Name**: The Pub/Sub topic name to publish messages to
    

### Optional Configuration

-   **Service Account Key**: Base64-encoded service account credentials (optional)
    

### Message Publishing

The Kamelet publishes messages to the specified Google Cloud Pub/Sub topic, enabling reliable message delivery and processing across distributed systems.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-pubsub-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-pubsub-sink.kamelet.yaml)