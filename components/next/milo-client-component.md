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

As an alternative to URI-embedded credentials (`user:password`), you can provide credentials explicitly using the endpoint parameters `username` and `password`. This is recommended when credentials contain special characters (for example `?`, `/`, `@`, `&`, `%`(%25)) that can make URI-embedded credentials difficult to handle.

For example:

milo-client:opc.tcp://host:port/path/to/service?node=RAW(nsu=urn:foo:bar;s=item-1)&username=RAW(my?user@name)&password=RAW(p@ss/w&rd)

When both styles are provided, the explicit `username`/`password` parameters take precedence over credentials embedded in the URI.

All configuration options in the group client are applicable to the shared client instance. Endpoints will share client instances for each endpoint URI plus `requestedPublishingInterval`. So the first time a request for that endpoint URI (plus `requestedPublishingInterval`) is made, the options of the client group are applied. All further instances will be ignored.

If you need alternate options for the same endpoint URI it is possible though to set the clientId option which will be added internally to the endpoint URI in order to select a different shared connection instance. In other words, shared connections located by the combination of endpoint URI, `requestedPublishingInterval` and client id.

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

The OPC UA Client component supports the following options which are listed below.

   
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
| **reconnectTimeout** (client) | The delay in milliseconds before the client tries again to connect to the server after an attempt failed, and between two attempts to create the monitored items that the server refused. Neither attempt is made while the OPC UA client recovers a lost session on its own. | 10000 | long |
| **requestedPublishingInterval** (client) | The requested publishing interval in milliseconds. | 1\_000.0 | Double |
| **requestTimeout** (client) | Request timeout in milliseconds. |  | Long |
| **sessionName** (client) | Session name. |  | String |
| **sessionTimeout** (client) | Session timeout in milliseconds. |  | Long |
| **certificateValidator** (security) | A custom validator for the certificate of the OPC UA server. When set, it is used instead of the trust list configured with trustListDirectory. Endpoints share a connection only when they use the same validator instance. |  | CertificateValidator |
| **password** (security) | The password for authentication. Use this instead of embedding credentials in the endpoint URI when the password contains special characters (such as \\{code }, \\{code /}, \\{code }, \\{code &}). |  | String |
| **trustAllCertificates** (security) | Whether to accept any certificate presented by the OPC UA server. This is insecure: the connection is encrypted, but the client does not authenticate the server it talks to. It only applies when neither certificateValidator nor trustListDirectory is configured. | false | boolean |
| **trustListDirectory** (security) | The directory holding the trust list used to validate the certificate of the OPC UA server, in the layout used by Eclipse Milo: trusted certificates in trusted/certs, CRLs of trusted certificates in trusted/crl, certificates of issuing CAs in issuer/certs and their CRLs in issuer/crl. The directories are created if they do not exist. Besides the chain of trust, the validity period, the revocation by a CRL of the trust list and the application URI of the server certificate are checked. A certificate issued by a CA is refused when the trust list holds no CRL of that CA; an empty CRL is enough. A server certificate that does not chain up to a trusted certificate is written to rejected/certs, from where it can be moved to trusted/certs once it has been checked. |  | String |
| **username** (security) | The username for authentication. Use this instead of embedding credentials in the endpoint URI when the username contains special characters (such as \\{code }, \\{code /}, \\{code }, \\{code &}). |  | String |

## Endpoint Options

The OPC UA Client endpoint is configured using URI syntax:

