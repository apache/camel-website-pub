# Apicurio Registry

**Since Camel 4.24**

**Both producer and consumer are supported**

The Apicurio Registry component provides integration with [Apicurio Registry](https://www.apicur.io/registry/) v3 using the [Apicurio Registry Java SDK](https://github.com/Apicurio/apicurio-registry).

It supports CRUD operations on artifacts, groups, and versions, as well as schema validation and polling for new artifact versions.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-apicurio-registry</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

apicurio-registry:groupId/artifactId\[?options\]

Where `groupId` and `artifactId` identify the registry artifact. Both are optional for operations that do not require them (e.g., `searchArtifacts`, `createGroup`).

The first `/` separates the group ID from the artifact ID. Group IDs containing `/` cannot be represented in the URI path. Producers can instead supply the group ID using the `CamelApicurioRegistryGroupId` header, which overrides the URI value.

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

The Apicurio Registry component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **registryUrl** (common) | **Required** The Apicurio Registry base URL. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **fetchContent** (consumer) | Whether to fetch the content for each new version found by the consumer. | false | boolean |
| **artifactType** (producer) | The default artifact type. | JSON | String |
| **failOnValidation** (producer) | Whether to throw an exception on validation failure (validate operation). When false, sets result headers instead. | true | boolean |
| **ifExists** (producer) | 
Behavior when artifact already exists.

Enum values:

-   FAIL
    
-   CREATE\_VERSION
    
-   FIND\_OR\_CREATE\_VERSION
    





 | FAIL | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 

The operation to perform.

Enum values:

-   createArtifact
    
-   updateArtifact
    
-   deleteArtifact
    
-   getArtifactContent
    
-   getArtifactMetadata
    
-   searchArtifacts
    
-   listVersions
    
-   createGroup
    
-   testCompatibility
    
-   validate
    





 |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | The component configuration. |  | ApicurioRegistryConfiguration |
| **vertx** (advanced) | **Autowired** To use an existing Vert.x instance for the registry clients. If not set, the component creates one shared Vert.x instance on first use and closes it when the component stops. |  | Vertx |
| **proxyHost** (proxy) | The proxy host to use for registry (and OAuth2 token) requests. |  | String |
| **proxyPassword** (proxy) | The password for proxy authentication. |  | String |
| **proxyPort** (proxy) | The proxy port. |  | Integer |
| **proxyUsername** (proxy) | The username for proxy authentication. |  | String |
| **authType** (security) | 

The authentication type to use.

Enum values:

-   none
    
-   basic
    
-   oidc
    





 | none | String |
| **clientId** (security) | OAuth2 client ID. |  | String |
| **clientSecret** (security) | OAuth2 client secret. |  | String |
| **password** (security) | Password for basic authentication. |  | String |
| **scope** (security) | OAuth2 scope. |  | String |
| **sslContextParameters** (security) | To configure TLS, such as a trust store for a registry with a private CA or a client certificate (mTLS), using the Camel JSSE configuration. Also applies to the OAuth2 token endpoint. |  | SSLContextParameters |
| **tokenEndpoint** (security) | OAuth2 token endpoint URL. |  | String |
| **username** (security) | Username for basic authentication. |  | String |

## Endpoint Options

The Apicurio Registry endpoint is configured using URI syntax:

apicurio-registry:groupId/artifactId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **groupId** (common) | The artifact group ID. |  | String |
| **artifactId** (common) | The artifact ID. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **registryUrl** (common) | **Required** The Apicurio Registry base URL. |  | String |
| **fetchContent** (consumer) | Whether to fetch the content for each new version found by the consumer. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **artifactType** (producer) | The default artifact type. | JSON | String |
| **failOnValidation** (producer) | Whether to throw an exception on validation failure (validate operation). When false, sets result headers instead. | true | boolean |
| **ifExists** (producer) | 

Behavior when artifact already exists.

Enum values:

-   FAIL
    
-   CREATE\_VERSION
    
-   FIND\_OR\_CREATE\_VERSION
    





 | FAIL | String |
| **operation** (producer) | 

The operation to perform.

Enum values:

-   createArtifact
    
-   updateArtifact
    
-   deleteArtifact
    
-   getArtifactContent
    
-   getArtifactMetadata
    
-   searchArtifacts
    
-   listVersions
    
-   createGroup
    
-   testCompatibility
    
-   validate
    





 |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **registryClient** (advanced) | To use a pre-configured RegistryClient instance. |  | RegistryClient |
| **proxyHost** (proxy) | The proxy host to use for registry (and OAuth2 token) requests. |  | String |
| **proxyPassword** (proxy) | The password for proxy authentication. |  | String |
| **proxyPort** (proxy) | The proxy port. |  | Integer |
| **proxyUsername** (proxy) | The username for proxy authentication. |  | String |
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
| **authType** (security) | 

The authentication type to use.

Enum values:

-   none
    
-   basic
    
-   oidc
    





 | none | String |
| **clientId** (security) | OAuth2 client ID. |  | String |
| **clientSecret** (security) | OAuth2 client secret. |  | String |
| **password** (security) | Password for basic authentication. |  | String |
| **scope** (security) | OAuth2 scope. |  | String |
| **sslContextParameters** (security) | To configure TLS, such as a trust store for a registry with a private CA or a client certificate (mTLS), using the Camel JSSE configuration. Also applies to the OAuth2 token endpoint. |  | SSLContextParameters |
| **tokenEndpoint** (security) | OAuth2 token endpoint URL. |  | String |
| **username** (security) | Username for basic authentication. |  | String |

## Message Headers

The Apicurio Registry component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelApicurioRegistryOperation** (common) Constant: [`HEADER_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_OPERATION) | The operation to perform. |  | String |
| **CamelApicurioRegistryGroupId** (common) Constant: [`HEADER_GROUP_ID`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_GROUP_ID) | The artifact group ID. |  | String |
| **CamelApicurioRegistryArtifactId** (common) Constant: [`HEADER_ARTIFACT_ID`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_ARTIFACT_ID) | The artifact ID. |  | String |
| **CamelApicurioRegistryArtifactType** (common) Constant: [`HEADER_ARTIFACT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_ARTIFACT_TYPE) | The artifact type (e.g. AVRO, PROTOBUF, JSON, OPENAPI). |  | String |
| **CamelApicurioRegistryVersion** (common) Constant: [`HEADER_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_VERSION) | The artifact version expression. |  | String |
| **CamelApicurioRegistryArtifactName** (common) Constant: [`HEADER_ARTIFACT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_ARTIFACT_NAME) | The artifact name. |  | String |
| **CamelApicurioRegistryArtifactDescription** (common) Constant: [`HEADER_ARTIFACT_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_ARTIFACT_DESCRIPTION) | The artifact description. |  | String |
| **CamelApicurioRegistryIfExists** (common) Constant: [`HEADER_IF_EXISTS`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_IF_EXISTS) | Behavior when artifact already exists (FAIL, CREATE\_VERSION, FIND\_OR\_CREATE\_VERSION). |  | String |
| **CamelApicurioRegistryContentType** (common) Constant: [`HEADER_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_CONTENT_TYPE) | The content type of the artifact. |  | String |
| **CamelApicurioRegistryGlobalId** (consumer) Constant: [`HEADER_GLOBAL_ID`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_GLOBAL_ID) | The version global ID. |  | Long |
| **CamelApicurioRegistryContentId** (consumer) Constant: [`HEADER_CONTENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_CONTENT_ID) | The content ID. |  | Long |
| **CamelApicurioRegistryVersionState** (consumer) Constant: [`HEADER_VERSION_STATE`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_VERSION_STATE) | The version state. |  | String |
| **CamelApicurioRegistryValidationResult** (common) Constant: [`HEADER_VALIDATION_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_VALIDATION_RESULT) | Whether the check passed. Set by validate and testCompatibility. |  | Boolean |
| **CamelApicurioRegistryValidationErrors** (common) Constant: [`HEADER_VALIDATION_ERRORS`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_VALIDATION_ERRORS) | Rule violation details from validate or testCompatibility. Cleared before each check. |  | String |
| **CamelApicurioRegistryLabels** (producer) Constant: [`HEADER_LABELS`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_LABELS) | Labels to filter searchArtifacts by, as key:value pairs. Either a comma-separated String or a collection. |  | String |
| **CamelApicurioRegistrySearchOffset** (producer) Constant: [`HEADER_SEARCH_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_SEARCH_OFFSET) | The number of results to skip in searchArtifacts. Defaults to 0. |  | Integer |
| **CamelApicurioRegistrySearchLimit** (producer) Constant: [`HEADER_SEARCH_LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_SEARCH_LIMIT) | The maximum number of results returned by searchArtifacts. The registry defaults to 20. |  | Integer |
| **CamelApicurioRegistrySearchOrder** (producer) Constant: [`HEADER_SEARCH_ORDER`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_SEARCH_ORDER) | The sort order for searchArtifacts: asc or desc. |  | String |
| **CamelApicurioRegistrySearchOrderBy** (producer) Constant: [`HEADER_SEARCH_ORDER_BY`](https://javadoc.io/doc/org.apache.camel/camel-apicurio-registry/latest/org/apache/camel/component/apicurioregistry/ApicurioRegistryConstants.html#HEADER_SEARCH_ORDER_BY) | The field to sort searchArtifacts by: groupId, artifactId, createdOn, modifiedOn, artifactType or name. |  | String |

## Producer Operations

The producer supports the following operations, set via the `operation` endpoint option or the `CamelApicurioRegistryOperation` header:

 
| Operation | Description |
| --- | --- |
| `createArtifact` | Create a new artifact. Body contains the artifact content. |
| `updateArtifact` | Create a new version of an existing artifact. Body contains the new content. |
| `deleteArtifact` | Delete an artifact. Apicurio Registry 3.x disables artifact deletion by default; the registry must run with `apicurio.rest.deletion.artifact.enabled=true` (environment variable `APICURIO_REST_DELETION_ARTIFACT_ENABLED=true`), otherwise the operation fails with HTTP 405. |
| `getArtifactContent` | Retrieve the content of an artifact version. |
| `getArtifactMetadata` | Retrieve artifact metadata. |
| `searchArtifacts` | Search for artifacts. See the "Searching artifacts" section below. |
| `listVersions` | List all versions of an artifact, ordered by global ID. The component follows the registry’s pagination and returns every page. |
| `createGroup` | Create a new group. |
| `testCompatibility` | Test schema compatibility (dry run). Returns `true`/`false` in the body. |
| `validate` | Validate the message body against the artifact’s rules (dry run). Throws `ApicurioRegistryValidationException` on failure when `failOnValidation=true`. |

Artifact content supplied to `createArtifact`, `updateArtifact`, `validate`, and `testCompatibility` is converted to a string for the SDK’s `VersionContent` model. Its content type is taken from the `CamelApicurioRegistryContentType` header. Without the header, it is derived from the content: `application/json` when it starts with `{` or `[`, `application/xml` when it starts with `<`, `application/x-protobuf` or `application/graphql` for PROTOBUF and GRAPHQL artifacts, and `application/x-yaml` otherwise (for example OpenAPI or AsyncAPI documents written in YAML). For AVRO and PROTOBUF, supply the schema definition, rather than serialized message data. `getArtifactContent` returns a `byte[]`; the component closes the SDK response stream before passing the content to the route.

`validate` and `testCompatibility` check a proposed artifact version against the registry’s configured rules without storing it. They do not validate application messages against a stored schema. Authentication, connectivity, and other non-rule failures propagate as exceptions, rather than returning a negative validation result.

Both operations set `CamelApicurioRegistryValidationErrors` to the rule violation details when a check fails and clear any previous value before checking. Both set `CamelApicurioRegistryValidationResult`; `testCompatibility` also returns the boolean result in the body, while `validate` preserves the body.

Operations that act on a specific group or artifact fail with an `IllegalArgumentException` when the group or artifact ID is set neither in the endpoint path nor in a header.

### Searching artifacts

`searchArtifacts` filters by group ID and artifact ID (endpoint path or headers), and by the `CamelApicurioRegistryArtifactName`, `CamelApicurioRegistryArtifactDescription`, `CamelApicurioRegistryArtifactType` and `CamelApicurioRegistryLabels` headers. The body is an `ArtifactSearchResults` holding one page of results and the total `count`.

Results are paged: the registry returns at most 20 artifacts unless you set `CamelApicurioRegistrySearchLimit`. Use `CamelApicurioRegistrySearchOffset` to request further pages, and `CamelApicurioRegistrySearchOrder` (`asc` or `desc`) and `CamelApicurioRegistrySearchOrderBy` (`groupId`, `artifactId`, `createdOn`, `modifiedOn`, `artifactType` or `name`) to sort them.

### Headers from a consumer

The consumer sets the group, artifact and version headers on every exchange, and producers give these headers precedence over their endpoint path. When a route forwards consumed versions to another registry endpoint, remove them first so the producer uses its own path:

```java
from("apicurio-registry:dev/orders?registryUrl={{dev.registry}}&fetchContent=true")
    .removeHeaders("CamelApicurioRegistry*")
    .to("apicurio-registry:prod/orders?registryUrl={{prod.registry}}&operation=updateArtifact");
```

## Consumer

The consumer polls the registry for new versions of the specified artifact. It tracks the last seen `globalId` and only delivers new versions. Set the `delay` option to control the polling interval (default: 500ms).

On first start, all existing versions of the artifact are emitted as exchanges. Subsequent polls only deliver versions created after the consumer started. The watermark is held in memory and resets on route/context restart.

Once it has a watermark, each poll first asks only for the newest version, so an idle poll transfers a single entry. When there is something new, the consumer requests versions newest first, one page at a time, and stops at the first version it has already seen. Paging is offset-based: if a version is deleted while the consumer is reading pages, an older new version can move to a page that was already read and be skipped.

All version states are listed, so `DRAFT` versions are delivered as soon as they appear. If the registry allows changing the content of a version, a version is not delivered again after its content changes. With `fetchContent=true`, `DISABLED` versions are skipped, because the registry does not return their content. If the content of a version is not found (HTTP 404), the consumer retries it on later polls, since a registry node with replicated storage may not have the version yet; if it is still not found once at least one polling `delay` has passed (also with `greedy=true`), the version is skipped with a warning. Skipped versions are not delivered again, even if a disabled version is enabled later.

If fetching content fails, or the route fails to process a version (including failures handled by the error handler without being rethrown, such as with the default error handler), the consumer stops the current poll without advancing the watermark. The failed version and any newer ones are delivered again on the next poll. A version that always fails therefore blocks newer versions. To skip such a version, mark the failure as handled, which lets the consumer advance past it:

```java
onException(MyPermanentException.class).handled(true).to("log:skipped");
```

When `fetchContent=true`, the consumer fetches the version content and sets it as a `byte[]` exchange body, closing the SDK response stream before processing the exchange. Otherwise, the version metadata object is set as the body.

## Examples

### Create an artifact

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:create")
    .setBody(constant("{\"type\":\"record\",\"name\":\"Test\",\"fields\":[]}"))
    .to("apicurio-registry:myGroup/myArtifact?registryUrl=http://localhost:8080/apis/registry/v3&operation=createArtifact&artifactType=AVRO");
```

```xml
<route>
  <from uri="direct:create"/>
  <setBody><constant>{"type":"record","name":"Test","fields":[]}</constant></setBody>
  <to uri="apicurio-registry:myGroup/myArtifact?registryUrl=http://localhost:8080/apis/registry/v3&amp;operation=createArtifact&amp;artifactType=AVRO"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:create
      steps:
        - setBody:
            constant: '{"type":"record","name":"Test","fields":[]}'
        - to:
            uri: apicurio-registry:myGroup/myArtifact
            parameters:
              registryUrl: http://localhost:8080/apis/registry/v3
              operation: createArtifact
              artifactType: AVRO
```

### Poll for new versions

-   Java
    
-   XML
    
-   YAML
    

```java
from("apicurio-registry:myGroup/myArtifact?registryUrl=http://localhost:8080/apis/registry/v3&delay=5000")
    .log("New version detected: ${header.CamelApicurioRegistryVersion}")
    .to("log:newVersions");
```

```xml
<route>
  <from uri="apicurio-registry:myGroup/myArtifact?registryUrl=http://localhost:8080/apis/registry/v3&amp;delay=5000"/>
  <log message="New version detected: ${header.CamelApicurioRegistryVersion}"/>
  <to uri="log:newVersions"/>
</route>
```

```yaml
- route:
    from:
      uri: apicurio-registry:myGroup/myArtifact
      parameters:
        registryUrl: http://localhost:8080/apis/registry/v3
        delay: 5000
      steps:
        - log:
            message: "New version detected: ${header.CamelApicurioRegistryVersion}"
        - to:
            uri: log:newVersions
```

### Validate a proposed schema version

```java
from("direct:validateSchema")
    .doTry()
        .to("apicurio-registry:my-group/order-schema?operation=validate&registryUrl=http://localhost:8080/apis/registry/v3")
        .to("direct:publishSchema")
    .doCatch(ApicurioRegistryValidationException.class)
        .setHeader(Exchange.HTTP_RESPONSE_CODE, constant(400))
        .setBody(simple("${exception.validationErrors}"))
    .end();
```

## Connection settings

All endpoints of the component share a single Vert.x instance for their SDK clients. The component creates it on first use and closes it when the component stops. To reuse an existing Vert.x instance, set the `vertx` component option or bind a single `Vertx` bean in the registry; the component does not close a Vert.x instance it did not create.

A client supplied through `registryClient` remains caller-owned; the caller is responsible for its underlying HTTP resources.

For HTTPS registries that use a private CA or require client certificates (mTLS), configure `sslContextParameters`. Use `proxyHost`, `proxyPort`, `proxyUsername` and `proxyPassword` to go through an HTTP proxy. Both settings also apply to the OAuth2 token endpoint.

## Authentication

The component never follows HTTP redirects, so credentials are never sent to another host. Configure `registryUrl` with the final address of the registry API.

The producer makes blocking calls. It cannot run on a Vert.x event loop thread, for example in a route started by an event-loop consumer of the same Vert.x instance; it fails with an `IllegalStateException` there. Hand the exchange to a worker thread first, for example with `threads()`.

The component supports three authentication modes via the `authType` option:

-   `none` (default): No authentication.
    
-   `basic`: Basic authentication using `username` and `password`.
    
-   `oidc`: OAuth2/OIDC using `tokenEndpoint`, `clientId`, `clientSecret`, and optionally `scope`.
    

Example with OIDC:

```java
from("direct:secured")
    .to("apicurio-registry:myGroup/myArtifact?registryUrl=http://localhost:8080/apis/registry/v3"
        + "&operation=getArtifactContent"
        + "&authType=oidc"
        + "&tokenEndpoint=http://keycloak:8080/realms/registry/protocol/openid-connect/token"
        + "&clientId=registry-client&clientSecret=secret");
```