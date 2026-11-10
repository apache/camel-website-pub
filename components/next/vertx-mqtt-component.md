# Vert.x MQTT

**Since Camel 4.24**

**Both producer and consumer are supported**

The Vert.x MQTT component is an MQTT client for MQTT 3.1.1 and MQTT 5. A consumer subscribes to a topic filter, a producer publishes on a topic. It uses the [Vert.x MQTT](https://vertx.io/docs/vertx-mqtt/java/) client, which the Vert.x project marks as a technology preview, its MQTT 5 support included.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-vertx-mqtt</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

vertx-mqtt:topic\[?options\]

The topic of a producer names one topic, the topic filter of a consumer may hold the wildcards `+` and `#`.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Vert.x MQTT component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **automaticReconnect** (common) | Whether the client connects again when the connection is lost, and keeps trying when the first connection fails. Without, a failed first connection fails the start of the route. | true | boolean |
| **brokerUrl** (common) | The URL of the broker: tcp://host:port or mqtt://host:port for a plain connection, ssl://host:port or mqtts://host:port for TLS. Without a port 1883 is used for a plain connection and 8883 for TLS. | tcp://localhost:1883 | String |
| **cleanStart** (common) | Whether the broker discards the session of the client when it connects, the clean session flag of MQTT 3.1.1. | true | boolean |
| **clientId** (common) | The client identifier. A random one is generated if none is set. A broker allows one connection per client identifier, so two endpoints must not share one. |  | String |
| **configuration** (common) | The shared configuration of the endpoints. |  | VertxMqttConfiguration |
| **keepAliveInterval** (common) | The keep alive interval in seconds. 0 switches keep alive off. | 30 | int |
| **mqttVersion** (common) | 
The version of the MQTT protocol.

Enum values:

-   MQTT\_3\_1\_1
    
-   MQTT\_5\_0
    





 | MQTT\_5\_0 | VertxMqttVersion |
| **qos** (common) | 

The quality of service: 0 (at most once), 1 (at least once) or 2 (exactly once). For a consumer the maximum quality of service of its subscription.

Enum values:

-   0
    
-   1
    
-   2
    





 | 1 | int |
| **retained** (common) | Whether the broker retains a published message for subscribers that arrive later. | false | boolean |
| **sessionExpiryInterval** (common) | MQTT 5 only. How long the broker keeps the session after the connection closed, in seconds. 0 ends it with the connection. | 0 | long |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **manualAcksEnabled** (consumer) | Whether a message of quality of service 1 or 2 is acknowledged only once its exchange completed successfully. Otherwise the client acknowledges it as soon as it arrives. | false | boolean |
| **receiveMaximum** (consumer) | MQTT 5 only. The most messages of quality of service 1 and 2 the broker sends before the client acknowledges them. 0 leaves it to the broker. | 0 | int |
| **maxPendingMessages** (consumer (advanced)) | The most received messages waiting for their exchange to complete. Beyond it the client stops reading from the connection until the consumer caught up, which holds back the broker for every quality of service. | 1000 | int |
| **ackTimeout** (producer) | How long a message of quality of service 1 or 2 waits for its acknowledgement, in seconds. The exchange fails when the time is up. 0 or less waits without a limit. | 30 | int |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxInflightQueue** (producer) | The most messages of quality of service 1 and 2 the client has sent without an acknowledgement. A message beyond it fails. | 10 | int |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **connectTimeout** (advanced) | How long to wait for the connection to the broker, in milliseconds. | 30000 | long |
| **maxMessageSize** (advanced) | The largest message in bytes the client receives, the protocol maximum by default. Every message is read into memory as a whole, so lower it for a broker whose publishers are not trusted. | 268435455 | int |
| **maxReconnectDelay** (advanced) | The longest delay between two attempts to reconnect, in milliseconds. | 60000 | long |
| **reconnectDelay** (advanced) | The delay before the first attempt to reconnect, in milliseconds. Every further attempt doubles it, up to the maximum reconnect delay. | 1000 | long |
| **vertx** (advanced) | **Autowired** The Vert.x instance to use. Without, the one of the registry if there is exactly one, else a Vert.x instance of the component’s own, closed when the component stops. |  | Vertx |
| **vertxOptions** (advanced) | The options of the Vert.x instance the component creates when none is given. |  | VertxOptions |
| **willPayload** (advanced) | The payload of the will message. |  | String |
| **willQos** (advanced) | 

The quality of service of the will message.

Enum values:

-   0
    
-   1
    
-   2
    





 | 0 | int |
| **willRetained** (advanced) | Whether the will message is retained. | false | boolean |
| **willTopic** (advanced) | The topic of the will message the broker publishes when the client goes away without disconnecting. |  | String |
| **password** (security) | The password to authenticate with. |  | String |
| **sslContextParameters** (security) | The TLS configuration of a connection to an ssl:// or mqtts:// broker: key managers for a client certificate, trust managers, protocols and cipher suites. Without it the trust store of the JVM is used. The host name of the broker is always verified against its certificate: there is intentionally no option to switch the check off. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Whether to use the global SSL context parameters of the Camel context for an endpoint that sets none. | false | boolean |
| **username** (security) | The user name to authenticate with. |  | String |

## Endpoint Options

The Vert.x MQTT endpoint is configured using URI syntax:

vertx-mqtt:topic

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topic** (common) | **Required** The topic to publish on, or the topic filter to subscribe to. A filter may hold the wildcards + and #, a topic to publish on may not. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **automaticReconnect** (common) | Whether the client connects again when the connection is lost, and keeps trying when the first connection fails. Without, a failed first connection fails the start of the route. | true | boolean |
| **brokerUrl** (common) | The URL of the broker: tcp://host:port or mqtt://host:port for a plain connection, ssl://host:port or mqtts://host:port for TLS. Without a port 1883 is used for a plain connection and 8883 for TLS. | tcp://localhost:1883 | String |
| **cleanStart** (common) | Whether the broker discards the session of the client when it connects, the clean session flag of MQTT 3.1.1. | true | boolean |
| **clientId** (common) | The client identifier. A random one is generated if none is set. A broker allows one connection per client identifier, so two endpoints must not share one. |  | String |
| **keepAliveInterval** (common) | The keep alive interval in seconds. 0 switches keep alive off. | 30 | int |
| **mqttVersion** (common) | 
The version of the MQTT protocol.

Enum values:

-   MQTT\_3\_1\_1
    
-   MQTT\_5\_0
    





 | MQTT\_5\_0 | VertxMqttVersion |
| **qos** (common) | 

The quality of service: 0 (at most once), 1 (at least once) or 2 (exactly once). For a consumer the maximum quality of service of its subscription.

Enum values:

-   0
    
-   1
    
-   2
    





 | 1 | int |
| **retained** (common) | Whether the broker retains a published message for subscribers that arrive later. | false | boolean |
| **sessionExpiryInterval** (common) | MQTT 5 only. How long the broker keeps the session after the connection closed, in seconds. 0 ends it with the connection. | 0 | long |
| **manualAcksEnabled** (consumer) | Whether a message of quality of service 1 or 2 is acknowledged only once its exchange completed successfully. Otherwise the client acknowledges it as soon as it arrives. | false | boolean |
| **receiveMaximum** (consumer) | MQTT 5 only. The most messages of quality of service 1 and 2 the broker sends before the client acknowledges them. 0 leaves it to the broker. | 0 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **maxPendingMessages** (consumer (advanced)) | The most received messages waiting for their exchange to complete. Beyond it the client stops reading from the connection until the consumer caught up, which holds back the broker for every quality of service. | 1000 | int |
| **ackTimeout** (producer) | How long a message of quality of service 1 or 2 waits for its acknowledgement, in seconds. The exchange fails when the time is up. 0 or less waits without a limit. | 30 | int |
| **maxInflightQueue** (producer) | The most messages of quality of service 1 and 2 the client has sent without an acknowledgement. A message beyond it fails. | 10 | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connectTimeout** (advanced) | How long to wait for the connection to the broker, in milliseconds. | 30000 | long |
| **maxMessageSize** (advanced) | The largest message in bytes the client receives, the protocol maximum by default. Every message is read into memory as a whole, so lower it for a broker whose publishers are not trusted. | 268435455 | int |
| **maxReconnectDelay** (advanced) | The longest delay between two attempts to reconnect, in milliseconds. | 60000 | long |
| **reconnectDelay** (advanced) | The delay before the first attempt to reconnect, in milliseconds. Every further attempt doubles it, up to the maximum reconnect delay. | 1000 | long |
| **willPayload** (advanced) | The payload of the will message. |  | String |
| **willQos** (advanced) | 

The quality of service of the will message.

Enum values:

-   0
    
-   1
    
-   2
    





 | 0 | int |
| **willRetained** (advanced) | Whether the will message is retained. | false | boolean |
| **willTopic** (advanced) | The topic of the will message the broker publishes when the client goes away without disconnecting. |  | String |
| **password** (security) | The password to authenticate with. |  | String |
| **sslContextParameters** (security) | The TLS configuration of a connection to an ssl:// or mqtts:// broker: key managers for a client certificate, trust managers, protocols and cipher suites. Without it the trust store of the JVM is used. The host name of the broker is always verified against its certificate: there is intentionally no option to switch the check off. |  | SSLContextParameters |
| **username** (security) | The user name to authenticate with. |  | String |

## Message Headers

The Vert.x MQTT component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelVertxMqttTopic** (consumer) Constant: [`TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#TOPIC) | The topic the message was published on. |  | String |
| **CamelVertxMqttQos** (consumer) Constant: [`QOS`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#QOS) | The quality of service the message was delivered with: 0, 1 or 2. |  | Integer |
| **CamelVertxMqttRetained** (consumer) Constant: [`RETAINED`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#RETAINED) | Whether the broker delivered a retained message. |  | Boolean |
| **CamelVertxMqttDuplicate** (consumer) Constant: [`DUPLICATE`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#DUPLICATE) | Whether the broker delivers the message again. |  | Boolean |
| **CamelVertxMqttMessageId** (consumer) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#MESSAGE_ID) | The packet identifier of a message of quality of service 1 or 2. |  | Integer |
| **CamelVertxMqttOverrideTopic** (producer) Constant: [`OVERRIDE_TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#OVERRIDE_TOPIC) | The topic to publish on instead of the topic of the endpoint. |  | String |
| **CamelVertxMqttOverrideQos** (producer) Constant: [`OVERRIDE_QOS`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#OVERRIDE_QOS) | The quality of service to publish with instead of the qos option of the endpoint: 0, 1 or 2. |  | Integer |
| **CamelVertxMqttOverrideRetained** (producer) Constant: [`OVERRIDE_RETAINED`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#OVERRIDE_RETAINED) | Whether to publish the message as retained, instead of the retained option of the endpoint. |  | Boolean |
| **CamelVertxMqttUserProperties** (common) Constant: [`USER_PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#USER_PROPERTIES) | MQTT 5 only. The user properties of the message, in their order and with keys that occur more than once. The producer also takes a Map. |  | List |
| **CamelVertxMqttContentType** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#CONTENT_TYPE) | MQTT 5 only. The content type of the message. |  | String |
| **CamelVertxMqttResponseTopic** (common) Constant: [`RESPONSE_TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#RESPONSE_TOPIC) | MQTT 5 only. The topic a response is expected on. |  | String |
| **CamelVertxMqttCorrelationData** (common) Constant: [`CORRELATION_DATA`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#CORRELATION_DATA) | MQTT 5 only. The data that relates a response to its request. |  | byte\[\] |
| **CamelVertxMqttMessageExpiryInterval** (common) Constant: [`MESSAGE_EXPIRY_INTERVAL`](https://javadoc.io/doc/org.apache.camel/camel-vertx-mqtt/latest/org/apache/camel/component/vertx/mqtt/VertxMqttConstants.html#MESSAGE_EXPIRY_INTERVAL) | MQTT 5 only. The lifetime of the message in seconds. |  | Long |

## Usage

### Broker URL

The `brokerUrl` option names the broker and how to reach it:

  
| Scheme | Default port | Connection |
| --- | --- | --- |
| `tcp`, `mqtt` | 1883 | plain TCP |
| `ssl`, `mqtts` | 8883 | TLS |

User information in the URL is refused. Credentials belong into the `username` and `password` options, so that they do not end up in logs together with the URL. The WebSocket schemes `ws` and `wss` are refused as well, until the Vert.x MQTT client supports the WebSocket transport.

### Payload

The consumer sets the body to the payload as a `byte[]`, the topic it arrived on is in the `CamelVertxMqttTopic` header. The producer sends whatever the body converts to a `byte[]`: text, bytes, a stream or a file. A message without a body is sent with an empty payload.

The headers the consumer sets, `CamelVertxMqttQos` and `CamelVertxMqttRetained` among them, describe the message that arrived. The producer does not read them: a route that bridges one broker to another would otherwise publish every retained message it receives as retained again. To choose the quality of service, the retained flag or the topic of a single message, the producer reads `CamelVertxMqttOverrideQos`, `CamelVertxMqttOverrideRetained` and `CamelVertxMqttOverrideTopic`.

### Connection

The consumer and the producer of an endpoint share one connection. It is opened when the first of them starts and closed when the last of them stops. Two endpoints are two connections, and since a broker allows one connection per client identifier, two endpoints must not share a `clientId`. Without a `clientId` a connection gets a random one, which it keeps for every reconnect. A session the broker keeps (`cleanStart=false`) is only found again after a restart of the route with a `clientId` set.

With `automaticReconnect` (the default) a lost connection is opened again, after `reconnectDelay` and then with a delay that doubles on every attempt, up to `maxReconnectDelay`, plus up to a fifth of it at random, so that the clients of a broker that went away do not all come back at the same moment. Every attempt uses a new Vert.x client, so that nothing of the lost connection carries over. If the broker cannot be reached when a route starts, the route starts all the same and the component keeps trying. A producer waits up to `connectTimeout` for the connection before the exchange fails. Without `automaticReconnect` a broker that cannot be reached fails the start of the route.

The Vert.x client keeps no session of its own: a message the broker did not acknowledge when the connection was lost is not sent again, its exchange fails. A redelivery by the error handler of the route sends it as a new message, so across a lost connection quality of service 2 gives at least once, not exactly once: the broker can receive the message twice.

After a reconnect the exchanges that waited for the connection are sent at once. More of them than `maxInflightQueue` fail right away, as they would while connected.

With `cleanStart=false` the broker keeps the session of the client, with MQTT 5 for `sessionExpiryInterval` seconds. Keep `maxReconnectDelay` well below `sessionExpiryInterval`: a reconnect after a lost connection that comes later finds no session, and the messages the broker held for it are gone. A consumer that stops then keeps its subscription at the broker, which holds the messages of quality of service 1 and 2 until the consumer connects again with the same `clientId`. After a reconnect to a session the broker kept, the consumer does not subscribe again: the session still holds the subscription, and subscribing again would deliver the retained messages once more. With `cleanStart=true` (the default) a consumer subscribes after every connect, and unsubscribes when it stops.

The keep alive of the Vert.x client only sends a PINGREQ when it wrote nothing for `keepAliveInterval` seconds. A producer that publishes continuously therefore does not notice a broker that stopped answering, until `ackTimeout` fails its messages of quality of service 1 and 2.

### Quality of service and acknowledgement

The producer completes an exchange when the broker acknowledged the message, with PUBACK for quality of service 1 and PUBCOMP for 2. A message of quality of service 0 completes when it is written. A message without an acknowledgement within `ackTimeout` seconds fails, and so does a message beyond `maxInflightQueue` unacknowledged messages.

The producer completes the exchange on a worker thread, never on the event loop of the client: the rest of the route, and a redelivery delay of its error handler, would otherwise block the keep alive of every connection on that event loop.

The consumer acknowledges a message of quality of service 1 or 2 as soon as it arrives. With `manualAcksEnabled` it acknowledges it once its exchange completed successfully. A message whose exchange failed is handled as follows:

-   At quality of service 1 with a session that outlives the connection (`cleanStart=false`, and with MQTT 5 a `sessionExpiryInterval` above 0) and `automaticReconnect`, the consumer does not acknowledge it. It stops reading, lets the exchanges it already received finish and acknowledges those, then closes the connection and connects again, and the broker delivers the message again from the session. The route sees it again, with `CamelVertxMqttDuplicate` set by most brokers. Delivery is at least once, a route must tolerate duplicates. A message whose exchange fails every time comes back after every reconnect: the error handler of the route, a dead letter channel for example, has to complete it. While the failures repeat and no other exchange succeeds in between, the reconnect delay keeps growing up to `maxReconnectDelay`, but with MQTT 5 never beyond half of `sessionExpiryInterval`, so that the reconnect reaches the session before the broker lets it expire. Every such close is logged as a warning.
    
-   Otherwise the consumer acknowledges it all the same, and it is not delivered again. Left unacknowledged it would hold one of the in-flight slots of the broker until the next connect, and after `receiveMaximum` such failures the broker would send nothing more. At quality of service 2 the Vert.x client sends the PUBREC as soon as the message arrives, whatever `manualAcksEnabled` says, and the broker never sends a message again after its PUBREC, so manual acknowledgement only holds back the PUBCOMP.
    

### Back pressure

The consumer processes the exchanges in the order the messages arrive, on a Vert.x worker of one thread, never on the event loop of the client, which also keeps the connection alive. When more than `maxPendingMessages` messages wait for their exchange, the client stops reading from the connection until half of them are done, also across a reconnect. The broker is then held back by TCP, for every quality of service. The bound is a soft one: messages the client had already read when it paused still arrive, and are acknowledged on arrival unless `manualAcksEnabled` is set. With MQTT 5 `receiveMaximum` also limits the messages of quality of service 1 and 2 the broker sends before they are acknowledged.

The consumer and the producer of an endpoint share the connection, so while the consumer holds the client back, the acknowledgements for the producer wait as well, and a close for a redelivery fails the messages of quality of service 1 and 2 the producer is waiting for. When the consumer of an endpoint with `cleanStart=false` stops while its producer still uses the connection, the subscription stays at the broker, and messages that arrive meanwhile are acknowledged and dropped. Use two endpoints when both carry load.

When the consumer stops, and during a graceful shutdown, it first stops reading, then waits for the exchanges of the messages it already received, and only then unsubscribes and disconnects: a message acknowledged on arrival would otherwise be lost.

### TLS

A broker URL with `ssl` or `mqtts` connects over TLS. The `sslContextParameters` give the trust managers, the key managers for a client certificate, the protocols and the cipher suites. Without them the trust store of the JVM is used. The host name of the broker is always verified against its certificate, there is no option to switch the check off or to trust every certificate.

### Vert.x instance

The component uses the Vert.x instance set on it, or the one in the registry if there is exactly one. Otherwise it creates one of its own, configured by `vertxOptions`, and closes it when it shuts down.

## Examples

### Receiving messages

-   Java
    
-   YAML
    

```java
from("vertx-mqtt:sensors/+/temperature?brokerUrl=tcp://broker.example.com:1883&qos=1")
    .log("${header.CamelVertxMqttTopic}: ${body}");
```

```yaml
- from:
    uri: vertx-mqtt:sensors/+/temperature
    parameters:
      brokerUrl: tcp://broker.example.com:1883
      qos: 1
    steps:
      - log: "${header.CamelVertxMqttTopic}: ${body}"
```

### Publishing messages

```java
from("timer:status?period=60000")
    .setBody(constant("online"))
    .to("vertx-mqtt:devices/gateway-1/status?brokerUrl=ssl://broker.example.com&retained=true"
        + "&username=gateway-1&password=RAW(secret)&sslContextParameters=#brokerTls");
```

### MQTT 5 properties

```java
from("direct:request")
    .setHeader("CamelVertxMqttResponseTopic", constant("replies/gateway-1"))
    .setHeader("CamelVertxMqttContentType", constant("application/json"))
    .to("vertx-mqtt:requests?brokerUrl=tcp://broker.example.com");
```

### MQTT 3.1.1

```java
from("vertx-mqtt:legacy/#?brokerUrl=tcp://broker.example.com&mqttVersion=MQTT_3_1_1")
    .to("log:legacy");
```

## Current limitations

-   No WebSocket transport (`ws`, `wss`) yet.
    
-   No connection through a proxy.
    
-   The client keeps no session: messages of quality of service 1 and 2 that were not acknowledged before a connection was lost are not sent again by the client.
    
-   The Vert.x client does not reconnect by itself yet ([vertx-mqtt#197](https://github.com/vert-x3/vertx-mqtt/pull/197)), the component does it.
    
-   With a kept session, a PUBREL the broker sends again after a reconnect is not answered by the Vert.x client, so a message of quality of service 2 whose PUBCOMP was lost with the connection stays incomplete at the broker.