milo-client:endpointUri

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpointUri** (common) | **Required** The OPC UA server endpoint. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | A virtual client id to force the creation of a new connection instance. |  | String |
| **dataChangeFilterDeadbandType** (common) | Deadband type for MonitorFilterType DataChangeFilter. | 0 | Integer |
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
| **omitNullValues** (common) | Omit a data change whose value is null and whose status is Good. A data change with a Bad or Uncertain status is always delivered. | true | boolean |
| **queueSize** (common) | The queue size used for OPC UA subscriptions. If not set, a queue size of 1 is requested. |  | Integer |
| **samplingInterval** (common) | The sampling interval in milliseconds. | 1000.0 | Double |
| **nodes** (consumer) | Comma-separated node definitions to monitor with one consumer, instead of node (see Node ID). |  | String |
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
| **reconnectTimeout** (client) | The delay in milliseconds before the client tries again to connect to the server after an attempt failed, and between two attempts to create the monitored items that the server refused. Neither attempt is made while the OPC UA client recovers a lost session on its own. | 10000 | long |
| **requestedPublishingInterval** (client) | The requested publishing interval in milliseconds. | 1\_000.0 | Double |
| **requestTimeout** (client) | Request timeout in milliseconds. |  | Long |
| **sessionName** (client) | Session name. |  | String |
| **sessionTimeout** (client) | Session timeout in milliseconds. |  | Long |
| **certificateValidator** (security) | A custom validator for the certificate of the OPC UA server. When set, it is used instead of the trust list configured with trustListDirectory. Endpoints share a connection only when they use the same validator instance. |  | CertificateValidator |
| **password** (security) | The password for authentication. Use this instead of embedding credentials in the endpoint URI when the password contains special characters (such as \\{code }, \\{code /}, \\{code }, \\{code &}). |  | String |
| **trustAllCertificates** (security) | Whether to accept any certificate presented by the OPC UA server. This is insecure: the connection is encrypted, but the client does not authenticate the server it talks to. It only applies when neither certificateValidator nor trustListDirectory is configured. | false | boolean |
| **trustListDirectory** (security) | The directory holding the trust list used to validate the certificate of the OPC UA server, in the layout used by Eclipse Milo: trusted certificates in trusted/certs, CRLs of trusted certificates in trusted/crl, certificates of issuing CAs in issuer/certs and their CRLs in issuer/crl. The directories are created if they do not exist. Besides the chain of trust, the validity period, the revocation by a CRL of the trust list and the application URI of the server certificate are checked. A certificate issued by a CA is refused when the trust list holds no CRL of that CA; an empty CRL is enough. A server certificate that does not chain up to a trusted certificate is written to rejected/certs, from where it can be moved to trusted/certs once it has been checked. |  | String |
| **username** (security) | The username for authentication. Use this instead of embedding credentials in the endpoint URI when the username contains special characters (such as \\{code }, \\{code /}, \\{code }, \\{code &}). |  | String |

## Message Headers

