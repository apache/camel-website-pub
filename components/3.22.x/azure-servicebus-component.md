# Azure ServiceBus

**Since Camel 3.12**

**Both producer and consumer are supported**

The azure-servicebus component that integrates [Azure ServiceBus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview). Azure ServiceBus is a fully managed enterprise integration message broker. Service Bus can decouple applications and services. Service Bus offers a reliable and secure platform for asynchronous transfer of data and state. Data is transferred between different applications and services using messages.

Prerequisites

You must have a valid Windows Azure Storage account. More information is available at [Azure Documentation Portal](https://docs.microsoft.com/azure/).

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-servicebus</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The Azure ServiceBus component supports 25 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amqpRetryOptions** (common) | Sets the retry options for Service Bus clients. If not specified, the default retry options are used. |  | AmqpRetryOptions |
| **amqpTransportType** (common) | 
Sets the transport type by which all the communication with Azure Service Bus occurs. Default value is AmqpTransportType#AMQP.

Enum values:

-   Amqp
    
-   AmqpWebSockets
    





 | AMQP | AmqpTransportType |
| **clientOptions** (common) | Sets the ClientOptions to be sent from the client built from this builder, enabling customization of certain properties, as well as support the addition of custom header information. Refer to the ClientOptions documentation for more information. |  | ClientOptions |
| **configuration** (common) | The component configurations. |  | ServiceBusConfiguration |
| **proxyOptions** (common) | Sets the proxy configuration to use for ServiceBusSenderAsyncClient. When a proxy is configured, AmqpTransportType#AMQP\_WEB\_SOCKETS must be used for the transport type. |  | ProxyOptions |
| **serviceBusType** (common) | 

**Required** The service bus type of connection to execute. Queue is for typical queue option and topic for subscription based model.

Enum values:

-   queue
    
-   topic
    





 | queue | ServiceBusType |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerOperation** (consumer) | 

Sets the desired operation to be used in the consumer.

Enum values:

-   receiveMessages
    
-   peekMessages
    





 | receiveMessages | ServiceBusConsumerOperationDefinition |
| **disableAutoComplete** (consumer) | Disables auto-complete and auto-abandon of received messages. By default, a successfully processed message is \\{link ServiceBusReceiverAsyncClient#complete(ServiceBusReceivedMessage) completed}. If an error happens when the message is processed, it is \\{link ServiceBusReceiverAsyncClient#abandon(ServiceBusReceivedMessage) abandoned}. | false | boolean |
| **maxAutoLockRenewDuration** (consumer) | Sets the amount of time to continue auto-renewing the lock. Setting Duration#ZERO or null disables auto-renewal. For \\{link ServiceBusReceiveMode#RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE} mode, auto-renewal is disabled. | 5m | Duration |
| **peekNumMaxMessages** (consumer) | Set the max number of messages to be peeked during the peek operation. |  | Integer |
| **prefetchCount** (consumer) | Sets the prefetch count of the receiver. For both \\{link ServiceBusReceiveMode#PEEK\_LOCK PEEK\_LOCK} and \\{link ServiceBusReceiveMode#RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE} modes the default value is 1. Prefetch speeds up the message flow by aiming to have a message readily available for local retrieval when and before the application asks for one using ServiceBusReceiverAsyncClient#receiveMessages(). Setting a non-zero value will prefetch that number of messages. Setting the value to zero turns prefetch off. |  | int |
| **receiverAsyncClient** (consumer) | **Autowired** Sets the receiverAsyncClient in order to consume messages by the consumer. |  | ServiceBusReceiverAsyncClient |
| **serviceBusReceiveMode** (consumer) | 

Sets the receive mode for the receiver.

Enum values:

-   PEEK\_LOCK
    
-   RECEIVE\_AND\_DELETE
    





 | PEEK\_LOCK | ServiceBusReceiveMode |
| **subQueue** (consumer) | 

Sets the type of the SubQueue to connect to.

Enum values:

-   NONE
    
-   DEAD\_LETTER\_QUEUE
    
-   TRANSFER\_DEAD\_LETTER\_QUEUE
    





 |  | SubQueue |
| **subscriptionName** (consumer) | Sets the name of the subscription in the topic to listen to. topicOrQueueName and serviceBusType=topic must also be set. This property is required if serviceBusType=topic and the consumer is in use. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **producerOperation** (producer) | 

Sets the desired operation to be used in the producer.

Enum values:

-   sendMessages
    
-   scheduleMessages
    





 | sendMessages | ServiceBusProducerOperationDefinition |
| **scheduledEnqueueTime** (producer) | Sets OffsetDateTime at which the message should appear in the Service Bus queue or topic. |  | OffsetDateTime |
| **senderAsyncClient** (producer) | **Autowired** Sets SenderAsyncClient to be used in the producer. |  | ServiceBusSenderAsyncClient |
| **serviceBusTransactionContext** (producer) | Represents transaction in service. This object just contains transaction id. |  | ServiceBusTransactionContext |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **connectionString** (security) | Sets the connection string for a Service Bus namespace or a specific Service Bus resource. |  | String |
| **fullyQualifiedNamespace** (security) | Fully Qualified Namespace of the service bus. |  | String |
| **tokenCredential** (security) | A TokenCredential for Azure AD authentication, implemented in com.azure.identity. |  | TokenCredential |

## Endpoint Options

The Azure ServiceBus endpoint is configured using URI syntax:

azure-servicebus:topicOrQueueName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topicOrQueueName** (common) | Selected topic name or the queue name, that is depending on serviceBusType config. For example if serviceBusType=queue, then this will be the queue name and if serviceBusType=topic, this will be the topic name. |  | String |

### Query Parameters (25 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amqpRetryOptions** (common) | Sets the retry options for Service Bus clients. If not specified, the default retry options are used. |  | AmqpRetryOptions |
| **amqpTransportType** (common) | 
Sets the transport type by which all the communication with Azure Service Bus occurs. Default value is AmqpTransportType#AMQP.

Enum values:

-   Amqp
    
-   AmqpWebSockets
    





 | AMQP | AmqpTransportType |
| **clientOptions** (common) | Sets the ClientOptions to be sent from the client built from this builder, enabling customization of certain properties, as well as support the addition of custom header information. Refer to the ClientOptions documentation for more information. |  | ClientOptions |
| **proxyOptions** (common) | Sets the proxy configuration to use for ServiceBusSenderAsyncClient. When a proxy is configured, AmqpTransportType#AMQP\_WEB\_SOCKETS must be used for the transport type. |  | ProxyOptions |
| **serviceBusType** (common) | 

**Required** The service bus type of connection to execute. Queue is for typical queue option and topic for subscription based model.

Enum values:

-   queue
    
-   topic
    





 | queue | ServiceBusType |
| **consumerOperation** (consumer) | 

Sets the desired operation to be used in the consumer.

Enum values:

-   receiveMessages
    
-   peekMessages
    





 | receiveMessages | ServiceBusConsumerOperationDefinition |
| **disableAutoComplete** (consumer) | Disables auto-complete and auto-abandon of received messages. By default, a successfully processed message is \\{link ServiceBusReceiverAsyncClient#complete(ServiceBusReceivedMessage) completed}. If an error happens when the message is processed, it is \\{link ServiceBusReceiverAsyncClient#abandon(ServiceBusReceivedMessage) abandoned}. | false | boolean |
| **maxAutoLockRenewDuration** (consumer) | Sets the amount of time to continue auto-renewing the lock. Setting Duration#ZERO or null disables auto-renewal. For \\{link ServiceBusReceiveMode#RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE} mode, auto-renewal is disabled. | 5m | Duration |
| **peekNumMaxMessages** (consumer) | Set the max number of messages to be peeked during the peek operation. |  | Integer |
| **prefetchCount** (consumer) | Sets the prefetch count of the receiver. For both \\{link ServiceBusReceiveMode#PEEK\_LOCK PEEK\_LOCK} and \\{link ServiceBusReceiveMode#RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE} modes the default value is 1. Prefetch speeds up the message flow by aiming to have a message readily available for local retrieval when and before the application asks for one using ServiceBusReceiverAsyncClient#receiveMessages(). Setting a non-zero value will prefetch that number of messages. Setting the value to zero turns prefetch off. |  | int |
| **receiverAsyncClient** (consumer) | **Autowired** Sets the receiverAsyncClient in order to consume messages by the consumer. |  | ServiceBusReceiverAsyncClient |
| **serviceBusReceiveMode** (consumer) | 

Sets the receive mode for the receiver.

Enum values:

-   PEEK\_LOCK
    
-   RECEIVE\_AND\_DELETE
    





 | PEEK\_LOCK | ServiceBusReceiveMode |
| **subQueue** (consumer) | 

Sets the type of the SubQueue to connect to.

Enum values:

-   NONE
    
-   DEAD\_LETTER\_QUEUE
    
-   TRANSFER\_DEAD\_LETTER\_QUEUE
    





 |  | SubQueue |
| **subscriptionName** (consumer) | Sets the name of the subscription in the topic to listen to. topicOrQueueName and serviceBusType=topic must also be set. This property is required if serviceBusType=topic and the consumer is in use. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **producerOperation** (producer) | 

Sets the desired operation to be used in the producer.

Enum values:

-   sendMessages
    
-   scheduleMessages
    





 | sendMessages | ServiceBusProducerOperationDefinition |
| **scheduledEnqueueTime** (producer) | Sets OffsetDateTime at which the message should appear in the Service Bus queue or topic. |  | OffsetDateTime |
| **senderAsyncClient** (producer) | **Autowired** Sets SenderAsyncClient to be used in the producer. |  | ServiceBusSenderAsyncClient |
| **serviceBusTransactionContext** (producer) | Represents transaction in service. This object just contains transaction id. |  | ServiceBusTransactionContext |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connectionString** (security) | Sets the connection string for a Service Bus namespace or a specific Service Bus resource. |  | String |
| **fullyQualifiedNamespace** (security) | Fully Qualified Namespace of the service bus. |  | String |
| **tokenCredential** (security) | A TokenCredential for Azure AD authentication, implemented in com.azure.identity. |  | TokenCredential |

## Async Consumer and Producer

This component implements the async Consumer and producer.

This allows camel route to consume and produce events asynchronously without blocking any threads.

## Usage

## Message Headers

The Azure ServiceBus component supports 25 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureServiceBusApplicationProperties** (common) Constant: [`APPLICATION_PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#APPLICATION_PROPERTIES) | The application properties (also known as custom properties) on messages sent and received by the producer and consumer, respectively. |  | Map |
| **CamelAzureServiceBusContentType** (consumer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#CONTENT_TYPE) | Gets the content type of the message. |  | String |
| **CamelAzureServiceBusCorrelationId** (consumer) Constant: [`CORRELATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#CORRELATION_ID) | Gets a correlation identifier. |  | String |
| **CamelAzureServiceBusDeadLetterErrorDescription** (consumer) Constant: [`DEAD_LETTER_ERROR_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#DEAD_LETTER_ERROR_DESCRIPTION) | Gets the description for a message that has been dead-lettered. |  | String |
| **CamelAzureServiceBusDeadLetterReason** (consumer) Constant: [`DEAD_LETTER_REASON`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#DEAD_LETTER_REASON) | Gets the reason a message was dead-lettered. |  | String |
| **CamelAzureServiceBusDeadLetterSource** (consumer) Constant: [`DEAD_LETTER_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#DEAD_LETTER_SOURCE) | Gets the name of the queue or subscription that this message was enqueued on, before it was dead-lettered. |  | String |
| **CamelAzureServiceBusDeliveryCount** (consumer) Constant: [`DELIVERY_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#DELIVERY_COUNT) | Gets the number of the times this message was delivered to clients. |  | long |
| **CamelAzureServiceBusEnqueuedSequenceNumber** (consumer) Constant: [`ENQUEUED_SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#ENQUEUED_SEQUENCE_NUMBER) | Gets the enqueued sequence number assigned to a message by Service Bus. |  | long |
| **CamelAzureServiceBusEnqueuedTime** (consumer) Constant: [`ENQUEUED_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#ENQUEUED_TIME) | Gets the datetime at which this message was enqueued in Azure Service Bus. |  | OffsetDateTime |
| **CamelAzureServiceBusExpiresAt** (consumer) Constant: [`EXPIRES_AT`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#EXPIRES_AT) | Gets the datetime at which this message will expire. |  | OffsetDateTime |
| **CamelAzureServiceBusLockToken** (consumer) Constant: [`LOCK_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#LOCK_TOKEN) | Gets the lock token for the current message. |  | String |
| **CamelAzureServiceBusLockedUntil** (consumer) Constant: [`LOCKED_UNTIL`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#LOCKED_UNTIL) | Gets the datetime at which the lock of this message expires. |  | OffsetDateTime |
| **CamelAzureServiceBusMessageId** (consumer) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#MESSAGE_ID) | Gets the identifier for the message. |  | String |
| **CamelAzureServiceBusPartitionKey** (consumer) Constant: [`PARTITION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#PARTITION_KEY) | Gets the partition key for sending a message to a partitioned entity. |  | String |
| **CamelAzureServiceBusRawAmqpMessage** (consumer) Constant: [`RAW_AMQP_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#RAW_AMQP_MESSAGE) | The representation of message as defined by AMQP protocol. |  | AmqpAnnotatedMessage |
| **CamelAzureServiceBusReplyTo** (consumer) Constant: [`REPLY_TO`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#REPLY_TO) | Gets the address of an entity to send replies to. |  | String |
| **CamelAzureServiceBusReplyToSessionId** (consumer) Constant: [`REPLY_TO_SESSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#REPLY_TO_SESSION_ID) | Gets or sets a session identifier augmenting the ReplyTo address. |  | String |
| **CamelAzureServiceBusSequenceNumber** (consumer) Constant: [`SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#SEQUENCE_NUMBER) | Gets the unique number assigned to a message by Service Bus. |  | long |
| **CamelAzureServiceBusSessionId** (consumer) Constant: [`SESSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#SESSION_ID) | Gets the session id of the message. |  | String |
| **CamelAzureServiceBusSubject** (consumer) Constant: [`SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#SUBJECT) | Gets the subject for the message. |  | String |
| **CamelAzureServiceBusTimeToLive** (consumer) Constant: [`TIME_TO_LIVE`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#TIME_TO_LIVE) | Gets the duration before this message expires. |  | Duration |
| **CamelAzureServiceBusTo** (consumer) Constant: [`TO`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#TO) | Gets the to address. |  | String |
| **CamelAzureServiceBusScheduledEnqueueTime** (common) Constant: [`SCHEDULED_ENQUEUE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#SCHEDULED_ENQUEUE_TIME) | (producer)Overrides the OffsetDateTime at which the message should appear in the Service Bus queue or topic. (consumer) Gets the scheduled enqueue time of this message. |  | OffsetDateTime |
| **CamelAzureServiceBusServiceBusTransactionContext** (producer) Constant: [`SERVICE_BUS_TRANSACTION_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#SERVICE_BUS_TRANSACTION_CONTEXT) | Overrides the transaction in service. This object just contains transaction id. |  | ServiceBusTransactionContext |
| **CamelAzureServiceBusProducerOperation** (producer) Constant: [`PRODUCER_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#PRODUCER_OPERATION) | 
Overrides the desired operation to be used in the producer.

Enum values:

-   sendMessages
    
-   scheduleMessages
    





 |  | ServiceBusProducerOperationDefinition |

### Message Body

In the producer, this component accepts message body of `String` type or `List<String>` to send batch messages.

In the consumer, the returned message body will be of type \`String.

### Azure ServiceBus Producer operations

 
| Operation | Description |
| --- | --- |
| `sendMessages` | Sends a set of messages to a Service Bus queue or topic using a batched approach. |
| `scheduleMessages` | Sends a scheduled message to the Azure Service Bus entity this sender is connected to. A scheduled message is enqueued and made available to receivers only at the scheduled enqueue time. |

### Azure ServiceBus Consumer operations

 
| Operation | Description |
| --- | --- |
| `receiveMessages` | Receives an <b>infinite</b> stream of messages from the Service Bus entity. |
| `peekMessages` | Reads the next batch of active messages without changing the state of the receiver or the message source. |

#### Examples

-   `sendMessages`
    

```java
from("direct:start")
  .process(exchange -> {
         final List<Object> inputBatch = new LinkedList<>();
            inputBatch.add("test batch 1");
            inputBatch.add("test batch 2");
            inputBatch.add("test batch 3");
            inputBatch.add(123456);

            exchange.getIn().setBody(inputBatch);
       })
  .to("azure-servicebus:test//?connectionString=test")
  .to("mock:result");
```

-   `scheduleMessages`
    

```java
from("direct:start")
  .process(exchange -> {
         final List<Object> inputBatch = new LinkedList<>();
            inputBatch.add("test batch 1");
            inputBatch.add("test batch 2");
            inputBatch.add("test batch 3");
            inputBatch.add(123456);

            exchange.getIn().setHeader(ServiceBusConstants.SCHEDULED_ENQUEUE_TIME, OffsetDateTime.now());
            exchange.getIn().setBody(inputBatch);
       })
  .to("azure-servicebus:test//?connectionString=test&producerOperation=scheduleMessages")
  .to("mock:result");
```

-   `receiveMessages`
    

```java
from("azure-servicebus:test//?connectionString=test")
  .log("${body}")
  .to("mock:result");
```

-   `peekMessages`
    

```java
from("azure-servicebus:test//?connectionString=test&consumerOperation=peekMessages&peekNumMaxMessages=3")
  .log("${body}")
  .to("mock:result");
```

## Spring Boot Auto-Configuration

When using azure-servicebus with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-azure-servicebus-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 26 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.azure-servicebus.amqp-retry-options** | Sets the retry options for Service Bus clients. If not specified, the default retry options are used. The option is a com.azure.core.amqp.AmqpRetryOptions type. |  | AmqpRetryOptions |
| **camel.component.azure-servicebus.amqp-transport-type** | Sets the transport type by which all the communication with Azure Service Bus occurs. Default value is AmqpTransportType#AMQP. |  | AmqpTransportType |
| **camel.component.azure-servicebus.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.azure-servicebus.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.azure-servicebus.client-options** | Sets the ClientOptions to be sent from the client built from this builder, enabling customization of certain properties, as well as support the addition of custom header information. Refer to the ClientOptions documentation for more information. The option is a com.azure.core.util.ClientOptions type. |  | ClientOptions |
| **camel.component.azure-servicebus.configuration** | The component configurations. The option is a org.apache.camel.component.azure.servicebus.ServiceBusConfiguration type. |  | ServiceBusConfiguration |
| **camel.component.azure-servicebus.connection-string** | Sets the connection string for a Service Bus namespace or a specific Service Bus resource. |  | String |
| **camel.component.azure-servicebus.consumer-operation** | Sets the desired operation to be used in the consumer. |  | ServiceBusConsumerOperationDefinition |
| **camel.component.azure-servicebus.disable-auto-complete** | Disables auto-complete and auto-abandon of received messages. By default, a successfully processed message is \\{link ServiceBusReceiverAsyncClient#complete(ServiceBusReceivedMessage) completed}. If an error happens when the message is processed, it is \\{link ServiceBusReceiverAsyncClient#abandon(ServiceBusReceivedMessage) abandoned}. | false | Boolean |
| **camel.component.azure-servicebus.enabled** | Whether to enable auto configuration of the azure-servicebus component. This is enabled by default. |  | Boolean |
| **camel.component.azure-servicebus.fully-qualified-namespace** | Fully Qualified Namespace of the service bus. |  | String |
| **camel.component.azure-servicebus.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.azure-servicebus.max-auto-lock-renew-duration** | Sets the amount of time to continue auto-renewing the lock. Setting Duration#ZERO or null disables auto-renewal. For \\{link ServiceBusReceiveMode#RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE} mode, auto-renewal is disabled. The option is a java.time.Duration type. |  | Duration |
| **camel.component.azure-servicebus.peek-num-max-messages** | Set the max number of messages to be peeked during the peek operation. |  | Integer |
| **camel.component.azure-servicebus.prefetch-count** | Sets the prefetch count of the receiver. For both \\{link ServiceBusReceiveMode#PEEK\_LOCK PEEK\_LOCK} and \\{link ServiceBusReceiveMode#RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE} modes the default value is 1. Prefetch speeds up the message flow by aiming to have a message readily available for local retrieval when and before the application asks for one using ServiceBusReceiverAsyncClient#receiveMessages(). Setting a non-zero value will prefetch that number of messages. Setting the value to zero turns prefetch off. |  | Integer |
| **camel.component.azure-servicebus.producer-operation** | Sets the desired operation to be used in the producer. |  | ServiceBusProducerOperationDefinition |
| **camel.component.azure-servicebus.proxy-options** | Sets the proxy configuration to use for ServiceBusSenderAsyncClient. When a proxy is configured, AmqpTransportType#AMQP\_WEB\_SOCKETS must be used for the transport type. The option is a com.azure.core.amqp.ProxyOptions type. |  | ProxyOptions |
| **camel.component.azure-servicebus.receiver-async-client** | Sets the receiverAsyncClient in order to consume messages by the consumer. The option is a com.azure.messaging.servicebus.ServiceBusReceiverAsyncClient type. |  | ServiceBusReceiverAsyncClient |
| **camel.component.azure-servicebus.scheduled-enqueue-time** | Sets OffsetDateTime at which the message should appear in the Service Bus queue or topic. The option is a java.time.OffsetDateTime type. |  | OffsetDateTime |
| **camel.component.azure-servicebus.sender-async-client** | Sets SenderAsyncClient to be used in the producer. The option is a com.azure.messaging.servicebus.ServiceBusSenderAsyncClient type. |  | ServiceBusSenderAsyncClient |
| **camel.component.azure-servicebus.service-bus-receive-mode** | Sets the receive mode for the receiver. |  | ServiceBusReceiveMode |
| **camel.component.azure-servicebus.service-bus-transaction-context** | Represents transaction in service. This object just contains transaction id. The option is a com.azure.messaging.servicebus.ServiceBusTransactionContext type. |  | ServiceBusTransactionContext |
| **camel.component.azure-servicebus.service-bus-type** | The service bus type of connection to execute. Queue is for typical queue option and topic for subscription based model. |  | ServiceBusType |
| **camel.component.azure-servicebus.sub-queue** | Sets the type of the SubQueue to connect to. |  | SubQueue |
| **camel.component.azure-servicebus.subscription-name** | Sets the name of the subscription in the topic to listen to. topicOrQueueName and serviceBusType=topic must also be set. This property is required if serviceBusType=topic and the consumer is in use. |  | String |
| **camel.component.azure-servicebus.token-credential** | A TokenCredential for Azure AD authentication, implemented in com.azure.identity. The option is a com.azure.core.credential.TokenCredential type. |  | TokenCredential |