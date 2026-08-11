# REST OpenApi

**Since Camel 3.1**

**Both producer and consumer are supported**

The REST OpenApi configures rest producers from [OpenApi](https://www.openapis.org/) (Open API) specification document and delegates to a component implementing the _RestProducerFactory_ interface. Currently, known working components are:

-   [http](http-component.md)
    
-   [netty-http](netty-http-component.md)
    
-   [undertow](undertow-component.md)
    
-   [vertx-http](vertx-http-component.md)
    

> **Important**
> Only OpenAPI spec version 3.x is supported. You cannot use the old Swagger 2.0 spec.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-rest-openapi</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

rest-openapi:\[specificationPath#\]operationId

Where `operationId` is the ID of the operation in the OpenApi specification, and `specificationPath` is the path to the specification. If the `specificationPath` is not specified it defaults to `openapi.json`. The lookup mechanism uses Camels `ResourceHelper` to load the resource, which means that you can use CLASSPATH resources (`classpath:my-specification.json`), files (`file:/some/path.json`), the web (`http://api.example.com/openapi.json`) or reference a bean (`ref:nameOfBean`) or use a method of a bean (`bean:nameOfBean.methodName`) to get the specification resource, failing that OpenApi’s own resource loading support.

This component does not act as an HTTP client. It delegates that to another component mentioned above. The lookup mechanism searches for a single component that implements the `RestProducerFactory` interface and uses that. If the `_CLASSPATH_` contains more than one, then the property `componentName` should be set to indicate which component to delegate to.

Most of the configuration is taken from the OpenApi specification, but the option exists to override those by specifying them on the component or on the endpoint. Typically, you would need to override the `host` or `basePath` if those differ from the specification.

> **Note**
> The `host` parameter should contain the absolute URI containing scheme, hostname and port number, for instance: `https://api.example.com`

With `componentName` you specify what component is used to perform the requests, this named component needs to be present in the Camel context and implement the required _RestProducerFactory_ interface — as do the components listed at the top.

If you do not specify the _componentName_ at either component or endpoint level, `_CLASSPATH_` is searched for a suitable delegate. There should be only one component present on the `_CLASSPATH_` that implements the `RestProducerFactory` interface for this to work.

This component’s endpoint URI is lenient which means that in addition to message headers you can specify REST operation’s parameters as endpoint parameters, these will be constant for all subsequent invocations, so it makes sense to use this feature only for parameters that are indeed constant for all invocations — for example API version in path such as `/api/{version}/users/{id}`.

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

The REST OpenApi component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **basePath** (common) | API basePath, for example /v2. Default is unset, if set overrides the value present in OpenApi specification. |  | String |
| **specificationUri** (common) | Path to the OpenApi specification file. The scheme, host base path are taken from this specification, but these can be overridden with properties on the component or endpoint level. If not given the component tries to load openapi.json resource. Note that the host defined on the component and endpoint of this Component should contain the scheme, hostname and optionally the port in the URI syntax (i.e. [https://api.example.com:8080](https://api.example.com:8080)). Can be overridden in endpoint configuration. |  | String |
| **apiContextPath** (consumer) | Sets the context-path to use for servicing the OpenAPI specification. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **clientRequestValidation** (consumer) | Whether to enable validation of the client request to check if the incoming request is valid according to the OpenAPI specification. | false | boolean |
| **clientResponseValidation** (consumer) | Whether to enable validation of the client request to check if the outgoing response from Camel is valid according to the OpenAPI specification. | false | boolean |
| **missingOperation** (consumer) | 
Whether the consumer should fail,ignore or return a mock response for OpenAPI operations that are not mapped to a corresponding route.

Enum values:

-   fail
    
-   ignore
    
-   mock
    





 | fail | String |
| **bindingPackageScan** (consumer (advanced)) | Package name to use as base (offset) for classpath scanning of POJO classes are located when using binding mode is enabled for JSon or XML. Multiple package names can be separated by comma. |  | String |
| **consumerComponentName** (consumer (advanced)) | Name of the Camel component that will service the requests. The component must be present in Camel registry and it must implement RestOpenApiConsumerFactory service provider interface. If not set CLASSPATH is searched for single component that implements RestOpenApiConsumerFactory SPI. Can be overridden in endpoint configuration. |  | String |
| **mockIncludePattern** (consumer (advanced)) | Used for inclusive filtering of mock data from directories. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma. | classpath:camel-mock/\*\* | String |
| **restOpenapiProcessorStrategy** (consumer (advanced)) | To use a custom strategy for how to process Rest DSL requests. |  | RestOpenapiProcessorStrategy |
| **host** (producer) | Scheme hostname and port to direct the HTTP requests to in the form of [https://hostname:port](https://hostname:port). Can be configured at the endpoint, component or in the corresponding REST configuration in the Camel Context. If you give this component a name (e.g. petstore) that REST configuration is consulted first, rest-openapi next, and global configuration last. If set overrides any value found in the OpenApi specification, RestConfiguration. Can be overridden in endpoint configuration. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **requestValidationEnabled** (producer) | Enable validation of requests against the configured OpenAPI specification. | false | boolean |
| **componentName** (producer (advanced)) | Name of the Camel component that will perform the requests. The component must be present in Camel registry and it must implement RestProducerFactory service provider interface. If not set CLASSPATH is searched for single component that implements RestProducerFactory SPI. Can be overridden in endpoint configuration. |  | String |
| **consumes** (producer (advanced)) | What payload type this component capable of consuming. Could be one type, like application/json or multiple types as application/json, application/xml; q=0.5 according to the RFC7231. This equates to the value of Accept HTTP header. If set overrides any value found in the OpenApi specification. Can be overridden in endpoint configuration. |  | String |
| **produces** (producer (advanced)) | What payload type this component is producing. For example application/json according to the RFC7231. This equates to the value of Content-Type HTTP header. If set overrides any value present in the OpenApi specification. Can be overridden in endpoint configuration. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **sslContextParameters** (security) | Customize TLS parameters used by the component. If not set defaults to the TLS parameters set in the Camel context. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The REST OpenApi endpoint is configured using URI syntax:

rest-openapi:specificationUri#operationId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **specificationUri** (common) | Path to the OpenApi specification file. The scheme, host base path are taken from this specification, but these can be overridden with properties on the component or endpoint level. If not given the component tries to load openapi.json resource from the classpath. Note that the host defined on the component and endpoint of this Component should contain the scheme, hostname and optionally the port in the URI syntax (i.e. [http://api.example.com:8080](http://api.example.com:8080)). Overrides component configuration. The OpenApi specification can be loaded from different sources by prefixing with file: classpath: http: https:. Support for https is limited to using the JDK installed UrlHandler, and as such it can be cumbersome to setup TLS/SSL certificates for https (such as setting a number of javax.net.ssl JVM system properties). How to do that consult the JDK documentation for UrlHandler. Default value notice: By default loads openapi.json file. | openapi.json | String |
| **operationId** (producer) | ID of the operation from the OpenApi specification. This is required when using producer. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **basePath** (common) | API basePath, for example /v3. Default is unset, if set overrides the value present in OpenApi specification and in the component configuration. |  | String |
| **apiContextPath** (consumer) | Sets the context-path to use for servicing the OpenAPI specification. |  | String |
| **clientRequestValidation** (consumer) | Whether to enable validation of the client request to check if the incoming request is valid according to the OpenAPI specification. | false | boolean |
| **clientResponseValidation** (consumer) | Whether to enable validation of the client request to check if the outgoing response from Camel is valid according to the OpenAPI specification. | false | boolean |
| **consumes** (consumer) | What payload type this component capable of consuming. Could be one type, like application/json or multiple types as application/json, application/xml; q=0.5 according to the RFC7231. This equates or multiple types as application/json, application/xml; q=0.5 according to the RFC7231. This equates to the value of Accept HTTP header. If set overrides any value found in the OpenApi specification and. in the component configuration. |  | String |
| **missingOperation** (consumer) | 
Whether the consumer should fail,ignore or return a mock response for OpenAPI operations that are not mapped to a corresponding route.

Enum values:

-   fail
    
-   ignore
    
-   mock
    





 | fail | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerComponentName** (consumer (advanced)) | Name of the Camel component that will service the requests. The component must be present in Camel registry and it must implement RestOpenApiConsumerFactory service provider interface. If not set CLASSPATH is searched for single component that implements RestOpenApiConsumerFactory SPI. Overrides component configuration. |  | String |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **mockIncludePattern** (consumer (advanced)) | Used for inclusive filtering of mock data from directories. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma. | classpath:camel-mock/\*\* | String |
| **restOpenapiProcessorStrategy** (consumer (advanced)) | To use a custom strategy for how to process Rest DSL requests. |  | RestOpenapiProcessorStrategy |
| **host** (producer) | Scheme hostname and port to direct the HTTP requests to in the form of [https://hostname:port](https://hostname:port). Can be configured at the endpoint, component or in the corresponding REST configuration in the Camel Context. If you give this component a name (e.g. petstore) that REST configuration is consulted first, rest-openapi next, and global configuration last. If set overrides any value found in the OpenApi specification, RestConfiguration. Overrides all other configuration. |  | String |
| **produces** (producer) | What payload type this component is producing. For example application/json according to the RFC7231. This equates to the value of Content-Type HTTP header. If set overrides any value present in the OpenApi specification. Overrides all other configuration. |  | String |
| **requestValidationEnabled** (producer) | Enable validation of requests against the configured OpenAPI specification. | false | boolean |
| **componentName** (producer (advanced)) | Name of the Camel component that will perform the requests. The component must be present in Camel registry and it must implement RestProducerFactory service provider interface. If not set CLASSPATH is searched for single component that implements RestProducerFactory SPI. Overrides component configuration. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **oauthProfile** (security) | OAuth profile name passed to the HTTP consumer delegate for validating incoming Authorization: Bearer tokens. The selected consumer component must support the oauthProfile option; delegates that ignore unknown options will start without endpoint protection. |  | String |

## Usage

### Consumer OAuth Bearer token validation

When `rest-openapi` is used as a consumer, HTTP requests are served by the selected `RestOpenApiConsumerFactory` delegate, such as the built-in `platform-http` delegate or a custom delegate. To validate incoming `Authorization: Bearer` tokens from Rest DSL contract-first routes, pass the delegate endpoint option `oauthProfile` through the REST configuration endpoint properties.

_Java-only: configuring REST with OAuth profile_

```java
restConfiguration()
    .component("platform-http")
    .endpointProperty("oauthProfile", "myprofile");

rest().openApi("petstore-v3.json");
```

For direct `rest-openapi` consumer routes, pass the delegate endpoint option directly on the consumer endpoint URI. Consumer URIs identify the OpenAPI specification and do not include an `#operationId` fragment.

-   Java
    
-   XML
    
-   YAML
    

```java
from("rest-openapi:petstore-v3.json?consumerComponentName=platform-http&oauthProfile=myprofile")
    .to("direct:businessLogic");
```

```xml
<route>
  <from uri="rest-openapi:petstore-v3.json?consumerComponentName=platform-http&amp;oauthProfile=myprofile"/>
  <to uri="direct:businessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: rest-openapi:petstore-v3.json
      parameters:
        consumerComponentName: platform-http
        oauthProfile: myprofile
      steps:
        - to:
            uri: direct:businessLogic
```

The selected delegate component must support the `oauthProfile` endpoint option. The built-in `platform-http` delegate supports this option. An `OAuthTokenValidationFactory` must be available, for example from [camel-oauth](../4.22.x/others/oauth.md) or from the runtime integration. OpenAPI `securitySchemes` and operation security requirements are not converted into `oauthProfile` configuration; select the OAuth profile explicitly with the REST endpoint property or direct endpoint URI option. The `oauthProfile` option is a first-class `rest-openapi` endpoint option that is forwarded to the selected delegate, which is responsible for enforcing it. The route fails at startup when the resolved `RestOpenApiConsumerFactory` does not declare that its consumers enforce `oauthProfile`, so a misconfigured delegate cannot start without the expected protection. Custom factories that enforce the option must override `RestOpenApiConsumerFactory.supportsOAuthProfile()` to return `true`.

## Request validation

API requests can be validated against the configured OpenAPI specification before they are sent by setting the `requestValidationEnabled` option to `true`. Validation is provided by the [swagger-request-validator](https://bitbucket.org/atlassian/swagger-request-validator/src/master/).

The validator checks for the following conditions:

-   request body - Checks if the request body is required and whether there is any body on the Camel Exchange.
    
-   valid json - Checks if the content-type is `application/json` that the message body can be parsed as valid JSon.
    
-   content-type - Validates whether the `Content-Type` header for the request is valid for the API operation. The value is taken from the `Content-Type` Camel message exchange header.
    
-   request parameters - Validates whether an HTTP header required by the API operation is present. The header is expected to be present among the Camel message exchange headers.
    
-   query parameters - Validates whether an HTTP query parameter required by the API operation is present. The query parameter is expected to be present among the Camel message exchange headers.
    

If any of the validation checks fail, then a `RestOpenApiValidationException` is thrown. The exception object has a `getValidationErrors` method that returns the error messages from the validator.

## Examples

### PetStore

Checkout the `rest-openapi-simple` example project in the [camel-spring-boot-examples](https://github.com/apache/camel-spring-boot-examples) repository.

For example, if you wanted to use the [_PetStore_](https://petstore3.swagger.io/api/v3/) provided REST API simply reference the specification URI and desired operation id from the OpenApi specification or download the specification and store it as `openapi.json` (in the root) of `_CLASSPATH_` that way it will be automatically used. Let’s use the [HTTP](http-component.md) component to perform all the requests and Camel’s excellent support for Spring Boot.

Here are our dependencies defined in Maven POM file:

Example pom.xml

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-http-starter</artifactId>
</dependency>

<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-rest-openapi-starter</artifactId>
</dependency>
```

Start by defining a `RestOpenApiComponent` bean:

_Java-only: defining a RestOpenApiComponent bean for PetStore_

```java
@Bean
public Component petstore(CamelContext camelContext) {
    RestOpenApiComponent petstore = new RestOpenApiComponent(camelContext);
    petstore.setSpecificationUri("https://petstore3.swagger.io/api/v3/openapi.json");
    petstore.setHost("https://petstore3.swagger.io");
    return petstore;
}
```

> **Note**
> Support in Camel for Spring Boot will auto create the `HttpComponent` Spring bean, and you can configure it using `application.properties` (or `application.yml`) using prefix `camel.component.http.`. We are defining the `petstore` component here to have a named component in the Camel context that we can use to interact with the PetStore REST API, if this is the only `rest-openapi` component used we might configure it in the same manner (using `application.properties`).
>
> In this example, there is no need to explicitly associate the `petstore` component with the `HttpComponent` as Camel will use the first class on the `_CLASSPATH_` that implements `RestProducerFactory`. However, if a different component is required, then calling `petstore.setComponentName("http")` would use the named component from the Camel registry.

Now in our application we can simply use the `ProducerTemplate` to invoke PetStore REST methods:

_Java-only: invoking PetStore REST methods with ProducerTemplate_

```java
@Autowired
ProducerTemplate template;

String getPetJsonById(int petId) {
    return template.requestBodyAndHeader("petstore:getPetById", null, "petId", petId);
}
```