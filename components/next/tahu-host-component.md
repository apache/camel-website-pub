# Tahu Host Application

**Since Camel 4.8**

**Only consumer is supported**

## URI format

Host Application endpoints, where `hostId` is the Sparkplug Host Application ID

tahu-host://hostId?options

Example: Host Application Consumer for Host App 'BasicHostApp' using MQTT Client ID 'HostClient1'

tahu-host:BasicHostApp?clientId=HostClient1

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

The Tahu Host Application component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **checkClientIdLength** (common) | MQTT client ID length check enabled. | false | boolean |
| **clientId** (common) | **Required** MQTT client ID to use for all server definitions, rather than specifying the same one for each. Note that if neither the 'clientId' parameter nor an 'MqttClientId' are defined for an MQTT Server, a random MQTT Client ID will be generated automatically, prefaced with 'Camel'. |  | String |
| **keepAliveTimeout** (common) | MQTT connection keep alive timeout, in seconds. | 30 | int |
| **rebirthDebounceDelay** (common) | Delay before recurring node rebirth messages will be sent. | 5000 | long |
| **servers** (common) | **Required** MQTT server definitions, given with the following syntax in a comma-separated list: MqttServerName:(MqttClientId:)(tcp/ssl)://hostname(:port),…​ |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use a shared Tahu configuration. |  | TahuConfiguration |
| **password** (security) | Password for MQTT server authentication. |  | String |
| **sslContextParameters** (security) | SSL configuration for MQTT server connections. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable/disable global SSL context parameters use. | false | boolean |
| **username** (security) | Username for MQTT server authentication. |  | String |

## Endpoint Options

The Tahu Host Application endpoint is configured using URI syntax:

tahu-host:hostId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **hostId** (consumer) | **Required** ID for the host application. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **checkClientIdLength** (common) | MQTT client ID length check enabled. | false | boolean |
| **clientId** (common) | **Required** MQTT client ID to use for all server definitions, rather than specifying the same one for each. Note that if neither the 'clientId' parameter nor an 'MqttClientId' are defined for an MQTT Server, a random MQTT Client ID will be generated automatically, prefaced with 'Camel'. |  | String |
| **keepAliveTimeout** (common) | MQTT connection keep alive timeout, in seconds. | 30 | int |
| **rebirthDebounceDelay** (common) | Delay before recurring node rebirth messages will be sent. | 5000 | long |
| **servers** (common) | **Required** MQTT server definitions, given with the following syntax in a comma-separated list: MqttServerName:(MqttClientId:)(tcp/ssl)://hostname(:port),…​ |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **password** (security) | Password for MQTT server authentication. |  | String |
| **sslContextParameters** (security) | SSL configuration for MQTT server connections. |  | SSLContextParameters |
| **username** (security) | Username for MQTT server authentication. |  | String |

## Message Headers

The Tahu Host Application component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelTahuMessageType** (consumer) Constant: [`MESSAGE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#MESSAGE_TYPE) | 
The Sparkplug message type of the message.

Enum values:

-   NBIRTH
    
-   NDATA
    
-   NDEATH
    
-   DBIRTH
    
-   DDATA
    
-   DDEATH
    





 |  | String |
| **CamelTahuEdgeNodeDescriptor** (consumer) Constant: [`EDGE_NODE_DESCRIPTOR`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#EDGE_NODE_DESCRIPTOR) | The Sparkplug edge node descriptor string source of a message or metric. |  | String |
| **CamelTahuMessageTimestamp** (consumer) Constant: [`MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#MESSAGE_TIMESTAMP) | The timestamp of a Sparkplug message. |  | Long |
| **CamelTahuMessageUUID** (consumer) Constant: [`MESSAGE_UUID`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#MESSAGE_UUID) | The UUID of a Sparkplug message. |  | UUID |
| **CamelTahuMessageSequenceNumber** (consumer) Constant: [`MESSAGE_SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#MESSAGE_SEQUENCE_NUMBER) | The sequence number of a Sparkplug message. |  | Long |