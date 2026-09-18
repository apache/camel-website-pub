# Tahu Edge Node / Device

**Since Camel 4.8**

**Only producer is supported**

## URI format

Tahu Edge Nodes and Devices use the same URI scheme and Tahu Edge Component and Endpoint.

Edge Node endpoints, where `groupId` and `edgeNodeId` are the Sparkplug Group and Edge Node IDs describing the Edge Node.

tahu-edge://groupId/edgeNodeId?options

Example: Edge Node Producer for Group 'Basic' and Edge Node 'EdgeNode' using MQTT Client ID 'EdgeClient1' connecting to Host Application 'BasicHostApp'

tahu-edge://Basic/EdgeNode?clientId=EdgeClient1&primaryHostId=BasicHostApp&deviceIds=D2,D3,D4

Device endpoints, where `groupId`, `edgeNodeId`, and `deviceId` are the Sparkplug Group, Edge Node, and Device IDs describing the Device.

tahu-edge://groupId/edgeNodeId/deviceId

Example: Device Producers for Devices 'D2', 'D3', and 'D4' connected to Edge Node 'EdgeNode' in Group 'Basic', i.e. the Devices of the Edge Node in the example above

tahu-edge://Basic/EdgeNode/D2
tahu-edge://Basic/EdgeNode/D3
tahu-edge://Basic/EdgeNode/D4

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

The Tahu Edge Node / Device component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **checkClientIdLength** (common) | MQTT client ID length check enabled. | false | boolean |
| **clientId** (common) | **Required** MQTT client ID to use for all server definitions, rather than specifying the same one for each. Note that if neither the 'clientId' parameter nor an 'MqttClientId' are defined for an MQTT Server, a random MQTT Client ID will be generated automatically, prefaced with 'Camel'. |  | String |
| **keepAliveTimeout** (common) | MQTT connection keep alive timeout, in seconds. | 30 | int |
| **rebirthDebounceDelay** (common) | Delay before recurring node rebirth messages will be sent. | 5000 | long |
| **servers** (common) | **Required** MQTT server definitions, given with the following syntax in a comma-separated list: MqttServerName:(MqttClientId:)(tcp/ssl)://hostname(:port),…​ |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use a shared Tahu configuration. |  | TahuConfiguration |
| **password** (security) | Password for MQTT server authentication. |  | String |
| **sslContextParameters** (security) | SSL configuration for MQTT server connections. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable/disable global SSL context parameters use. | false | boolean |
| **username** (security) | Username for MQTT server authentication. |  | String |

## Endpoint Options

The Tahu Edge Node / Device endpoint is configured using URI syntax:

tahu-edge:groupId/edgeNode

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **groupId** (producer) | **Required** ID of the group. |  | String |
| **edgeNode** (producer) | **Required** ID of the edge node. |  | String |
| **deviceId** (producer (device only)) | ID of this edge node device. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **checkClientIdLength** (common) | MQTT client ID length check enabled. | false | boolean |
| **clientId** (common) | **Required** MQTT client ID to use for all server definitions, rather than specifying the same one for each. Note that if neither the 'clientId' parameter nor an 'MqttClientId' are defined for an MQTT Server, a random MQTT Client ID will be generated automatically, prefaced with 'Camel'. |  | String |
| **keepAliveTimeout** (common) | MQTT connection keep alive timeout, in seconds. | 30 | int |
| **rebirthDebounceDelay** (common) | Delay before recurring node rebirth messages will be sent. | 5000 | long |
| **servers** (common) | **Required** MQTT server definitions, given with the following syntax in a comma-separated list: MqttServerName:(MqttClientId:)(tcp/ssl)://hostname(:port),…​ |  | String |
| **metricDataTypePayloadMap** (producer) | **Required** Tahu SparkplugBPayloadMap to configure metric data types for this edge node or device. Note that this payload is used exclusively as a Sparkplug B spec-compliant configuration for all possible edge node or device metric names, aliases, and data types. This configuration is required to publish proper Sparkplug B NBIRTH and DBIRTH payloads. |  | SparkplugBPayloadMap |
| **headerFilterStrategy** (producer (advanced)) | To use a custom HeaderFilterStrategy to filter headers used as Sparkplug metrics. Default value notice: Defaults to sending all Camel Message headers with name prefixes of CamelTahuMetric., including those with null values. |  | HeaderFilterStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **bdSeqManager** (advanced) | To use a specific org.eclipse.tahu.message.BdSeqManager implementation to manage edge node birth-death sequence numbers. | org.apache.camel.component.tahu.CamelBdSeqManager | BdSeqManager |
| **bdSeqNumPath** (advanced) | Path for Sparkplug B NBIRTH/NDEATH sequence number persistence files. This path will contain files named as -bdSeqNum and must be writable by the executing process' user. | ${sys:java.io.tmpdir}/CamelTahuTemp | String |
| **useAliases** (advanced) | Flag enabling support for metric aliases. | false | boolean |
| **deviceIds** (producer (edge node only)) | ID of each device connected to this edge node, as a comma-separated list. |  | String |
| **primaryHostId** (producer (edge node only)) | Host ID of the primary host application for this edge node. |  | String |
| **password** (security) | Password for MQTT server authentication. |  | String |
| **sslContextParameters** (security) | SSL configuration for MQTT server connections. |  | SSLContextParameters |
| **username** (security) | Username for MQTT server authentication. |  | String |

