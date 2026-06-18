# OPC UA Browser

**Since Camel 3.15**

**Only producer is supported**

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

milo-browse:opc.tcp://\[user:password@\]host:port/path/to/service?node=RAW(nsu=urn:foo:bar;s=item-1)

Please refer to the [Milo Client](milo-client-component.md) component for further details about the construction of the URI.

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

The OPC UA Browser component supports 25 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (producer) | A virtual client id to force the creation of a new connection instance. |  | String |
| **configuration** (producer) | All default options for client configurations. |  | MiloClientConfiguration |
| **discoveryEndpointSuffix** (producer) | A suffix for endpoint URI when discovering. |  | String |
| **discoveryEndpointUri** (producer) | An alternative discovery URI. |  | String |
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

The OPC UA Browser endpoint is configured using URI syntax:

milo-browse:endpointUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpointUri** (producer) | **Required** The OPC UA server endpoint. |  | String |

### Query Parameters (30 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (producer) | A virtual client id to force the creation of a new connection instance. |  | String |
| **depth** (producer) | When browsing recursively into sub-types, what’s the maximum search depth for diving into the tree. Default value notice: Maximum depth for browsing recursively (only if recursive = true). | 3 | int |
| **direction** (producer) | 
The direction to browse (forward, inverse, …​). Default value notice: The direction to browse; see org.eclipse.milo.opcua.stack.core.types.enumerated.BrowseDirection.

Enum values:

-   Forward
    
-   Inverse
    
-   Both
    





 | Forward | BrowseDirection |
| **discoveryEndpointSuffix** (producer) | A suffix for endpoint URI when discovering. |  | String |
| **discoveryEndpointUri** (producer) | An alternative discovery URI. |  | String |
| **filter** (producer) | Filter out node ids to limit browsing. Default value notice: Regular filter expression matching node ids. | None | String |
| **includeSubTypes** (producer) | Whether to include sub-types for browsing; only applicable for non-recursive browsing. | true | boolean |
| **maxNodeIdsPerRequest** (producer) | The maximum number node ids requested per server call. Default value notice: Maximum number of node ids requested per browse call (applies to browsing sub-types only; only if recursive = true). | 10 | int |
| **node** (producer) | The node definition (see Node ID). Default value notice: Root folder as per OPC-UA spec. | ns=0;id=84 | String |
| **nodeClasses** (producer) | The mask indicating the node classes of interest in browsing. Default value notice: Comma-separated node class list; see org.eclipse.milo.opcua.stack.core.types.enumerated.NodeClass. | Variable,Object,DataType | String |
| **recursive** (producer) | Whether to browse recursively into sub-types, ignores includeSubTypes setting as it’s implied to be set to true. Default value notice: Whether to recursively browse sub-types: truefalse. | false | boolean |
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

The OPC UA Browser component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMiloNodeIds** (producer) Constant: [`HEADER_NODE_IDS`](https://javadoc.io/doc/org.apache.camel/camel-milo/latest/org/apache/camel/component/milo/MiloConstants.html#HEADER_NODE_IDS) | The node ids. |  | List |

### Client

The browse component shares the same base options like the Camel Milo Client component, e.g. concerning topics like discovery, security policies, the construction of node ids, etc.

Please refer to the documentation of the Camel Milo Client component for further details.

### Browsing

The main use of this component is to be able to determine the nodes values to be retrieved or to be written by first browsing the node tree of the OPC-UA server, e.g. to avoid hard-coding a significant number of node ids within the configuration of Camel routes. The component is designed to work in conjunction with the Camel Milo Client component as illustrated in the following example:

_Java-only: browsing OPC UA nodes and enriching with client values_

```java
from("direct:start")

    // Browse sub tree
    .setHeader("CamelMiloNodeIds", constant(Arrays.asList("ns=1;s=folder-id")))
    .enrich("milo-browse:opc.tcp://localhost:4334", (oldExchange, newExchange) -> newExchange)

    // Filter specific ids
    .filter(...)

        // Retrieve the values for the nodes of interest
        .enrich("milo-client:opc.tcp://localhost:4334", (oldExchange, newExchange) -> newExchange)
```

### Recursion

Dependent to the OPC-UA server there it might be required to browse a hierarchy of nodes. Be aware that this is potentially a very expensive operation.

### Milo 1.0.5 Migration Notes

With Milo 1.0.5, the browse API remains largely compatible, but shares the same security-related changes as the client and server components. Please refer to the [Milo Client](milo-client-component.md) documentation for details on security configuration changes.

## Spring Boot Auto-Configuration

When using milo-browse with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

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