# REST Postman

**Since Camel 4.23**

**Both producer and consumer are supported**

The REST Postman component configures rest producers and contract-first rest consumers from a [Postman Collection](https://learning.postman.com/docs/collections/collections-overview/), and delegates to a component implementing the _RestProducerFactory_ interface. Currently, known working components are:

-   [http](http-component.md)
    
-   [netty-http](netty-http-component.md)
    
-   [undertow](undertow-component.md)
    
-   [vertx-http](vertx-http-component.md)
    

It is the Postman equivalent of [rest-openapi](rest-openapi-component.md). Use it when a Postman Collection is the description of the API you have, rather than an OpenAPI specification.

> **Important**
> Only the Postman Collection Format v2.1 is supported.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-rest-postman</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

rest-postman:\[collectionSource#\]requestId

`collectionSource` is either a resource URI of a Collection v2.1 JSON document (`classpath:`, `file:` or `http:`), or the uid of a collection to fetch from the Postman cloud. It defaults to `postman-collection.json` on the classpath.

`requestId` selects what to invoke:

 
| Fragment | Selects |
| --- | --- |
| `getPetById` | the single request whose name slugifies to `getPetById` |
| `pets/addPet` | the request `Add Pet` inside the folder `Pets`, used when a name is not unique |
| `3f2504e0-4f89-11d3-9a0c-0305e82c3301` | the request with that `id`, which only collections fetched from the cloud carry |
| `pets` | every request in the folder `Pets` |
| `pets/` | the folder `Pets`, forced, for when a request and a folder share a name |
| _omitted_ | every request in the collection |

This component’s endpoint URI is lenient, which means that in addition to message headers you can specify a request’s parameters as endpoint parameters. These will be constant for all subsequent invocations, so it makes sense to use this feature only for parameters that are indeed constant for all invocations.

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

The REST Postman component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **basePath** (common) | API basePath, for example /v2. Default is unset, if set overrides the value derived from the request URL in the collection. |  | String |
| **collectionSource** (common) | The Postman Collection to use, when it is not given on the endpoint. Either a resource URI of a Collection v2.1 JSON document (classpath:, file: or http:), or the uid of a collection to fetch from the Postman cloud. |  | String |
| **collectionSourceType** (common) | 
How to interpret collectionSource. With auto, a bare collection UUID or {ownerId}-{uuid} is fetched from the Postman cloud and anything else is resolved as a resource (classpath:, file:, http:). Use resource or cloud to decide explicitly.

Enum values:

-   auto
    
-   resource
    
-   cloud
    





 | auto | String |
| **variables** (common) | Values for the \\{{variable}} placeholders used in the collection. These override the variables declared by the collection and its folders. This is a multi-value option with prefix: variable. |  | Map |
| **failOnUnresolvedVariable** (common (advanced)) | Whether to fail if a \\{{variable}} placeholder used by the selected request cannot be resolved. When false the placeholder is left as-is. | false | boolean |
| **apiContextPath** (consumer) | Sets the context-path to use for servicing the Postman collection document. The document is served with all auth blocks and all secret variables removed. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **clientRequestValidation** (consumer) | Whether to enable validation of the client request. A Postman collection has no schemas, so this is a best-effort check of required headers, query parameters and body presence only. | false | boolean |
| **missingRequest** (consumer) | 

Whether the consumer should fail, ignore or return a mock response for requests in the collection that are not mapped to a corresponding route.

Enum values:

-   fail
    
-   ignore
    
-   mock
    





 | fail | String |
| **consumerComponentName** (consumer (advanced)) | Name of the Camel component that will service the requests. The component must be present in Camel registry and it must be able to service contract-first REST consumers, as platform-http does. If not set CLASSPATH is searched for a single component with that capability. |  | String |
| **mockIncludePattern** (consumer (advanced)) | Used for inclusive filtering of mock data from directories. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma. Saved example responses in the collection are preferred over these files. | classpath:camel-mock/\*\* | String |
| **requestFilter** (consumer (advanced)) | Filters which requests of the collection are used, as comma separated Ant-style patterns matched against the folder qualified request id. Prefix a pattern with ! to exclude. |  | String |
| **restPostmanProcessorStrategy** (consumer (advanced)) | To use a custom strategy for how to service the requests of the collection. |  | RestPostmanProcessorStrategy |
| **host** (producer) | Scheme hostname and port to direct the HTTP requests to in the form of [https://hostname:port](https://hostname:port). If set overrides any value derived from the collection. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **runFailFast** (producer) | When the endpoint runs more than one request, that is when it selects a folder or the whole collection, whether to stop and fail on the first request that fails. When false every request is attempted and the failure is recorded in its result. | true | boolean |
| **componentName** (producer (advanced)) | Name of the Camel component that will perform the requests. The component must be present in Camel registry and it must implement RestProducerFactory service provider interface. If not set CLASSPATH is searched for single component that implements RestProducerFactory SPI. |  | String |
| **consumes** (producer (advanced)) | What payload type this component is capable of consuming. This equates to the value of the Accept HTTP header. A Postman collection does not describe responses, so unlike an OpenAPI specification there is nothing to infer this from and it is unset by default. |  | String |
| **produces** (producer (advanced)) | What payload type this component is producing. This equates to the value of the Content-Type HTTP header. If not set it is inferred from the body mode of the request in the collection. |  | String |
| **queryParameterMode** (producer (advanced)) | 

How to treat the query parameters declared in the collection. With placeholder the parameter names are bound to message headers and the values in the collection are ignored as sample data. With literal the values in the collection are sent as-is.

Enum values:

-   placeholder
    
-   literal
    





 | placeholder | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **collectionCacheTtl** (advanced) | How long a loaded collection is cached, in milliseconds. Use -1 to cache for the lifetime of the component. | \-1 | long |
| **configuration** (advanced) | The shared configuration used as the template for every endpoint created by this component. |  | RestPostmanConfiguration |
| **connectTimeout** (advanced) | Connection timeout in milliseconds when fetching a collection from the Postman cloud. | 15000 | long |
| **requestTimeout** (advanced) | Request timeout in milliseconds when fetching a collection from the Postman cloud. | 30000 | long |
| **collectionAuth** (security) | 

What to do with the auth block the collection declares for the target API. With ignore the block is not applied, and a warning names the type that was found. With header the basic, bearer and apikey types are applied as a static header or query parameter, and any other type fails at startup rather than silently sending no credential. With fail any auth block other than noauth is rejected.

Enum values:

-   ignore
    
-   header
    
-   fail
    





 | ignore | String |
| **oauthProfile** (security) | The OAuth profile to use for authenticating the incoming requests. The profile is enforced by the consumer component servicing the requests. |  | String |
| **postmanApiKey** (security) | The Postman API key used to fetch the collection from the Postman cloud. This credential authenticates against Postman itself and is never sent to the API the collection describes. |  | String |
| **postmanApiKeyHeader** (security) | The HTTP header used to send the Postman API key when fetching a collection. | X-Api-Key | String |
| **sslContextParameters** (security) | Customize TLS parameters used by the component. If not set defaults to the TLS parameters set in the Camel context. These parameters are used both when fetching a collection from the Postman cloud and by the delegate producer. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **postmanApiUrl** (security (advanced)) | The base URL of the Postman API used to fetch collections. Must use https, except for localhost, because plain http would send the Postman API key in clear text. | [https://api.getpostman.com](https://api.getpostman.com) | String |

## Endpoint Options

The REST Postman endpoint is configured using URI syntax:

rest-postman:collectionSource#requestId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collectionSource** (common) | The Postman Collection to use. Either a resource URI of a Collection v2.1 JSON document (classpath:, file: or http:), or the uid of a collection to fetch from the Postman cloud, which requires postmanApiKey. Default value notice: By default loads the postman-collection.json file. | postman-collection.json | String |
| **requestId** (producer) | The request to invoke, identified by its id in the collection or by its slugified name, for example getUserById. Use a folder id to run every request in that folder, and leave it out to run the whole collection. Append a slash to force a folder match when a request and a folder share a name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **basePath** (common) | API basePath, for example /v2. Default is unset, if set overrides the value derived from the request URL in the collection. |  | String |
| **collectionSourceType** (common) | 
How to interpret collectionSource. With auto, a bare collection UUID or {ownerId}-{uuid} is fetched from the Postman cloud and anything else is resolved as a resource (classpath:, file:, http:). Use resource or cloud to decide explicitly.

Enum values:

-   auto
    
-   resource
    
-   cloud
    





 | auto | String |
| **variables** (common) | Values for the \\{{variable}} placeholders used in the collection. These override the variables declared by the collection and its folders. This is a multi-value option with prefix: variable. |  | Map |
| **failOnUnresolvedVariable** (common (advanced)) | Whether to fail if a \\{{variable}} placeholder used by the selected request cannot be resolved. When false the placeholder is left as-is. | false | boolean |
| **apiContextPath** (consumer) | Sets the context-path to use for servicing the Postman collection document. The document is served with all auth blocks and all secret variables removed. |  | String |
| **clientRequestValidation** (consumer) | Whether to enable validation of the client request. A Postman collection has no schemas, so this is a best-effort check of required headers, query parameters and body presence only. | false | boolean |
| **missingRequest** (consumer) | 

Whether the consumer should fail, ignore or return a mock response for requests in the collection that are not mapped to a corresponding route.

Enum values:

-   fail
    
-   ignore
    
-   mock
    





 | fail | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerComponentName** (consumer (advanced)) | Name of the Camel component that will service the requests. The component must be present in Camel registry and it must be able to service contract-first REST consumers, as platform-http does. If not set CLASSPATH is searched for a single component with that capability. |  | String |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **mockIncludePattern** (consumer (advanced)) | Used for inclusive filtering of mock data from directories. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma. Saved example responses in the collection are preferred over these files. | classpath:camel-mock/\*\* | String |
| **requestFilter** (consumer (advanced)) | Filters which requests of the collection are used, as comma separated Ant-style patterns matched against the folder qualified request id. Prefix a pattern with ! to exclude. |  | String |
| **host** (producer) | Scheme hostname and port to direct the HTTP requests to in the form of [https://hostname:port](https://hostname:port). If set overrides any value derived from the collection. |  | String |
| **runFailFast** (producer) | When the endpoint runs more than one request, that is when it selects a folder or the whole collection, whether to stop and fail on the first request that fails. When false every request is attempted and the failure is recorded in its result. | true | boolean |
| **componentName** (producer (advanced)) | Name of the Camel component that will perform the requests. The component must be present in Camel registry and it must implement RestProducerFactory service provider interface. If not set CLASSPATH is searched for single component that implements RestProducerFactory SPI. |  | String |
| **consumes** (producer (advanced)) | What payload type this component is capable of consuming. This equates to the value of the Accept HTTP header. A Postman collection does not describe responses, so unlike an OpenAPI specification there is nothing to infer this from and it is unset by default. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **produces** (producer (advanced)) | What payload type this component is producing. This equates to the value of the Content-Type HTTP header. If not set it is inferred from the body mode of the request in the collection. |  | String |
| **queryParameterMode** (producer (advanced)) | 

How to treat the query parameters declared in the collection. With placeholder the parameter names are bound to message headers and the values in the collection are ignored as sample data. With literal the values in the collection are sent as-is.

Enum values:

-   placeholder
    
-   literal
    





 | placeholder | String |
| **collectionCacheTtl** (advanced) | How long a loaded collection is cached, in milliseconds. Use -1 to cache for the lifetime of the component. | \-1 | long |
| **connectTimeout** (advanced) | Connection timeout in milliseconds when fetching a collection from the Postman cloud. | 15000 | long |
| **requestTimeout** (advanced) | Request timeout in milliseconds when fetching a collection from the Postman cloud. | 30000 | long |
| **collectionAuth** (security) | 

What to do with the auth block the collection declares for the target API. With ignore the block is not applied, and a warning names the type that was found. With header the basic, bearer and apikey types are applied as a static header or query parameter, and any other type fails at startup rather than silently sending no credential. With fail any auth block other than noauth is rejected.

Enum values:

-   ignore
    
-   header
    
-   fail
    





 | ignore | String |
| **oauthProfile** (security) | The OAuth profile to use for authenticating the incoming requests. The profile is enforced by the consumer component servicing the requests. |  | String |
| **postmanApiKey** (security) | The Postman API key used to fetch the collection from the Postman cloud. This credential authenticates against Postman itself and is never sent to the API the collection describes. |  | String |
| **postmanApiKeyHeader** (security) | The HTTP header used to send the Postman API key when fetching a collection. | X-Api-Key | String |
| **sslContextParameters** (security) | Customize TLS parameters used by the component. If not set defaults to the TLS parameters set in the Camel context. These parameters are used both when fetching a collection from the Postman cloud and by the delegate producer. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **postmanApiUrl** (security (advanced)) | The base URL of the Postman API used to fetch collections. Must use https, except for localhost, because plain http would send the Postman API key in clear text. | [https://api.getpostman.com](https://api.getpostman.com) | String |

## Message Headers

The REST Postman component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelRestPostmanRequestId** (common) Constant: [`REQUEST_ID`](https://javadoc.io/doc/org.apache.camel/camel-rest-postman/latest/org/apache/camel/component/rest/postman/RestPostmanConstants.html#REQUEST_ID) | The id of the Postman request being invoked or serviced. |  | String |
| **CamelRestPostmanRequestName** (common) Constant: [`REQUEST_NAME`](https://javadoc.io/doc/org.apache.camel/camel-rest-postman/latest/org/apache/camel/component/rest/postman/RestPostmanConstants.html#REQUEST_NAME) | The name of the Postman request, as written in the collection. |  | String |
| **CamelRestPostmanFolderPath** (common) Constant: [`FOLDER_PATH`](https://javadoc.io/doc/org.apache.camel/camel-rest-postman/latest/org/apache/camel/component/rest/postman/RestPostmanConstants.html#FOLDER_PATH) | The folder path of the Postman request, with folders separated by a slash. |  | String |
| **CamelRestPostmanRequestCount** (common) Constant: [`REQUEST_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-rest-postman/latest/org/apache/camel/component/rest/postman/RestPostmanConstants.html#REQUEST_COUNT) | The number of requests executed when running a folder or a whole collection. |  | Integer |
| **CamelRestPostmanFailedCount** (common) Constant: [`FAILED_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-rest-postman/latest/org/apache/camel/component/rest/postman/RestPostmanConstants.html#FAILED_COUNT) | The number of requests that failed when running a folder or a whole collection with runFailFast disabled. |  | Integer |

## Usage

### Identifying requests

A Postman item has a human readable name rather than an operation id, so this component slugifies it: `Get Pet By Id` becomes `getPetById`. When two requests slugify to the same thing, both are addressed by their folder qualified id instead, such as `pets/get` and `users/get`, and using the bare `get` is an error that lists the alternatives.

`item.id` is also accepted when the collection records one. Note that it is optional in the v2.1 schema, and Postman’s exporter strips auto-generated item ids, so an exported `collection.json` usually has none. Collections fetched from the Postman cloud do.

> **Important**
> Because the common case is to address a request by its slugified name, renaming a request in the Postman UI changes its id and will break routes bound to it.

### Invoking a single request

```java
from("direct:start")
    .to("rest-postman:petstore.json#getPetById");
```

The message body and headers of the exchange are what is sent. The collection supplies the method, the URL, and any headers the message does not already carry; the body written in the collection is treated as sample data and is not sent.

Path parameters written as `:petId` become `{petId}` placeholders resolved per exchange from the message header of the same name, falling back to the value declared in `url.variable`. Query parameters are bound to message headers in the same way and are dropped when unresolved. Set `queryParameterMode=literal` to send the values written in the collection instead.

### Running a folder or a whole collection

Naming a folder, or naming nothing at all, runs every request in turn, in the manner of Postman’s collection runner:

```java
from("direct:smokeTest")
    .to("rest-postman:petstore.json#pets")    // every request in the Pets folder
    .to("rest-postman:petstore.json");        // every request in the collection
```

Because one exchange body cannot stand in for many different requests, each request sends the body and headers written in the collection. `raw`, `graphql` and `urlencoded` bodies are reconstructed; `formdata` and `file` bodies cannot be, and are skipped with a warning. The `file` body mode is never read from disk, as it records a path on the machine of whoever authored the collection.

The message body becomes a `List` of `PostmanRunResult`, one per request, each carrying the request id, method, URI, status code, response body, headers and any failure. The headers `CamelRestPostmanRequestCount` and `CamelRestPostmanFailedCount` summarise the run.

By default the run stops and fails on the first request that fails. Set `runFailFast=false` to attempt every request and record the failures in their results instead:

```java
from("timer:smoke?period=60000")
    .to("rest-postman:petstore.json?runFailFast=false")
    .split(body())
        .filter(simple("${body.success} == false"))
        .to("log:failures");
```

### Contract-first consumer

Pointing a route’s `from` at a collection serves its requests over HTTP, dispatching each one to a route consuming from `direct:<requestId>`:

```java
from("rest-postman:petstore.json")
    .to("direct:dummy");

from("direct:getPetById")
    .setBody(constant("{ \"id\": 42 }"));
```

Use a folder id to serve only part of a collection, and `requestFilter` to include or exclude requests by Ant-style patterns over their folder qualified ids.

Because a collection does not describe a base path, the split between base path and route path is inferred from what `{{baseUrl}}` expands to. Set `basePath` explicitly to control the context path the consumer serves on.

`missingRequest` decides what happens when a request has no corresponding route: `fail` (the default) refuses to start, `ignore` warns, and `mock` returns a mocked response. Mock responses are taken from the collection’s own saved example responses where there are any, which is the one place a collection is richer than an OpenAPI specification, and fall back to files matched by `mockIncludePattern`.

If two requests share an HTTP method and path, which is common when a collection keeps a success and an error variant of the same call, the consumer fails at startup rather than letting one silently shadow the other. Use `requestFilter` to choose between them.

### Variables

`{{variable}}` placeholders are resolved from the collection’s own `variable` arrays, with folder scopes overriding the collection scope, then from the endpoint’s `variables` option, then from Camel property placeholders:

```java
from("direct:start")
    .to("rest-postman:petstore.json#getPetById?variable.baseUrl=https://staging.example.com/v3");
```

Postman environment files are not supported. Unresolved placeholders are left as they are unless `failOnUnresolvedVariable=true`.

A placeholder name written in the `prefix:value` form of a Camel property placeholder function — `{{env:HOME}}`, `{{sys:user.home}}`, `{{bean:foo}}` and the vault functions among them — is deliberately **not** resolved from Camel properties. A collection is route-author configuration, but a cloud-hosted one is editable by anyone with access to the Postman workspace, and resolving those would let its content pull an environment variable into an outgoing request. Supply such values through the `variables` option instead.

> **Note**
> Pre-request and test scripts in the collection’s `event` blocks are never parsed or executed.

## Security

### Two different credentials

There are two unrelated credentials in play, and the option names keep them apart:

`postmanApiKey`

authenticates against **Postman itself**, in order to download a collection from the Postman cloud. It is sent only to `postmanApiUrl`, and never to the API that the collection describes.

the collection’s own `auth` block

authenticates against **the API the collection describes**. It is governed by the `collectionAuth` option.

### Fetching a collection from the Postman cloud

```java
from("direct:start")
    .to("rest-postman:12ece9e1-2abf-4edc-8e34-de66e74114d2#getPetById?postmanApiKey=PMAK-xxxx");
```

Prefer resolving the key from a vault or a property placeholder over writing it in the URI. Redirects from `postmanApiUrl` are rejected rather than followed, because following one would send the key to the redirect target, and `postmanApiUrl` must use HTTPS unless it names a loopback host.

### Applying the collection’s auth block

`collectionAuth` defaults to `ignore`: the block is not applied, and a warning names the type that was found. This is deliberate, because the values in a collection’s auth block are usually unresolved `{{placeholders}}`, and silently attaching a credential found in a configuration file to outbound requests is surprising.

Set `collectionAuth=header` to apply it. The `basic`, `bearer` and `apikey` types are reproduced as a static header or query parameter. The types that require per-request signing or a token exchange — `awsv4`, `digest`, `hawk`, `edgegrid`, `ntlm`, `oauth1` and `oauth2` — fail at startup rather than silently sending no credential; configure those on the delegate HTTP component instead. `collectionAuth=fail` rejects any auth block at all.

On the consumer side the collection’s auth block describes what a client must present, and is **not** enforced. Use `oauthProfile`, or the delegate consumer component’s own authentication, for that.

### Serving the collection document

When `apiContextPath` is set, the collection is served on that path with every `auth` block removed and the value of every variable of type `secret` replaced. This redaction is unconditional.