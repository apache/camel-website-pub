# ![salesforce pubsub source](_images/kamelets/salesforce-pubsub-source.svg) Salesforce Pub/Sub Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives the events of a Salesforce channel, such as a Platform Event or the Change Data Capture events of a kind of record, through the Pub/Sub API, one message per event.

Use it to react to what happens in Salesforce, for example to an `Order_Shipped__e` Platform Event that a Flow publishes, or to every change of an account through `/data/AccountChangeEvent`. To be told about records that match a SOQL query, through a PushTopic, use `salesforce-source`.

Output: by default (`deserializeType` `JSON`) the body is the event as JSON text, with the fields of the event. The `CamelSalesforcePubSubReplayId` header holds the replay ID of the event, and `CamelSalesforcePubSubEventId` its ID.

Good to know: by default only the events published after the start are received. The Kamelet does not remember where it stopped: to go on after a restart, set `replayPreset` to `CUSTOM` and `replayId` to the replay ID of the last event processed.

## Configuration Options

The following table summarizes the configuration options available for the `salesforce-pubsub-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clientId** | Consumer Key | **Required** The consumer key of the connected app that the Kamelet logs in through. In Salesforce Setup, open App Manager, choose View on the app, then Manage Consumer Details. | string |  |  |
| **clientSecret** | Consumer Secret | **Required** The consumer secret of the same connected app, shown next to the consumer key under Manage Consumer Details. | string |  |  |
| **topic** | Topic | **Required** The channel to subscribe to: `/event/` and the API name of a Platform Event, such as `/event/Order_Shipped__e`, or `/data/` and the name of a change event of Change Data Capture, such as `/data/AccountChangeEvent`. | string |  | /event/BatchApexErrorEvent |
| **authenticationType** | Authentication Type | How the Kamelet logs in. `USERNAME_PASSWORD` needs `userName` and `password`; `CLIENT_CREDENTIALS` needs only the consumer key and secret, and a run-as user set for the client credentials flow in the connected app; `REFRESH_TOKEN` needs `refreshToken`; `JWT` needs `userName`, `keystore` and `jwtAudience`. Enum values: \* USERNAME\_PASSWORD \* CLIENT\_CREDENTIALS \* REFRESH\_TOKEN \* JWT | string | USERNAME\_PASSWORD |  |
| **batchSize** | Batch Size | How many events to ask the Pub/Sub API for at a time. | integer | 100 |  |
| **deserializeType** | Deserialize Type | What the body of each event is: `JSON` gives JSON text, which any other Kamelet can read. `GENERIC_RECORD` gives an Avro record object, `SPECIFIC_RECORD` an object of a generated Avro class, `AVRO` the one or the other, and `POJO` an object of `pojoClass`: these objects are for Java code that follows the Kamelet. Enum values: \* AVRO \* SPECIFIC\_RECORD \* GENERIC\_RECORD \* POJO \* JSON | string | JSON |  |
| **instanceUrl** | Instance URL | The address of your org, such as `[https://mycompany.my.salesforce.com](https://mycompany.my.salesforce.com)`. Only needed when the answer to the login does not give it. | string |  | https://myinstance.my.salesforce.com |
| **jwtAudience** | JWT Audience | The audience of the JWT that the Kamelet signs to log in: `[https://login.salesforce.com](https://login.salesforce.com)` for a production org, or `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox. Only used by `JWT`. | string |  | https://login.salesforce.com |
| **keystore** | Keystore | A reference to a bean of type `org.apache.camel.support.jsse.KeyStoreParameters`, written as `#bean:` and the name of the bean, holding the private key that signs the JWT. Its certificate must be uploaded to the connected app, under Use Digital Signatures. Only used by `JWT`. | string |  | #bean:myKeystore |
| **loginUrl** | Login URL | The address the Kamelet logs in to. Keep the default for a production org, use `[https://test.salesforce.com](https://test.salesforce.com)` for a sandbox, or the My Domain address of your org. | string | [https://login.salesforce.com](https://login.salesforce.com) | https://test.salesforce.com |
| **password** | Password | The password of `userName`. When Salesforce asks for a security token, such as from outside the trusted IP ranges of the org, add the token of the user at the end of the password; the user gets a new one from Reset My Security Token in their personal settings. Only used by `USERNAME_PASSWORD`. | string |  |  |
| **pojoClass** | POJO Class | The fully qualified name of the Java class to turn each event into. Only used when `deserializeType` is `POJO`. | string |  | com.example.events.OrderShipped |
| **refreshToken** | Refresh Token | A refresh token of the connected app for the user to act as, obtained once through an OAuth login in a browser with the `refresh_token` scope. Only used by `REFRESH_TOKEN`. | string |  |  |
| **replayId** | Replay Id | The replay ID of the last event already processed, as its `CamelSalesforcePubSubReplayId` header gave it, to receive the events after it. Only used when `replayPreset` is `CUSTOM`. | string |  |  |
| **replayPreset** | Replay Preset | Where to start reading the channel: `LATEST` receives only the events published after the start, `EARLIEST` also the older events that Salesforce still keeps, and `CUSTOM` the events after `replayId`. Enum values: \* LATEST \* EARLIEST \* CUSTOM | string | LATEST |  |
| **userName** | Username | The user name of the Salesforce user to log in as, which looks like an email address. Used by the `USERNAME_PASSWORD` and `JWT` authentication types. | string |  |  |

## Dependencies

At runtime, the `salesforce-pubsub-source` Kamelet relies upon the presence of the following dependencies:

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

`deserializeType` defaults to JSON so the body is JSON text, usable downstream without further decoding. The component’s own default is AVRO, which gives an Avro record object instead. Use POJO together with `pojoClass` to deserialise into a generated class.

### Replay

By default (`replayPreset` set to `LATEST`) the Kamelet receives only the events published after it starts. Each event carries its replay ID in the `CamelSalesforcePubSubReplayId` header. To go on from a given event after a restart, set `replayPreset` to `CUSTOM` and `replayId` to the replay ID of the last event processed.

### Runtime Dependency

The Pub/Sub API is gRPC based and needs a `protobuf-java` new enough for the generated stubs in `camel-salesforce`. Under Camel JBang an older protobuf is resolved and the route fails to start during class loading:

java.lang.NoClassDefFoundError: com/google/protobuf/RuntimeVersion$RuntimeDomain

Adding protobuf-java as an explicit dependency resolves it.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-pubsub-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/salesforce-pubsub-source.kamelet.yaml)