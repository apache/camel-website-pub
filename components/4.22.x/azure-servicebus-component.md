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

The Azure ServiceBus component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amqpRetryOptions** (common) | Sets the retry options for Service Bus clients. If not specified, the default retry options are used. |  | AmqpRetryOptions |
| **amqpTransportType** (common) | 
Sets the transport type by which all the communication with Azure Service Bus occurs. Default value is AMQP.

Enum values:

-   Amqp
    
-   AmqpWebSockets
    





 | AMQP | AmqpTransportType |
| **clientOptions** (common) | Sets the ClientOptions to be sent from the client built from this builder, enabling customization of certain properties, as well as support the addition of custom header information. |  | ClientOptions |
| **configuration** (common) | The component configurations. |  | ServiceBusConfiguration |
| **headerFilterStrategy** (common) | To use a custom HeaderFilterStrategy to filter Service Bus application properties to and from Camel message headers. |  | HeaderFilterStrategy |
| **proxyOptions** (common) | Sets the proxy configuration to use for ServiceBusSenderClient. When a proxy is configured, AMQP\_WEB\_SOCKETS must be used for the transport type. |  | ProxyOptions |
| **serviceBusType** (common) | 

**Required** The service bus type of connection to execute. Queue is for typical queue option and topic for subscription based model.

Enum values:

-   queue
    
-   topic
    





 | queue | ServiceBusType |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **enableDeadLettering** (consumer) | Enable application level deadlettering to the subscription deadletter subqueue if deadletter related headers are set. | false | boolean |
| **maxAutoLockRenewDuration** (consumer) | Sets the amount of time (millis) to continue auto-renewing the lock. Setting ZERO disables auto-renewal. For ServiceBus receive mode (RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE), auto-renewal is disabled. | 300000 | long |
| **maxConcurrentCalls** (consumer) | Sets maximum number of concurrent calls. | 1 | int |
| **prefetchCount** (consumer) | Sets the prefetch count of the receiver. For both PEEK\_LOCK PEEK\_LOCK and RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE receive modes the default value is 1. Prefetch speeds up the message flow by aiming to have a message readily available for local retrieval when and before the application asks for one using receive message. Setting a non-zero value will prefetch that number of messages. Setting the value to zero turns prefetch off. |  | int |
| **processorClient** (consumer) | **Autowired** Sets the processorClient in order to consume messages by the consumer. |  | ServiceBusProcessorClient |
| **serviceBusReceiveMode** (consumer) | 

Sets the receive mode for the receiver.

Enum values:

-   PEEK\_LOCK
    
-   RECEIVE\_AND\_DELETE
    





 | PEEK\_LOCK | ServiceBusReceiveMode |
| **sessionEnabled** (consumer) | Enable session support. | false | boolean |
| **subQueue** (consumer) | 

Sets the type of the SubQueue to connect to.

Enum values:

-   NONE
    
-   DEAD\_LETTER\_QUEUE
    
-   TRANSFER\_DEAD\_LETTER\_QUEUE
    





 |  | SubQueue |
| **subscriptionName** (consumer) | Sets the name of the subscription in the topic to listen to. topicOrQueueName and serviceBusType=topic must also be set. This property is required if serviceBusType=topic and the consumer is in use. |  | String |
| **binary** (producer) | Set binary mode. If true, message body will be sent as byte. By default, it is false. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **producerOperation** (producer) | 

Sets the desired operation to be used in the producer.

Enum values:

-   sendMessages
    
-   scheduleMessages
    





 | sendMessages | ServiceBusProducerOperationDefinition |
| **scheduledEnqueueTime** (producer) | Sets OffsetDateTime at which the message should appear in the Service Bus queue or topic. |  | OffsetDateTime |
| **senderClient** (producer) | **Autowired** Sets senderClient to be used in the producer. |  | ServiceBusSenderClient |
| **serviceBusTransactionContext** (producer) | Represents transaction in service. This object just contains transaction id. |  | ServiceBusTransactionContext |
| **sessionId** (producer) | Session ID for session-enabled queues or topics. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **connectionString** (security) | Sets the connection string for a Service Bus namespace or a specific Service Bus resource. Connection strings commonly contain characters with a special meaning in URIs (the SharedAccessKey is a Base64 value that may contain plus, slash or equals characters): when configuring the connection string directly in an endpoint URI, wrap the value with RAW() so it is not URI-decoded. |  | String |
| **credentialType** (security) | 

Determines the credential strategy to adopt.

Enum values:

-   AZURE\_IDENTITY
    
-   CONNECTION\_STRING
    
-   TOKEN\_CREDENTIAL
    





 | CONNECTION\_STRING | CredentialType |
| **fullyQualifiedNamespace** (security) | Fully Qualified Namespace of the service bus. |  | String |
| **tokenCredential** (security) | **Autowired** A TokenCredential for Azure AD authentication. |  | TokenCredential |

## Endpoint Options

The Azure ServiceBus endpoint is configured using URI syntax:

azure-servicebus:topicOrQueueName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topicOrQueueName** (common) | Selected topic name or the queue name, that is depending on serviceBusType config. For example if serviceBusType=queue, then this will be the queue name and if serviceBusType=topic, this will be the topic name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amqpRetryOptions** (common) | Sets the retry options for Service Bus clients. If not specified, the default retry options are used. |  | AmqpRetryOptions |
| **amqpTransportType** (common) | 
Sets the transport type by which all the communication with Azure Service Bus occurs. Default value is AMQP.

Enum values:

-   Amqp
    
-   AmqpWebSockets
    





 | AMQP | AmqpTransportType |
| **clientOptions** (common) | Sets the ClientOptions to be sent from the client built from this builder, enabling customization of certain properties, as well as support the addition of custom header information. |  | ClientOptions |
| **headerFilterStrategy** (common) | To use a custom HeaderFilterStrategy to filter Service Bus application properties to and from Camel message headers. |  | HeaderFilterStrategy |
| **proxyOptions** (common) | Sets the proxy configuration to use for ServiceBusSenderClient. When a proxy is configured, AMQP\_WEB\_SOCKETS must be used for the transport type. |  | ProxyOptions |
| **serviceBusType** (common) | 

**Required** The service bus type of connection to execute. Queue is for typical queue option and topic for subscription based model.

Enum values:

-   queue
    
-   topic
    





 | queue | ServiceBusType |
| **enableDeadLettering** (consumer) | Enable application level deadlettering to the subscription deadletter subqueue if deadletter related headers are set. | false | boolean |
| **maxAutoLockRenewDuration** (consumer) | Sets the amount of time (millis) to continue auto-renewing the lock. Setting ZERO disables auto-renewal. For ServiceBus receive mode (RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE), auto-renewal is disabled. | 300000 | long |
| **maxConcurrentCalls** (consumer) | Sets maximum number of concurrent calls. | 1 | int |
| **prefetchCount** (consumer) | Sets the prefetch count of the receiver. For both PEEK\_LOCK PEEK\_LOCK and RECEIVE\_AND\_DELETE RECEIVE\_AND\_DELETE receive modes the default value is 1. Prefetch speeds up the message flow by aiming to have a message readily available for local retrieval when and before the application asks for one using receive message. Setting a non-zero value will prefetch that number of messages. Setting the value to zero turns prefetch off. |  | int |
| **processorClient** (consumer) | **Autowired** Sets the processorClient in order to consume messages by the consumer. |  | ServiceBusProcessorClient |
| **serviceBusReceiveMode** (consumer) | 

Sets the receive mode for the receiver.

Enum values:

-   PEEK\_LOCK
    
-   RECEIVE\_AND\_DELETE
    





 | PEEK\_LOCK | ServiceBusReceiveMode |
| **sessionEnabled** (consumer) | Enable session support. | false | boolean |
| **subQueue** (consumer) | 

Sets the type of the SubQueue to connect to.

Enum values:

-   NONE
    
-   DEAD\_LETTER\_QUEUE
    
-   TRANSFER\_DEAD\_LETTER\_QUEUE
    





 |  | SubQueue |
| **subscriptionName** (consumer) | Sets the name of the subscription in the topic to listen to. topicOrQueueName and serviceBusType=topic must also be set. This property is required if serviceBusType=topic and the consumer is in use. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **binary** (producer) | Set binary mode. If true, message body will be sent as byte. By default, it is false. | false | boolean |
| **producerOperation** (producer) | 

Sets the desired operation to be used in the producer.

Enum values:

-   sendMessages
    
-   scheduleMessages
    





 | sendMessages | ServiceBusProducerOperationDefinition |
| **scheduledEnqueueTime** (producer) | Sets OffsetDateTime at which the message should appear in the Service Bus queue or topic. |  | OffsetDateTime |
| **senderClient** (producer) | **Autowired** Sets senderClient to be used in the producer. |  | ServiceBusSenderClient |
| **serviceBusTransactionContext** (producer) | Represents transaction in service. This object just contains transaction id. |  | ServiceBusTransactionContext |
| **sessionId** (producer) | Session ID for session-enabled queues or topics. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connectionString** (security) | Sets the connection string for a Service Bus namespace or a specific Service Bus resource. Connection strings commonly contain characters with a special meaning in URIs (the SharedAccessKey is a Base64 value that may contain plus, slash or equals characters): when configuring the connection string directly in an endpoint URI, wrap the value with RAW() so it is not URI-decoded. |  | String |
| **credentialType** (security) | 

Determines the credential strategy to adopt.

Enum values:

-   AZURE\_IDENTITY
    
-   CONNECTION\_STRING
    
-   TOKEN\_CREDENTIAL
    





 | CONNECTION\_STRING | CredentialType |