The OPC UA Client component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMiloNodeIds** (producer) Constant: [`HEADER_NODE_IDS`](https://javadoc.io/doc/org.apache.camel/camel-milo/latest/org/apache/camel/component/milo/MiloConstants.html#HEADER_NODE_IDS) | The node ids. |  | List |
| **CamelMiloAwait** (producer) Constant: [`HEADER_AWAIT`](https://javadoc.io/doc/org.apache.camel/camel-milo/latest/org/apache/camel/component/milo/MiloConstants.html#HEADER_AWAIT) | The await setting for writes. |  | Boolean |
| **CamelMiloNodeId** (consumer) Constant: [`HEADER_NODE_ID`](https://javadoc.io/doc/org.apache.camel/camel-milo/latest/org/apache/camel/component/milo/MiloConstants.html#HEADER_NODE_ID) | The node ID of the value, as configured in the node or nodes option. Not to be confused with CamelMiloNodeIds, the list of nodes that the producer reads. |  | String |

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

A producer request for a node whose namespace URI (`nsu=`) is not in the namespace table of the server is answered like a request for a node that the server does not have. A write returns the status code `Bad_NodeIdUnknown`. A read, or a browse of the [Milo Browse](milo-browse-component.md) component, returns that status code for this node and the results of the other nodes. The connection and the consumers that share it are not affected.

### Monitoring and writing a node

The following routes monitor one node and write another, on the server of the [OPC UA Server](milo-server-component.md) example. A consumer receives a `DataValue` for each change, and `${body.value.value}` is the value. A producer writes the message body to its node:

```yaml
- route:
    from:
      uri: milo-client:opc.tcp://localhost:12685
      parameters:
        node: "RAW(nsu=urn:org:apache:camel;s=temperature)"
        samplingInterval: 1000
        username: camel
        password: secret
        allowedSecurityPolicies: None
      steps:
        - log:
            message: "Temperature: ${body.value.value}"
- route:
    from:
      uri: timer:setpoint
      parameters:
        repeatCount: 1
      steps:
        - setBody:
            expression:
              constant:
                expression: "42"
        - to:
            uri: milo-client:opc.tcp://localhost:12685
            parameters:
              node: "RAW(nsu=urn:org:apache:camel;s=setpoint)"
              username: camel
              password: secret
              allowedSecurityPolicies: None
```

### Monitoring several nodes

A consumer can monitor several nodes with the `nodes` option instead of `node` (the two options cannot be combined). The consumer creates the monitored items of all nodes together and deletes them together when it stops. Every value arrives in its own exchange, and the `CamelMiloNodeId` header holds the node ID as it was configured.

The `nodes` option takes a comma-separated list of [Node IDs](#nodeid). The entries are trimmed, empty entries are skipped and a node that is listed twice is monitored once:

milo-client:opc.tcp://localhost:12345?nodes=RAW(ns=2;s=line1/temperature,ns=2;s=line1/pressure)

A string node ID that contains a comma cannot be used in `nodes`; monitor it with the `node` option instead. Long lists can come from a property placeholder, for example `nodes=RAW({{tags}})`.

All nodes of the list share the `samplingInterval`, `queueSize` and `omitNullValues` options of the consumer and its monitor filter (`monitorFilterType`, `dataChangeFilter*`). Tags that need a different sampling interval or deadband need a consumer of their own.

A node that does not exist on the server does not affect the other nodes. A node that cannot be monitored is reported once with its status code, and Camel tries to create its monitored item again every `reconnectTimeout` (10 seconds by default) while the connection lasts, for all such nodes of the connection in one request. A failed attempt delivers nothing; once the item is created, the node delivers its current value as its first value. This covers a node that is added to the server later, for example with a new PLC program, and a server that refused the item because it had too many. A rebuilt connection creates the monitored items of all nodes again, and a stopped consumer is not retried. A node whose namespace URI (`nsu=`) is not in the namespace table of the server is reported and retried in the same way, so a namespace that the server adds later is found. The consumer delivers one exchange with the bad status code for such a node, and the `CamelMiloNodeId` header names it.

The `milo-client` developer console (`/q/dev/milo-client`, for example with `camel run --console`) shows which nodes are not monitored: for each connection of the consumers, it lists the routes that use it, whether its session is active, the number of monitored nodes, and the refused nodes, each with the status of the latest attempt to create its monitored item. Reading it does not wait for a request to the server in progress.

### Status codes and null values

A data change with a Bad or Uncertain status is always delivered, even when its value is null; `omitNullValues` only omits a null value with a Good status. This includes the first notification of a monitored item: it carries the current value of the node, at startup and again after a reconnect, so it can be a Bad status such as `Bad_WaitingForInitialData` or the status of a `milo-server` item that was not written yet. To skip such a notification, a route filters on its status code (`getStatusCode()` of the `DataValue` body); a filter on `isGood()` would also drop the Bad status of a failed sensor.

The default `omitNullValues=true` also omits a null value with a Good status that follows a Bad status, so the route does not learn that the node recovered. Set `omitNullValues=false` for a node whose value can be null, such as a `String`.

### Communication loss and recovery

When the client loses communication with the server, every node that a consumer monitors delivers an exchange with the status `Bad_NoCommunication` and a null value, stamped with the time the client recognised the loss. Communication is lost when the session with the server stops being active, for example because the network connection closed or the server stopped answering, and when Camel rebuilds the connection. With the default settings, a connection that stops answering without closing is recognised after 10 to 15 seconds. A consumer that starts while the server cannot be reached delivers the status for its nodes when it starts. A node delivers the status once per loss; a node that the server refused to monitor keeps the status of that refusal instead, and nothing is delivered when a consumer stops or the Camel context shuts down.

Once communication is restored, every node delivers its current value, also when the value did not change. In the existing session, Camel asks the server to send the current values again with the `ResendData` method; when the server does not provide it, Camel creates the subscription again, and the values the server queued during the loss are not delivered. Values can arrive more than once after a loss, and a value received before Camel rebuilt the connection can arrive after the first value of the new connection. A route that counts values, computes differences or detects changes must tolerate this. A value that did not change during the loss keeps its earlier timestamps.

Routes run while communication is lost. An OPC UA request that a route makes while the client reconnects, for example a write, waits for the next reconnect attempt and is sent if that attempt succeeds, so it can take effect after communication is restored. A request that fails completes with its failure; the connection is kept, and a lost session is recovered by the client as described above. The client recovers it with the endpoint and the server certificate it found when it connected, so a server that changes either while it cannot be reached is reached again only when Camel rebuilds the connection, for example when the Camel context restarts. A request does not wait while a consumer of the same connection creates or deletes its monitored items.

Camel keeps no last value. A route that needs one keeps the last good value of each node itself. To recognise the status, check the status code of the `DataValue` body, for example with `${body.statusCode.bad}`.

### Subscriptions that stop publishing

The consumers of a connection share one subscription on the server. When the server stops publishing for it (no notification or keep-alive within about one and a half keep-alive intervals), Camel checks whether the server still has the subscription. If the server does not confirm it, or when the server reports that the subscription timed out (`Bad_Timeout`), Camel deletes it and, once the server has confirmed that it is gone, creates it again in the existing session. A node that can no longer be monitored is reported as described above and does not affect the other nodes.

A route that is slow to process a value stops the publishing as well, because the client asks the server for more notifications only as the routes finish processing the ones it received. The subscription is then kept, unless the route takes longer than the lifetime of the subscription, which lets it time out on the server.

A check or a delete that fails because the connection was lost is left to the session recovery of the client, which restores the session once the server can be reached again. The subscription then resumes publishing, or it is created again as above when the server no longer has it. If the server no longer has the session either, for example after a restart, the subscription cannot be transferred to a new session and the connection is rebuilt. A network that drops silently can stop the publishing before the client notices that the connection is lost; if the network is back before that, the check reaches the server and is handled as above.

Any other failure of the delete, or a subscription that cannot be created again, rebuilds the connection to the server. After the subscription is recreated, every monitored item delivers its current value again, and value changes in between are not delivered.

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

-   Java
    
-   YAML
    

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

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelMiloNodeIds
            expression:
              groovy:
                expression: "['nsu=urn:org:apache:camel;s=myitem1']"
        - setHeader:
            name: CamelMiloAwait
            expression:
              constant:
                expression: "true"
        - enrich:
            expression:
              constant:
                expression: milo-client:opc.tcp://localhost:4334
        - to:
            uri: mock:test1
```

The read is asynchronous. Without the `CamelMiloAwait` header, or `defaultAwaitWrites=true` on the endpoint, the route goes on before the values are in the body.

### Custom data types: accessing the underlying milo OpcUaClient

Built-in OPC UA data types are read and written transparently. Values whose node has a **custom** (server-defined) data type are instead returned as an `org.eclipse.milo.opcua.stack.core.types.builtin.ExtensionObject`, which can only be decoded (or, for writes, encoded) with an `EncodingContext` obtained from the underlying milo client.

The component does not decode these values automatically, because it cannot reliably determine which encoding context applies. Instead, the active `OpcUaClient` is exposed through `MiloClientConnection.getOpcUaClient()`, so you can obtain its encoding contexts and perform the encode/decode yourself:

_Java-only: accessing the underlying OpcUaClient for custom data type encoding/decoding_

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

When `allowedSecurityPolicies` is not set, the client accepts every security policy the server offers and uses the endpoint with the highest security level reported by the server, which can be `None`. To make sure the connection is secured, set `allowedSecurityPolicies` to the secured policies you expect the server to offer.

### Validating the server certificate

When the selected endpoint uses a security policy other than `None`, the client validates the certificate of the server when it opens the secure channel and the session. Configure the trusted certificates with one of these options:

-   `trustListDirectory`: a directory holding the trust list, in the layout used by Eclipse Milo. Put the certificate of the server, or the certificate of the CA that issued it, in `trusted/certs`. Certificates of intermediate CAs that are only used to build the chain go in `issuer/certs`, and certificate revocation lists in `trusted/crl` and `issuer/crl`. The directories are created if they do not exist.
    
-   `certificateValidator`: a custom `org.eclipse.milo.opcua.stack.core.security.CertificateValidator`. It is used instead of `trustListDirectory` when both are set. Endpoints share a connection only when they use the same validator instance.
    

With `trustListDirectory`, the client refuses a server certificate that:

-   does not chain up to a certificate in `trusted/certs`, possibly through the certificates in `issuer/certs`,
    
-   is outside its validity period,
    
-   is revoked by a certificate revocation list in `trusted/crl` or `issuer/crl`. A certificate issued by a CA is also refused, with `Bad_CertificateRevocationUnknown`, when the trust list holds no revocation list of that CA. An empty CRL signed by the CA is enough. A self-signed certificate in `trusted/certs` is not checked for revocation,
    
-   or holds an application URI that differs from the one the server announces in its endpoint description.
    

A failed host name, key usage or extended key usage check is only logged. A certificate that does not chain up to a trusted certificate is written to `rejected/certs`, from where it can be moved to `trusted/certs` once it has been checked. A certificate refused for another reason is not written there. To use other checks, configure a `certificateValidator`, for example a `DefaultClientCertificateValidator` created with the `ValidationCheck` set you need.

If neither option is configured, the client does not connect to an endpoint that uses a security policy other than `None`. Setting `trustAllCertificates` to `true` makes the client accept any server certificate instead. This is insecure: the connection is encrypted, but the client does not authenticate the server it talks to.

When the server certificate cannot be validated, the client logs a `WARN` message that starts with `Failed to connect`, and tries again after `reconnectTimeout` (10 seconds by default), so a certificate moved to `trusted/certs` is used at the next attempt. A producer fails with `IllegalStateException: No connected`, whose cause gives the reason.

The same validator checks the server certificate that the user name and password are encrypted with. With the security policy `None`, the server is not authenticated, whatever the configuration.

A secured policy also requires a client certificate and key, configured with `keyStoreUrl` and the related options. For example:

milo-client:opc.tcp://localhost:4840?node=RAW(ns=2;s=Temperature)&allowedSecurityPolicies=Basic256Sha256&keyStoreUrl=file:/etc/opcua/client.p12&keyStorePassword=RAW(changeit)&keyAlias=client&keyPassword=RAW(changeit)&trustListDirectory=/etc/opcua/pki

#### Milo 1.0.5 Migration Notes

With Milo 1.0.5, several security-related API changes were introduced:

-   The `ServerCertificateValidator` class has been replaced with `CertificateValidator` in the core security package
    
-   Certificate validation now uses `org.eclipse.milo.opcua.stack.core.security.CertificateValidator`
    
-   A validator configured with the `certificateValidator` option must implement this interface