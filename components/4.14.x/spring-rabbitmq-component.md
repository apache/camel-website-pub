# Spring RabbitMQ

**Since Camel 3.8**

**Both producer and consumer are supported**

The Spring RabbitMQ component allows you to produce and consume messages from [RabbitMQ](http://www.rabbitmq.com/) instances. Using the Spring RabbitMQ client.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-rabbitmq</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

spring-rabbitmq:exchangeName?\[options\]

The exchange name determines the exchange to which the produced messages will be sent to. In the case of consumers, the exchange name determines the exchange the queue will be bound to.

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

The Spring RabbitMQ component supports 31 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amqpAdmin** (common) | **Autowired** Optional AMQP Admin service to use for auto declaring elements (queues, exchanges, bindings). |  | AmqpAdmin |
| **connectionFactory** (common) | **Autowired** The connection factory to be use. A connection factory must be configured either on the component or endpoint. |  | ConnectionFactory |
| **testConnectionOnStartup** (common) | Specifies whether to test the connection on startup. This ensures that when Camel starts that all the JMS consumers have a valid connection to the JMS broker. If a connection cannot be granted then Camel throws an exception on startup. This ensures that Camel is not started with failed connections. The JMS producers is tested as well. | false | boolean |
| **autoDeclare** (consumer) | Specifies whether the consumer should auto declare binding between exchange, queue and routing key when starting. Enabling this can be good for development to make it easy to standup exchanges, queues and bindings on the broker. | true | boolean |
| **autoStartup** (consumer) | Specifies whether the consumer container should auto-startup. | true | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **deadLetterExchange** (consumer) | The name of the dead letter exchange. |  | String |
| **deadLetterExchangeType** (consumer) | 
The type of the dead letter exchange.

Enum values:

-   direct
    
-   fanout
    
-   headers
    
-   topic
    





 | direct | String |
| **deadLetterQueue** (consumer) | The name of the dead letter queue. |  | String |
| **deadLetterRoutingKey** (consumer) | The routing key for the dead letter exchange. |  | String |
| **maximumRetryAttempts** (consumer) | How many times a Rabbitmq consumer will retry the same message if Camel failed to process the message. | 5 | int |
| **rejectAndDontRequeue** (consumer) | Whether a Rabbitmq consumer should reject the message without requeuing. This enables failed messages to be sent to a Dead Letter Exchange/Queue, if the broker is so configured. | true | boolean |
| **retryDelay** (consumer) | Delay in msec a Rabbitmq consumer will wait before redelivering a message that Camel failed to process. | 1000 | int |
| **concurrentConsumers** (consumer (advanced)) | The number of consumers. | 1 | int |
| **errorHandler** (consumer (advanced)) | To use a custom ErrorHandler for handling exceptions from the message listener (consumer). |  | ErrorHandler |
| **listenerContainerFactory** (consumer (advanced)) | To use a custom factory for creating and configuring ListenerContainer to be used by the consumer for receiving messages. |  | ListenerContainerFactory |
| **maxConcurrentConsumers** (consumer (advanced)) | The maximum number of consumers (available only with SMLC). |  | Integer |
| **messageListenerContainerType** (consumer (advanced)) | 

The type of the MessageListenerContainer.

Enum values:

-   DMLC
    
-   SMLC
    





 | DMLC | String |
| **prefetchCount** (consumer (advanced)) | Tell the broker how many messages to send to each consumer in a single request. Often this can be set quite high to improve throughput. | 250 | int |
| **retry** (consumer (advanced)) | Custom retry configuration to use. If this is configured then the other settings such as maximumRetryAttempts for retry are not in use. |  | RetryOperationsInterceptor |
| **shutdownTimeout** (consumer (advanced)) | The time to wait for workers in milliseconds after the container is stopped. If any workers are active when the shutdown signal comes they will be allowed to finish processing as long as they can finish within this timeout. | 5000 | long |
| **allowNullBody** (producer) | Whether to allow sending messages with no body. If this option is false and the message body is null, then an MessageConversionException is thrown. | false | boolean |
| **autoDeclareProducer** (producer) | Specifies whether the producer should auto declare binding between exchange, queue and routing key when starting. Enabling this can be good for development to make it easy to standup exchanges, queues and bindings on the broker. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **replyTimeout** (producer) | Specify the timeout in milliseconds to be used when waiting for a reply message when doing request/reply messaging. The default value is 5 seconds. A negative value indicates an indefinite timeout. | 5000 | long |
| **args** (advanced) | Specify arguments for configuring the different RabbitMQ concepts, a different prefix is required for each element: consumer. exchange. queue. binding. dlq.exchange. dlq.queue. dlq.binding. For example to declare a queue with message ttl argument: queue.x-message-ttl=60000. |  | Map |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **ignoreDeclarationExceptions** (advanced) | Switch on ignore exceptions such as mismatched properties when declaring. | false | boolean |
| **messageConverter** (advanced) | To use a custom MessageConverter so you can be in control how to map to/from a org.springframework.amqp.core.Message. |  | MessageConverter |
| **messagePropertiesConverter** (advanced) | To use a custom MessagePropertiesConverter so you can be in control how to map to/from a org.springframework.amqp.core.MessageProperties. |  | MessagePropertiesConverter |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Endpoint Options

The Spring RabbitMQ endpoint is configured using URI syntax:

spring-rabbitmq:exchangeName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **exchangeName** (common) | **Required** The exchange name determines the exchange to which the produced messages will be sent to. In the case of consumers, the exchange name determines the exchange the queue will be bound to. Note: to use default exchange then do not use empty name, but use default instead. |  | String |

### Query Parameters (41 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionFactory** (common) | The connection factory to be use. A connection factory must be configured either on the component or endpoint. |  | ConnectionFactory |
| **deadLetterExchange** (common) | The name of the dead letter exchange. |  | String |
| **deadLetterExchangeType** (common) | 
The type of the dead letter exchange.

Enum values:

-   direct
    
-   fanout
    
-   headers
    
-   topic
    





 | direct | String |
| **deadLetterQueue** (common) | The name of the dead letter queue. |  | String |
| **deadLetterRoutingKey** (common) | The routing key for the dead letter exchange. |  | String |
| **disableReplyTo** (common) | Specifies whether Camel ignores the ReplyTo header in messages. If true, Camel does not send a reply back to the destination specified in the ReplyTo header. You can use this option if you want Camel to consume from a route and you do not want Camel to automatically send back a reply message because another component in your code handles the reply message. You can also use this option if you want to use Camel as a proxy between different message brokers and you want to route message from one system to another. | false | boolean |
| **queues** (common) | The queue(s) to use for consuming or producing messages. Multiple queue names can be separated by comma. If none has been configured then Camel will generate an unique id as the queue name. |  | String |
| **routingKey** (common) | The value of a routing key to use. Default is empty which is not helpful when using the default (or any direct) exchange, but fine if the exchange is a headers exchange for instance. |  | String |
| **testConnectionOnStartup** (common) | Specifies whether to test the connection on startup. This ensures that when Camel starts that all the JMS consumers have a valid connection to the JMS broker. If a connection cannot be granted then Camel throws an exception on startup. This ensures that Camel is not started with failed connections. The JMS producers is tested as well. | false | boolean |
| **acknowledgeMode** (consumer) | 

Flag controlling the behaviour of the container with respect to message acknowledgement. The most common usage is to let the container handle the acknowledgements (so the listener doesn’t need to know about the channel or the message). Set to AcknowledgeMode.MANUAL if the listener will send the acknowledgements itself using Channel.basicAck(long, boolean). Manual acks are consistent with either a transactional or non-transactional channel, but if you are doing no other work on the channel at the same other than receiving a single message then the transaction is probably unnecessary. Set to AcknowledgeMode.NONE to tell the broker not to expect any acknowledgements, and it will assume all messages are acknowledged as soon as they are sent (this is autoack in native Rabbit broker terms). If AcknowledgeMode.NONE then the channel cannot be transactional (so the container will fail on start up if that flag is accidentally set).

Enum values:

-   NONE
    
-   MANUAL
    
-   AUTO
    





 |  | AcknowledgeMode |
| **asyncConsumer** (consumer) | Whether the consumer processes the Exchange asynchronously. If enabled then the consumer may pickup the next message from the queue, while the previous message is being processed asynchronously (by the Asynchronous Routing Engine). This means that messages may be processed not 100% strictly in order. If disabled (as default) then the Exchange is fully processed before the consumer will pickup the next message from the queue. | false | boolean |
| **autoDeclare** (consumer) | Specifies whether the consumer should auto declare binding between exchange, queue and routing key when starting. | true | boolean |
| **autoStartup** (consumer) | Specifies whether the consumer container should auto-startup. | true | boolean |
| **exchangeType** (consumer) | 

The type of the exchange.

Enum values:

-   direct
    
-   fanout
    
-   headers
    
-   topic
    





 | direct | String |
| **exclusive** (consumer) | Set to true for an exclusive consumer. | false | boolean |
| **maximumRetryAttempts** (consumer) | How many times a Rabbitmq consumer will try the same message if Camel failed to process the message (The number of attempts includes the initial try). | 5 | int |
| **noLocal** (consumer) | Set to true for an no-local consumer. | false | boolean |
| **rejectAndDontRequeue** (consumer) | Whether a Rabbitmq consumer should reject the message without requeuing. This enables failed messages to be sent to a Dead Letter Exchange/Queue, if the broker is so configured. | true | boolean |
| **retryDelay** (consumer) | Delay in millis a Rabbitmq consumer will wait before redelivering a message that Camel failed to process. | 1000 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **concurrentConsumers** (consumer (advanced)) | The number of consumers. |  | Integer |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **maxConcurrentConsumers** (consumer (advanced)) | The maximum number of consumers (available only with SMLC). |  | Integer |
| **messageListenerContainerType** (consumer (advanced)) | 

The type of the MessageListenerContainer.

Enum values:

-   DMLC
    
-   SMLC
    





 | DMLC | String |
| **prefetchCount** (consumer (advanced)) | Tell the broker how many messages to send in a single request. Often this can be set quite high to improve throughput. |  | Integer |
| **retry** (consumer (advanced)) | Custom retry configuration to use. If this is configured then the other settings such as maximumRetryAttempts for retry are not in use. |  | RetryOperationsInterceptor |
| **allowNullBody** (producer) | Whether to allow sending messages with no body. If this option is false and the message body is null, then an MessageConversionException is thrown. | false | boolean |
| **autoDeclareProducer** (producer) | Specifies whether the producer should auto declare binding between exchange, queue and routing key when starting. | false | boolean |
| **confirm** (producer) | 

Controls whether to wait for confirms. The connection factory must be configured for publisher confirms and this method. auto = Camel detects if the connection factory uses confirms or not. disabled = Confirms is disabled. enabled = Confirms is enabled.

Enum values:

-   auto
    
-   enabled
    
-   disabled
    





 | auto | String |
| **confirmTimeout** (producer) | Specify the timeout in milliseconds to be used when waiting for a message sent to be confirmed by RabbitMQ when doing send only messaging (InOnly). The default value is 5 seconds. A negative value indicates an indefinite timeout. | 5000 | long |
| **replyTimeout** (producer) | Specify the timeout in milliseconds to be used when waiting for a reply message when doing request/reply (InOut) messaging. The default value is 30 seconds. A negative value indicates an indefinite timeout (Beware that this will cause a memory leak if a reply is not received). | 30000 | long |
| **skipBindQueue** (producer) | If true the queue will not be bound to the exchange after declaring it. | false | boolean |
| **skipDeclareExchange** (producer) | This can be used if we need to declare the queue but not the exchange. | false | boolean |
| **skipDeclareQueue** (producer) | If true the producer will not declare and bind a queue. This can be used for directing messages via an existing routing key. | false | boolean |
| **usePublisherConnection** (producer) | Use a separate connection for publishers and consumers. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **args** (advanced) | Specify arguments for configuring the different RabbitMQ concepts, a different prefix is required for each element: arg.consumer. arg.exchange. arg.queue. arg.binding. arg.dlq.exchange. arg.dlq.queue. arg.dlq.binding. For example to declare a queue with message ttl argument: args=arg.queue.x-message-ttl=60000. This is a multi-value option with prefix: arg. |  | Map |
| **messageConverter** (advanced) | To use a custom MessageConverter so you can be in control how to map to/from a org.springframework.amqp.core.Message. |  | MessageConverter |
| **messagePropertiesConverter** (advanced) | To use a custom MessagePropertiesConverter so you can be in control how to map to/from a org.springframework.amqp.core.MessageProperties. |  | MessagePropertiesConverter |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |

## Message Headers

The Spring RabbitMQ component supports 20 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSpringRabbitmqRoutingOverrideKey** (producer) Constant: [`ROUTING_OVERRIDE_KEY`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#ROUTING_OVERRIDE_KEY) | To override the endpoint configuration’s routing key. |  | String |
| **CamelSpringRabbitmqExchangeOverrideName** (producer) Constant: [`EXCHANGE_OVERRIDE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#EXCHANGE_OVERRIDE_NAME) | To override the endpoint configuration’s exchange name. |  | String |
| **CamelSpringRabbitmqRedelivered** (consumer) Constant: [`REDELIVERED`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#REDELIVERED) | Whether the message was previously delivered and requeued. |  | Boolean |
| **CamelSpringRabbitmqDeliveryTag** (consumer) Constant: [`DELIVERY_TAG`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#DELIVERY_TAG) | Delivery tag for manual acknowledge mode. |  | long |
| **CamelSpringRabbitmqExchangeName** (consumer) Constant: [`EXCHANGE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#EXCHANGE_NAME) | The exchange name that was used when publishing the message. |  | String |
| **CamelSpringRabbitmqRoutingKey** (consumer) Constant: [`ROUTING_KEY`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#ROUTING_KEY) | The routing key that was used when publishing the message. |  | String |
| **CamelSpringRabbitmqDeliveryMode** (common) Constant: [`DELIVERY_MODE`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#DELIVERY_MODE) | The message delivery mode. |  | MessageDeliveryMode |
| **CamelSpringRabbitmqType** (common) Constant: [`TYPE`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#TYPE) | Application-specific message type. |  | String |
| **CamelSpringRabbitmqContentType** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#CONTENT_TYPE) | The message content type. |  | String |
| **CamelSpringRabbitmqContentLength** (common) Constant: [`CONTENT_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#CONTENT_LENGTH) | The message content length. |  | long |
| **CamelSpringRabbitmqContentEncoding** (common) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#CONTENT_ENCODING) | Content encoding used by applications. |  | String |
| **CamelSpringRabbitmqMessageId** (common) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#MESSAGE_ID) | Arbitrary message id. |  | String |
| **CamelSpringRabbitmqCorrelationId** (common) Constant: [`CORRELATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#CORRELATION_ID) | Identifier to correlate RPC responses with requests. |  | String |
| **CamelSpringRabbitmqReplyTo** (common) Constant: [`REPLY_TO`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#REPLY_TO) | Commonly used to name a callback queue. |  | String |
| **CamelSpringRabbitmqExpiration** (common) Constant: [`EXPIRATION`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#EXPIRATION) | Per-message TTL. |  | String |
| **CamelSpringRabbitmqTimestamp** (common) Constant: [`TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#TIMESTAMP) | Application-provided timestamp. |  | Date |
| **CamelSpringRabbitmqUserId** (common) Constant: [`USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#USER_ID) | Validated user id. |  | String |
| **CamelSpringRabbitmqAppId** (common) Constant: [`APP_ID`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#APP_ID) | The application name. |  | String |
| **CamelSpringRabbitmqPriority** (common) Constant: [`PRIORITY`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#PRIORITY) | The message priority. |  | Integer |
| **CamelSpringRabbitmqClusterId** (common) Constant: [`CLUSTER_ID`](https://javadoc.io/doc/org.apache.camel/camel-spring-rabbitmq/latest/org/apache/camel/component/springrabbit/SpringRabbitMQConstants.html#CLUSTER_ID) | The cluster id. |  | String |

## Usage

### Using a connection factory

To connect to RabbitMQ, you need to set up a `ConnectionFactory` (same as with JMS) with the login details such as:

> **Tip**
> It is recommended to use `CachingConnectionFactory` from spring-rabbit as it comes with connection pooling out of the box.

```xml
<bean id="rabbitConnectionFactory" class="org.springframework.amqp.rabbit.connection.CachingConnectionFactory">
  <property name="uri" value="amqp://localhost:5672"/>
</bean>
```

The `ConnectionFactory` is auto-detected by default, so you can do:

```xml
<camelContext>
  <route>
    <from uri="direct:cheese"/>
    <to uri="spring-rabbitmq:foo?routingKey=cheese"/>
  </route>
</camelContext>
```

### Default Exchange Name

To use default exchange name (which would be an empty exchange name in RabbitMQ) then you should use `default` as name in the endpoint uri, such as:

```java
to("spring-rabbitmq:default?routingKey=foo")
```

### Auto declare exchanges, queues and bindings

Before you can send or receive messages from RabbitMQ, then exchanges, queues and bindings must be setup first.

In development mode, it may be desirable to let Camel automatic do this. You can enable this by setting `autoDeclare=true` on the `SpringRabbitMQComponent`.

Then Spring RabbitMQ will automatically declare the necessary elements and set up the binding between the exchange, queue and routing keys.

The elements can be configured using the multivalued `args` option.

For example, to specify the queue as durable and exclusive, you can configure the endpoint uri with `arg.queue.durable=true&arg.queue.exclusive=true`.

**Exchanges**

   
| Option | Type | Description | Default |
| --- | --- | --- | --- |
| autoDelete | boolean | True if the server should delete the exchange when it is no longer in use (if all bindings are deleted). | false |
| durable | boolean | A durable exchange will survive a server restart. | true |

You can also configure any additional `x-` arguments. See details in the RabbitMQ documentation.

**Queues**

   
| Option | Type | Description | Default |
| --- | --- | --- | --- |
| autoDelete | boolean | True if the server should delete the exchange when it is no longer in use (if all bindings are deleted). | false |
| durable | boolean | A durable queue will survive a server restart. | false |
| exclusive | boolean | Whether the queue is exclusive | false |
| x-dead-letter-exchange | String | The name of the dead letter exchange. If none configured, then the component configured value is used. |  |
| x-dead-letter-routing-key | String | The routing key for the dead letter exchange. If none configured, then the component configured value is used. |  |

You can also configure any additional `x-` arguments, such as the message time to live, via `x-message-ttl`, and many others. See details in the RabbitMQ documentation.

### Mapping from Camel to RabbitMQ

The message body is mapped from Camel Message body to a `byte[]` which is the type that RabbitMQ uses for message body. Camel will use its type converter to convert the message body to a byte array.

Spring Rabbit comes out of the box with support for mapping Java serialized objects, but Camel Spring RabbitMQ does **not** support this due to security vulnerabilities and using Java objects is a bad design as it enforces strong coupling.

Custom message headers are mapped from Camel Message headers to RabbitMQ headers. This behaviour can be customized by configuring a new implementation of `HeaderFilterStrategy` on the Camel component.

### Request / Reply

Request and reply messaging is supported using [RabbitMQ direct reply-to](https://www.rabbitmq.com/direct-reply-to.md).

The example below will do request/reply, where the message is sent via the cheese exchange name and routing key `foo.bar`, which is being consumed by the second Camel route, that prepends the message with \`Hello \`, and then sends back the message.

So if we send `World` as message body to _direct:start_ then, we will se the message being logged

-   `log:request → World`
    
-   `log:input → World`
    
-   `log:response → Hello World`
    

```java
from("direct:start")
    .to("log:request")
    .to(ExchangePattern.InOut, "spring-rabbitmq:cheese?routingKey=foo.bar")
    .to("log:response");

from("spring-rabbitmq:cheese?queues=myqueue&routingKey=foo.bar")
    .to("log:input")
    .transform(body().prepend("Hello "));
```

### Reuse endpoint and send to different destinations computed at runtime

If you need to send messages to a lot of different RabbitMQ exchanges, it makes sense to reuse an endpoint and specify the real destination in a message header. This allows Camel to reuse the same endpoint, but send to different exchanges. This greatly reduces the number of endpoints created and economizes on memory and thread resources.

> **Tip**
> Using [toD](eips/toD-eip.md) is easier than specifying the dynamic destination with headers

You can specify using the following headers:

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelSpringRabbitmqExchangeOverrideName` | `String` | The exchange name. |
| `CamelSpringRabbitmqRoutingOverrideKey` | `String` | The routing key. |

For example, the following route shows how you can compute a destination at run time and use it to override the exchange appearing in the endpoint URL:

```java
from("file://inbox")
  .to("bean:computeDestination")
  .to("spring-rabbitmq:dummy");
```

The exchange name, `dummy`, is just a placeholder. It must be provided as part of the RabbitMQ endpoint URL, but it will be ignored in this example.

In the `computeDestination` bean, specify the real destination by setting the `CamelRabbitmqExchangeOverrideName` header as follows:

```java
public void setExchangeHeader(Exchange exchange) {
   String region = ....
   exchange.getIn().setHeader("CamelSpringRabbitmqExchangeOverrideName", "order-" + region);
}
```

Then Camel will read this header and use it as the exchange name instead of the one configured on the endpoint. So, in this example Camel sends the message to `spring-rabbitmq:order-emea`, assuming the `region` value was `emea`.

Keep in mind that the producer removes both `CamelSpringRabbitmqExchangeOverrideName` and `CamelSpringRabbitmqRoutingOverrideKey` headers from the exchange and do not propagate them to the created Rabbitmq message to avoid the accidental loops in the routes (in scenarios when the message will be forwarded to another RabbitMQ endpoint).

### Using toD

If you need to send messages to a lot of different exchanges, it makes sense to reuse an endpoint and specify the dynamic destinations with simple language using [toD](eips/toD-eip.md).

For example, suppose you need to send messages to exchanges with order types, then using toD could, for example, be done as follows:

Example SJMS2 route with `toD`

```java
from("direct:order")
  .toD("spring-rabbit:order-${header.orderType}");
```

### Manual Acknowledgement

If we need to manually acknowledge a message for some use case, we can do it by setting and acknowledgeMode to Manual and using the below snippet of code to get Channel and deliveryTag to manually acknowledge the message:

```java
from("spring-rabbitmq:%s?queues=%s&acknowledgeMode=MANUAL")
    .process(exchange -> {
        Channel channel = exchange.getProperty(SpringRabbitMQConstants.CHANNEL, Channel.class);
        long deliveryTag = exchange.getMessage().getHeader(SpringRabbitMQConstants.DELIVERY_TAG, long.class);
        channel.basicAck(deliveryTag, false);
    })
```

## Spring Boot Auto-Configuration

When using spring-rabbitmq with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-spring-rabbitmq-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 32 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.spring-rabbitmq.allow-null-body** | Whether to allow sending messages with no body. If this option is false and the message body is null, then an MessageConversionException is thrown. | false | Boolean |
| **camel.component.spring-rabbitmq.amqp-admin** | Optional AMQP Admin service to use for auto declaring elements (queues, exchanges, bindings). The option is a org.springframework.amqp.core.AmqpAdmin type. |  | AmqpAdmin |
| **camel.component.spring-rabbitmq.args** | Specify arguments for configuring the different RabbitMQ concepts, a different prefix is required for each element: consumer. exchange. queue. binding. dlq.exchange. dlq.queue. dlq.binding. For example to declare a queue with message ttl argument: queue.x-message-ttl=60000. |  | Map |
| **camel.component.spring-rabbitmq.auto-declare** | Specifies whether the consumer should auto declare binding between exchange, queue and routing key when starting. Enabling this can be good for development to make it easy to standup exchanges, queues and bindings on the broker. | true | Boolean |
| **camel.component.spring-rabbitmq.auto-declare-producer** | Specifies whether the producer should auto declare binding between exchange, queue and routing key when starting. Enabling this can be good for development to make it easy to standup exchanges, queues and bindings on the broker. | false | Boolean |
| **camel.component.spring-rabbitmq.auto-startup** | Specifies whether the consumer container should auto-startup. | true | Boolean |
| **camel.component.spring-rabbitmq.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.spring-rabbitmq.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.spring-rabbitmq.concurrent-consumers** | The number of consumers. | 1 | Integer |
| **camel.component.spring-rabbitmq.connection-factory** | The connection factory to be use. A connection factory must be configured either on the component or endpoint. The option is a org.springframework.amqp.rabbit.connection.ConnectionFactory type. |  | ConnectionFactory |
| **camel.component.spring-rabbitmq.dead-letter-exchange** | The name of the dead letter exchange. |  | String |
| **camel.component.spring-rabbitmq.dead-letter-exchange-type** | The type of the dead letter exchange. | direct | String |
| **camel.component.spring-rabbitmq.dead-letter-queue** | The name of the dead letter queue. |  | String |
| **camel.component.spring-rabbitmq.dead-letter-routing-key** | The routing key for the dead letter exchange. |  | String |
| **camel.component.spring-rabbitmq.enabled** | Whether to enable auto configuration of the spring-rabbitmq component. This is enabled by default. |  | Boolean |
| **camel.component.spring-rabbitmq.error-handler** | To use a custom ErrorHandler for handling exceptions from the message listener (consumer). The option is a org.springframework.util.ErrorHandler type. |  | ErrorHandler |
| **camel.component.spring-rabbitmq.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.spring-rabbitmq.ignore-declaration-exceptions** | Switch on ignore exceptions such as mismatched properties when declaring. | false | Boolean |
| **camel.component.spring-rabbitmq.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.spring-rabbitmq.listener-container-factory** | To use a custom factory for creating and configuring ListenerContainer to be used by the consumer for receiving messages. The option is a org.apache.camel.component.springrabbit.ListenerContainerFactory type. |  | ListenerContainerFactory |
| **camel.component.spring-rabbitmq.max-concurrent-consumers** | The maximum number of consumers (available only with SMLC). |  | Integer |
| **camel.component.spring-rabbitmq.maximum-retry-attempts** | How many times a Rabbitmq consumer will retry the same message if Camel failed to process the message. | 5 | Integer |
| **camel.component.spring-rabbitmq.message-converter** | To use a custom MessageConverter so you can be in control how to map to/from a org.springframework.amqp.core.Message. The option is a org.springframework.amqp.support.converter.MessageConverter type. |  | MessageConverter |
| **camel.component.spring-rabbitmq.message-listener-container-type** | The type of the MessageListenerContainer. | DMLC | String |
| **camel.component.spring-rabbitmq.message-properties-converter** | To use a custom MessagePropertiesConverter so you can be in control how to map to/from a org.springframework.amqp.core.MessageProperties. The option is a org.apache.camel.component.springrabbit.MessagePropertiesConverter type. |  | MessagePropertiesConverter |
| **camel.component.spring-rabbitmq.prefetch-count** | Tell the broker how many messages to send to each consumer in a single request. Often this can be set quite high to improve throughput. | 250 | Integer |
| **camel.component.spring-rabbitmq.reject-and-dont-requeue** | Whether a Rabbitmq consumer should reject the message without requeuing. This enables failed messages to be sent to a Dead Letter Exchange/Queue, if the broker is so configured. | true | Boolean |
| **camel.component.spring-rabbitmq.reply-timeout** | Specify the timeout in milliseconds to be used when waiting for a reply message when doing request/reply messaging. The default value is 5 seconds. A negative value indicates an indefinite timeout. The option is a long type. | 5000 | Long |
| **camel.component.spring-rabbitmq.retry** | Custom retry configuration to use. If this is configured then the other settings such as maximumRetryAttempts for retry are not in use. The option is a org.springframework.retry.interceptor.RetryOperationsInterceptor type. |  | RetryOperationsInterceptor |
| **camel.component.spring-rabbitmq.retry-delay** | Delay in msec a Rabbitmq consumer will wait before redelivering a message that Camel failed to process. | 1000 | Integer |
| **camel.component.spring-rabbitmq.shutdown-timeout** | The time to wait for workers in milliseconds after the container is stopped. If any workers are active when the shutdown signal comes they will be allowed to finish processing as long as they can finish within this timeout. The option is a long type. | 5000 | Long |
| **camel.component.spring-rabbitmq.test-connection-on-startup** | Specifies whether to test the connection on startup. This ensures that when Camel starts that all the JMS consumers have a valid connection to the JMS broker. If a connection cannot be granted then Camel throws an exception on startup. This ensures that Camel is not started with failed connections. The JMS producers is tested as well. | false | Boolean |