| **fullyQualifiedNamespace** (security) | Fully Qualified Namespace of the service bus. |  | String |
| **tokenCredential** (security) | **Autowired** A TokenCredential for Azure AD authentication. |  | TokenCredential |

## Message Headers

The Azure ServiceBus component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureServiceBusApplicationProperties** (common) Constant: [`APPLICATION_PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#APPLICATION_PROPERTIES) | The application properties (also known as custom properties) on messages sent and received by the producer and consumer, respectively. |  | Map |
| **CamelAzureServiceBusContentType** (consumer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#CONTENT_TYPE) | Gets the content type of the message. |  | String |
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
| **CamelAzureServiceBusCorrelationId** (common) Constant: [`CORRELATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-servicebus/latest/org/apache/camel/component/azure/servicebus/ServiceBusConstants.html#CORRELATION_ID) | Gets or Sets a correlation identifier. |  | String |

## Usage

### Consumer and Producer

This component implements the Consumer and Producer.

### Authentication Information

There are three different Credential Types: `AZURE_IDENTITY`, `TOKEN_CREDENTIAL` and `CONNECTION_STRING`. To use this component, you have three options to provide the required Azure authentication information:

**CONNECTION\_STRING**:

-   Provide `connectionString` string it is the simplest option to get started.
    

> **Important**
> The `SharedAccessKey` part of a connection string is a Base64-encoded value that often contains characters with a special meaning in URIs (such as `+`, `/` or `=`). When the `connectionString` is configured directly in an endpoint URI (including the Endpoint DSL), wrap the value with `RAW()` so it is not URI-decoded, otherwise authentication fails with `status-code: 401 …​ InvalidSignature: The token has an invalid signature`:
>
> ```java
> from("azure-servicebus:myQueue?connectionString=RAW(Endpoint=sb://myhost.servicebus.windows.net/;SharedAccessKeyName=test;SharedAccessKey=aBc+dEf/123=)")
>     .to("mock:result");
> ```
>
> See [Configuring parameter values using raw values](../../manual/endpoint.html#_configuring_parameter_values_using_raw_values_such_as_passwords) for more details.

**TOKEN\_CREDENTIAL**:

-   Provide an implementation of `com.azure.core.credential.TokenCredential` into the Camel’s Registry, e.g., using the `com.azure.identity.DefaultAzureCredentialBuilder().build();` API. See the documentation [here about Azure-AD authentication](https://docs.microsoft.com/en-us/azure/active-directory/authentication/overview-authentication).
    

**AZURE\_IDENTITY**:

-   This will use `com.azure.identity.DefaultAzureCredentialBuilder().build();` instance. This will follow the Default Azure Credential Chain. See the documentation [here about Azure-AD authentication](https://docs.microsoft.com/en-us/azure/active-directory/authentication/overview-authentication).
    

### Custom Client Instance

It is possible to provide a custom client instance on either the consumer or producer endpoints. `com.azure.messaging.servicebus.ServiceBusSenderClient` for sending messages and `com.azure.messaging.servicebus.ServiceBusReceiverClient` to receive messages. When clients are bound to the Camel registry, they will be autowired into the Service Bus component.

### Message Body

In the producer, this component accepts a message body of `String`, `byte[]` and `BinaryData` types. Or `List<String>`, `List<byte[]>` and `List<BinaryData>` to send batch messages.

In the consumer, the returned message body will be of type `String`.

### Azure ServiceBus Producer operations

 
| Operation | Description |
| --- | --- |
| `sendMessages` | Sends a set of messages to a Service Bus queue or topic using a batched approach. |
| `scheduleMessages` | Sends a scheduled message to the Azure Service Bus queue or topic. A scheduled message is enqueued and made available to receivers only at the scheduled time. |

## Examples

-   `sendMessages`
    

_Java-only: building a batch message list with a Processor_

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

_Java-only: sending a batch message with a session ID_

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
  .to("azure-servicebus:test//?connectionString=test&sessionId=123")
  .to("mock:result");
```

-   `scheduleMessages`
    

_Java-only: scheduling messages with a Processor and ServiceBusConstants_

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
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-servicebus:test//?connectionString=test")
  .log("${body}")
  .to("mock:result");
```

```xml
<route>
  <from uri="azure-servicebus:test//?connectionString=test"/>
  <log message="${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-servicebus:test//
      parameters:
        connectionString: test
      steps:
        - log:
            message: "${body}"
        - to:
            uri: mock:result
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-servicebus:test//?connectionString=test&sessionEnabled=true")
  .log("${body}")
  .to("mock:result");
```

```xml
<route>
  <from uri="azure-servicebus:test//?connectionString=test&amp;sessionEnabled=true"/>
  <log message="${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-servicebus:test//
      parameters:
        connectionString: test
        sessionEnabled: true
      steps:
        - log:
            message: "${body}"
        - to:
            uri: mock:result
```