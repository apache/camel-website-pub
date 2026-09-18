# Olingo2

> **Warning**
> **Deprecated:** This olingo2 is deprecated and may be removed in a future release.

**Since Camel 2.14**

**Both producer and consumer are supported**

> **Note**
> This component is deprecated since Camel 4.18 and will be removed in a future release. Apache Olingo project has been moved to the Apache Attic and is no longer maintained.

> **Note**
> Starting with Camel 4.0, our project has migrated to JakartaEE. Some parts of Apache Olingo2 may depend on J2EE, which may result in unexpected behavior and other runtime problems.

The Olingo2 component uses [Apache Olingo](http://olingo.apache.org/) version 2.0 APIs to interact with OData 2.0 compliant services. A number of popular commercial and enterprise vendors and products support the OData protocol. A sample list of supporting products can be found on the OData [website](http://www.odata.org/ecosystem/).

The Olingo2 component supports reading feeds, delta feeds, entities, simple and complex properties, links, counts, using custom and OData system query parameters. It supports updating entities, properties, and association links. It also supports submitting queries and change requests as a single OData batch operation.

The component supports configuring HTTP connection parameters and headers for OData service connection. This allows configuring use of SSL, OAuth2.0, etc. as required by the target OData service.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-olingo2</artifactId>
    <version>${camel-version}</version>
</dependency>
```

## URI format

olingo2://endpoint/<resource-path>?\[options\]

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

The Olingo2 component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | To use the shared configuration. |  | Olingo2Configuration |
| **connectTimeout** (common) | HTTP connection creation timeout in milliseconds, defaults to 30,000 (30 seconds). | 30000 | int |
| **contentType** (common) | Content-Type header value can be used to specify JSON or XML message format, defaults to application/json;charset=utf-8. | application/json;charset=utf-8 | String |
| **entityProviderReadProperties** (common) | Custom entity provider read properties applied to all read operations. |  | EntityProviderReadProperties |
| **entityProviderWriteProperties** (common) | Custom entity provider write properties applied to create, update, patch, batch and merge operations. For instance users can skip the Json object wrapper or enable content only mode when sending request data. A service URI set in the properties will always be overwritten by the serviceUri configuration parameter. Please consider to using the serviceUri configuration parameter instead of setting the respective write property here. |  | EntityProviderWriteProperties |
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

The Olingo2 endpoint is configured using URI syntax:

olingo2:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   DEFAULT
    





 |  | Olingo2ApiName |
| **methodName** (common) | **Required** What sub operation to use for the selected operation. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectTimeout** (common) | HTTP connection creation timeout in milliseconds, defaults to 30,000 (30 seconds). | 30000 | int |
| **contentType** (common) | Content-Type header value can be used to specify JSON or XML message format, defaults to application/json;charset=utf-8. | application/json;charset=utf-8 | String |
| **entityProviderReadProperties** (common) | Custom entity provider read properties applied to all read operations. |  | EntityProviderReadProperties |
| **entityProviderWriteProperties** (common) | Custom entity provider write properties applied to create, update, patch, batch and merge operations. For instance users can skip the Json object wrapper or enable content only mode when sending request data. A service URI set in the properties will always be overwritten by the serviceUri configuration parameter. Please consider to using the serviceUri configuration parameter instead of setting the respective write property here. |  | EntityProviderWriteProperties |
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

The Olingo2 endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

olingo2:apiName/methodName

There are 1 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**DEFAULT**](#_api_DEFAULT) | Both | Olingo2 Client Api Interface |

Each API is documented in the following sections to come.

### API: DEFAULT

**Both producer and consumer are supported**

The DEFAULT API is defined in the syntax as follows:

```none
olingo2:DEFAULT/methodName?[parameters]
```

The 8 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**batch**](#_api_DEFAULT_method_batch) |  | Executes a batch request |
| [**create**](#_api_DEFAULT_method_create) |  | Creates a new OData resource |
| [**delete**](#_api_DEFAULT_method_delete) |  | Deletes an OData resource and invokes callback with org |
| [**merge**](#_api_DEFAULT_method_merge) |  | Patches/merges an OData resource using HTTP MERGE |
| [**patch**](#_api_DEFAULT_method_patch) |  | Patches/merges an OData resource using HTTP PATCH |
| [**read**](#_api_DEFAULT_method_read) |  | Reads an OData resource and invokes callback with appropriate result |
| [**update**](#_api_DEFAULT_method_update) |  | Updates an OData resource |
| [**uread**](#_api_DEFAULT_method_uread) |  | Reads an OData resource and invokes callback with the unparsed input stream |

#### Method batch

Signatures:

-   void batch(org.apache.olingo.odata2.api.edm.Edm edm, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo2.api.Olingo2ResponseHandler<java.util.List<org.apache.camel.component.olingo2.api.batch.Olingo2BatchResponse>> responseHandler);
    

The olingo2/batch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Ordered org.apache.camel.component.olingo2.api.batch.Olingo2BatchRequest list | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **responseHandler** | Callback handler | Olingo2ResponseHandler |

#### Method create

Signatures:

-   void create(org.apache.olingo.odata2.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo2.api.Olingo2ResponseHandler responseHandler);
    

The olingo2/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Request data | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path to create | String |
| **responseHandler** | Callback handler | Olingo2ResponseHandler |

#### Method delete

Signatures:

-   void delete(String resourcePath, java.util.Map<String, String> endpointHttpHeaders, org.apache.camel.component.olingo2.api.Olingo2ResponseHandler<org.apache.olingo.odata2.api.commons.HttpStatusCodes> responseHandler);
    

The olingo2/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path for Entry | String |
| **responseHandler** | Org.apache.olingo.odata2.api.commons.HttpStatusCodes callback handler | Olingo2ResponseHandler |

#### Method merge

Signatures:

-   void merge(org.apache.olingo.odata2.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo2.api.Olingo2ResponseHandler responseHandler);
    

The olingo2/merge API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Patch/merge data | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path to update | String |
| **responseHandler** | Org.apache.olingo.odata2.api.ep.entry.ODataEntry callback handler | Olingo2ResponseHandler |

#### Method patch

Signatures:

-   void patch(org.apache.olingo.odata2.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo2.api.Olingo2ResponseHandler responseHandler);
    

The olingo2/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Patch/merge data | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path to update | String |
| **responseHandler** | Org.apache.olingo.odata2.api.ep.entry.ODataEntry callback handler | Olingo2ResponseHandler |

#### Method read

Signatures:

-   void read(org.apache.olingo.odata2.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> queryParams, java.util.Map<String, String> endpointHttpHeaders, org.apache.camel.component.olingo2.api.Olingo2ResponseHandler responseHandler);
    

The olingo2/read API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **edm** | Service Edm, read from calling read(null, $metdata, null, responseHandler) | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **queryParams** | OData query params from [http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SystemQueryOptions](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SystemQueryOptions) | Map |
| **resourcePath** | OData Resource path | String |
| **responseHandler** | Callback handler | Olingo2ResponseHandler |

#### Method update

Signatures:

-   void update(org.apache.olingo.odata2.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> endpointHttpHeaders, Object data, org.apache.camel.component.olingo2.api.Olingo2ResponseHandler responseHandler);
    

The olingo2/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **data** | Updated data | Object |
| **edm** | Service Edm | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **resourcePath** | Resource path to update | String |
| **responseHandler** | Org.apache.olingo.odata2.api.ep.entry.ODataEntry callback handler | Olingo2ResponseHandler |

#### Method uread

Signatures:

-   void uread(org.apache.olingo.odata2.api.edm.Edm edm, String resourcePath, java.util.Map<String, String> queryParams, java.util.Map<String, String> endpointHttpHeaders, org.apache.camel.component.olingo2.api.Olingo2ResponseHandler<java.io.InputStream> responseHandler);
    

The olingo2/uread API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **edm** | Service Edm, read from calling read(null, $metdata, null, responseHandler) | Edm |
| **endpointHttpHeaders** | HTTP Headers to add/override the component versions | Map |
| **queryParams** | OData query params from [http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SystemQueryOptions](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SystemQueryOptions) | Map |
| **resourcePath** | OData Resource path | String |
| **responseHandler** | Callback handler | Olingo2ResponseHandler |

In addition to the parameters above, the olingo2 API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelOlingo2.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelOlingo2.myParameterNameHere` header.

## Message Headers

The Olingo2 component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOlingo2.responseHttpHeaders** (producer) Constant: [`RESPONSE_HTTP_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-olingo2/latest/org/apache/camel/component/olingo2/internal/Olingo2Constants.html#RESPONSE_HTTP_HEADERS) | The response Http headers. |  | Map |
> **Note**
> This is an API-based component, so per-call parameters can be supplied through `Camel`\-prefixed exchange headers in addition to the endpoint options. If the route consumes messages from untrusted producers, strip these internal headers at the trust boundary — for example with `removeHeaders("Camel*")` — before the message reaches this component, so that a sender cannot override the API call. See [the Camel security model](../../manual/security-model.md) for details.

## Usage

### Endpoint HTTP Headers

The component level configuration property **httpHeaders** supplies static HTTP header information. However, some systems require dynamic header information to be passed to and received from the endpoint. A sample use case would be systems that require dynamic security tokens. The **endpointHttpHeaders** and **responseHttpHeaders** endpoint properties provide this capability. Set headers that need to be passed to the endpoint in the **`CamelOlingo2.endpointHttpHeaders`** property and the response headers will be returned in a **`CamelOlingo2.responseHttpHeaders`** property. Both properties are of the type `java.util.Map<String, String>`.

### OData Resource Type Mapping

The result of **read** endpoint and data type of **data** option depends on the OData resource being queried, created or modified.

  
| OData Resource Type | Resource URI from resourcePath and keyPredicate | In or Out Body Type |
| --- | --- | --- |
| Entity data model | $metadata | `org.apache.olingo.odata2.api.edm.Edm` |
| Service document | / | `org.apache.olingo.odata2.api.servicedocument.ServiceDocument` |
| OData feed | <entity-set> | `org.apache.olingo.odata2.api.ep.feed.ODataFeed` |
| OData entry | <entity-set>(<key-predicate>) | `org.apache.olingo.odata2.api.ep.entry.ODataEntry` for Out body (response) `java.util.Map<String, Object>` for In body (request) |
| Simple property | <entity-set>(<key-predicate>)/<simple-property> | The appropriate Java data type as described by Olingo EdmProperty |
| Simple property value | <entity-set>(<key-predicate>)/<simple-property>/$value | The appropriate Java data type as described by Olingo EdmProperty |
| Complex property | <entity-set>(<key-predicate>)/<complex-property> | java.util.Map<String, Object> |
| Zero or one association link | <entity-set>(<key-predicate>/$link/<one-to-one-entity-set-property> | String for response `java.util.Map<String, Object>` with key property names and values for request |
| Zero or many association links | <entity-set>(<key-predicate>/$link/<one-to-many-entity-set-property> | `java.util.List<String>` for response `java.util.List<java.util.Map<String, Object>>` containing a list of key property names and values for request |
| Count | <resource-uri>/$count | java.lang.Long |

## Examples

The following route reads top 5 entries from the Manufacturer feed ordered by ascending Name property.

_Java-only: uses setHeader with Java constant_

```java
from("direct:...")
    .setHeader("CamelOlingo2.$top", "5");
    .to("olingo2://read/Manufacturers?orderBy=Name%20asc");
```

The following route reads Manufacturer entry using the key property value in incoming **id** header.

_Java-only: uses setHeader with header() expression_

```java
from("direct:...")
    .setHeader("CamelOlingo2.keyPredicate", header("id"))
    .to("olingo2://read/Manufacturers");
```

The following route creates Manufacturer entry using the `java.util.Map<String, Object>` in the body message.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:...")
    .to("olingo2://create/Manufacturers");
```

```xml
<route>
    <from uri="direct:..."/>
    <to uri="olingo2://create/Manufacturers"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:...
    steps:
      - to:
          uri: olingo2://create/Manufacturers
```

The following route polls Manufacturer [delta feed](http://olingo.apache.org/doc/tutorials/deltaClient.md) every 30 seconds. The bean **blah** updates the bean **paramsBean** to add an updated **!deltatoken** property with the value returned in the **ODataDeltaFeed** result. Since the initial delta token is not known, the consumer endpoint will produce an **ODataFeed** value the first time, and **ODataDeltaFeed** on subsequent polls.

-   Java
    
-   XML
    
-   YAML
    

```java
from("olingo2://read/Manufacturers?queryParams=#paramsBean&timeUnit=SECONDS&delay=30")
    .to("bean:blah");
```

```xml
<route>
    <from uri="olingo2://read/Manufacturers?queryParams=#paramsBean&amp;timeUnit=SECONDS&amp;delay=30"/>
    <to uri="bean:blah"/>
</route>
```

```yaml
- route:
    from:
      uri: olingo2://read/Manufacturers
      parameters:
        queryParams: "#paramsBean"
        timeUnit: SECONDS
        delay: 30
    steps:
      - to:
          uri: bean:blah
```