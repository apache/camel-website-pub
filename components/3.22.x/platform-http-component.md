# Platform HTTP

**Since Camel 3.0**

**Only consumer is supported**

The Platform HTTP is used to allow Camel to use the existing HTTP server from the runtime. For example when running Camel on Spring Boot, Quarkus, or other runtimes.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-platform-http</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Platform HTTP Provider

To use Platform HTTP a provider (engine) is required to be available on the classpath. The purpose is to have drivers for different runtimes such as Quarkus, or Spring Boot.

To use Quarkus:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-platform-http</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel Quarkus version -->
</dependency>
```

And for Spring Boot:

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-platform-http-starter</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel version -->
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

The Platform HTTP component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **engine** (advanced) | An HTTP Server engine implementation to serve the requests. |  | PlatformHttpEngine |

## Endpoint Options

The Platform HTTP endpoint is configured using URI syntax:

platform-http:path

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **path** (consumer) | **Required** The path under which this endpoint serves the HTTP requests, for proxy use 'proxy'. |  | String |

### Query Parameters (11 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **consumes** (consumer) | The content type this endpoint accepts as an input, such as application/xml or application/json. null or \*/\* mean no restriction. |  | String |
| **httpMethodRestrict** (consumer) | A comma separated list of HTTP methods to serve, e.g. GET,POST . If no methods are specified, all methods will be served. |  | String |
| **matchOnUriPrefix** (consumer) | Whether or not the consumer should try to find a target consumer by matching the URI prefix if no exact match is found. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | true | boolean |
| **produces** (consumer) | The content type this endpoint produces, such as application/xml or application/json. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **fileNameExtWhitelist** (consumer (advanced)) | A comma or whitespace separated list of file extensions. Uploads having these extensions will be stored locally. Null value or asterisk () will allow all files. |  | String |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter headers to and from Camel message. |  | HeaderFilterStrategy |
| **platformHttpEngine** (advanced) | An HTTP Server engine implementation to serve the requests of this endpoint. |  | PlatformHttpEngine |

## Spring Boot Auto-Configuration

When using platform-http with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-platform-http-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.platform-http.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.platform-http.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.platform-http.enabled** | Whether to enable auto configuration of the platform-http component. This is enabled by default. |  | Boolean |
| **camel.component.platform-http.engine** | An HTTP Server engine implementation to serve the requests. The option is a org.apache.camel.component.platform.http.spi.PlatformHttpEngine type. |  | PlatformHttpEngine |

## Implementing a reverse proxy

Platform HTTP component can act as a reverse proxy, in that case some headers are populated from the absolute URL received on the request line of the HTTP request. Those headers are specific to the underlining platform.

At this moment, this feature is only supported for Quarkus implemented in `camel-platform-http-vertx` component.