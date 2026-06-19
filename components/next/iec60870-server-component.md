# IEC 60870 Server

> **Warning**
> **Deprecated:** This iec60870-server is deprecated and may be removed in a future release.

**Since Camel 2.20**

**Both producer and consumer are supported**

The **IEC 60870-5-104 Server** component provides access to IEC 60870 servers using the [Eclipse NeoSCADA](http://eclipse.org/eclipsescada) implementation.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-iec60870</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

The URI syntax of the endpoint is:

iec60870-server:host:port/00-01-02-03-04

The information object address is encoded in the path in the syntax above. Please note that always the full, 5-octet address format is being used. Unused octets have to be filled with zero.

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

The IEC 60870 Server component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **defaultConnectionOptions** (common) | Default connection options. |  | ServerOptions |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The IEC 60870 Server endpoint is configured using URI syntax:

iec60870-server:uriPath

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **uriPath** (common) | **Required** The object information address. |  | ObjectAddress |

### Query Parameters (21 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataModuleOptions** (common) | Data module options. |  | DataModuleOptions |
| **filterNonExecute** (common) | Filter out all requests which don’t have the execute bit set. | true | boolean |
| **protocolOptions** (common) | Protocol options. |  | ProtocolOptions |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **acknowledgeWindow** (connection) | Parameter W - Acknowledgment window. | 10 | short |
| **adsuAddressType** (connection) | 

The common ASDU address size. May be either SIZE\_1 or SIZE\_2.

Enum values:

-   SIZE\_1
    
-   SIZE\_2
    





 |  | ASDUAddressType |
| **causeOfTransmissionType** (connection) | 

The cause of transmission type. May be either SIZE\_1 or SIZE\_2.

Enum values:

-   SIZE\_1
    
-   SIZE\_2
    





 |  | CauseOfTransmissionType |
| **informationObjectAddressType** (connection) | 

The information address size. May be either SIZE\_1, SIZE\_2 or SIZE\_3.

Enum values:

-   SIZE\_1
    
-   SIZE\_2
    
-   SIZE\_3
    





 |  | InformationObjectAddressType |
| **maxUnacknowledged** (connection) | Parameter K - Maximum number of un-acknowledged messages. | 15 | short |
| **timeout1** (connection) | Timeout T1 in milliseconds. | 15000 | int |
| **timeout2** (connection) | Timeout T2 in milliseconds. | 10000 | int |
| **timeout3** (connection) | Timeout T3 in milliseconds. | 20000 | int |
| **causeSourceAddress** (data) | Whether to include the source address. |  | byte |
| **connectionTimeout** (data) | Timeout in millis to wait for client to establish a connected connection. | 10000 | int |
| **ignoreBackgroundScan** (data) | Whether background scan transmissions should be ignored. | true | boolean |
| **ignoreDaylightSavingTime** (data) | Whether to ignore or respect DST. | false | boolean |
| **timeZone** (data) | The timezone to use. May be any Java time zone string. | UTC | TimeZone |
| **connectionId** (id) | An identifier grouping connection instances. |  | String |

## Message Headers

The IEC 60870 Server component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **address** (consumer) Constant: [`ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#ADDRESS) | The address as ObjectAddress. |  | ObjectAddress |
| **value** (consumer) Constant: [`VALUE`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#VALUE) | The value. |  | Object |
| **informationObjectAddress** (consumer) Constant: [`INFORMATION_OBJECT_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#INFORMATION_OBJECT_ADDRESS) | The address as InformationObjectAddress. |  | InformationObjectAddress |
| **asduHeader** (consumer) Constant: [`ASDU_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#ASDU_HEADER) | The ASDU header. |  | ASDUHeader |
| **type** (consumer) Constant: [`TYPE`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#TYPE) | The type. |  | byte |
| **execute** (consumer) Constant: [`EXECUTE`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#EXECUTE) | Is execute. |  | boolean |