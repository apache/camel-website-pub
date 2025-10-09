# Nats

**Since Camel 2.17**

**Both producer and consumer are supported**

[NATS](http://nats.io/) is a fast and reliable messaging platform.

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-nats</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.y.z</version>
</dependency>
```

## URI format

nats:topic\[?options\]

Where **topic** is the topic name

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Nats component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **servers** (common) | URLs to one or more NAT servers. Use comma to separate URLs when specifying multiple servers. |  | String |
| **verbose** (common) | Whether or not running in verbose mode. | false | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Nats endpoint is configured using URI syntax:

nats:topic

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topic** (common) | **Required** The name of topic we want to use. |  | String |

### Query Parameters (29 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (common) | Timeout for connection attempts. (in milliseconds). | 2000 | int |
| **flushConnection** (common) | Define if we want to flush connection when stopping or not. | true | boolean |
| **flushTimeout** (common) | Set the flush timeout (in milliseconds). | 1000 | int |
| **maxPingsOut** (common) | maximum number of pings have not received a response allowed by the client. | 2 | int |
| **maxReconnectAttempts** (common) | Max reconnection attempts. | 60 | int |
| **noEcho** (common) | Turn off echo. If supported by the gnatsd version you are connecting to this flag will prevent the server from echoing messages back to the connection if it has subscriptions on the subject being published to. | false | boolean |
| **noRandomizeServers** (common) | Whether or not randomizing the order of servers for the connection attempts. | false | boolean |
| **pedantic** (common) | Whether or not running in pedantic mode (this affects performance). | false | boolean |
| **pingInterval** (common) | Ping interval to be aware if connection is still alive (in milliseconds). | 120000 | int |
| **reconnect** (common) | Whether or not using reconnection feature. | true | boolean |
| **reconnectTimeWait** (common) | Waiting time before attempts reconnection (in milliseconds). | 2000 | int |
| **requestCleanupInterval** (common) | Interval to clean up cancelled/timed out requests. | 5000 | int |
| **servers** (common) | URLs to one or more NAT servers. Use comma to separate URLs when specifying multiple servers. |  | String |
| **verbose** (common) | Whether or not running in verbose mode. | false | boolean |
| **maxMessages** (consumer) | Stop receiving messages from a topic we are subscribing to after maxMessages. |  | String |
| **poolSize** (consumer) | Consumer thread pool size (default is 10). | 10 | int |
| **queueName** (consumer) | The Queue name if we are using nats for a queue configuration. |  | String |
| **replyToDisabled** (consumer) | Can be used to turn off sending back reply message in the consumer. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **replySubject** (producer) | the subject to which subscribers should send response. |  | String |
| **requestTimeout** (producer) | Request timeout in milliseconds. | 20000 | long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connection** (advanced) | Reference an already instantiated connection to Nats server. |  | Connection |
| **headerFilterStrategy** (advanced) | Define the header filtering strategy. |  | HeaderFilterStrategy |
| **traceConnection** (advanced) | Whether or not connection trace messages should be printed to standard out for fine grained debugging of connection issues. | false | boolean |
| **secure** (security) | Set secure option indicating TLS is required. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |

## Message Headers

The Nats component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelNatsMessageTimestamp** (common) Constant: [`NATS_MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_MESSAGE_TIMESTAMP) | The timestamp of a consumed message. |  | long |
| **CamelNatsSID** (common) Constant: [`NATS_SID`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_SID) | The SID of a consumed message. |  | String |
| **CamelNatsReplyTo** (common) Constant: [`NATS_REPLY_TO`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_REPLY_TO) | The ReplyTo of a consumed message (may be null). |  | String |
| **CamelNatsSubject** (common) Constant: [`NATS_SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_SUBJECT) | The Subject of a consumed message. |  | String |
| **CamelNatsQueueName** (common) Constant: [`NATS_QUEUE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_QUEUE_NAME) | The Queue name of a consumed message (may be null). |  | String |

## Configuring servers

You configure the NATS servers on either the component or the endpoint.

For example to configure this once on the component you can do:

```java
NatsComponent nats = context.getComponent("nats", NatsComponent.class);
nats.setServers("someserver:4222,someotherserver:42222");
```

Notice how you can specify multiple servers separated by comma.

Or you can specify the servers in the endpoint URI

```java
from("direct:send").to("nats:test?servers=localhost:4222");
```

The endpoint configuration will override any server configuration on the component level.

### Configuring username and password or token

You can specify username and password for the servers in the server URLs, where its `username:password@url`, or `token@url` etc:

```java
NatsComponent nats = context.getComponent("nats", NatsComponent.class);
nats.setServers("scott:tiger@someserver:4222,superman:123@someotherserver:42222");
```

If you are using Camel Main or Spring Boot you can configure the server urls in the `application.properties` file

```properties
camel.component.nats.servers=scott:tiger@someserver:4222,superman:123@someotherserver:42222
```

## Request/Reply support

The producer supports request/reply where it can wait for an expected reply message.

The consumer will when routing the message is complete, send back the message as reply-message if required.

## Examples

**Producer example:**

```java
from("direct:send")
  .to("nats:mytopic");
```

In case of using Authorization you can directly specify your credentials in the server URL

```java
from("direct:send")
  .to("nats:mytopic?servers=username:password@localhost:4222");
```

or your token

```java
from("direct:send")
  .to("nats:mytopic?servers=token@localhost:4222);
```

**Consumer example:**

```java
from("nats:mytopic?maxMessages=5&queueName=myqueue")
  .to("mock:result");
```

## Spring Boot Auto-Configuration

When using nats with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-nats-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.nats.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.nats.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.nats.enabled** | Whether to enable auto configuration of the nats component. This is enabled by default. |  | Boolean |
| **camel.component.nats.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.nats.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.nats.servers** | URLs to one or more NAT servers. Use comma to separate URLs when specifying multiple servers. |  | String |
| **camel.component.nats.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.nats.verbose** | Whether or not running in verbose mode. | false | Boolean |