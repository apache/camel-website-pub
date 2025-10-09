# Iggy

**Since Camel 4.17**

**Both producer and consumer are supported**

The Iggy component is used for communicating with [Iggy](https://iggy.incubator.apache.org/) message broker.

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-iggy</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Netty Version Requirement

The Iggy client library requires Netty 4.2.x or later. If your application uses an older version of Netty (e.g., 4.1.x), you will need to import the Netty 4.2.x BOM in your `dependencyManagement` section to ensure compatibility with the Iggy client:

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>io.netty</groupId>
            <artifactId>netty-bom</artifactId>
            <version>4.2.7.Final</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

## URI format

iggy:topic\[?options\]

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

The Iggy component supports 31 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateStream** (common) | Whether to automatically create stream if it does not exist. | true | boolean |
| **autoCreateTopic** (common) | Whether to automatically create topic if it does not exist. | true | boolean |
| **clientTransport** (common) | 
Polling strategy.

Enum values:

-   TCP
    
-   HTTP
    





 | TCP | String |
| **compressionAlgorithm** (common) | 

Compression algorithm for message payload.

Enum values:

-   None
    
-   Gzip
    





 | None | CompressionAlgorithm |
| **configuration** (common) | Allows to pre-configure the Iggy component with common options that the endpoints will reuse. |  | IggyConfiguration |
| **host** (common) | Iggy server hostname or IP address. | localhost | String |
| **maxTopicSize** (common) | Maximum topic size in bytes (0 means unlimited). | 0 | Long |
| **messageExpiry** (common) | Message expiry time in seconds (0 means no expiry). | 0 | Long |
| **partitionsCount** (common) | Number of partitions for the topic. | 1 | Long |
| **password** (common) | Iggy password. |  | String |
| **port** (common) | Iggy server port number. | 8090 | int |
| **replicationFactor** (common) | Replication factor for the topic. |  | Short |
| **streamId** (common) | Stream identifier. |  | Long |
| **streamName** (common) | Stream name. |  | String |
| **autoCommit** (consumer) | Controls message acknowledgment behavior. When true, messages are automatically marked as processed after consumption. When false, enables manual offset management and allows setting a custom starting offset position. | true | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerGroupName** (consumer) | The name of the consumer group. |  | String |
| **consumersCount** (consumer) | Camel Iggy consumers count. | 1 | int |
| **partitionId** (consumer) | The consumer partition id. |  | Long |
| **pollBatchSize** (consumer) | The consumer poll batch size. | 10 | Long |
| **pollingStrategy** (consumer) | 

Polling strategy.

Enum values:

-   next
    
-   first
    
-   last
    





 | next | String |
| **shutdownTimeout** (consumer) | Camel Iggy shutdown timeout. | 30000 | int |
| **startingOffset** (consumer) | Defines the initial message offset position when autoCommit is disabled. Use 0 to start from the beginning of the stream, or specify a custom offset to resume from a particular point. | 0 | Long |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **partitioning** (producer) | Partitioning strategy for message distribution. | balanced | Partitioning |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **sslContextParameters** (security) | SSL configuration using an org.apache.camel.support.jsse.SSLContextParameters instance. This takes precedence over tlsEnabled and tlsCertificatePath when configured. |  | SSLContextParameters |
| **tlsCertificatePath** (security) | Path to the TLS certificate file for the connection to the Iggy server. |  | String |
| **tlsEnabled** (security) | Whether to enable TLS for the connection to the Iggy server. | false | boolean |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **username** (security) | Iggy username. |  | String |

## Endpoint Options

The Iggy endpoint is configured using URI syntax:

iggy:topicName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topicName** (common) | **Required** Name of the topic. |  | String |

### Query Parameters (30 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateStream** (common) | Whether to automatically create stream if it does not exist. | true | boolean |
| **autoCreateTopic** (common) | Whether to automatically create topic if it does not exist. | true | boolean |
| **clientTransport** (common) | 
Polling strategy.

Enum values:

-   TCP
    
-   HTTP
    





 | TCP | String |
| **compressionAlgorithm** (common) | 

Compression algorithm for message payload.

Enum values:

-   None
    
-   Gzip
    





 | None | CompressionAlgorithm |
| **host** (common) | Iggy server hostname or IP address. | localhost | String |
| **maxTopicSize** (common) | Maximum topic size in bytes (0 means unlimited). | 0 | Long |
| **messageExpiry** (common) | Message expiry time in seconds (0 means no expiry). | 0 | Long |
| **partitionsCount** (common) | Number of partitions for the topic. | 1 | Long |
| **password** (common) | Iggy password. |  | String |
| **port** (common) | Iggy server port number. | 8090 | int |
| **replicationFactor** (common) | Replication factor for the topic. |  | Short |
| **streamId** (common) | Stream identifier. |  | Long |
| **streamName** (common) | Stream name. |  | String |
| **autoCommit** (consumer) | Controls message acknowledgment behavior. When true, messages are automatically marked as processed after consumption. When false, enables manual offset management and allows setting a custom starting offset position. | true | boolean |
| **consumerGroupName** (consumer) | The name of the consumer group. |  | String |
| **consumersCount** (consumer) | Camel Iggy consumers count. | 1 | int |
| **partitionId** (consumer) | The consumer partition id. |  | Long |
| **pollBatchSize** (consumer) | The consumer poll batch size. | 10 | Long |
| **pollingStrategy** (consumer) | 

Polling strategy.

Enum values:

-   next
    
-   first
    
-   last
    





 | next | String |
| **shutdownTimeout** (consumer) | Camel Iggy shutdown timeout. | 30000 | int |
| **startingOffset** (consumer) | Defines the initial message offset position when autoCommit is disabled. Use 0 to start from the beginning of the stream, or specify a custom offset to resume from a particular point. | 0 | Long |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **partitioning** (producer) | Partitioning strategy for message distribution. | balanced | Partitioning |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **sslContextParameters** (security) | SSL configuration using an org.apache.camel.support.jsse.SSLContextParameters instance. This takes precedence over tlsEnabled and tlsCertificatePath when configured. |  | SSLContextParameters |
| **tlsCertificatePath** (security) | Path to the TLS certificate file for the connection to the Iggy server. |  | String |
| **tlsEnabled** (security) | Whether to enable TLS for the connection to the Iggy server. | false | boolean |
| **username** (security) | Iggy username. |  | String |

## Iggy Headers

The following headers are set on the exchange when consuming messages from Iggy:

  
| Header | Type | Description |
| --- | --- | --- |
| `` `CamelIggyMessageId` `` | `` `String` `` | The unique identifier of the message. |
| `` `CamelIggyMessageOffset` `` | `` `long` `` | The offset of the message in the partition. |
| `` `CamelIggyMessageTimestamp` `` | `` `long` `` | The timestamp of the message. |
| `` `CamelIggyMessageOriginTimestamp` `` | `` `long` `` | The original timestamp of the message. |
| `` `CamelIggyMessageChecksum` `` | `` `long` `` | The checksum of the message. |
| `` `CamelIggyMessageLength` `` | `` `int` `` | The length of the message. |
| `` `CamelIggyMessageSize` `` | `` `int` `` | The size of the message. |

## Examples

### Consuming messages from Iggy

Here is a minimal route to read messages from an Iggy topic:

```java
from("iggy:my_topic?streamName=my_stream&consumerGroupName=my_consumer_group&host=localhost&port=8090")
    .log("Message received from Iggy : ${body}")
    .log("    with id ${headers[CamelIggyMessageId]}")
    .log("    and offset ${headers[CamelIggyMessageOffset]}");
```

### Producing messages to Iggy

Here is a minimal route to produce messages to an Iggy topic:

```java
from("direct:start")
    .setBody(constant("Message from Camel"))
    .to("iggy:my_topic?streamName=my_stream&host=localhost&port=8090");
```