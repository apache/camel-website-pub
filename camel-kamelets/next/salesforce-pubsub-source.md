Kamelet Catalog

# ![salesforce pubsub source](_images/kamelets/salesforce-pubsub-source.svg) Salesforce Pub/Sub Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive events from the Salesforce Pub/Sub API.

This is the gRPC based Pub/Sub API, not the older streaming API that salesforce-source uses. Subscribe to a channel such as /event/MyEvent\_\_e, /topic/MyTopic or /data/AccountChangeEvent.

The Pub/Sub API is gRPC based and needs a protobuf-java new enough for the generated stubs in camel-salesforce. Under Camel JBang an older protobuf is resolved and the route fails to start with NoClassDefFoundError on com.google.protobuf.RuntimeVersion; adding protobuf-java as an explicit dependency resolves it.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-pubsub-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The Salesforce application consumer key. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The Salesforce application consumer secret. | string |  |  |
| **password** | Password | **Required** The Salesforce user password. | string |  |  |
| **topic** | Topic | **Required** The Pub/Sub channel to subscribe to. | string |  | /event/BatchApexErrorEvent |
| **userName** | Username | **Required** The Salesforce username. | string |  |  |
| **batchSize** | Batch Size | The number of events requested from the Pub/Sub API in a single fetch. | integer | 100 |  |
| **deserializeType** | Deserialize Type | How to deserialise the received events. This Kamelet defaults to JSON so the body is usable downstream without further decoding; the component’s own default is AVRO, which emits binary. Use POJO together with pojoClass to deserialise into a generated class. Enum values: \* AVRO \* SPECIFIC\_RECORD \* GENERIC\_RECORD \* POJO \* JSON | string | JSON |  |
| **loginUrl** | Login URL | The Salesforce instance used to authenticate. | string | [https://login.salesforce.com](https://login.salesforce.com) |  |
| **pojoClass** | POJO Class | The fully qualified class name to deserialise into. Only used when deserializeType is POJO. | string |  |  |
| **replayId** | Replay Id | The replay id to resume from. Only used when replayPreset is CUSTOM. | string |  |  |
| **replayPreset** | Replay Preset | Where to start reading the channel. LATEST receives only new events, EARLIEST replays from the retention window, CUSTOM starts from replayId. Enum values: \* LATEST \* EARLIEST \* CUSTOM | string | LATEST |  |

## Dependencies

At runtime, the `salesforce-pubsub-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:salesforce
    
-   camel:kamelet
    

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
      uri: "kamelet:salesforce-pubsub-source"
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-pubsub-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-pubsub-source.kamelet.yaml)