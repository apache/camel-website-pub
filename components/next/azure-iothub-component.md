# Azure IoT Hub

**Since Camel 4.24**

**Only producer is supported**

The Azure IoT Hub component provides the capability to send device-to-cloud telemetry and to update device-twin reported properties on [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/), using the Azure IoT device SDK. Device connections are pooled and reused by the resolved hub/device/module identity from the connection string.

**Prerequisites**

You must have a valid Microsoft Azure IoT Hub and a per-device connection string. More information is available at the [Azure IoT Hub Documentation](https://learn.microsoft.com/azure/iot-hub/).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-iothub</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

```none
azure-iothub:deviceId[?options]
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

The Azure IoT Hub component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The shared component configuration. |  | IoTHubConfiguration |
| **contentType** (producer) | Content type applied to telemetry messages. | application/json | String |
| **deliveryMode** (producer) | 
How the message body is delivered: telemetry, device twin reported properties, or both.

Enum values:

-   TELEMETRY
    
-   TWIN
    
-   BOTH
    





 | TELEMETRY | IoTHubDeliveryMode |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **protocol** (producer) | 

The protocol used to connect to Azure IoT Hub.

Enum values:

-   HTTPS
    
-   AMQPS
    
-   MQTT
    
-   AMQPS\_WS
    
-   MQTT\_WS
    





 | MQTT | IotHubClientProtocol |
| **sendTimeout** (producer) | Timeout for telemetry sends and twin reported-property updates. | 10s | Duration |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **deviceClientEvictionInterval** (advanced) | How often the pool is scanned for idle device clients to evict. | 30s | Duration |
| **deviceClientIdleTimeout** (advanced) | Idle time after which a pooled device client is evicted and closed. | 5m | Duration |
| **connectionString** (security) | The IoT Hub device connection string. Can be overridden per message via the CamelAzureIoTHubConnectionString header. |  | String |

## Endpoint Options

The Azure IoT Hub endpoint is configured using URI syntax:

azure-iothub:deviceId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **deviceId** (producer) | Default device id used when the message does not carry a device id header. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **contentType** (producer) | Content type applied to telemetry messages. | application/json | String |
| **deliveryMode** (producer) | 
How the message body is delivered: telemetry, device twin reported properties, or both.

Enum values:

-   TELEMETRY
    
-   TWIN
    
-   BOTH
    





 | TELEMETRY | IoTHubDeliveryMode |
| **protocol** (producer) | 

The protocol used to connect to Azure IoT Hub.

Enum values:

-   HTTPS
    
-   AMQPS
    
-   MQTT
    
-   AMQPS\_WS
    
-   MQTT\_WS
    





 | MQTT | IotHubClientProtocol |
| **sendTimeout** (producer) | Timeout for telemetry sends and twin reported-property updates. | 10s | Duration |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connectionString** (security) | The IoT Hub device connection string. Can be overridden per message via the CamelAzureIoTHubConnectionString header. |  | String |

## Message Headers

The Azure IoT Hub component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureIoTHubDeviceId** (producer) Constant: [`DEVICE_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-iothub/latest/org/apache/camel/component/azure/iothub/IoTHubConstants.html#DEVICE_ID) | The target device id. Overrides the device id configured on the endpoint. |  | String |
| **CamelAzureIoTHubConnectionString** (producer) Constant: [`CONNECTION_STRING`](https://javadoc.io/doc/org.apache.camel/camel-azure-iothub/latest/org/apache/camel/component/azure/iothub/IoTHubConstants.html#CONNECTION_STRING) | The per-device IoT Hub connection string. Overrides the connection string configured on the endpoint. |  | String |
| **CamelAzureIoTHubDeliveryMode** (producer) Constant: [`DELIVERY_MODE`](https://javadoc.io/doc/org.apache.camel/camel-azure-iothub/latest/org/apache/camel/component/azure/iothub/IoTHubConstants.html#DELIVERY_MODE) | 
Overrides the configured delivery mode for this message.

Enum values:

-   TELEMETRY
    
-   TWIN
    
-   BOTH
    





 |  | IoTHubDeliveryMode |
| **CamelAzureIoTHubTwinProperties** (producer) Constant: [`TWIN_PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-azure-iothub/latest/org/apache/camel/component/azure/iothub/IoTHubConstants.html#TWIN_PROPERTIES) | Device twin reported properties to apply, as a Map. Used for TWIN delivery and, in BOTH mode, alongside the telemetry message body. |  | Map |

## Usage

The producer sends the message body to Azure IoT Hub. The delivery mode selects how the body is interpreted:

-   `TELEMETRY` - the body is sent as a device-to-cloud message, using the payload as a `byte[]`/`String`\-compatible value.
    
-   `TWIN` - the body (a `java.util.Map`) is applied as device-twin reported properties using a delta update (only changed properties are sent).
    
-   `BOTH` - sends the message body as telemetry and applies twin reported properties from the `CamelAzureIoTHubTwinProperties` header.
    

Any payload decoding (for example Protobuf or CloudEvent to `Map`) must be done by a preceding processor in the route; this component is payload-agnostic.

### Scope and non-goals

This component deliberately covers only the **data plane** - the per-message act of connecting as an already-provisioned device and sending telemetry or twin updates. It is credential- and payload-agnostic: it expects a ready-to-use per-device connection string (supplied on the endpoint or via the `CamelAzureIoTHubConnectionString` header) and a payload already in the shape it expects.

> **Warning**
> Passing the IoT Hub connection string in a message header is sensitive because it may travel through tracing, logging, or downstream endpoints. Use it only when needed and avoid persisting it in a message body or route metadata.

The following **control plane** and application-specific concerns are intentionally **out of scope** and must be handled by the application or dedicated tooling before a message reaches this component:

-   **Device provisioning** via the Azure Device Provisioning Service (DPS) - enrollment groups, id scopes, attestation and the registration handshake.
    
-   **Device registry lifecycle** - creating, disabling or deleting device identities in IoT Hub.
    
-   **Credential resolution and storage** - deriving or retrieving SAS keys, integrating with a secret store such as Azure Key Vault, caching and refresh policies.
    
-   **Payload decoding** - converting application formats (for example Protobuf or CloudEvents) into the `byte[]`/`String` telemetry body or the `Map` of twin reported properties.
    

This mirrors the other Azure Camel components (for example `azure-eventhubs` and `azure-servicebus`), which likewise accept a connection string or token credential and leave resource provisioning to the application. Keeping provisioning out of the component makes it reusable across tenants, avoids coupling a hot data path to a slow one-time control path, and keeps environment-specific security details out of the component.

### Example

Send telemetry to a fixed device:

```java
from("direct:telemetry")
    .to("azure-iothub:myDevice?deliveryMode=TELEMETRY&connectionString=RAW(HostName=...;DeviceId=myDevice;SharedAccessKey=...)");
```

Route messages to different devices dynamically using headers:

```java
from("direct:dynamic")
    .setHeader("CamelAzureIoTHubDeviceId", simple("${header.deviceId}"))
    .setHeader("CamelAzureIoTHubConnectionString", simple("${header.deviceConnectionString}"))
    .to("azure-iothub:placeholder?deliveryMode=TWIN");
```

> **Important**
> The connection string is secret and should not be logged or propagated downstream unless it is strictly required. Prefer configuring it on the endpoint when possible.