## Message Headers

The Tahu Edge Node / Device component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelTahuMessageType** (producer) Constant: [`MESSAGE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#MESSAGE_TYPE) | 
The Sparkplug message type of the message.

Enum values:

-   NBIRTH
    
-   NDATA
    
-   NDEATH
    
-   DBIRTH
    
-   DDATA
    
-   DDEATH
    





 |  | String |
| **CamelTahuEdgeNodeDescriptor** (producer) Constant: [`EDGE_NODE_DESCRIPTOR`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#EDGE_NODE_DESCRIPTOR) | The Sparkplug edge node descriptor string source of a message or metric. |  | String |
| **CamelTahuMessageTimestamp** (producer) Constant: [`MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#MESSAGE_TIMESTAMP) | The timestamp of a Sparkplug message. |  | Long |
| **CamelTahuMessageUUID** (producer) Constant: [`MESSAGE_UUID`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#MESSAGE_UUID) | The UUID of a Sparkplug message. |  | UUID |
| **CamelTahuMessageSequenceNumber** (producer) Constant: [`MESSAGE_SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-tahu/latest/org/apache/camel/component/tahu/TahuConstants.html#MESSAGE_SEQUENCE_NUMBER) | The sequence number of a Sparkplug message. |  | Long |

## Usage

### Edge Node Endpoint Configuration

Sparkplug Edge Nodes are identified by a unique combination of Group ID and Edge Node ID, the Edge Node Descriptor. These two elements form the path of an Edge Node Endpoint URI. All other Edge Node Endpoint configuration properties use query string variables or are set via Endpoint property setters.

If an Edge Node is tied to a particular Host Application, the `primaryHostId` query string variable can be set to enable the required Sparkplug behavior.

Metric aliasing is handled automatically by the Eclipse Tahu library and enabled with the `useAliases` query string variable.

#### Birth/Death Sequence Numbers

The Sparkplug specification requires careful handling of NBIRTH/NDEATH sequence numbers for Host Applications to correlate Edge Nodes' session behavior with the metrics the Host Application receives.

By default, each Edge Node Endpoint writes a local file to store the next sequence number that Edge Node should use when publishing its NBIRTH message and setting its NDEATH MQTT Will Message when establishing an MQTT Server connection. The local path for this file can be set using the `bdSeqNumPath` query string variable.

Should another Sparkplug spec-compliant Eclipse Tahu `BdSeqManager` instance be required, use the `bdSeqManager` Endpoint property setter method.

### Device Endpoint Configuration

Sparkplug Devices are identified by a unique combination of the Edge Node Descriptor to which the Device is connected and the Device’s Device ID. These three elements form the path of a Device Endpoint URI. Since any Sparkplug Device is associated with exactly one Edge Node, an MQTT Server connection and its associated Sparkplug behavior is managed per Edge Node, not per Device. This means all Device Endpoint configuration must be completed prior to starting the Edge Node Producer for a given Device Endpoint.

Device Endpoints inherit all MQTT Server connection information from their associated Edge Node Endpoint. Setting Component- or Endpoint-level configuration values on Device Components or Endpoints is unnecessary and should be avoided.

### Edge Node and Device Endpoint Interaction

Sparkplug Edge Nodes are not required to have a Device hierarchy and physical devices may be represented directly as Edge Nodes—​this decision is left to Sparkplug application developers.

However if an Edge Node will be reporting Device-level metrics in addition to and Edge Node-level metrics, the Edge Node Endpoint is required to have a `deviceIds` list configured to publish correct NBIRTH and DBIRTH payloads required by the Sparkplug specification.

Additionally, a Tahu `SparkplugBPayloadMap` instance is required to be set on each Edge Node and Device Endpoint to populate the NBIRTH/DBIRTH message with the required Sparkplug Metric names and data types. This is accomplished using the `metricDataTypePayloadMap` Endpoint property setter method.

These requirements allow Sparkplug 3.0.0 compliant behavior.