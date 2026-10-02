# HiveMQ

**Since Camel 4.23**

**Both producer and consumer are supported**

The HiveMQ component provides connectivity to MQTT message brokers using the [HiveMQ MQTT Client](https://www.hivemq.com/) library. It supports both **MQTT 5** (the default) and **MQTT 3.1.1**, selected with the `mqttVersion` option.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-hivemq</artifactId>
    <version>x.y.z</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

hivemq:topic\[?options\]

Where `topic` is the name of the MQTT topic.

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

The HiveMQ component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cleanStart** (common) | Whether to initiate a clean session upon connecting to the broker (called clean session in MQTT 3.1.1 and clean start in MQTT 5). The two protocol versions behave differently when this is false: with MQTT 3.1.1 the broker keeps the session (subscriptions and queued QoS 1/2 messages) indefinitely, while with MQTT 5 the session still expires on disconnect, since this component does not set a session expiry interval. | true | boolean |
| **clientId** (common) | Client identifier used when connecting to the HiveMQ broker. |  | String |
| **configuration** (common) | Component configuration. |  | HiveMQConfiguration |
| **host** (common) | Hostname or IP address of the HiveMQ MQTT broker. | localhost | String |
| **mqttVersion** (common) | 
The MQTT protocol version to use when connecting to the broker.

Enum values:

-   MQTT\_3\_1\_1
    
-   MQTT\_5\_0
    





 | MQTT\_5\_0 | MqttVersion |
| **port** (common) | Port number of the HiveMQ MQTT broker. | 1883 | int |
| **qos** (common) | 

Default Quality of Service (QoS) level to use for messages.

Enum values:

-   AT\_MOST\_ONCE
    
-   AT\_LEAST\_ONCE
    
-   EXACTLY\_ONCE
    





 | AT\_LEAST\_ONCE | MqttQos |
| **retained** (common) | Whether published messages should be retained by the MQTT broker. | false | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **password** (security) | Password for authentication with the HiveMQ broker. |  | String |
| **ssl** (security) | Whether to enable SSL/TLS encryption for the broker connection. | false | boolean |
| **username** (security) | Username for authentication with the HiveMQ broker. |  | String |

## Endpoint Options

The HiveMQ endpoint is configured using URI syntax:

hivemq:topic

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topic** (common) | **Required** The MQTT topic name or pattern to subscribe to or publish on. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cleanStart** (common) | Whether to initiate a clean session upon connecting to the broker (called clean session in MQTT 3.1.1 and clean start in MQTT 5). The two protocol versions behave differently when this is false: with MQTT 3.1.1 the broker keeps the session (subscriptions and queued QoS 1/2 messages) indefinitely, while with MQTT 5 the session still expires on disconnect, since this component does not set a session expiry interval. | true | boolean |
| **clientId** (common) | Client identifier used when connecting to the HiveMQ broker. |  | String |
| **host** (common) | Hostname or IP address of the HiveMQ MQTT broker. | localhost | String |
| **mqttVersion** (common) | 
The MQTT protocol version to use when connecting to the broker.

Enum values:

-   MQTT\_3\_1\_1
    
-   MQTT\_5\_0
    





 | MQTT\_5\_0 | MqttVersion |
| **port** (common) | Port number of the HiveMQ MQTT broker. | 1883 | int |
| **qos** (common) | 

Default Quality of Service (QoS) level to use for messages.

Enum values:

-   AT\_MOST\_ONCE
    
-   AT\_LEAST\_ONCE
    
-   EXACTLY\_ONCE
    





 | AT\_LEAST\_ONCE | MqttQos |
| **retained** (common) | Whether published messages should be retained by the MQTT broker. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **password** (security) | Password for authentication with the HiveMQ broker. |  | String |
| **ssl** (security) | Whether to enable SSL/TLS encryption for the broker connection. | false | boolean |
| **username** (security) | Username for authentication with the HiveMQ broker. |  | String |

## Message Headers

The HiveMQ component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHiveMQTopic** (common) Constant: [`MQTT_TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-hivemq/latest/org/apache/camel/component/hivemq/HiveMQConstants.html#MQTT_TOPIC) | The topic to publish/subscribe to. |  | String |
| **CamelHiveMQQos** (common) Constant: [`MQTT_QOS`](https://javadoc.io/doc/org.apache.camel/camel-hivemq/latest/org/apache/camel/component/hivemq/HiveMQConstants.html#MQTT_QOS) | 
The QoS level of the message.

Enum values:

-   AT\_MOST\_ONCE
    
-   AT\_LEAST\_ONCE
    
-   EXACTLY\_ONCE
    





 |  | MqttQos |
| **CamelHiveMQRetained** (common) Constant: [`MQTT_RETAINED`](https://javadoc.io/doc/org.apache.camel/camel-hivemq/latest/org/apache/camel/component/hivemq/HiveMQConstants.html#MQTT_RETAINED) | Whether the message should be retained. |  | Boolean |
| **CamelHiveMQOverrideTopic** (common) Constant: [`OVERRIDE_TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-hivemq/latest/org/apache/camel/component/hivemq/HiveMQConstants.html#OVERRIDE_TOPIC) | Header to dynamically override the target topic for publishing. |  | String |

## Usage

### Default payload type

By default, the Camel HiveMQ component operates on binary payloads extracted from or sent to the MQTT message:

_Java-only: receiving and sending binary payloads using the HiveMQ component_

```java
// Receive payload
byte[] payload = (byte[]) consumerTemplate.receiveBody("hivemq:topic");

// Send payload
byte[] payload = "message".getBytes();
producerTemplate.sendBody("hivemq:topic", payload);
```

Camel’s built-in [type conversion API](../../manual/type-converter.md) can perform automatic data type transformations. For example, a binary MQTT payload can be automatically converted to a `String`:

_Java-only: automatic type conversion of payloads_

```java
// Receive payload
String payload = consumerTemplate.receiveBody("hivemq:topic", String.class);

// Send payload
String payload = "message";
producerTemplate.sendBody("hivemq:topic", payload);
```

## Examples

For example, the following snippet reads messages from an MQTT broker running on the same host as the Camel router:

-   Java
    
-   XML
    
-   YAML
    

```java
from("hivemq:some/topic")
    .to("mock:test");
```

```xml
<route>
  <from uri="hivemq:some/topic"/>
  <to uri="mock:test"/>
</route>
```

```yaml
- route:
    from:
      uri: hivemq:some/topic
      steps:
        - to:
            uri: mock:test
```

The following example sends a message to the MQTT broker:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:test")
    .to("hivemq:some/topic");
```

```xml
<route>
  <from uri="direct:test"/>
  <to uri="hivemq:some/topic"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:test
      steps:
        - to:
            uri: hivemq:some/topic
```

### Connecting to a remote broker

The `host` and `port` options can be used to connect to a remote MQTT broker:

-   Java
    
-   XML
    
-   YAML
    

```java
from("hivemq:some/topic?host=mqtt.example.com&port=1883")
    .to("mock:test");
```

```xml
<route>
  <from uri="hivemq:some/topic?host=mqtt.example.com&amp;port=1883"/>
  <to uri="mock:test"/>
</route>
```

```yaml
- route:
    from:
      uri: hivemq:some/topic
      parameters:
        host: mqtt.example.com
        port: 1883
      steps:
        - to:
            uri: mock:test
```

### Authentication

The HiveMQ component supports username and password authentication. The `username` and `password` options can be used to configure MQTT simple authentication:

```java
from("hivemq:some/topic"
    + "?host=mqtt.example.com"
    + "&port=1883"
    + "&username=myuser"
    + "&password=mypassword")
    .to("mock:test");
```

The `password` option is treated as a secret and is marked as such in the generated component metadata.

### TLS

TLS can be enabled using the `ssl` option. When enabled, the HiveMQ client uses its default SSL configuration (the JVM default trust store). Camel `sslContextParameters` is not supported yet.

```java
from("hivemq:some/topic"
    + "?host=mqtt.example.com"
    + "&port=8883"
    + "&ssl=true")
    .to("mock:test");
```

### MQTT protocol version

By default, the HiveMQ component connects using MQTT 5. Set `mqttVersion=MQTT_3_1_1` to connect to a broker using MQTT 3.1.1 instead:

```java
from("hivemq:some/topic"
    + "?host=mqtt.example.com"
    + "&port=1883"
    + "&mqttVersion=MQTT_3_1_1")
    .to("mock:test");
```

The `cleanStart` option behaves differently between the two protocol versions when set to `false`. With MQTT 3.1.1, the broker keeps the session (subscriptions and queued QoS 1/2 messages) indefinitely; with MQTT 5 the session still expires on disconnect, since this component does not set a session expiry interval.

### Client identifier

A custom MQTT client identifier can be configured using the `clientId` option:

```java
from("hivemq:some/topic"
    + "?host=mqtt.example.com"
    + "&port=1883"
    + "&clientId=my-camel-client")
    .to("mock:test");
```

Each producer and each consumer opens its own MQTT connection. If `clientId` is omitted, the HiveMQ client library generates a unique identifier per connection. If you set `clientId`, it **must be unique** for every concurrent connection. Using the same `clientId` on a producer and a consumer (including the same endpoint URI used as both `from` and `to`) typically causes the broker to disconnect one of the clients.

### Acknowledgement

Incoming MQTT messages are acknowledged automatically by the HiveMQ client when they are received. Acknowledgement is **not** tied to Camel route success or failure. Manual acknowledgement is not supported.

### Current limitations

The following MQTT 5 / client features are **not** implemented and may be added in follow-up work:

-   Will messages
    
-   MQTT 5 publish properties (user properties, content type, correlation data, response topic, expiry, and similar)
    
-   Subscription options beyond topic filter and QoS
    
-   Manual acknowledgement
    
-   WebSocket transport
    
-   Connection listeners and connection-tuning options
    
-   Camel `sslContextParameters` (custom keystores / truststores)