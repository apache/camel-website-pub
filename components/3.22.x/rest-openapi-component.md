# REST OpenApi

**Since Camel 3.1**

**Only producer is supported**

The REST OpenApi\* configures rest producers from [OpenApi](https://www.openapis.org/) (Open API) specification document and delegates to a component implementing the _RestProducerFactory_ interface. Currently known working components are:

-   [http](http-component.md)
    
-   [netty-http](netty-http-component.md)
    
-   [undertow](undertow-component.md)
    
-   [vertx-http](vertx-http-component.md)
    

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

This component does not act as a HTTP client, it delegates that to another component mentioned above. The lookup mechanism searches for a single component that implements the _RestProducerFactory_ interface and uses that. If the CLASSPATH contains more than one, then the property `componentName` should be set to indicate which component to delegate to.

Most of the configuration is taken from the OpenApi specification but the option exists to override those by specifying them on the component or on the endpoint. Typically you would just need to override the `host` or `basePath` if those differ from the specification.

> **Note**
> The `host` parameter should contain the absolute URI containing scheme, hostname and port number, for instance: `https://api.example.com`

With `componentName` you specify what component is used to perform the requests, this named component needs to be present in the Camel context and implement the required _RestProducerFactory_ interface — as do the components listed at the top.

If you do not specify the _componentName_ at either component or endpoint level, CLASSPATH is searched for a suitable delegate. There should be only one component present on the CLASSPATH that implements the _RestProducerFactory_ interface for this to work.

This component’s endpoint URI is lenient which means that in addition to message headers you can specify REST operation’s parameters as endpoint parameters, these will be constant for all subsequent invocations so it makes sense to use this feature only for parameters that are indeed constant for all invocations — for example API version in path such as `/api/{version}/users/{id}`.

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

The REST OpenApi component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **basePath** (producer) | API basePath, for example /v2. Default is unset, if set overrides the value present in OpenApi specification. |  | String |
| **componentName** (producer) | Name of the Camel component that will perform the requests. The component must be present in Camel registry and it must implement RestProducerFactory service provider interface. If not set CLASSPATH is searched for single component that implements RestProducerFactory SPI. Can be overridden in endpoint configuration. |  | String |
| **consumes** (producer) | What payload type this component capable of consuming. Could be one type, like application/json or multiple types as application/json, application/xml; q=0.5 according to the RFC7231. This equates to the value of Accept HTTP header. If set overrides any value found in the OpenApi specification. Can be overridden in endpoint configuration. |  | String |
| **host** (producer) | Scheme hostname and port to direct the HTTP requests to in the form of [https://hostname:port](https://hostname:port). Can be configured at the endpoint, component or in the corresponding REST configuration in the Camel Context. If you give this component a name (e.g. petstore) that REST configuration is consulted first, rest-openapi next, and global configuration last. If set overrides any value found in the OpenApi specification, RestConfiguration. Can be overridden in endpoint configuration. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **produces** (producer) | What payload type this component is producing. For example application/json according to the RFC7231. This equates to the value of Content-Type HTTP header. If set overrides any value present in the OpenApi specification. Can be overridden in endpoint configuration. |  | String |
| **specificationUri** (producer) | Path to the OpenApi specification file. The scheme, host base path are taken from this specification, but these can be overridden with properties on the component or endpoint level. If not given the component tries to load openapi.json resource. Note that the host defined on the component and endpoint of this Component should contain the scheme, hostname and optionally the port in the URI syntax (i.e. [https://api.example.com:8080](https://api.example.com:8080)). Can be overridden in endpoint configuration. | openapi.json | URI |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **sslContextParameters** (security) | Customize TLS parameters used by the component. If not set defaults to the TLS parameters set in the Camel context. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The REST OpenApi endpoint is configured using URI syntax:

rest-openapi:specificationUri#operationId

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **specificationUri** (producer) | Path to the OpenApi specification file. The scheme, host base path are taken from this specification, but these can be overridden with properties on the component or endpoint level. If not given the component tries to load openapi.json resource from the classpath. Note that the host defined on the component and endpoint of this Component should contain the scheme, hostname and optionally the port in the URI syntax (i.e. [http://api.example.com:8080](http://api.example.com:8080)). Overrides component configuration. The OpenApi specification can be loaded from different sources by prefixing with file: classpath: http: https:. Support for https is limited to using the JDK installed UrlHandler, and as such it can be cumbersome to setup TLS/SSL certificates for https (such as setting a number of javax.net.ssl JVM system properties). How to do that consult the JDK documentation for UrlHandler. Default value notice: By default loads openapi.json file. | openapi.json | URI |
| **operationId** (producer) | **Required** ID of the operation from the OpenApi specification. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **basePath** (producer) | API basePath, for example /v2. Default is unset, if set overrides the value present in OpenApi specification and in the component configuration. |  | String |
| **componentName** (producer) | Name of the Camel component that will perform the requests. The component must be present in Camel registry and it must implement RestProducerFactory service provider interface. If not set CLASSPATH is searched for single component that implements RestProducerFactory SPI. Overrides component configuration. |  | String |
| **consumes** (producer) | What payload type this component capable of consuming. Could be one type, like application/json or multiple types as application/json, application/xml; q=0.5 according to the RFC7231. This equates to the value of Accept HTTP header. If set overrides any value found in the OpenApi specification and. in the component configuration. |  | String |
| **host** (producer) | Scheme hostname and port to direct the HTTP requests to in the form of [https://hostname:port](https://hostname:port). Can be configured at the endpoint, component or in the corresponding REST configuration in the Camel Context. If you give this component a name (e.g. petstore) that REST configuration is consulted first, rest-openapi next, and global configuration last. If set overrides any value found in the OpenApi specification, RestConfiguration. Overrides all other configuration. |  | String |
| **produces** (producer) | What payload type this component is producing. For example application/json according to the RFC7231. This equates to the value of Content-Type HTTP header. If set overrides any value present in the OpenApi specification. Overrides all other configuration. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Example: PetStore

Checkout the `rest-openapi-simple` example project in the [https://github.com/apache/camel-spring-boot-examples](https://github.com/apache/camel-spring-boot-examples) repository.

For example if you wanted to use the [_PetStore_](https://petstore3.swagger.io/api/v3/) provided REST API simply reference the specification URI and desired operation id from the OpenApi specification or download the specification and store it as `openapi.json` (in the root) of CLASSPATH that way it will be automaticaly used. Let’s use the [HTTP](http-component.md) component to perform all the requests and Camel’s excellent support for Spring Boot.

Here are our dependencies defined in Maven POM file:

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

Start by defining a _RestOpenApiComponent_ bean:

```java
@Bean
public Component petstore(CamelContext camelContext) {
    RestOpenApiComponent petstore = new RestOpenApiComponent(camelContext);
    petstore.setSpecificationUri(new URI("https://petstore3.swagger.io/api/v3/openapi.json"));
    petstore.setHost("https://petstore3.swagger.io");
    return petstore;
}
```

> **Note**
> Support in Camel for Spring Boot will auto create the `HttpComponent` Spring bean, and you can configure it using `application.properties` (or `application.yml`) using prefix `camel.component.http.`. We are defining the `petstore` component here in order to have a named component in the Camel context that we can use to interact with the PetStore REST API, if this is the only `rest-openapi` component used we might configure it in the same manner (using `application.properties`).
>
> In this example, there is no need to explicitly associate the `petstore` component with the `HttpComponent` as Camel will use the first class on the CLASSPATH that implements `RestProducerFactory`. However, if a different component is required, then calling `petstore.setComponentName("http")` would use the named component from the Camel registry.

Now in our application we can simply use the `ProducerTemplate` to invoke PetStore REST methods:

```java
@Autowired
ProducerTemplate template;

String getPetJsonById(int petId) {
    return template.requestBodyAndHeader("petstore:getPetById", null, "petId", petId);
}
```

## Spring Boot Auto-Configuration

When using rest-openapi with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-rest-openapi-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.rest-openapi.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.rest-openapi.base-path** | API basePath, for example /v2. Default is unset, if set overrides the value present in OpenApi specification. |  | String |
| **camel.component.rest-openapi.component-name** | Name of the Camel component that will perform the requests. The component must be present in Camel registry and it must implement RestProducerFactory service provider interface. If not set CLASSPATH is searched for single component that implements RestProducerFactory SPI. Can be overridden in endpoint configuration. |  | String |
| **camel.component.rest-openapi.consumes** | What payload type this component capable of consuming. Could be one type, like application/json or multiple types as application/json, application/xml; q=0.5 according to the RFC7231. This equates to the value of Accept HTTP header. If set overrides any value found in the OpenApi specification. Can be overridden in endpoint configuration. |  | String |
| **camel.component.rest-openapi.enabled** | Whether to enable auto configuration of the rest-openapi component. This is enabled by default. |  | Boolean |
| **camel.component.rest-openapi.host** | Scheme hostname and port to direct the HTTP requests to in the form of [https://hostname:port](https://hostname:port). Can be configured at the endpoint, component or in the corresponding REST configuration in the Camel Context. If you give this component a name (e.g. petstore) that REST configuration is consulted first, rest-openapi next, and global configuration last. If set overrides any value found in the OpenApi specification, RestConfiguration. Can be overridden in endpoint configuration. |  | String |
| **camel.component.rest-openapi.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.rest-openapi.produces** | What payload type this component is producing. For example application/json according to the RFC7231. This equates to the value of Content-Type HTTP header. If set overrides any value present in the OpenApi specification. Can be overridden in endpoint configuration. |  | String |
| **camel.component.rest-openapi.specification-uri** | Path to the OpenApi specification file. The scheme, host base path are taken from this specification, but these can be overridden with properties on the component or endpoint level. If not given the component tries to load openapi.json resource. Note that the host defined on the component and endpoint of this Component should contain the scheme, hostname and optionally the port in the URI syntax (i.e. [https://api.example.com:8080](https://api.example.com:8080)). Can be overridden in endpoint configuration. |  | URI |
| **camel.component.rest-openapi.ssl-context-parameters** | Customize TLS parameters used by the component. If not set defaults to the TLS parameters set in the Camel context. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.rest-openapi.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |