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

The Nats component supports 43 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | To use a shared configuration. |  | NatsConfiguration |
| **connectionTimeout** (common) | Timeout for connection attempts. (in milliseconds). | 2000 | int |
| **flushConnection** (common) | Define if we want to flush connection when stopping or not. | true | boolean |
| **flushTimeout** (common) | Set the flush timeout (in milliseconds). | 1000 | int |
| **jetstreamEnabled** (common) | Sets whether to enable JetStream support for this endpoint. | false | boolean |
| **jetstreamName** (common) | Sets the name of the JetStream stream to use. |  | String |
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
| **ackPolicy** (consumer) | 
Acknowledgement mode. none = Messages are acknowledged as soon as the server sends them (danger: messages that Camel failed to process is also ack). Clients do not need to ack. all = All messages with a sequence number less than the message acked are also acknowledged. E.g. reading a batch of messages 1..100. Ack on message 100 will acknowledge 1..99 as well. explicit (default) = Each message is acknowledged individually by Camel after the message has been processed, this ensures the message is only ack if success and nack if processing failed due to an exception during routing. Message can be acked out of sequence and create gaps of unacknowledged messages in the consumer.

Enum values:

-   None
    
-   All
    
-   Explicit
    





 | Explicit | AckPolicy |
| **ackWait** (consumer) | After a message is delivered to a consumer, the server waits 30 seconds (default) for an acknowledgement. If none arrives (timeout), the message becomes eligible for redelivery. | 30000 | long |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **durableName** (consumer) | Sets the name to assign to the JetStream durable consumer. Setting this value makes the consumer durable. The value is used to set the durable() field in the underlying NATS ConsumerConfiguration.Builder. |  | String |
| **maxDeliver** (consumer) | Maximum number of attempts to deliver a message from Nats to a consumer. Once MaxDeliver is reached, the NATS server stops attempting to deliver that specific message. The message is not deleted, it remains in the stream but is simply skipped. It is recommended to set this option to a sensible value in case a message is poison and can not successfully be processed and would always keep failing. |  | long |
| **maxMessages** (consumer) | Stop receiving messages from a topic we are subscribing to after maxMessages. |  | String |
| **nackWait** (consumer) | For negative acknowledgements (NAK), redelivery is delayed by 5 seconds (default). Setting this to 0 or negative makes the redelivery immediately. Be careful as this can cause the consumer to keep re-processing the same message over and over again due to intermediate error that last a while. | 5000 | long |
| **poolSize** (consumer) | Consumer thread pool size (default is 10). | 10 | int |
| **pullBatchSize** (consumer) | Maximum number of messages to fetch per pull request when using a JetStream Pull Subscription. Only used when \\{code pullSubscription=true}. | 10 | int |
| **pullFetchTimeout** (consumer) | Maximum time (in milliseconds) to wait for a batch of messages to be available on the server during a single fetch when using a JetStream Pull Subscription. Only used when \\{code pullSubscription=true}. | 1000 | long |
| **pullSubscription** (consumer) | Sets the consumer subscription type for JetStream. Set to true to use a Pull Subscription (consumer explicitly requests messages). Set to false to use a Push Subscription (messages are automatically delivered). | true | boolean |
| **queueName** (consumer) | The Queue name if we are using nats for a queue configuration. |  | String |
| **replyToDisabled** (consumer) | Can be used to turn off sending back reply message in the consumer. | false | boolean |
| **consumerConfiguration** (consumer (advanced)) | Sets a custom ConsumerConfiguration object for the JetStream consumer. This is an advanced option typically used when you need to configure properties not exposed as simple Camel URI parameters. When set, this object will be used to build the final consumer subscription options. |  | ConsumerConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **replySubject** (producer) | the subject to which subscribers should send response. |  | String |
| **requestTimeout** (producer) | Request timeout in milliseconds. | 20000 | long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **connection** (advanced) | Reference an already instantiated connection to Nats server. |  | Connection |
| **headerFilterStrategy** (advanced) | To use a custom header filter strategy. |  | HeaderFilterStrategy |
| **jetstreamAsync** (advanced) | Sets whether to operate JetStream requests asynchronously. | true | boolean |
| **traceConnection** (advanced) | Whether or not connection trace messages should be printed to standard out for fine grained debugging of connection issues. | false | boolean |
| **credentialsFilePath** (security) | If we use useCredentialsFile to true we’ll need to set the credentialsFilePath option. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **secure** (security) | Set secure option indicating TLS is required. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Nats endpoint is configured using URI syntax:

nats:topic

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topic** (common) | **Required** The name of topic we want to use. |  | String |

### Query Parameters (42 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (common) | Timeout for connection attempts. (in milliseconds). | 2000 | int |
| **flushConnection** (common) | Define if we want to flush connection when stopping or not. | true | boolean |
| **flushTimeout** (common) | Set the flush timeout (in milliseconds). | 1000 | int |
| **jetstreamEnabled** (common) | Sets whether to enable JetStream support for this endpoint. | false | boolean |
| **jetstreamName** (common) | Sets the name of the JetStream stream to use. |  | String |
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
| **ackPolicy** (consumer) | 
Acknowledgement mode. none = Messages are acknowledged as soon as the server sends them (danger: messages that Camel failed to process is also ack). Clients do not need to ack. all = All messages with a sequence number less than the message acked are also acknowledged. E.g. reading a batch of messages 1..100. Ack on message 100 will acknowledge 1..99 as well. explicit (default) = Each message is acknowledged individually by Camel after the message has been processed, this ensures the message is only ack if success and nack if processing failed due to an exception during routing. Message can be acked out of sequence and create gaps of unacknowledged messages in the consumer.

Enum values:

-   None
    
-   All
    
-   Explicit
    





 | Explicit | AckPolicy |
| **ackWait** (consumer) | After a message is delivered to a consumer, the server waits 30 seconds (default) for an acknowledgement. If none arrives (timeout), the message becomes eligible for redelivery. | 30000 | long |
| **durableName** (consumer) | Sets the name to assign to the JetStream durable consumer. Setting this value makes the consumer durable. The value is used to set the durable() field in the underlying NATS ConsumerConfiguration.Builder. |  | String |
| **maxDeliver** (consumer) | Maximum number of attempts to deliver a message from Nats to a consumer. Once MaxDeliver is reached, the NATS server stops attempting to deliver that specific message. The message is not deleted, it remains in the stream but is simply skipped. It is recommended to set this option to a sensible value in case a message is poison and can not successfully be processed and would always keep failing. |  | long |
| **maxMessages** (consumer) | Stop receiving messages from a topic we are subscribing to after maxMessages. |  | String |
| **nackWait** (consumer) | For negative acknowledgements (NAK), redelivery is delayed by 5 seconds (default). Setting this to 0 or negative makes the redelivery immediately. Be careful as this can cause the consumer to keep re-processing the same message over and over again due to intermediate error that last a while. | 5000 | long |
| **poolSize** (consumer) | Consumer thread pool size (default is 10). | 10 | int |
| **pullBatchSize** (consumer) | Maximum number of messages to fetch per pull request when using a JetStream Pull Subscription. Only used when \\{code pullSubscription=true}. | 10 | int |
| **pullFetchTimeout** (consumer) | Maximum time (in milliseconds) to wait for a batch of messages to be available on the server during a single fetch when using a JetStream Pull Subscription. Only used when \\{code pullSubscription=true}. | 1000 | long |
| **pullSubscription** (consumer) | Sets the consumer subscription type for JetStream. Set to true to use a Pull Subscription (consumer explicitly requests messages). Set to false to use a Push Subscription (messages are automatically delivered). | true | boolean |
| **queueName** (consumer) | The Queue name if we are using nats for a queue configuration. |  | String |
| **replyToDisabled** (consumer) | Can be used to turn off sending back reply message in the consumer. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerConfiguration** (consumer (advanced)) | Sets a custom ConsumerConfiguration object for the JetStream consumer. This is an advanced option typically used when you need to configure properties not exposed as simple Camel URI parameters. When set, this object will be used to build the final consumer subscription options. |  | ConsumerConfiguration |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **replySubject** (producer) | the subject to which subscribers should send response. |  | String |
| **requestTimeout** (producer) | Request timeout in milliseconds. | 20000 | long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connection** (advanced) | Reference an already instantiated connection to Nats server. |  | Connection |
| **headerFilterStrategy** (advanced) | To use a custom header filter strategy. |  | HeaderFilterStrategy |
| **jetstreamAsync** (advanced) | Sets whether to operate JetStream requests asynchronously. | true | boolean |
| **traceConnection** (advanced) | Whether or not connection trace messages should be printed to standard out for fine grained debugging of connection issues. | false | boolean |
| **credentialsFilePath** (security) | If we use useCredentialsFile to true we’ll need to set the credentialsFilePath option. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **secure** (security) | Set secure option indicating TLS is required. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |

## Message Headers

The Nats component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelNatsMessageTimestamp** (common) Constant: [`NATS_MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_MESSAGE_TIMESTAMP) | The timestamp of a consumed message. |  | long |
| **CamelNatsSID** (common) Constant: [`NATS_SID`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_SID) | The SID of a consumed message. |  | String |
| **CamelNatsReplyTo** (common) Constant: [`NATS_REPLY_TO`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_REPLY_TO) | The ReplyTo of a consumed message (may be null). |  | String |
| **CamelNatsSubject** (common) Constant: [`NATS_SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_SUBJECT) | The Subject of a consumed message. |  | String |
| **CamelNatsQueueName** (common) Constant: [`NATS_QUEUE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_QUEUE_NAME) | The Queue name of a consumed message (may be null). |  | String |
| **CamelNatsStatusCode** (consumer) Constant: [`NATS_STATUS_CODE`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_STATUS_CODE) | Status message code. |  | int |
| **CamelNatsStatusError** (consumer) Constant: [`NATS_STATUS_ERROR`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_STATUS_ERROR) | Status message error message. |  | String |
| **CamelNatsDeliveryCounter** (consumer) Constant: [`NATS_DELIVERY_COUNTER`](https://javadoc.io/doc/org.apache.camel/camel-nats/latest/org/apache/camel/component/nats/NatsConstants.html#NATS_DELIVERY_COUNTER) | Number of times this message has been delivered (1 = first, 1 then message has been redelivered). |  | long |

## Usage

### Configuring servers

You configure the NATS servers on either the component or the endpoint.

For example, to configure this once on the component, you can do:

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

If you are using Camel Main or Spring Boot, you can configure the server urls in the `application.properties` file

```properties
camel.component.nats.servers=scott:tiger@someserver:4222,superman:123@someotherserver:42222
```

### Request/Reply support

The producer supports request/reply where it can wait for an expected reply message.

The consumer will, when routing the message is complete, send back the message as reply-message if required.

## Examples

### Producer example

```java
from("direct:send")
  .to("nats:mytopic");
```

In case of using authorization, you can directly specify your credentials in the server URL

```java
from("direct:send")
  .to("nats:mytopic?servers=username:password@localhost:4222");
```

or your token

```java
from("direct:send")
  .to("nats:mytopic?servers=token@localhost:4222);
```

### Consumer example

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

The component supports 42 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.nats.ack-policy** | Acknowledgement mode. none = Messages are acknowledged as soon as the server sends them (danger: messages that Camel failed to process is also ack). Clients do not need to ack. all = All messages with a sequence number less than the message acked are also acknowledged. E.g. reading a batch of messages 1..100. Ack on message 100 will acknowledge 1..99 as well. explicit (default) = Each message is acknowledged individually by Camel after the message has been processed, this ensures the message is only ack if success and nack if processing failed due to an exception during routing. Message can be acked out of sequence and create gaps of unacknowledged messages in the consumer. | explicit | AckPolicy |
| **camel.component.nats.ack-wait** | After a message is delivered to a consumer, the server waits 30 seconds (default) for an acknowledgement. If none arrives (timeout), the message becomes eligible for redelivery. | 30000 | Long |
| **camel.component.nats.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.nats.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.nats.configuration** | To use a shared configuration. The option is a org.apache.camel.component.nats.NatsConfiguration type. |  | NatsConfiguration |
| **camel.component.nats.connection** | Reference an already instantiated connection to Nats server. The option is a io.nats.client.Connection type. |  | Connection |
| **camel.component.nats.connection-timeout** | Timeout for connection attempts. (in milliseconds). | 2000 | Integer |
| **camel.component.nats.consumer-configuration** | Sets a custom ConsumerConfiguration object for the JetStream consumer. This is an advanced option typically used when you need to configure properties not exposed as simple Camel URI parameters. When set, this object will be used to build the final consumer subscription options. The option is a io.nats.client.api.ConsumerConfiguration type. |  | ConsumerConfiguration |
| **camel.component.nats.credentials-file-path** | If we use useCredentialsFile to true we’ll need to set the credentialsFilePath option. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **camel.component.nats.durable-name** | Sets the name to assign to the JetStream durable consumer. Setting this value makes the consumer durable. The value is used to set the durable() field in the underlying NATS ConsumerConfiguration.Builder. |  | String |
| **camel.component.nats.enabled** | Whether to enable auto configuration of the nats component. This is enabled by default. |  | Boolean |
| **camel.component.nats.flush-connection** | Define if we want to flush connection when stopping or not. | true | Boolean |
| **camel.component.nats.flush-timeout** | Set the flush timeout (in milliseconds). | 1000 | Integer |
| **camel.component.nats.header-filter-strategy** | To use a custom header filter strategy. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.nats.jetstream-async** | Sets whether to operate JetStream requests asynchronously. | true | Boolean |
| **camel.component.nats.jetstream-enabled** | Sets whether to enable JetStream support for this endpoint. | false | Boolean |
| **camel.component.nats.jetstream-name** | Sets the name of the JetStream stream to use. |  | String |
| **camel.component.nats.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.nats.max-deliver** | Maximum number of attempts to deliver a message from Nats to a consumer. Once MaxDeliver is reached, the NATS server stops attempting to deliver that specific message. The message is not deleted, it remains in the stream but is simply skipped. It is recommended to set this option to a sensible value in case a message is poison and can not successfully be processed and would always keep failing. |  | Long |
| **camel.component.nats.max-messages** | Stop receiving messages from a topic we are subscribing to after maxMessages. |  | String |
| **camel.component.nats.max-pings-out** | maximum number of pings have not received a response allowed by the client. | 2 | Integer |
| **camel.component.nats.max-reconnect-attempts** | Max reconnection attempts. | 60 | Integer |
| **camel.component.nats.nack-wait** | For negative acknowledgements (NAK), redelivery is delayed by 5 seconds (default). Setting this to 0 or negative makes the redelivery immediately. Be careful as this can cause the consumer to keep re-processing the same message over and over again due to intermediate error that last a while. | 5000 | Long |
| **camel.component.nats.no-echo** | Turn off echo. If supported by the gnatsd version you are connecting to this flag will prevent the server from echoing messages back to the connection if it has subscriptions on the subject being published to. | false | Boolean |
| **camel.component.nats.no-randomize-servers** | Whether or not randomizing the order of servers for the connection attempts. | false | Boolean |
| **camel.component.nats.pedantic** | Whether or not running in pedantic mode (this affects performance). | false | Boolean |
| **camel.component.nats.ping-interval** | Ping interval to be aware if connection is still alive (in milliseconds). | 120000 | Integer |
| **camel.component.nats.pool-size** | Consumer thread pool size (default is 10). | 10 | Integer |
| **camel.component.nats.pull-subscription** | Sets the consumer subscription type for JetStream. Set to true to use a Pull Subscription (consumer explicitly requests messages). Set to false to use a Push Subscription (messages are automatically delivered). | true | Boolean |
| **camel.component.nats.queue-name** | The Queue name if we are using nats for a queue configuration. |  | String |
| **camel.component.nats.reconnect** | Whether or not using reconnection feature. | true | Boolean |
| **camel.component.nats.reconnect-time-wait** | Waiting time before attempts reconnection (in milliseconds). | 2000 | Integer |
| **camel.component.nats.reply-subject** | the subject to which subscribers should send response. |  | String |
| **camel.component.nats.reply-to-disabled** | Can be used to turn off sending back reply message in the consumer. | false | Boolean |
| **camel.component.nats.request-cleanup-interval** | Interval to clean up cancelled/timed out requests. | 5000 | Integer |
| **camel.component.nats.request-timeout** | Request timeout in milliseconds. | 20000 | Long |
| **camel.component.nats.secure** | Set secure option indicating TLS is required. | false | Boolean |
| **camel.component.nats.servers** | URLs to one or more NAT servers. Use comma to separate URLs when specifying multiple servers. |  | String |
| **camel.component.nats.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.nats.trace-connection** | Whether or not connection trace messages should be printed to standard out for fine grained debugging of connection issues. | false | Boolean |
| **camel.component.nats.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.nats.verbose** | Whether or not running in verbose mode. | false | Boolean |