# ![salesforce pubsub source](_images/kamelets/salesforce-pubsub-source.svg) Salesforce Pub/Sub Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive events from the Salesforce Pub/Sub API.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-pubsub-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The Salesforce application consumer key. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The Salesforce application consumer secret. | string |  |  |
| **topic** | Topic | **Required** The Pub/Sub channel to subscribe to. | string |  | /event/BatchApexErrorEvent |
| **authenticationType** | Authentication Type | Authentication type to use. USERNAME\_PASSWORD needs userName and password, CLIENT\_CREDENTIALS needs only the consumer key and secret, REFRESH\_TOKEN needs refreshToken, JWT needs keystore and jwtAudience. Enum values: \* USERNAME\_PASSWORD \* CLIENT\_CREDENTIALS \* REFRESH\_TOKEN \* JWT | string | USERNAME\_PASSWORD |  |
| **batchSize** | Batch Size | The number of events requested from the Pub/Sub API in a single fetch. | integer | 100 |  |
| **deserializeType** | Deserialize Type | How to deserialise the received events. This Kamelet defaults to JSON so the body is usable downstream without further decoding; the component’s own default is AVRO, which emits binary. Use POJO together with pojoClass to deserialise into a generated class. Enum values: \* AVRO \* SPECIFIC\_RECORD \* GENERIC\_RECORD \* POJO \* JSON | string | JSON |  |
| **instanceUrl** | Instance URL | Salesforce instance URL, needed when the authentication response does not carry one. | string |  | https://myinstance.my.salesforce.com |
| **jwtAudience** | JWT Audience | Audience claim for the JWT authentication type, usually the login URL of the target org. | string |  | https://login.salesforce.com |
| **keystore** | Keystore | Reference to a registry bean of type org.apache.camel.support.jsse.KeyStoreParameters, written as "#bean:myBeanName", holding the certificate that signs the JWT. Required by the JWT authentication type and ignored by the others. | string |  | #bean:myKeystore |
| **loginUrl** | Login URL | The Salesforce instance used to authenticate. | string | [https://login.salesforce.com](https://login.salesforce.com) |  |
| **password** | Password | The Salesforce user password. | string |  |  |
| **pojoClass** | POJO Class | The fully qualified class name to deserialise into. Only used when deserializeType is POJO. | string |  |  |
| **refreshToken** | Refresh Token | Refresh token used by the REFRESH\_TOKEN authentication type. | string |  |  |
| **replayId** | Replay Id | The replay id to resume from. Only used when replayPreset is CUSTOM. | string |  |  |
| **replayPreset** | Replay Preset | Where to start reading the channel. LATEST receives only new events, EARLIEST replays from the retention window, CUSTOM starts from replayId. Enum values: \* LATEST \* EARLIEST \* CUSTOM | string | LATEST |  |
| **userName** | Username | The Salesforce username. | string |  |  |

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

## Salesforce Pub/Sub Source Kamelet Description

### Which API

This is the gRPC based Pub/Sub API, not the older streaming API that `salesforce-source` uses. Subscribe to a channel such as `/event/MyEvent__e`, `/topic/MyTopic` or `/data/AccountChangeEvent`.

### Deserialization

`deserializeType` defaults to JSON so the body is usable downstream without further decoding. The component’s own default is AVRO, which emits binary. Use POJO together with `pojoClass` to deserialise into a generated class.

### Runtime Dependency

The Pub/Sub API is gRPC based and needs a `protobuf-java` new enough for the generated stubs in `camel-salesforce`. Under Camel JBang an older protobuf is resolved and the route fails to start during class loading:

java.lang.NoClassDefFoundError: com/google/protobuf/RuntimeVersion$RuntimeDomain

Adding protobuf-java as an explicit dependency resolves it.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-pubsub-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-pubsub-source.kamelet.yaml)