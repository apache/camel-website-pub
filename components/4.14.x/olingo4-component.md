# Olingo4

**Since Camel 2.19**

**Both producer and consumer are supported**

The Olingo4 component uses [Apache Olingo](http://olingo.apache.org/) version 4.0 APIs to interact with OData 4.0 compliant service. Since version 4.0, OData is an OASIS standard and a number of popular open source and commercial vendors and products support this protocol. A sample list of supporting products can be found on the OData [website](http://www.odata.org/ecosystem/).

The Olingo4 component supports reading entity sets, entities, simple and complex properties, counts, using custom and OData system query parameters. It supports updating entities and properties. It also supports submitting queries and change requests as a single OData batch operation.

The component supports configuring HTTP connection parameters and headers for OData service connection. This allows configuring use of SSL, OAuth2.0, etc. as required by the target OData service.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-olingo4</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

olingo4://endpoint/<resource-path>?\[options\]

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

The Olingo4 component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | To use the shared configuration. |  | Olingo4Configuration |
| **connectTimeout** (common) | HTTP connection creation timeout in milliseconds, defaults to 30,000 (30 seconds). | 30000 | int |
| **contentType** (common) | Content-Type header value can be used to specify JSON or XML message format, defaults to application/json;charset=utf-8. | application/json;charset=utf-8 | String |
| **filterAlreadySeen** (common) | Set this to true to filter out results that have already been communicated by this component. | false | boolean |
| **httpHeaders** (common) | Custom HTTP headers to inject into every request, this could include OAuth tokens, etc. |  | Map |
| **proxy** (common) | HTTP proxy server configuration. |  | HttpHost |
| **serviceUri** (common) | Target OData service base URI, e.g. [http://services.odata.org/OData/OData.svc](http://services.odata.org/OData/OData.svc). |  | String |
| **socketTimeout** (common) | HTTP request timeout in milliseconds, defaults to 30,000 (30 seconds). | 30000 | int |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **splitResult** (consumer) | For endpoints that return an array or collection, a consumer endpoint will map every element to distinct messages, unless splitResult is set to false. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **httpAsyncClientBuilder** (advanced) | Custom HTTP async client builder for more complex HTTP client configuration, overrides connectionTimeout, socketTimeout, proxy and sslContext. Note that a socketTimeout MUST be specified in the builder, otherwise OData requests could block indefinitely. |  | HttpAsyncClientBuilder |
| **httpClientBuilder** (advanced) | Custom HTTP client builder for more complex HTTP client configuration, overrides connectionTimeout, socketTimeout, proxy and sslContext. Note that a socketTimeout MUST be specified in the builder, otherwise OData requests could block indefinitely. |  | HttpClientBuilder |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Olingo4 endpoint is configured using URI syntax:

olingo4:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   DEFAULT
    





 |  | Olingo4ApiName |
| **methodName** (common) | **Required** What sub operation to use for the selected operation. |  | String |

### Query Parameters (32 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectTimeout** (common) | HTTP connection creation timeout in milliseconds, defaults to 30,000 (30 seconds). | 30000 | int |
| **contentType** (common) | Content-Type header value can be used to specify JSON or XML message format, defaults to application/json;charset=utf-8. | application/json;charset=utf-8 | String |
| **filterAlreadySeen** (common) | Set this to true to filter out results that have already been communicated by this component. | false | boolean |
| **httpHeaders** (common) | Custom HTTP headers to inject into every request, this could include OAuth tokens, etc. |  | Map |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **proxy** (common) | HTTP proxy server configuration. |  | HttpHost |
| **serviceUri** (common) | Target OData service base URI, e.g. [http://services.odata.org/OData/OData.svc](http://services.odata.org/OData/OData.svc). |  | String |
| **socketTimeout** (common) | HTTP request timeout in milliseconds, defaults to 30,000 (30 seconds). | 30000 | int |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **splitResult** (consumer) | For endpoints that return an array or collection, a consumer endpoint will map every element to distinct messages, unless splitResult is set to false. | true | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **httpAsyncClientBuilder** (advanced) | Custom HTTP async client builder for more complex HTTP client configuration, overrides connectionTimeout, socketTimeout, proxy and sslContext. Note that a socketTimeout MUST be specified in the builder, otherwise OData requests could block indefinitely. |  | HttpAsyncClientBuilder |
| **httpClientBuilder** (advanced) | Custom HTTP client builder for more complex HTTP client configuration, overrides connectionTimeout, socketTimeout, proxy and sslContext. Note that a socketTimeout MUST be specified in the builder, otherwise OData requests could block indefinitely. |  | HttpClientBuilder |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |

## API Parameters (1 APIs)

The Olingo4 endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

olingo4:apiName/methodName

There are 1 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**DEFAULT**](#_api_DEFAULT) | Both | Olingo4 Client Api Interface |

Each API is documented in the following sections to come.

### API: DEFAULT

**Both producer and consumer are supported**

The DEFAULT API is defined in the syntax as follows:

```none
olingo4:DEFAULT/methodName?[parameters]
```

The 9 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**action**](#_api_DEFAULT_method_action) |  | Calls a OData action |
| [**batch**](#_api_DEFAULT_method_batch) |  | Executes a batch request |
| [**create**](#_api_DEFAULT_method_create) |  | Creates a new OData resource |
| [**delete**](#_api_DEFAULT_method_delete) |  | Deletes an OData resource and invokes callback with org |
| [**merge**](#_api_DEFAULT_method_merge) |  | Patches/merges an OData resource using HTTP MERGE |
| [**patch**](#_api_DEFAULT_method_patch) |  | Patches/merges an OData resource using HTTP PATCH |
| [**read**](#_api_DEFAULT_method_read) |  | Reads an OData resource and invokes callback with appropriate result |
| [**update**](#_api_DEFAULT_method_update) |  | Updates an OData resource |
| [**uread**](#_api_DEFAULT_method_uread) |  | Reads an OData resource and invokes callback with the unparsed input stream |

#### Method action

Signatures:

-   void action(org.apache.olingo.commons.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo4.api.Olingo4ResponseHandler responseHandler);
    

The olingo4/action API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Action data | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path to action | String |
| **responseHandler** | Org.apache.olingo.client.api.domain.ClientEntity callback handler | Olingo4ResponseHandler |

#### Method batch

Signatures:

-   void batch(org.apache.olingo.commons.api.edm.Edm edm, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo4.api.Olingo4ResponseHandler<java.util.List<org.apache.camel.component.olingo4.api.batch.Olingo4BatchResponse>> responseHandler);
    

The olingo4/batch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Ordered org.apache.camel.component.olingo4.api.batch.Olingo4BatchRequest list | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **responseHandler** | Callback handler | Olingo4ResponseHandler |

#### Method create

Signatures:

-   void create(org.apache.olingo.commons.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo4.api.Olingo4ResponseHandler responseHandler);
    

The olingo4/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Request data | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path to create | String |
| **responseHandler** | Callback handler | Olingo4ResponseHandler |

#### Method delete

Signatures:

-   void delete(String resourcePath, java.util.Map<String, String> endpointHttpHeaders, org.apache.camel.component.olingo4.api.Olingo4ResponseHandler<org.apache.olingo.commons.api.http.HttpStatusCode> responseHandler);
    

The olingo4/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path for Entry | String |
| **responseHandler** | Org.apache.olingo.commons.api.http.HttpStatusCode callback handler | Olingo4ResponseHandler |

#### Method merge

Signatures:

-   void merge(org.apache.olingo.commons.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo4.api.Olingo4ResponseHandler responseHandler);
    

The olingo4/merge API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Patch/merge data | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path to update | String |
| **responseHandler** | Org.apache.olingo.client.api.domain.ClientEntity callback handler | Olingo4ResponseHandler |

#### Method patch

Signatures:

-   void patch(org.apache.olingo.commons.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo4.api.Olingo4ResponseHandler responseHandler);
    

The olingo4/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Patch/merge data | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path to update | String |
| **responseHandler** | Org.apache.olingo.client.api.domain.ClientEntity callback handler | Olingo4ResponseHandler |

#### Method read

Signatures:

-   void read(org.apache.olingo.commons.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> queryParams, java.util.Map<String, String> endpointHttpHeaders, org.apache.camel.component.olingo4.api.Olingo4ResponseHandler responseHandler);
    

The olingo4/read API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **edm** | Service Edm, read from calling read(null, $metdata, null, responseHandler) | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **queryParams** | OData query params [http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html#\_Toc453752288](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html#_Toc453752288) | Map |
| **resourcePath** | OData Resource path | String |
| **responseHandler** | Callback handler | Olingo4ResponseHandler |

#### Method update

Signatures:

-   void update(org.apache.olingo.commons.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo4.api.Olingo4ResponseHandler responseHandler);
    

The olingo4/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Updated data | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path to update | String |
| **responseHandler** | Org.apache.olingo.client.api.domain.ClientEntity callback handler | Olingo4ResponseHandler |

#### Method uread

Signatures:

-   void uread(org.apache.olingo.commons.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> queryParams, java.util.Map<String, String> endpointHttpHeaders, org.apache.camel.component.olingo4.api.Olingo4ResponseHandler<java.io.InputStream> responseHandler);
    

The olingo4/uread API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **edm** | Service Edm, read from calling read(null, $metdata, null, responseHandler) | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **queryParams** | OData query params [http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html#\_Toc453752288](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html#_Toc453752288) | Map |
| **resourcePath** | OData Resource path | String |
| **responseHandler** | Callback handler | Olingo4ResponseHandler |

In addition to the parameters above, the olingo4 API can also use any of the [Query Parameters (32 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelOlingo4.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelOlingo4.myParameterNameHere` header.

## Message Headers

The Olingo4 component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOlingo4.responseHttpHeaders** (producer) Constant: [`FULL_RESPONSE_HTTP_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-olingo4/latest/org/apache/camel/component/olingo4/internal/Olingo4Constants.html#FULL_RESPONSE_HTTP_HEADERS) | The response Http headers. |  | Map |

## Usage

### Endpoint HTTP Headers

The component level configuration property **httpHeaders** supplies static HTTP header information. However, some systems require dynamic header information to be passed to and received from the endpoint. A sample use case would be systems that require dynamic security tokens. The **endpointHttpHeaders** and **responseHttpHeaders** endpoint properties provide this capability. Set headers that need to be passed to the endpoint in the **`CamelOlingo4.endpointHttpHeaders`** property and the response headers will be returned in a **`CamelOlingo4.responseHttpHeaders`** property. Both properties are of the type **`java.util.Map<String, String>`**.

### OData Resource Type Mapping

The result of **read** endpoint and data type of **data** option depends on the OData resource being queried, created or modified.

  
| OData Resource Type | Resource URI from resourcePath and keyPredicate | In or Out Body Type |
| --- | --- | --- |
| Entity data model | $metadata | `org.apache.olingo.commons.api.edm.Edm` |
| Service document | / | `org.apache.olingo.client.api.domain.ClientServiceDocument` |
| OData entity set | <entity-set> | `org.apache.olingo.client.api.domain.ClientEntitySet` |
| OData entity | <entity-set>(<key-predicate>) | `org.apache.olingo.client.api.domain.ClientEntity` for Out body (response) `java.util.Map<String, Object>` for In body (request) |
| Simple property | <entity-set>(<key-predicate>)/<simple-property> | `org.apache.olingo.client.api.domain.ClientPrimitiveValue` |
| Simple property value | <entity-set>(<key-predicate>)/<simple-property>/$value | `org.apache.olingo.client.api.domain.ClientPrimitiveValue` |
| Complex property | <entity-set>(<key-predicate>)/<complex-property> | `org.apache.olingo.client.api.domain.ClientComplexValue` |
| Count | <resource-uri>/$count | `java.lang.Long` |

## Examples

The following route reads top 5 entries from the People entity ordered by ascending FirstName property.

```java
from("direct:...")
    .setHeader("CamelOlingo4.$top", "5");
    .to("olingo4://read/People?orderBy=FirstName%20asc");
```

The following route reads Airports entity using the key property value in incoming **id** header.

```java
from("direct:...")
    .setHeader("CamelOlingo4.keyPredicate", header("id"))
    .to("olingo4://read/Airports");
```

The following route creates People entity using the **ClientEntity** in body message.

```java
from("direct:...")
    .to("olingo4://create/People");
```

The following route calls an odata action using the **ClientEntity** in the body message. The body message may be null for actions that don’t expect an input.

```java
from("direct:...")
    .to("olingo4://action/People");
```

## Spring Boot Auto-Configuration

When using olingo4 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-olingo4-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 17 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.olingo4.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.olingo4.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.olingo4.configuration** | To use the shared configuration. The option is a org.apache.camel.component.olingo4.Olingo4Configuration type. |  | Olingo4Configuration |
| **camel.component.olingo4.connect-timeout** | HTTP connection creation timeout in milliseconds, defaults to 30,000 (30 seconds). | 30000 | Integer |
| **camel.component.olingo4.content-type** | Content-Type header value can be used to specify JSON or XML message format, defaults to application/json;charset=utf-8. | application/json;charset=utf-8 | String |
| **camel.component.olingo4.enabled** | Whether to enable auto configuration of the olingo4 component. This is enabled by default. |  | Boolean |
| **camel.component.olingo4.filter-already-seen** | Set this to true to filter out results that have already been communicated by this component. | false | Boolean |
| **camel.component.olingo4.http-async-client-builder** | Custom HTTP async client builder for more complex HTTP client configuration, overrides connectionTimeout, socketTimeout, proxy and sslContext. Note that a socketTimeout MUST be specified in the builder, otherwise OData requests could block indefinitely. The option is a org.apache.http.impl.nio.client.HttpAsyncClientBuilder type. |  | HttpAsyncClientBuilder |
| **camel.component.olingo4.http-client-builder** | Custom HTTP client builder for more complex HTTP client configuration, overrides connectionTimeout, socketTimeout, proxy and sslContext. Note that a socketTimeout MUST be specified in the builder, otherwise OData requests could block indefinitely. The option is a org.apache.http.impl.client.HttpClientBuilder type. |  | HttpClientBuilder |
| **camel.component.olingo4.http-headers** | Custom HTTP headers to inject into every request, this could include OAuth tokens, etc. |  | Map |
| **camel.component.olingo4.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.olingo4.proxy** | HTTP proxy server configuration. The option is a org.apache.http.HttpHost type. |  | HttpHost |
| **camel.component.olingo4.service-uri** | Target OData service base URI, e.g. [http://services.odata.org/OData/OData.svc](http://services.odata.org/OData/OData.svc). |  | String |
| **camel.component.olingo4.socket-timeout** | HTTP request timeout in milliseconds, defaults to 30,000 (30 seconds). | 30000 | Integer |
| **camel.component.olingo4.split-result** | For endpoints that return an array or collection, a consumer endpoint will map every element to distinct messages, unless splitResult is set to false. | true | Boolean |
| **camel.component.olingo4.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.olingo4.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |