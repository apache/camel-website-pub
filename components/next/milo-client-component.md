# OPC UA Client

**Since Camel 2.19**

**Both producer and consumer are supported**

The Milo Client component provides access to OPC UA servers using the [Eclipse Milo™](http://eclipse.org/milo) implementation.

**Java 11+**: This component requires Java 11+ at runtime.

> **Note**
> This component uses Eclipse Milo 1.0.5. When migrating from earlier versions, be aware that the Milo API has undergone significant changes in the 1.0.x series.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-milo</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

The URI syntax of the endpoint is:

milo-client:opc.tcp://\[user:password@\]host:port/path/to/service?node=RAW(nsu=urn:foo:bar;s=item-1)

If the server does not use a path, then it is possible to simply omit it:

milo-client:opc.tcp://\[user:password@\]host:port?node=RAW(nsu=urn:foo:bar;s=item-1)

If no user credentials are provided the client will switch to anonymous mode.

All configuration options in the group client are applicable to the shared client instance. Endpoints will share client instances for each endpoint URI. So the first time a request for that endpoint URI is made, the options of the client group are applied. All further instances will be ignored.

If you need alternate options for the same endpoint URI it is possible though to set the clientId option which will by added internally to the endpoint URI in order to select a different shared connection instance. In other words, shared connections located by the combination of endpoint URI and client id.

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

The OPC UA Client component supports 26 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | A virtual client id to force the creation of a new connection instance. |  | String |
| **configuration** (common) | All default options for client configurations. |  | MiloClientConfiguration |
| **discoveryEndpointSuffix** (common) | A suffix for endpoint URI when discovering. |  | String |
| **discoveryEndpointUri** (common) | An alternative discovery URI. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **allowedSecurityPolicies** (client) | A set of allowed security policy URIs. Default is to accept all and use the highest. |  | String |
| **applicationName** (client) | The application name. | Apache Camel adapter for Eclipse Milo | String |
| **applicationUri** (client) | The application URI. | [http://camel.apache.org/EclipseMilo/Client](http://camel.apache.org/EclipseMilo/Client) | String |
| **channelLifetime** (client) | Channel lifetime in milliseconds. |  | Long |
| **keyAlias** (client) | The name of the key in the keystore file. |  | String |
| **keyPassword** (client) | The key password. |  | String |
| **keyStorePassword** (client) | The keystore password. |  | String |
| **keyStoreType** (client) | The key store type. |  | String |
| **keyStoreUrl** (client) | The URL where the key should be loaded from. |  | String |
| **maxPendingPublishRequests** (client) | The maximum number of pending publish requests. |  | Long |
| **maxResponseMessageSize** (client) | The maximum number of bytes a response message may have. |  | Long |
| **miloClientConnectionManager** (client) | **Autowired** Instance for managing client connections. |  | MiloClientConnectionManager |
| **overrideHost** (client) | Override the server reported endpoint host with the host from the endpoint URI. | false | boolean |
| **overridePort** (client) | Override the server reported endpoint port with the port from the endpoint URI. | false | boolean |
| **productUri** (client) | The product URI. | [http://camel.apache.org/EclipseMilo](http://camel.apache.org/EclipseMilo) | String |
| **requestedPublishingInterval** (client) | The requested publishing interval in milliseconds. | 1\_000.0 | Double |
| **requestTimeout** (client) | Request timeout in milliseconds. |  | Long |
| **sessionName** (client) | Session name. |  | String |
| **sessionTimeout** (client) | Session timeout in milliseconds. |  | Long |

## Endpoint Options

The OPC UA Client endpoint is configured using URI syntax:

milo-client:endpointUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpointUri** (common) | **Required** The OPC UA server endpoint. |  | String |

### Query Parameters (34 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | A virtual client id to force the creation of a new connection instance. |  | String |
| **dataChangeFilterDeadbandType** (common) | Deadband type for MonitorFilterType DataChangeFilter. | 0 | UInteger |
| **dataChangeFilterDeadbandValue** (common) | Deadband value for MonitorFilterType DataChangeFilter. | 0.0 | Double |
| **dataChangeFilterTrigger** (common) | 
Data change trigger for data change monitor filter type.

Enum values:

-   Status
    
-   StatusValue
    
-   StatusValueTimestamp
    





 | StatusValueTimestamp | DataChangeTrigger |
| **defaultAwaitWrites** (common) | Default await setting for writes. | false | boolean |
| **discoveryEndpointSuffix** (common) | A suffix for endpoint URI when discovering. |  | String |
| **discoveryEndpointUri** (common) | An alternative discovery URI. |  | String |
| **method** (common) | The method definition (see Method ID). |  | String |
| **monitorFilterType** (common) | 

Monitor Filter Type for MonitoredItems.

Enum values:

-   dataChangeFilter
    





 |  | MonitorFilterType |
| **node** (common) | The node definition (see Node ID). |  | String |
| **omitNullValues** (common) | Omit notifications in case of null values. | true | boolean |
| **samplingInterval** (common) | The sampling interval in milliseconds. | 0.0 | Double |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **allowedSecurityPolicies** (client) | A set of allowed security policy URIs. Default is to accept all and use the highest. |  | String |
| **applicationName** (client) | The application name. | Apache Camel adapter for Eclipse Milo | String |
| **applicationUri** (client) | The application URI. | [http://camel.apache.org/EclipseMilo/Client](http://camel.apache.org/EclipseMilo/Client) | String |
| **channelLifetime** (client) | Channel lifetime in milliseconds. |  | Long |
| **keyAlias** (client) | The name of the key in the keystore file. |  | String |
| **keyPassword** (client) | The key password. |  | String |
| **keyStorePassword** (client) | The keystore password. |  | String |
| **keyStoreType** (client) | The key store type. |  | String |
| **keyStoreUrl** (client) | The URL where the key should be loaded from. |  | String |
| **maxPendingPublishRequests** (client) | The maximum number of pending publish requests. |  | Long |
| **maxResponseMessageSize** (client) | The maximum number of bytes a response message may have. |  | Long |
| **overrideHost** (client) | Override the server reported endpoint host with the host from the endpoint URI. | false | boolean |
| **overridePort** (client) | Override the server reported endpoint port with the port from the endpoint URI. | false | boolean |
| **productUri** (client) | The product URI. | [http://camel.apache.org/EclipseMilo](http://camel.apache.org/EclipseMilo) | String |
| **requestedPublishingInterval** (client) | The requested publishing interval in milliseconds. | 1\_000.0 | Double |
| **requestTimeout** (client) | Request timeout in milliseconds. |  | Long |
| **sessionName** (client) | Session name. |  | String |
| **sessionTimeout** (client) | Session timeout in milliseconds. |  | Long |

## Message Headers

The OPC UA Client component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMiloNodeIds** (producer) Constant: [`HEADER_NODE_IDS`](https://javadoc.io/doc/org.apache.camel/camel-milo/latest/org/apache/camel/component/milo/MiloConstants.html#HEADER_NODE_IDS) | The node ids. |  | List |
| **CamelMiloAwait** (producer) Constant: [`HEADER_AWAIT`](https://javadoc.io/doc/org.apache.camel/camel-milo/latest/org/apache/camel/component/milo/MiloConstants.html#HEADER_AWAIT) | The await setting for writes. |  | Boolean |

### Discovery

If the server uses a dedicated discovery endpoint (e.g. `/discovery`), which may support different (less secure) security policies, then you can make use of this via the parameter `discoveryEndpointSuffix`, which will be appended to the `endpointUri`. Or by using an explicit `discoveryEndpointUri`.

### Overriding the host name or port

The client uses the host and port information from the endpoint information, queried from the server. However in some situations this endpoint URI might be different, and wrong from the point of view of the connecting client (e.g. an internal hostname or internal port).

In this case it is possible to set the parameter(s) `overrideHost` or `overridePort` to `true`, which will take the discovered endpoint information, but override the host or port information with the value(s) of the original URI.

### Node ID

In order to define a target node a namespace and node id is required. In previous versions this was possible by specifying `nodeId` and either `namespaceUri` or `namespaceIndex`. However this only allowed for using string based node IDs. And while this configuration is still possible, the newer one is preferred.

The new approach is to specify a full namespace+node ID in the format `ns=1;i=1` which also allows to use the other node ID formats (like numeric, GUID/UUID or opaque). If the `node` parameter is used the older ones must not be used. The syntax of this node format is a set of `key=value` pairs delimited by a semi-colon (`;`).

Exactly one namespace and one node id key must be used. See the following table for possible keys:

  
| Key | Type | Description |
| --- | --- | --- |
| **ns** | namespace | Numeric namespace index |
| **nsu** | namespace | Namespace URI |
| **s** | node | String node ID |
| **i** | node | Numeric node ID |
| **g** | node | GUID/UUID node ID |
| **b** | node | Base64 encoded string for opaque node ID |

As the values generated by the syntax cannot be transparently encoded into a URI parameter value, it is necessary to escape them. However Camel allows to wrap the actual value inside `RAW(…)`, which makes escaping unnecessary. For example:

milo-client:opc.tcp://user:password@localhost:12345?node=RAW(nsu=http://foo.bar;s=foo/bar)

### Method ID

It is possible to perform methods calls on OPC UA nodes. If the parameter `method` is set to the Node ID of a method call (the node ID must be set to the parent object in this case), then a method call will be performed instead of a write operation.

Input parameters are taken from the body:

-   If the body is null, then an empty `Variant[]` will be used
    
-   If the body is a `Variant[]`, then it will be used as is
    
-   If the body is a `Variant`, then it will be wrapped in a `Variant[]` array
    
-   Otherwise the body will be converted into a `Variant` and wrapped in an array of `Variant[]`
    

### Read Values from Nodes

The component provide a producer to read values from multiple opc-ua nodes. The Node-IDs will be defined in the header `CamelMiloNodeIds` as list of strings. (see [Node-ID](#nodeid) for the ID format).

Example:

```java
from("direct:start")
    .setHeader("CamelMiloNodeIds", constant(Arrays.asList("nsu=urn:org:apache:camel;s=myitem1")))
    .setHeader("CamelMiloAwait", constant(true)) // CamelMiloAwait: parameter "defaultAwaitWrites"
        .enrich("milo-client:opc.tcp://localhost:4334", new AggregationStrategy() {

            @Override
            public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {
                return newExchange;
            }
        }).to("mock:test1");
```

### Custom data types: accessing the underlying milo OpcUaClient

Built-in OPC UA data types are read and written transparently. Values whose node has a **custom** (server-defined) data type are instead returned as an `org.eclipse.milo.opcua.stack.core.types.builtin.ExtensionObject`, which can only be decoded (or, for writes, encoded) with an `EncodingContext` obtained from the underlying milo client.

The component does not decode these values automatically, because it cannot reliably determine which encoding context applies. Instead, the active `OpcUaClient` is exposed through `MiloClientConnection.getOpcUaClient()`, so you can obtain its encoding contexts and perform the encode/decode yourself:

```java
MiloClientEndpoint endpoint = context.getEndpoint("milo-client:opc.tcp://localhost:4334", MiloClientEndpoint.class);
MiloClientConnection connection = endpoint.createConnection();
try {
    OpcUaClient client = connection.getOpcUaClient();
    // dynamic context resolves custom, server-defined types; static context covers built-in/generated types
    EncodingContext encodingContext = client.getDynamicEncodingContext();

    // decode a value read as ExtensionObject
    UaStructuredType decoded = extensionObject.decode(encodingContext);

    // or encode a structure before writing it
    ExtensionObject toWrite = ExtensionObject.encode(encodingContext, myStructure);
} finally {
    endpoint.releaseConnection(connection);
}
```

> **Note**
> The connection is established lazily and asynchronously, so `getOpcUaClient()` returns `null` until the client is connected, and again briefly while a connection is being re-established. The client is owned and managed by Camel: do not connect, disconnect or otherwise change its lifecycle, and fetch it on demand rather than caching the reference, as a reconnect replaces the instance.

### Security policies

When setting the allowing security policies is it possible to use the well known OPC UA URIs (e.g. `http://opcfoundation.org/UA/SecurityPolicy#Basic128Rsa15`) or to use the Milo enum literals (e.g. `None`). Specifying an unknown security policy URI or enum is an error.

The known security policy URIs and enum literals are can be seen here: [SecurityPolicy.java](https://github.com/eclipse/milo/blob/master/opc-ua-stack/stack-core/src/main/java/org/eclipse/milo/opcua/stack/core/security/SecurityPolicy.java)

> **Note**
> In any case security policies are considered case sensitive.

#### Milo 1.0.5 Migration Notes

With Milo 1.0.5, several security-related API changes were introduced:

-   The `ServerCertificateValidator` class has been replaced with `CertificateValidator` in the core security package
    
-   Certificate validation now uses `org.eclipse.milo.opcua.stack.core.security.CertificateValidator`
    
-   When configuring custom certificate validators, ensure you’re using the updated API
    

## Spring Boot Auto-Configuration

When using milo-client with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-milo-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 74 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.milo-browse.allowed-security-policies** | A set of allowed security policy URIs. Default is to accept all and use the highest. |  | String |
| **camel.component.milo-browse.application-name** | The application name. | Apache Camel adapter for Eclipse Milo | String |
| **camel.component.milo-browse.application-uri** | The application URI. | [http://camel.apache.org/EclipseMilo/Client](http://camel.apache.org/EclipseMilo/Client) | String |
| **camel.component.milo-browse.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.milo-browse.channel-lifetime** | Channel lifetime in milliseconds. |  | Long |
| **camel.component.milo-browse.client-id** | A virtual client id to force the creation of a new connection instance. |  | String |
| **camel.component.milo-browse.configuration** | All default options for client configurations. The option is a org.apache.camel.component.milo.client.MiloClientConfiguration type. |  | MiloClientConfiguration |
| **camel.component.milo-browse.discovery-endpoint-suffix** | A suffix for endpoint URI when discovering. |  | String |
| **camel.component.milo-browse.discovery-endpoint-uri** | An alternative discovery URI. |  | String |
| **camel.component.milo-browse.enabled** | Whether to enable auto configuration of the milo-browse component. This is enabled by default. |  | Boolean |
| **camel.component.milo-browse.key-alias** | The name of the key in the keystore file. |  | String |
| **camel.component.milo-browse.key-password** | The key password. |  | String |
| **camel.component.milo-browse.key-store-password** | The keystore password. |  | String |
| **camel.component.milo-browse.key-store-type** | The key store type. |  | String |
| **camel.component.milo-browse.key-store-url** | The URL where the key should be loaded from. |  | String |
| **camel.component.milo-browse.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.milo-browse.max-pending-publish-requests** | The maximum number of pending publish requests. |  | Long |
| **camel.component.milo-browse.max-response-message-size** | The maximum number of bytes a response message may have. |  | Long |
| **camel.component.milo-browse.milo-client-connection-manager** | Instance for managing client connections. The option is a org.apache.camel.component.milo.client.MiloClientConnectionManager type. |  | MiloClientConnectionManager |
| **camel.component.milo-browse.override-host** | Override the server reported endpoint host with the host from the endpoint URI. | false | Boolean |
| **camel.component.milo-browse.override-port** | Override the server reported endpoint port with the port from the endpoint URI. | false | Boolean |
| **camel.component.milo-browse.product-uri** | The product URI. | [http://camel.apache.org/EclipseMilo](http://camel.apache.org/EclipseMilo) | String |
| **camel.component.milo-browse.request-timeout** | Request timeout in milliseconds. |  | Long |
| **camel.component.milo-browse.requested-publishing-interval** | The requested publishing interval in milliseconds. |  | Double |
| **camel.component.milo-browse.session-name** | Session name. |  | String |
| **camel.component.milo-browse.session-timeout** | Session timeout in milliseconds. |  | Long |
| **camel.component.milo-client.allowed-security-policies** | A set of allowed security policy URIs. Default is to accept all and use the highest. |  | String |
| **camel.component.milo-client.application-name** | The application name. | Apache Camel adapter for Eclipse Milo | String |
| **camel.component.milo-client.application-uri** | The application URI. | [http://camel.apache.org/EclipseMilo/Client](http://camel.apache.org/EclipseMilo/Client) | String |
| **camel.component.milo-client.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.milo-client.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.milo-client.channel-lifetime** | Channel lifetime in milliseconds. |  | Long |
| **camel.component.milo-client.client-id** | A virtual client id to force the creation of a new connection instance. |  | String |
| **camel.component.milo-client.configuration** | All default options for client configurations. The option is a org.apache.camel.component.milo.client.MiloClientConfiguration type. |  | MiloClientConfiguration |
| **camel.component.milo-client.discovery-endpoint-suffix** | A suffix for endpoint URI when discovering. |  | String |
| **camel.component.milo-client.discovery-endpoint-uri** | An alternative discovery URI. |  | String |
| **camel.component.milo-client.enabled** | Whether to enable auto configuration of the milo-client component. This is enabled by default. |  | Boolean |
| **camel.component.milo-client.key-alias** | The name of the key in the keystore file. |  | String |
| **camel.component.milo-client.key-password** | The key password. |  | String |
| **camel.component.milo-client.key-store-password** | The keystore password. |  | String |
| **camel.component.milo-client.key-store-type** | The key store type. |  | String |
| **camel.component.milo-client.key-store-url** | The URL where the key should be loaded from. |  | String |
| **camel.component.milo-client.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.milo-client.max-pending-publish-requests** | The maximum number of pending publish requests. |  | Long |
| **camel.component.milo-client.max-response-message-size** | The maximum number of bytes a response message may have. |  | Long |
| **camel.component.milo-client.milo-client-connection-manager** | Instance for managing client connections. The option is a org.apache.camel.component.milo.client.MiloClientConnectionManager type. |  | MiloClientConnectionManager |
| **camel.component.milo-client.override-host** | Override the server reported endpoint host with the host from the endpoint URI. | false | Boolean |
| **camel.component.milo-client.override-port** | Override the server reported endpoint port with the port from the endpoint URI. | false | Boolean |
| **camel.component.milo-client.product-uri** | The product URI. | [http://camel.apache.org/EclipseMilo](http://camel.apache.org/EclipseMilo) | String |
| **camel.component.milo-client.request-timeout** | Request timeout in milliseconds. |  | Long |
| **camel.component.milo-client.requested-publishing-interval** | The requested publishing interval in milliseconds. |  | Double |
| **camel.component.milo-client.session-name** | Session name. |  | String |
| **camel.component.milo-client.session-timeout** | Session timeout in milliseconds. |  | Long |
| **camel.component.milo-server.application-name** | The application name. |  | String |
| **camel.component.milo-server.application-uri** | The application URI. |  | String |
| **camel.component.milo-server.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.milo-server.bind-addresses** | Set the addresses of the local addresses the server should bind to. |  | String |
| **camel.component.milo-server.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.milo-server.build-info** | Server build info. The option is a org.eclipse.milo.opcua.stack.core.types.structured.BuildInfo type. |  | BuildInfo |
| **camel.component.milo-server.certificate** | Server certificate. The option is a java.security.cert.X509Certificate type. |  | X509Certificate |
| **camel.component.milo-server.certificate-manager** | Server certificate manager. The option is a org.eclipse.milo.opcua.stack.core.security.CertificateManager type. |  | CertificateManager |
| **camel.component.milo-server.certificate-validator** | Validator for client certificates. The option is a org.eclipse.milo.opcua.stack.core.security.CertificateValidator type. |  | CertificateValidator |
| **camel.component.milo-server.default-certificate-validator** | Validator for client certificates using default file based approach. |  | String |
| **camel.component.milo-server.enable-anonymous-authentication** | Enable anonymous authentication, disabled by default. | false | Boolean |
| **camel.component.milo-server.enabled** | Whether to enable auto configuration of the milo-server component. This is enabled by default. |  | Boolean |
| **camel.component.milo-server.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.milo-server.namespace-uri** | The URI of the namespace, defaults to urn:org:apache:camel. | urn:org:apache:camel | String |
| **camel.component.milo-server.path** | The path to be appended to the end of the endpoint url. (doesn’t need to start with '/'). |  | String |
| **camel.component.milo-server.port** | The TCP port the server binds to. |  | Integer |
| **camel.component.milo-server.product-uri** | The product URI. |  | String |
| **camel.component.milo-server.security-policies** | Security policies. |  | Set |
| **camel.component.milo-server.security-policies-by-id** | Security policies by URI or name. Multiple policies can be separated by comma. |  | String |
| **camel.component.milo-server.user-authentication-credentials** | Set user password combinations in the form of user1:pwd1,user2:pwd2 Usernames and passwords will be URL decoded. |  | String |
| **camel.component.milo-server.username-security-policy-uri** | Set the UserTokenPolicy used when. |  | SecurityPolicy |