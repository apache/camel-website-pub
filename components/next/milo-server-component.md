# OPC UA Server

**Since Camel 2.19**

**Both producer and consumer are supported**

The Milo Server component provides an OPC UA server using the [Eclipse Milo™](http://eclipse.org/milo) implementation.

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

Messages sent to the endpoint from Camel will be available from the OPC UA server to OPC UA Clients. Value write requests from OPC UA Client will trigger messages which are sent into Apache Camel.

## URI format

milo-server:itemId\[?options\]

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
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **certificate** (security) | Server certificate. |  | X509Certificate |
| **certificateManager** (security) | Server certificate manager. |  | CertificateManager |
| **certificateValidator** (security) | Validator for client certificates. |  | CertificateValidator |
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

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **itemId** (common) | **Required** ID of the item. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

### Security Configuration

When configuring security for the OPC UA server, the following considerations apply:

-   Certificate validation uses `org.eclipse.milo.opcua.stack.core.security.CertificateValidator`
    
-   The component supports both certificate-based and username/password authentication
    
-   Security policies can be configured using the `securityPolicies` or `securityPoliciesById` options
    

#### Milo 1.0.5 Migration Notes

With Milo 1.0.5, several security-related API changes were introduced:

-   The `ServerCertificateValidator` class has been replaced with `CertificateValidator`
    
-   Certificate validation now uses `org.eclipse.milo.opcua.stack.core.security.CertificateValidator`
    
-   When configuring custom certificate validators programmatically, ensure you’re using the updated API