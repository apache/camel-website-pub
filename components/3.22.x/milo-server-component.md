# OPC UA Server

**Since Camel 2.19**

**Both producer and consumer are supported**

The Milo Server component provides an OPC UA server using the [Eclipse Milo™](http://eclipse.org/milo) implementation.

**Java 9+**: This component requires Java 9+ at runtime.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-milo</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

Messages sent to the endpoint from Camel will be available from the OPC UA server to OPC UA Clients. Value write requests from OPC UA Client will trigger messages which are sent into Apache Camel.

## URI format

milo-server:itemId\[?options\]

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

The OPC UA Server component supports 20 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | The application name. |  | String |
| **applicationUri** (common) | The application URI. |  | String |
| **bindAddresses** (common) | Set the addresses of the local addresses the server should bind to. |  | String |
| **buildInfo** (common) | Server build info. |  | BuildInfo |
| **namespaceUri** (common) | The URI of the namespace, defaults to urn:org:apache:camel. | urn:org:apache:camel | String |
| **path** (common) | The path to be appended to the end of the endpoint url. (doesn’t need to start with '/'). |  | String |
| **port** (common) | The TCP port the server binds to. |  | int |
| **productUri** (common) | The product URI. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **certificate** (security) | Server certificate. |  | X509Certificate |
| **certificateManager** (security) | Server certificate manager. |  | CertificateManager |
| **certificateValidator** (security) | Validator for client certificates. |  | ServerCertificateValidator |
| **defaultCertificateValidator** (security) | Validator for client certificates using default file based approach. |  | String |
| **enableAnonymousAuthentication** (security) | Enable anonymous authentication, disabled by default. | false | boolean |
| **securityPolicies** (security) | Security policies. |  | Set |
| **securityPoliciesById** (security) | Security policies by URI or name. Multiple policies can be separated by comma. |  | String |
| **userAuthenticationCredentials** (security) | Set user password combinations in the form of user1:pwd1,user2:pwd2 Usernames and passwords will be URL decoded. |  | String |
| **usernameSecurityPolicyUri** (security) | 
Set the UserTokenPolicy used when.

Enum values:

-   None
    
-   Basic128Rsa15
    
-   Basic256
    
-   Basic256Sha256
    
-   Aes128\_Sha256\_RsaOaep
    
-   Aes256\_Sha256\_RsaPss
    





 |  | SecurityPolicy |

## Endpoint Options

The OPC UA Server endpoint is configured using URI syntax:

milo-server:itemId

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **itemId** (common) | **Required** ID of the item. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Spring Boot Auto-Configuration

When using milo-server with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-milo-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 72 options, which are listed below.

   
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
| **camel.component.milo-browse.product-uri** | The product URI. | [http://camel.apache.org/EclipseMilo](http://camel.apache.org/EclipseMilo) | String |
| **camel.component.milo-browse.request-timeout** | Request timeout in milliseconds. |  | Long |
| **camel.component.milo-browse.requested-publishing-interval** | The requested publishing interval in milliseconds. |  | Double |
| **camel.component.milo-browse.session-name** | Session name. |  | String |
| **camel.component.milo-browse.session-timeout** | Session timeout in milliseconds. |  | Long |
| **camel.component.milo-client.allowed-security-policies** | A set of allowed security policy URIs. Default is to accept all and use the highest. |  | String |
| **camel.component.milo-client.application-name** | The application name. | Apache Camel adapter for Eclipse Milo | String |
| **camel.component.milo-client.application-uri** | The application URI. | [http://camel.apache.org/EclipseMilo/Client](http://camel.apache.org/EclipseMilo/Client) | String |
| **camel.component.milo-client.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.milo-client.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
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
| **camel.component.milo-client.product-uri** | The product URI. | [http://camel.apache.org/EclipseMilo](http://camel.apache.org/EclipseMilo) | String |
| **camel.component.milo-client.request-timeout** | Request timeout in milliseconds. |  | Long |
| **camel.component.milo-client.requested-publishing-interval** | The requested publishing interval in milliseconds. |  | Double |
| **camel.component.milo-client.session-name** | Session name. |  | String |
| **camel.component.milo-client.session-timeout** | Session timeout in milliseconds. |  | Long |
| **camel.component.milo-server.application-name** | The application name. |  | String |
| **camel.component.milo-server.application-uri** | The application URI. |  | String |
| **camel.component.milo-server.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.milo-server.bind-addresses** | Set the addresses of the local addresses the server should bind to. |  | String |
| **camel.component.milo-server.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.milo-server.build-info** | Server build info. The option is a org.eclipse.milo.opcua.stack.core.types.structured.BuildInfo type. |  | BuildInfo |
| **camel.component.milo-server.certificate** | Server certificate. The option is a java.security.cert.X509Certificate type. |  | X509Certificate |
| **camel.component.milo-server.certificate-manager** | Server certificate manager. The option is a org.eclipse.milo.opcua.stack.core.security.CertificateManager type. |  | CertificateManager |
| **camel.component.milo-server.certificate-validator** | Validator for client certificates. The option is a org.eclipse.milo.opcua.stack.server.security.ServerCertificateValidator type. |  | ServerCertificateValidator |
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