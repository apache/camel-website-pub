# ![google pubsub sink](_images/kamelets/google-pubsub-sink.svg) Google Pubsub Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Publishes each message to a topic in Google Cloud Pub/Sub.

Use it to send events or data to other applications that read the topic through a subscription, such as orders, sensor readings or notifications. To read messages from a subscription, use `google-pubsub-source`.

Input: the body becomes the data of the Pub/Sub message, as text (sent as UTF-8) or bytes. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The headers of the message, except the Camel ones, are sent as attributes of the Pub/Sub message.

Output: the message is unchanged, with the ID that Pub/Sub gave the published message in the `CamelGooglePubsubMessageId` header.

Good to know: the topic must exist; a message sent to a topic that does not exist fails. Without `serviceAccountKey`, it logs in with the Application Default Credentials of the environment where it runs.

## Configuration Options

The following table summarizes the configuration options available for the `google-pubsub-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Topic Name | **Required** The name of the topic to publish to, without the `projects/…​/topics/` part. | string |  | orders |
| **projectId** | Project ID | **Required** The ID of the Google Cloud project that holds the topic, as shown in the Google Cloud console. It is the project ID, not the project name or number. | string |  | my-project-123 |
| **serviceAccountKey** | Service Account Key | The JSON key of a service account that may publish to the topic, encoded in Base64: create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys, then encode the downloaded file, for example with `base64 -w0 key.json`. When it is not set, the Application Default Credentials are used: the key file named in the `GOOGLE_APPLICATION_CREDENTIALS` environment variable, or the service account of the Google Cloud machine it runs on. | binary |  |  |

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