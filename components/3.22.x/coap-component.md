# CoAP

**Since Camel 2.16**

**Both producer and consumer are supported**

Camel-CoAP is an [Apache Camel](http://camel.apache.org/) component that allows you to work with CoAP, a lightweight REST-type protocol for machine-to-machine operation. [CoAP](http://coap.technology/), Constrained Application Protocol is a specialized web transfer protocol for use with constrained nodes and constrained networks and it is based on RFC 7252.

Camel supports the DTLS, TCP and TLS protocols via the following URI schemes:

 
| Scheme | Protocol |
| --- | --- |
| coap | UDP |
| coaps | UDP + DTLS |
| coap+tcp | TCP |
| coaps+tcp | TCP + TLS |

There are a number of different configuration options to configure TLS. For both DTLS (the "coaps" uri scheme) and TCP + TLS (the "coaps+tcp" uri scheme), it is possible to use a "sslContextParameters" parameter, from which the camel-coap component will extract the required truststore / keystores etc to set up TLS. In addition, the DTLS protocol supports two alternative configuration mechanisms. To use a pre-shared key, configure a pskStore, and to work with raw public keys, configure privateKey + publicKey objects.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
 <groupId>org.apache.camel</groupId>
 <artifactId>camel-coap</artifactId>
 <version>x.x.x</version>
 <!-- use the same version as your Camel core version -->
</dependency>
```

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

The CoAP component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The CoAP endpoint is configured using URI syntax:

coap:uri

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **uri** (common) | The URI for the CoAP endpoint. |  | URI |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **coapMethodRestrict** (consumer) | 
Comma separated list of methods that the CoAP consumer will bind to. The default is to bind to all methods (DELETE, GET, POST, PUT).

Enum values:

-   DELETE
    
-   GET
    
-   POST
    
-   PUT
    





 |  | String |
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
| **alias** (security) | 

Sets the alias used to query the KeyStore for the private key and certificate. This parameter is used when we are enabling TLS with certificates on the service side, and similarly on the client side when TLS is used with certificates and client authentication. If the parameter is not specified then the default behavior is to use the first alias in the keystore that contains a key entry. This configuration parameter does not apply to configuring TLS via a Raw Public Key or a Pre-Shared Key.

Enum values:

-   NONE
    
-   WANT
    
-   REQUIRE
    





 |  | String |
| **cipherSuites** (security) | Sets the cipherSuites String. This is a comma separated String of ciphersuites to configure. If it is not specified, then it falls back to getting the ciphersuites from the sslContextParameters object. |  | String |
| **clientAuthentication** (security) | Sets the configuration options for server-side client-authentication requirements. The value must be one of NONE, WANT, REQUIRE. If this value is not specified, then it falls back to checking the sslContextParameters.getServerParameters().getClientAuthentication() value. |  | String |
| **privateKey** (security) | Set the configured private key for use with Raw Public Key. |  | PrivateKey |
| **pskStore** (security) | Set the PskStore to use for pre-shared key. |  | PskStore |
| **publicKey** (security) | Set the configured public key for use with Raw Public Key. |  | PublicKey |
| **recommendedCipherSuitesOnly** (security) | The CBC cipher suites are not recommended. If you want to use them, you first need to set the recommendedCipherSuitesOnly option to false. | true | boolean |
| **sslContextParameters** (security) | Set the SSLContextParameters object for setting up TLS. This is required for coapstcp, and for coaps when we are using certificates for TLS (as opposed to RPK or PKS). |  | SSLContextParameters |
| **trustedRpkStore** (security) | Set the TrustedRpkStore to use to determine trust in raw public keys. |  | TrustedRpkStore |

## Message Headers

The CoAP component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelCoapMethod** (common) Constant: [`COAP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-coap/latest/org/apache/camel/coap/CoAPConstants.html#COAP_METHOD) | The request method that the CoAP producer should use when calling the target CoAP server URI. Valid options are DELETE, GET, PING, POST & PUT. |  | String |
| **CamelCoapResponseCode** (common) Constant: [`COAP_RESPONSE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-coap/latest/org/apache/camel/coap/CoAPConstants.html#COAP_RESPONSE_CODE) | The CoAP response code sent by the external server. See RFC 7252 for details of what each code means. |  | String |
| **CamelCoapUri** (common) Constant: [`COAP_URI`](https://javadoc.io/doc/org.apache.camel/camel-coap/latest/org/apache/camel/coap/CoAPConstants.html#COAP_URI) | The URI of a CoAP server to call. Will override any existing URI configured directly on the endpoint. |  | String |
| **Content-Type** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-coap/latest/org/apache/camel/coap/CoAPConstants.html#CONTENT_TYPE) | The content type. |  | String |

### Configuring the CoAP producer request method

The following rules determine which request method the CoAP producer will use to invoke the target URI:

1.  The value of the `CamelCoapMethod` header
    
2.  **GET** if a query string is provided on the target CoAP server URI.
    
3.  **POST** if the message exchange body is not null.
    
4.  **GET** otherwise.
    

## Spring Boot Auto-Configuration

When using coap with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-coap-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.coap.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.coap.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.coap.enabled** | Whether to enable auto configuration of the coap component. This is enabled by default. |  | Boolean |
| **camel.component.coap.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |