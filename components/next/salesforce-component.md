# Salesforce

**Since Camel 2.12**

**Both producer and consumer are supported**

This component supports producer and consumer endpoints to communicate with Salesforce using Java DTOs. There is a companion [maven plugin](#MavenPlugin) that generates these DTOs.

> **Note**
> Developers wishing to contribute to the component are instructed to look at the [README.md](https://github.com/apache/camel/tree/main/components/camel-salesforce/camel-salesforce-component/README.md) file on instructions on how to get started and set up your environment for running integration tests.

## Getting Started

Follow these steps to get started with the Salesforce component.

1.  **Create a salesforce org**. If you don’t already have access to a salesforce org, you can create a [free developer org](https://developer.salesforce.com/signup).
    
2.  **Create a Connected App**. In salesforce, go to Setup > Apps > App Manager, then click on **New Connected App**. Make sure to check **Enable OAuth Settings** and include relevant OAuth Scopes, including the scope called **Perform requests at any time**. Click **Save**.
    
3.  **Get the Consumer Key and Consumer Secret**. You’ll need these to configure salesforce authentication. View your new connected app, then copy the key and secret and save in a safe place.
    
4.  **Add Maven dependency**.
    
    ```xml
    <dependency>
        <groupId>org.apache.camel</groupId>
        <artifactId>camel-salesforce</artifactId>
    </dependency>
    ```
    
    Spring Boot users should use the starter instead.
    
    ```xml
    <dependency>
        <groupId>org.apache.camel.springboot</groupId>
        <artifactId>camel-salesforce-starter</artifactId>
    </dependency>
    ```
    
5.  **Generate DTOs**. Optionally, generate Java DTOs to represent your salesforce objects. This step isn’t a hard requirement per se, but most use cases will benefit from the type safety and auto-completion. Use the [maven plugin](#MavenPlugin) to generate DTOs for the salesforce objects you’ll be working with.
    
6.  **Configure authentication**. Using the OAuth key and secret, you generated previously, configure salesforce [authentication](#AuthenticatingToSalesforce).
    
7.  **Create routes**. Starting creating routes that interact with salesforce!
    

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

The Salesforce component supports 108 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apexMethod** (common) | APEX method name. |  | String |
| **apexQueryParams** (common) | Query params for APEX method. |  | Map |
| **apiVersion** (common) | Salesforce API version. | 56.0 | String |
| **backoffIncrement** (common) | Backoff interval increment for Streaming connection restart attempts for failures beyond CometD auto-reconnect. | 1000 | long |
| **batchId** (common) | Bulk API Batch ID. |  | String |
| **contentType** (common) | 
Bulk API content type, one of XML, CSV, ZIP\_XML, ZIP\_CSV.

Enum values:

-   XML
    
-   CSV
    
-   JSON
    
-   ZIP\_XML
    
-   ZIP\_CSV
    
-   ZIP\_JSON
    





 |  | ContentType |
| **defaultReplayId** (common) | Default replayId setting if no value is found in initialReplayIdMap. | \-1 | Long |
| **fallBackReplayId** (common) | ReplayId to fall back to after an Invalid Replay Id response. | \-1 | Long |
| **format** (common) | 

Payload format to use for Salesforce API calls, either JSON or XML, defaults to JSON. As of Camel 3.12, this option only applies to the Raw operation.

Enum values:

-   JSON
    
-   XML
    





 |  | PayloadFormat |
| **httpClient** (common) | Custom Jetty Http Client to use to connect to Salesforce. |  | SalesforceHttpClient |
| **httpClientConnectionTimeout** (common) | Connection timeout used by the HttpClient when connecting to the Salesforce server. | 60000 | long |
| **httpClientIdleTimeout** (common) | Timeout used by the HttpClient when waiting for response from the Salesforce server. | 10000 | long |
| **httpMaxContentLength** (common) | Max content length of an HTTP response. |  | Integer |
| **httpRequestBufferSize** (common) | HTTP request buffer size. May need to be increased for large SOQL queries. | 8192 | Integer |
| **httpRequestTimeout** (common) | Timeout value for HTTP requests. | 60000 | long |
| **includeDetails** (common) | Include details in Salesforce1 Analytics report, defaults to false. | false | Boolean |
| **initialReplayIdMap** (common) | Replay IDs to start from per channel name. |  | Map |
| **instanceId** (common) | Salesforce1 Analytics report execution instance ID. |  | String |
| **jobId** (common) | Bulk API Job ID. |  | String |
| **limit** (common) | Limit on number of returned records. Applicable to some of the API, check the Salesforce documentation. |  | Integer |
| **locator** (common) | Locator provided by salesforce Bulk 2.0 API for use in getting results for a Query job. |  | String |
| **maxBackoff** (common) | Maximum backoff interval for Streaming connection restart attempts for failures beyond CometD auto-reconnect. | 30000 | long |
| **maxRecords** (common) | The maximum number of records to retrieve per set of results for a Bulk 2.0 Query. The request is still subject to the size limits. If you are working with a very large number of query results, you may experience a timeout before receiving all the data from Salesforce. To prevent a timeout, specify the maximum number of records your client is expecting to receive in the maxRecords parameter. This splits the results into smaller sets with this value as the maximum size. |  | Integer |
| **notFoundBehaviour** (common) | 

Sets the behaviour of 404 not found status received from Salesforce API. Should the body be set to NULL NotFoundBehaviour#NULL or should a exception be signaled on the exchange NotFoundBehaviour#EXCEPTION - the default.

Enum values:

-   EXCEPTION
    
-   NULL
    





 | EXCEPTION | NotFoundBehaviour |
| **notifyForFields** (common) | 

Notify for fields, options are ALL, REFERENCED, SELECT, WHERE.

Enum values:

-   ALL
    
-   REFERENCED
    
-   SELECT
    
-   WHERE
    





 |  | NotifyForFieldsEnum |
| **notifyForOperationCreate** (common) | Notify for create operation, defaults to false (API version >= 29.0). | false | Boolean |
| **notifyForOperationDelete** (common) | Notify for delete operation, defaults to false (API version >= 29.0). | false | Boolean |
| **notifyForOperations** (common) | 

Notify for operations, options are ALL, CREATE, EXTENDED, UPDATE (API version < 29.0).

Enum values:

-   ALL
    
-   CREATE
    
-   EXTENDED
    
-   UPDATE
    





 |  | NotifyForOperationsEnum |
| **notifyForOperationUndelete** (common) | Notify for un-delete operation, defaults to false (API version >= 29.0). | false | Boolean |
| **notifyForOperationUpdate** (common) | Notify for update operation, defaults to false (API version >= 29.0). | false | Boolean |
| **objectMapper** (common) | Custom Jackson ObjectMapper to use when serializing/deserializing Salesforce objects. |  | ObjectMapper |
| **packages** (common) | In what packages are the generated DTO classes. Typically the classes would be generated using camel-salesforce-maven-plugin. Set it if using the generated DTOs to gain the benefit of using short SObject names in parameters/header values. Multiple packages can be separated by comma. |  | String |
| **pkChunking** (common) | Use PK Chunking. Only for use in original Bulk API. Bulk 2.0 API performs PK chunking automatically, if necessary. | false | Boolean |
| **pkChunkingChunkSize** (common) | Chunk size for use with PK Chunking. If unspecified, salesforce default is 100,000. Maximum size is 250,000. |  | Integer |
| **pkChunkingParent** (common) | Specifies the parent object when you’re enabling PK chunking for queries on sharing objects. The chunks are based on the parent object’s records rather than the sharing object’s records. For example, when querying on AccountShare, specify Account as the parent object. PK chunking is supported for sharing objects as long as the parent object is supported. |  | String |
| **pkChunkingStartRow** (common) | Specifies the 15-character or 18-character record ID to be used as the lower boundary for the first chunk. Use this parameter to specify a starting ID when restarting a job that failed between batches. |  | String |
| **queryLocator** (common) | Query Locator provided by salesforce for use when a query results in more records than can be retrieved in a single call. Use this value in a subsequent call to retrieve additional records. |  | String |
| **rawPayload** (common) | Use raw payload String for request and response (either JSON or XML depending on format), instead of DTOs, false by default. | false | boolean |
| **reportId** (common) | Salesforce1 Analytics report Id. |  | String |
| **reportMetadata** (common) | Salesforce1 Analytics report metadata for filtering. |  | ReportMetadata |
| **resultId** (common) | Bulk API Result ID. |  | String |
| **sObjectBlobFieldName** (common) | SObject blob field name. |  | String |
| **sObjectClass** (common) | Fully qualified SObject class name, usually generated using camel-salesforce-maven-plugin. |  | String |
| **sObjectFields** (common) | SObject fields to retrieve. |  | String |
| **sObjectId** (common) | SObject ID if required by API. |  | String |
| **sObjectIdName** (common) | SObject external ID field name. |  | String |
| **sObjectIdValue** (common) | SObject external ID field value. |  | String |
| **sObjectName** (common) | SObject name if required or supported by API. |  | String |
| **sObjectQuery** (common) | Salesforce SOQL query string. |  | String |
| **sObjectSearch** (common) | Salesforce SOSL search string. |  | String |
| **streamQueryResult** (common) | If true, streams SOQL query result and transparently handles subsequent requests if there are multiple pages. Otherwise, results are returned one page at a time. | false | Boolean |
| **updateTopic** (common) | Whether to update an existing Push Topic when using the Streaming API, defaults to false. | false | boolean |
| **config** (common (advanced)) | Global endpoint configuration - use to set values that are common to all endpoints. |  | SalesforceEndpointConfig |
| **httpClientProperties** (common (advanced)) | Used to set any properties that can be configured on the underlying HTTP client. Have a look at properties of SalesforceHttpClient and the Jetty HttpClient for all available options. |  | Map |
| **longPollingTransportProperties** (common (advanced)) | Used to set any properties that can be configured on the LongPollingTransport used by the BayeuxClient (CometD) used by the streaming api. |  | Map |
| **workerPoolMaxSize** (common (advanced)) | Maximum size of the thread pool used to handle HTTP responses. | 20 | int |
| **workerPoolSize** (common (advanced)) | Size of the thread pool used to handle HTTP responses. | 10 | int |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **fallbackToLatestReplayId** (consumer) | Whether the pub/sub consumer needs to fallback to the latest replay id when the provided id is not valid. If set to false, the component will keep retrying; in order to treat this as an exception you can use BridgeExceptionHandlerToErrorHandler and handle the exception in the route. | false | boolean |
| **pubSubBatchSize** (consumer) | Max number of events to receive in a batch from the Pub/Sub API. | 100 | int |
| **pubSubDeserializeType** (consumer) | 

How to deserialize events consume from the Pub/Sub API. AVRO will try a SpecificRecord subclass if found, otherwise GenericRecord.

Enum values:

-   AVRO
    
-   SPECIFIC\_RECORD
    
-   GENERIC\_RECORD
    
-   POJO
    
-   JSON
    





 | AVRO | PubSubDeserializeType |
| **pubSubPojoClass** (consumer) | Fully qualified class name to deserialize Pub/Sub API event to. |  | String |
| **replayPreset** (consumer) | 

Replay preset for Pub/Sub API.

Enum values:

-   LATEST
    
-   EARLIEST
    
-   CUSTOM
    





 | LATEST | ReplayPreset |
| **consumerWorkerPoolEnabled** (consumer (advanced)) | Use thread pool for processing received Salesforce events, for example to process events in parallel. | false | boolean |
| **consumerWorkerPoolExecutorService** (consumer (advanced)) | To use a custom thread pool for processing received Salesforce events, for example to process events in parallel. |  | ExecutorService |
| **consumerWorkerPoolMaxSize** (consumer (advanced)) | Maximum thread pool size size for consumer worker pool. | 20 | int |
| **consumerWorkerPoolSize** (consumer (advanced)) | Core thread pool size size for consumer worker pool. | 10 | int |
| **initialReplyIdTimeout** (consumer (advanced)) | Timeout in seconds to validate when a custom pubSubReplayId has been configured, when starting the Camel Salesforce consumer. | 30 | int |
| **allOrNone** (producer) | Composite API option to indicate to rollback all records if any are not successful. | false | boolean |
| **apexUrl** (producer) | APEX method URL. |  | String |
| **compositeMethod** (producer) | Composite (raw) method. |  | String |
| **eventName** (producer) | Name of Platform Event, Change Data Capture Event, custom event, etc. |  | String |
| **eventSchemaFormat** (producer) | 

EXPANDED: Apache Avro format but doesn’t strictly adhere to the record complex type. COMPACT: Apache Avro, adheres to the specification for the record complex type. This parameter is available in API version 43.0 and later.

Enum values:

-   EXPANDED
    
-   COMPACT
    





 |  | EventSchemaFormatEnum |
| **eventSchemaId** (producer) | The ID of the event schema. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **rawHttpHeaders** (producer) | Comma separated list of message headers to include as HTTP parameters for Raw operation. |  | String |
| **rawMethod** (producer) | HTTP method to use for the Raw operation. |  | String |
| **rawPath** (producer) | The portion of the endpoint URL after the domain name. E.g., '/services/data/v52.0/sobjects/Account/'. |  | String |
| **rawQueryParameters** (producer) | Comma separated list of message headers to include as query parameters for Raw operation. Do not url-encode values as this will be done automatically. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **httpProxyExcludedAddresses** (proxy) | A list of addresses for which HTTP proxy server should not be used. |  | Set |
| **httpProxyHost** (proxy) | Hostname of the HTTP proxy server to use. |  | String |
| **httpProxyIncludedAddresses** (proxy) | A list of addresses for which HTTP proxy server should be used. |  | Set |
| **httpProxyPort** (proxy) | Port number of the HTTP proxy server to use. |  | Integer |
| **httpProxySocks4** (proxy) | If set to true the configures the HTTP proxy to use as a SOCKS4 proxy. | false | boolean |
| **pubsubAllowUseSystemProxy** (proxy) | Allow the Pub/Sub API client to use the proxy detected by java.net.ProxySelector. If false then no proxy server will be used. | true | boolean |
| **authenticationType** (security) | 

Explicit authentication method to be used, one of USERNAME\_PASSWORD, REFRESH\_TOKEN, CLIENT\_CREDENTIALS, or JWT. Salesforce component can auto-determine the authentication method to use from the properties set, set this property to eliminate any ambiguity.

Enum values:

-   USERNAME\_PASSWORD
    
-   REFRESH\_TOKEN
    
-   CLIENT\_CREDENTIALS
    
-   JWT
    





 |  | AuthenticationType |
| **clientId** (security) | **Required** OAuth Consumer Key of the connected app configured in the Salesforce instance setup. Typically a connected app needs to be configured but one can be provided by installing a package. |  | String |
| **clientSecret** (security) | OAuth Consumer Secret of the connected app configured in the Salesforce instance setup. |  | String |
| **httpProxyAuthUri** (security) | Used in authentication against the HTTP proxy server, needs to match the URI of the proxy server in order for the httpProxyUsername and httpProxyPassword to be used for authentication. |  | String |
| **httpProxyPassword** (security) | Password to use to authenticate against the HTTP proxy server. |  | String |
| **httpProxyRealm** (security) | Realm of the proxy server, used in preemptive Basic/Digest authentication methods against the HTTP proxy server. |  | String |
| **httpProxySecure** (security) | If set to false disables the use of TLS when accessing the HTTP proxy. | true | boolean |
| **httpProxyUseDigestAuth** (security) | If set to true Digest authentication will be used when authenticating to the HTTP proxy, otherwise Basic authorization method will be used. | false | boolean |
| **httpProxyUsername** (security) | Username to use to authenticate against the HTTP proxy server. |  | String |
| **instanceUrl** (security) | URL of the Salesforce instance used after authentication, by default received from Salesforce on successful authentication. |  | String |
| **jwtAudience** (security) | Value to use for the Audience claim (aud) when using OAuth JWT flow. If not set, the login URL will be used, which is appropriate in most cases. |  | String |
| **keystore** (security) | KeyStore parameters to use in OAuth JWT flow. The KeyStore should contain only one entry with private key and certificate. Salesforce does not verify the certificate chain, so this can easily be a selfsigned certificate. Make sure that you upload the certificate to the corresponding connected app. |  | KeyStoreParameters |
| **lazyLogin** (security) | If set to true prevents the component from authenticating to Salesforce with the start of the component. You would generally set this to the (default) false and authenticate early and be immediately aware of any authentication issues. Lazy login is not supported by salesforce consumers. | false | boolean |
| **loginConfig** (security) | All authentication configuration in one nested bean, all properties set there can be set directly on the component as well. |  | SalesforceLoginConfig |
| **loginUrl** (security) | **Required** URL of the Salesforce instance used for authentication, by default set to [https://login.salesforce.com](https://login.salesforce.com). | [https://login.salesforce.com](https://login.salesforce.com) | String |
| **password** (security) | Password used in OAuth flow to gain access to access token. It’s easy to get started with password OAuth flow, but in general one should avoid it as it is deemed less secure than other flows. Make sure that you append security token to the end of the password if using one. |  | String |
| **pubSubHost** (security) | Pub/Sub host. | api.pubsub.salesforce.com | String |
| **pubSubPort** (security) | Pub/Sub port. | 7443 | int |
| **refreshToken** (security) | Refresh token already obtained in the refresh token OAuth flow. One needs to setup a web application and configure a callback URL to receive the refresh token, or configure using the builtin callback at [https://login.salesforce.com/services/oauth2/success](https://login.salesforce.com/services/oauth2/success) or [https://test.salesforce.com/services/oauth2/success](https://test.salesforce.com/services/oauth2/success) and then retrive the refresh\_token from the URL at the end of the flow. Note that in development organizations Salesforce allows hosting the callback web application at localhost. |  | String |
| **sslContextParameters** (security) | SSL parameters to use, see SSLContextParameters class for all available options. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **userName** (security) | Username used in OAuth flow to gain access to access token. It’s easy to get started with password OAuth flow, but in general one should avoid it as it is deemed less secure than other flows. |  | String |

## Endpoint Options

The Salesforce endpoint is configured using URI syntax:

salesforce:operationName:topicName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operationName** (common) | 
**Required** The operation to use.

Enum values:

-   getVersions
    
-   getResources
    
-   getGlobalObjects
    
-   getBasicInfo
    
-   getDescription
    
-   getSObject
    
-   createSObject
    
-   updateSObject
    
-   deleteSObject
    
-   getSObjectWithId
    
-   upsertSObject
    
-   deleteSObjectWithId
    
-   getBlobField
    
-   query
    
-   queryMore
    
-   queryAll
    
-   search
    
-   apexCall
    
-   recent
    
-   getEventSchema
    
-   createJob
    
-   getJob
    
-   closeJob
    
-   abortJob
    
-   createBatch
    
-   getBatch
    
-   getAllBatches
    
-   getRequest
    
-   getResults
    
-   createBatchQuery
    
-   getQueryResultIds
    
-   getQueryResult
    
-   getRecentReports
    
-   getReportDescription
    
-   executeSyncReport
    
-   executeAsyncReport
    
-   getReportInstances
    
-   getReportResults
    
-   limits
    
-   approval
    
-   approvals
    
-   composite-tree
    
-   composite-batch
    
-   composite
    
-   compositeRetrieveSObjectCollections
    
-   compositeCreateSObjectCollections
    
-   compositeUpdateSObjectCollections
    
-   compositeUpsertSObjectCollections
    
-   compositeDeleteSObjectCollections
    
-   bulk2GetAllJobs
    
-   bulk2CreateJob
    
-   bulk2GetJob
    
-   bulk2CreateBatch
    
-   bulk2CloseJob
    
-   bulk2AbortJob
    
-   bulk2DeleteJob
    
-   bulk2GetSuccessfulResults
    
-   bulk2GetFailedResults
    
-   bulk2GetUnprocessedRecords
    
-   bulk2CreateQueryJob
    
-   bulk2GetQueryJob
    
-   bulk2GetAllQueryJobs
    
-   bulk2GetQueryJobResults
    
-   bulk2AbortQueryJob
    
-   bulk2DeleteQueryJob
    
-   raw
    
-   subscribe
    
-   pubSubSubscribe
    
-   pubSubPublish
    





 |  | OperationName |
| **topicName** (producer) | The name of the topic/channel to use. |  | String |

### Query Parameters (71 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apexMethod** (common) | APEX method name. |  | String |
| **apexQueryParams** (common) | Query params for APEX method. |  | Map |
| **apiVersion** (common) | Salesforce API version. | 56.0 | String |
| **backoffIncrement** (common) | Backoff interval increment for Streaming connection restart attempts for failures beyond CometD auto-reconnect. | 1000 | long |
| **batchId** (common) | Bulk API Batch ID. |  | String |
| **contentType** (common) | 
Bulk API content type, one of XML, CSV, ZIP\_XML, ZIP\_CSV.

Enum values:

-   XML
    
-   CSV
    
-   JSON
    
-   ZIP\_XML
    
-   ZIP\_CSV
    
-   ZIP\_JSON
    





 |  | ContentType |
| **defaultReplayId** (common) | Default replayId setting if no value is found in initialReplayIdMap. | \-1 | Long |
| **fallBackReplayId** (common) | ReplayId to fall back to after an Invalid Replay Id response. | \-1 | Long |
| **format** (common) | 

Payload format to use for Salesforce API calls, either JSON or XML, defaults to JSON. As of Camel 3.12, this option only applies to the Raw operation.

Enum values:

-   JSON
    
-   XML
    





 |  | PayloadFormat |
| **httpClient** (common) | Custom Jetty Http Client to use to connect to Salesforce. |  | SalesforceHttpClient |
| **includeDetails** (common) | Include details in Salesforce1 Analytics report, defaults to false. | false | Boolean |
| **initialReplayIdMap** (common) | Replay IDs to start from per channel name. |  | Map |
| **instanceId** (common) | Salesforce1 Analytics report execution instance ID. |  | String |
| **jobId** (common) | Bulk API Job ID. |  | String |
| **limit** (common) | Limit on number of returned records. Applicable to some of the API, check the Salesforce documentation. |  | Integer |
| **locator** (common) | Locator provided by salesforce Bulk 2.0 API for use in getting results for a Query job. |  | String |
| **maxBackoff** (common) | Maximum backoff interval for Streaming connection restart attempts for failures beyond CometD auto-reconnect. | 30000 | long |
| **maxRecords** (common) | The maximum number of records to retrieve per set of results for a Bulk 2.0 Query. The request is still subject to the size limits. If you are working with a very large number of query results, you may experience a timeout before receiving all the data from Salesforce. To prevent a timeout, specify the maximum number of records your client is expecting to receive in the maxRecords parameter. This splits the results into smaller sets with this value as the maximum size. |  | Integer |
| **notFoundBehaviour** (common) | 

Sets the behaviour of 404 not found status received from Salesforce API. Should the body be set to NULL NotFoundBehaviour#NULL or should a exception be signaled on the exchange NotFoundBehaviour#EXCEPTION - the default.

Enum values:

-   EXCEPTION
    
-   NULL
    





 | EXCEPTION | NotFoundBehaviour |
| **notifyForFields** (common) | 

Notify for fields, options are ALL, REFERENCED, SELECT, WHERE.

Enum values:

-   ALL
    
-   REFERENCED
    
-   SELECT
    
-   WHERE
    





 |  | NotifyForFieldsEnum |
| **notifyForOperationCreate** (common) | Notify for create operation, defaults to false (API version >= 29.0). | false | Boolean |
| **notifyForOperationDelete** (common) | Notify for delete operation, defaults to false (API version >= 29.0). | false | Boolean |
| **notifyForOperations** (common) | 

Notify for operations, options are ALL, CREATE, EXTENDED, UPDATE (API version < 29.0).

Enum values:

-   ALL
    
-   CREATE
    
-   EXTENDED
    
-   UPDATE
    





 |  | NotifyForOperationsEnum |
| **notifyForOperationUndelete** (common) | Notify for un-delete operation, defaults to false (API version >= 29.0). | false | Boolean |
| **notifyForOperationUpdate** (common) | Notify for update operation, defaults to false (API version >= 29.0). | false | Boolean |
| **objectMapper** (common) | Custom Jackson ObjectMapper to use when serializing/deserializing Salesforce objects. |  | ObjectMapper |
| **pkChunking** (common) | Use PK Chunking. Only for use in original Bulk API. Bulk 2.0 API performs PK chunking automatically, if necessary. | false | Boolean |
| **pkChunkingChunkSize** (common) | Chunk size for use with PK Chunking. If unspecified, salesforce default is 100,000. Maximum size is 250,000. |  | Integer |
| **pkChunkingParent** (common) | Specifies the parent object when you’re enabling PK chunking for queries on sharing objects. The chunks are based on the parent object’s records rather than the sharing object’s records. For example, when querying on AccountShare, specify Account as the parent object. PK chunking is supported for sharing objects as long as the parent object is supported. |  | String |
| **pkChunkingStartRow** (common) | Specifies the 15-character or 18-character record ID to be used as the lower boundary for the first chunk. Use this parameter to specify a starting ID when restarting a job that failed between batches. |  | String |
| **queryLocator** (common) | Query Locator provided by salesforce for use when a query results in more records than can be retrieved in a single call. Use this value in a subsequent call to retrieve additional records. |  | String |
| **rawPayload** (common) | Use raw payload String for request and response (either JSON or XML depending on format), instead of DTOs, false by default. | false | boolean |
| **reportId** (common) | Salesforce1 Analytics report Id. |  | String |
| **reportMetadata** (common) | Salesforce1 Analytics report metadata for filtering. |  | ReportMetadata |
| **resultId** (common) | Bulk API Result ID. |  | String |
| **sObjectBlobFieldName** (common) | SObject blob field name. |  | String |
| **sObjectClass** (common) | Fully qualified SObject class name, usually generated using camel-salesforce-maven-plugin. |  | String |
| **sObjectFields** (common) | SObject fields to retrieve. |  | String |
| **sObjectId** (common) | SObject ID if required by API. |  | String |
| **sObjectIdName** (common) | SObject external ID field name. |  | String |
| **sObjectIdValue** (common) | SObject external ID field value. |  | String |
| **sObjectName** (common) | SObject name if required or supported by API. |  | String |
| **sObjectQuery** (common) | Salesforce SOQL query string. |  | String |
| **sObjectSearch** (common) | Salesforce SOSL search string. |  | String |
| **streamQueryResult** (common) | If true, streams SOQL query result and transparently handles subsequent requests if there are multiple pages. Otherwise, results are returned one page at a time. | false | Boolean |
| **updateTopic** (common) | Whether to update an existing Push Topic when using the Streaming API, defaults to false. | false | boolean |
| **fallbackToLatestReplayId** (consumer) | Whether the pub/sub consumer needs to fallback to the latest replay id when the provided id is not valid. If set to false, the component will keep retrying; in order to treat this as an exception you can use BridgeExceptionHandlerToErrorHandler and handle the exception in the route. | false | boolean |
| **pubSubBatchSize** (consumer) | Max number of events to receive in a batch from the Pub/Sub API. | 100 | int |
| **pubSubDeserializeType** (consumer) | 

How to deserialize events consume from the Pub/Sub API. AVRO will try a SpecificRecord subclass if found, otherwise GenericRecord.

Enum values:

-   AVRO
    
-   SPECIFIC\_RECORD
    
-   GENERIC\_RECORD
    
-   POJO
    
-   JSON
    





 | AVRO | PubSubDeserializeType |
| **pubSubPojoClass** (consumer) | Fully qualified class name to deserialize Pub/Sub API event to. |  | String |
| **pubSubReplayId** (consumer) | The replayId value to use when subscribing to the Pub/Sub API. |  | String |
| **replayId** (consumer) | The replayId value to use when subscribing to the Streaming API. |  | Long |
| **replayPreset** (consumer) | 

Replay preset for Pub/Sub API.

Enum values:

-   LATEST
    
-   EARLIEST
    
-   CUSTOM
    





 | LATEST | ReplayPreset |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerWorkerPoolEnabled** (consumer (advanced)) | Use thread pool for processing received Salesforce events, for example to process events in parallel. | false | boolean |
| **consumerWorkerPoolExecutorService** (consumer (advanced)) | To use a custom thread pool for processing received Salesforce events, for example to process events in parallel. |  | ExecutorService |
| **consumerWorkerPoolMaxSize** (consumer (advanced)) | Maximum thread pool size size for consumer worker pool. | 20 | int |
| **consumerWorkerPoolSize** (consumer (advanced)) | Core thread pool size size for consumer worker pool. | 10 | int |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **allOrNone** (producer) | Composite API option to indicate to rollback all records if any are not successful. | false | boolean |
| **apexUrl** (producer) | APEX method URL. |  | String |
| **compositeMethod** (producer) | Composite (raw) method. |  | String |
| **eventName** (producer) | Name of Platform Event, Change Data Capture Event, custom event, etc. |  | String |
| **eventSchemaFormat** (producer) | 

EXPANDED: Apache Avro format but doesn’t strictly adhere to the record complex type. COMPACT: Apache Avro, adheres to the specification for the record complex type. This parameter is available in API version 43.0 and later.

Enum values:

-   EXPANDED
    
-   COMPACT
    





 |  | EventSchemaFormatEnum |
| **eventSchemaId** (producer) | The ID of the event schema. |  | String |
| **rawHttpHeaders** (producer) | Comma separated list of message headers to include as HTTP parameters for Raw operation. |  | String |
| **rawMethod** (producer) | HTTP method to use for the Raw operation. |  | String |
| **rawPath** (producer) | The portion of the endpoint URL after the domain name. E.g., '/services/data/v52.0/sobjects/Account/'. |  | String |
| **rawQueryParameters** (producer) | Comma separated list of message headers to include as query parameters for Raw operation. Do not url-encode values as this will be done automatically. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Salesforce component supports 22 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSalesforceReplayId** (consumer) Constant: [`HEADER_SALESFORCE_REPLAY_ID`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_REPLAY_ID) | The Streaming API replayId. |  | Object |
| **CamelSalesforceChangeEventSchema** (consumer) Constant: [`HEADER_SALESFORCE_CHANGE_EVENT_SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_CHANGE_EVENT_SCHEMA) | The change event schema. |  | Object |
| **CamelSalesforceEventType** (consumer) Constant: [`HEADER_SALESFORCE_EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_EVENT_TYPE) | The event type. |  | String |
| **CamelSalesforceCommitTimestamp** (consumer) Constant: [`HEADER_SALESFORCE_COMMIT_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_COMMIT_TIMESTAMP) | The commit timestamp. |  | Object |
| **CamelSalesforceCommitUser** (consumer) Constant: [`HEADER_SALESFORCE_COMMIT_USER`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_COMMIT_USER) | The commit user. |  | Object |
| **CamelSalesforceCommitNumber** (consumer) Constant: [`HEADER_SALESFORCE_COMMIT_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_COMMIT_NUMBER) | The commit number. |  | Object |
| **CamelSalesforceRecordIds** (consumer) Constant: [`HEADER_SALESFORCE_RECORD_IDS`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_RECORD_IDS) | The record ids. |  | Object |
| **CamelSalesforceChangeType** (consumer) Constant: [`HEADER_SALESFORCE_CHANGE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_CHANGE_TYPE) | The change type. |  | Object |
| **CamelSalesforceChangeOrigin** (consumer) Constant: [`HEADER_SALESFORCE_CHANGE_ORIGIN`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_CHANGE_ORIGIN) | The change origin. |  | Object |
| **CamelSalesforceTransactionKey** (consumer) Constant: [`HEADER_SALESFORCE_TRANSACTION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_TRANSACTION_KEY) | The transaction key. |  | Object |
| **CamelSalesforceSequenceNumber** (consumer) Constant: [`HEADER_SALESFORCE_SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_SEQUENCE_NUMBER) | The sequence number. |  | Object |
| **CamelSalesforceIsTransactionEnd** (consumer) Constant: [`HEADER_SALESFORCE_IS_TRANSACTION_END`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_IS_TRANSACTION_END) | Is transaction end. |  | Object |
| **CamelSalesforceEntityName** (consumer) Constant: [`HEADER_SALESFORCE_ENTITY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_ENTITY_NAME) | The entity name. |  | Object |
| **CamelSalesforcePlatformEventSchema** (consumer) Constant: [`HEADER_SALESFORCE_PLATFORM_EVENT_SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_PLATFORM_EVENT_SCHEMA) | The platform event schema. |  | Object |
| **CamelSalesforceCreatedDate** (consumer) Constant: [`HEADER_SALESFORCE_CREATED_DATE`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_CREATED_DATE) | The created date. |  | ZonedDateTime |
| **CamelSalesforceTopicName** (consumer) Constant: [`HEADER_SALESFORCE_TOPIC_NAME`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_TOPIC_NAME) | The topic name. |  | String |
| **CamelSalesforceChannel** (consumer) Constant: [`HEADER_SALESFORCE_CHANNEL`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_CHANNEL) | The channel. |  | String |
| **CamelSalesforceClientId** (consumer) Constant: [`HEADER_SALESFORCE_CLIENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_CLIENT_ID) | The client id. |  | String |
| **CamelSalesforcePubSubReplayId** (consumer) Constant: [`HEADER_SALESFORCE_PUBSUB_REPLAY_ID`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_PUBSUB_REPLAY_ID) | The Pub/Sub API replayId. |  | String |
| **CamelSalesforcePubSubEventId** (consumer) Constant: [`HEADER_SALESFORCE_PUBSUB_EVENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_PUBSUB_EVENT_ID) | The Pub/Sub API event id. |  | String |
| **CamelSalesforcePubSubRpcId** (consumer) Constant: [`HEADER_SALESFORCE_PUBSUB_RPC_ID`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_PUBSUB_RPC_ID) | The Pub/Sub API rpc id. |  | String |
| **CamelSalesforceQueryResultTotalSize** (producer) Constant: [`HEADER_SALESFORCE_QUERY_RESULT_TOTAL_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_QUERY_RESULT_TOTAL_SIZE) | Total number of records matching a query. |  | int |

## Usage

### Authenticating to Salesforce

The component supports four OAuth authentication flows:

-   [OAuth 2.0 Username-Password Flow](https://help.salesforce.com/articleView?id=remoteaccess_oauth_username_password_flow.htm)
    
-   [OAuth 2.0 Refresh Token Flow](https://help.salesforce.com/articleView?id=remoteaccess_oauth_refresh_token_flow.htm)
    
-   [OAuth 2.0 JWT Bearer Token Flow](https://help.salesforce.com/articleView?id=remoteaccess_oauth_jwt_flow.htm)
    
-   [OAuth 2.0 Client Credentials Flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_client_credentials_flow.htm)
    

For each of the flows, different sets of properties need to be set:

Table 1. Properties to set for each authentication flow   
| Property | Where to find it on Salesforce | Flow |
| --- | --- | --- |
| `clientId` | Connected App, Consumer Key | All flows |
| `clientSecret` | Connected App, Consumer Secret | Username-Password, Refresh Token, Client Credentials |
| `userName` | Salesforce user username | Username-Password, JWT Bearer Token |
| `password` | Salesforce user password | Username-Password |
| `refreshToken` | From OAuth flow callback | Refresh Token |
| `keystore` | Connected App, Digital Certificate | JWT Bearer Token |

The component auto determines what flow you’re trying to configure. In order to be explicit, set the `authenticationType` property.

> **Note**
> Using Username-Password Flow in production is not encouraged.

> **Note**
> The certificate used in JWT Bearer Token Flow can be a self-signed certificate. The KeyStore holding the certificate and the private key must contain only a single certificate-private key entry.

### General Usage

#### URI format

When used as a consumer, receiving streaming events, the URI scheme is:

salesforce:subscribe:topic?options

When used as a producer, invoking the Salesforce REST APIs, the URI scheme is:

salesforce:operationName?options

As a general example on using the operations in this salesforce component, the following producer endpoint uses the upsertSObject API, with the sObjectIdName parameter specifying 'Name' as the external id field. The request message body should be an SObject DTO generated using the maven plugin.

```java
...to("salesforce:upsertSObject?sObjectIdName=Name")...
```

### Passing in Salesforce headers and fetching Salesforce response headers

There is support to pass [Salesforce headers](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/headers.htm) via inbound message headers, header names that start with `Sforce` or `x-sfdc` on the Camel message will be passed on in the request, and response headers that start with `Sforce` will be present in the outbound message headers.

For example, to fetch API limits, you can specify:

```java
// in your Camel route set the header before Salesforce endpoint
//...
  .setHeader("Sforce-Limit-Info", constant("api-usage"))
  .to("salesforce:getGlobalObjects")
  .to(myProcessor);

// myProcessor will receive `Sforce-Limit-Info` header on the outbound
// message
class MyProcessor implements Processor {
    public void process(Exchange exchange) throws Exception {
        Message in = exchange.getIn();
        String apiLimits = in.getHeader("Sforce-Limit-Info", String.class);
   }
}
```

In addition, HTTP response status code and text are available as headers `Exchange.HTTP_RESPONSE_CODE` and `Exchange.HTTP_RESPONSE_TEXT`.

#### Sending null values to salesforce

By default, SObject fields with null values are not sent to salesforce. In order to send null values to salesforce, use the `fieldsToNull` property, as follows:

```java
accountSObject.getFieldsToNull().add("Site");
```

### Supported Salesforce APIs

Camel supports the following Salesforce APIs:

-   [REST API](#RESTAPI)
    
-   [Apex REST API](#ApexRESTAPI)
    
-   [Bulk 2 API](#Bulk2API)
    
-   [Bulk API](#BulkAPI)
    
-   [Pub/Sub API](#PubSubAPI)
    
-   [Streaming API](#StreamingAPI)
    
-   [Reports API](#ReportsAPI)
    

#### REST API

The following operations are supported:

-   [getVersions](#getVersions) - Gets supported Salesforce REST API versions.
    
-   [getResources](#getResources) - Gets available Salesforce REST Resource endpoints.
    
-   [limits](#limits) - Lists information about limits in your org.
    
-   [recent](#recent) - Gets the most recently accessed items that were viewed or referenced by the current user.
    
-   [getGlobalObjects](#getGlobalObjects) - Gets metadata for all available SObject types.
    
-   [getBasicInfo](#getBasicInfo) - Gets basic metadata for a specific SObject type.
    
-   [getDescription](#getDescription) - Gets comprehensive metadata for a specific SObject type.
    
-   [getSObject](#getSObject) - Gets an SObject.
    
-   [getSObjectWithId](#getSObjectWithId) - Gets an SObject using an External Id (user defined) field.
    
-   [getBlobField](#getSObjectWithId) - Retrieves the specified blob field from an individual record.
    
-   [createSObject](#createSObject) - Creates an SObject.
    
-   [updateSObject](#updateSObject) - Updates an SObject.
    
-   [deleteSObject](#deleteSObject) - Deletes an SObject.
    
-   [upsertSObject](#upsertSObject) - Inserts or updates an SObject using an External Id.
    
-   [deleteSObjectWithId](#deleteSObjectWithId) - Deletes an SObject using an External Id.
    
-   [query](#query) - Runs a Salesforce SOQL query.
    
-   [queryMore](#queryMore) - Retrieves more results (in case of a large number of results) using the result link returned from the 'query' API.
    
-   [queryAll](#queryAll) - Runs a SOQL query. Unlike the query operation, queryAll returns records that are deleted because of a merge or delete. queryAll also returns information about archived task and event records.
    
-   [search](#sosl_search) - Runs a Salesforce SOSL query.
    
-   [apexCall](#apexCall) - Executes a user defined APEX REST API call.
    
-   [approval](#approval) - Submits a record or records (batch) for approval process.
    
-   [approvals](#approvals) - Fetches a list of all approval processes.
    
-   [composite](#composite) - Executes up to 25 REST API requests in a single call. You can use the output of one request as the input to a subsequent request.
    
-   [composite-tree](#composite-tree) - Creates up to 200 records with parent-child relationships (up to 5 levels) in one go.
    
-   [composite-batch](#composite-batch) - Executes up to 25 sub-requests in a single request.
    
-   [compositeRetrieveSObjectCollections](#compositeRetrieveSObjectCollections) - Retrieves one or more records of the same object type.
    
-   [compositeCreateSObjectCollections](#compositeCreateSObjectCollections) - Creates up to 200 records.
    
-   [compositeUpdateSObjectCollections](#compositeUpdateSObjectCollections) - Update up to 200 records.
    
-   [compositeUpsertSObjectCollections](#compositeUpsertSObjectCollections) - Creates or updates up to 200 records based on an External Id field.
    
-   [compositeDeleteSObjectCollections](#compositeDeleteSObjectCollections) - Deletes up to 200 records.
    
-   [getEventSchema](#getEventSchema) - Gets the event schema for Platform Events, Change Data Capture events, etc.
    

Unless otherwise specified, DTO types for the following options are from `org.apache.camel.component.salesforce.api.dto` or one if its sub-packages.

##### Versions

`getVersions`

Lists summary information about each Salesforce version currently available, including the version, label, and a link to each version’s root.

**Output**

Type: `List<Version>`

##### Resources by Version

`getResources`

Lists available resources for the current API version, including resource name and URI.

**Output**

Type: `Map<String, String>`

##### Limits

`limits`

Lists information about limits in your org. For each limit, this resource returns the maximum allocation and the remaining allocation based on usage.

**Output**

Type: `Limits`

**Additional Usage Information**

With `salesforce:limits` operation you can fetch of API limits from Salesforce and then act upon that data received. The result of `salesforce:limits` operation is mapped to `org.apache.camel.component.salesforce.api.dto.Limits` class and can be used in a custom processors or expressions.

For instance, consider that you need to limit the API usage of Salesforce so that 10% of daily API requests is left for other routes. The body of output message contains an instance of `org.apache.camel.component.salesforce.api.dto.Limits` object that can be used in conjunction with Content Based Router and Content Based Router and [Spring Expression Language (SpEL)](languages/spel-language.md) to choose when to perform queries.

Notice how multiplying `1.0` with the integer value held in `body.dailyApiRequests.remaining` makes the expression evaluate as with floating point arithmetic, without it - it would end up making integral division which would result with either `0` (some API limits consumed) or `1` (no API limits consumed).

```java
from("direct:querySalesforce")
    .to("salesforce:limits")
    .choice()
    .when(spel("#{1.0 * body.dailyApiRequests.remaining / body.dailyApiRequests.max < 0.1}"))
        .to("salesforce:query?...")
    .otherwise()
        .setBody(constant("Used up Salesforce API limits, leaving 10% for critical routes"))
    .endChoice()
```

##### Recently Viewed Items

`recent`

Gets the most recently accessed items that were viewed or referenced by the current user. Salesforce stores information about record views in the interface and uses it to generate a list of recently viewed and referenced records, such as in the sidebar and for the auto-complete options in search.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `limit` | `int` | An optional limit that specifies the maximum number of records to be returned. If this parameter is not specified, the default maximum number of records returned is the maximum number of entries in RecentlyViewed, which is 200 records per object. |  |  |

**Output**

Type: `List<RecentItem>`

**Additional Usage Information**

To fetch the recent items use `salesforce:recent` operation. This operation returns an `java.util.List` of `org.apache.camel.component.salesforce.api.dto.RecentItem` objects (`List<RecentItem>`) that in turn contain the `Id`, `Name` and `Attributes` (with `type` and `url` properties). You can limit the number of returned items by specifying `limit` parameter set to maximum number of records to return. For example:

```java
from("direct:fetchRecentItems")
    to("salesforce:recent")
        .split().body()
            .log("${body.name} at ${body.attributes.url}");
```

##### Describe Global

`getGlobalObjects`

Lists the available objects and their metadata for your organization’s data. In addition, it provides the organization encoding, as well as the maximum batch size permitted in queries.

**Output**

Type: `GlobalObjects`

##### sObject Basic Information

`getBasicInfo`

Describes the individual metadata for the specified object.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `sObjectName` | `String` | Name of SObject, e.g. `Account`. Alternatively, can be supplied in Body. |  | x |

**Output**

Type: `SObjectBasicInfo`

##### sObject Describe

`getDescription`

Completely describes the individual metadata at all levels for the specified object. For example, this can be used to retrieve the fields, URLs, and child relationships for the Account object.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `sObjectName` | `String` | Name of SObject, e.g. `Account`. Alternatively, can be supplied in Body. |  | x |

**Output**

Type: `SObjectDescription`

##### Retrieve SObject

`getSObject`

Accesses record based on the specified object ID. This operation requires the `packages` option to be set.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `sObjectName` | `String` | Name of SObject, e.g. `Account` |  | x |
| `sObjectId` | `String` | Id of record to retrieve. |  | x |
| `sObjectFields` | `String` | Comma-separated list of fields to retrieve |  |  |
| Body | `AbstractSObjectBase` | Instance of SObject that is used to query salesforce. If supplied, overrides `sObjectName` and `sObjectId` parameters. |  |  |

**Output**

Type: Subclass of `AbstractSObjectBase`

##### Retrieve SObject by External Id

`getSObjectWithId`

Accesses record based on an External ID value. This operation requires the `packages` option to be set.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `sObjectIdName` | `String` | Name of External ID field |  | x |
| `sObjectIdValue` | `String` | External ID value |  | x |
| `sObjectName` | `String` | Name of SObject, e.g. `Account` |  | x |
| Body | `AbstractSObjectBase` | Instance of SObject that is used to query salesforce. If supplied, overrides `sObjectName` and `sObjectIdValue` parameters. |  |  |

**Output**

Type: Subclass of `AbstractSObjectBase`

##### sObject Blob Retrieve

`getBlobField`

Retrieves the specified blob field from an individual record.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `sObjectBlobFieldName` | `String` | SOSL query |  | x |
| `sObjectName` | `String` | Name of SObject, e.g., Account |  | Required if SObject not supplied in body |
| `sObjectId` | `String` | Id of SObject |  | Required if SObject not supplied in body |
| Body | `AbstractSObjectBase` | SObject to determine type and Id from. If not supplied, `sObjectId` and `sObjectName` parameters will be used. |  | Required if `sObjectId` and `sObjectName` are not supplied |

**Output**

Type: `InputStream`

##### Create SObject

`createSObject`

Creates a record in salesforce.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `AbstractSObjectBase` or `String` | Instance of SObject to create. |  | x |
| `sObjectName` | `String` | Name of SObject, e.g. `Account`. Only used if Camel cannot determine from Body. |  | If Body is a `String` |

**Output**

Type: `CreateSObjectResult`

**Multipart Support**

When creating records with blob/binary fields, you can use the automatic [multipart encoding](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_insert_update_blob.htm) feature by populating binary fields in your DTO. See [Binary Fields and Multipart Requests](#BinaryFields) for details.

##### Update SObject

`updateSObject`

Updates a record in salesforce.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `AbstractSObjectBase` or `String` | Instance of SObject to update. |  | x |
| `sObjectName` | `String` | Name of SObject, e.g. `Account`. Only used if Camel cannot determine from Body. |  | If Body is a `String` |
| `sObjectId` | `String` | Id of record to update. Only used if Camel cannot determine from Body. |  | If Body is a `String` |

**Multipart Support**

When updating records with blob/binary fields, you can use the automatic [multipart encoding](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_insert_update_blob.htm) feature by populating binary fields in your DTO. See [Binary Fields and Multipart Requests](#BinaryFields) for details.

##### Upsert SObject

`upsertSObject`

Upserts a record by External ID.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `AbstractSObjectBase` or `String` | SObject to update. |  | x |
| `sObjectIdName` | `String` | External ID field name. |  | x |
| `sObjectIdValue` | `String` | External ID value |  | If Body is a `String` |
| `sObjectName` | `String` | Name of SObject, e.g. `Account`. Only used if Camel cannot determine from Body. |  | If Body is a `String` |

**Output**

Type: `UpsertSObjectResult`

##### Delete SObject

`deleteSObject`

Deletes a record in salesforce.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `AbstractSObjectBase` | Instance of SObject to delete. |  |  |
| `sObjectName` | `String` | Name of SObject, e.g. `Account`. Only used if Camel cannot determine from Body. |  | If Body is not an `AbstractSObjectBase` instance |
| `sObjectId` | `String` | Id of record to delete. |  | If Body is not an `AbstractSObjectBase` instance |

##### Delete SObject by External Id

`deleteSObjectWithId`

Deletes a record in salesforce by External ID.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `AbstractSObjectBase` | Instance of SObject to delete. |  |  |
| `sObjectIdName` | `String` | Name of External ID field |  | If Body is not an `AbstractSObjectBase` instance |
| `sObjectIdValue` | `String` | External ID value |  | If Body is not an `AbstractSObjectBase` instance |
| `sObjectName` | `String` | Name of SObject, e.g. `Account`. Only used if Camel cannot determine from Body. |  | If Body is not an `AbstractSObjectBase` instance |

##### Query

`query`

Runs a Salesforce SOQL query. If neither `sObjectClass` nor `sObjectName` are set, Camel will attempt to determine the correct `AbstractQueryRecordsBase` sublcass based on the response.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body or `sObjectQuery` | `String` | SOQL query |  | x |
| streamQueryResult | `Boolean` | If true, returns a streaming `Iterator` and transparently retrieves all pages as needed. The `sObjectClass` option must reference an `AbstractQueryRecordsBase` subclass. | false |  |
| `sObjectClass` | `String` | Fully qualified name of class to deserialize response to. Usually a subclass of `AbstractQueryRecordsBase`, e.g. `org.my.dto.QueryRecordsAccount` |  |  |
| `sObjectName` | `String` | Simple name of class to deserialize response to. Usually a subclass of `AbstractQueryRecordsBase`, e.g. `QueryRecordsAccount`. Requires the `package` option be set. |  |  |

**Output**

Type: Instance of class supplied in `sObjectClass`, or `Iterator<SomeSObject>` if `streamQueryResult` is true. If `streamQueryResult` is true, the header `CamelSalesforceQueryResultTotalSize` is set to the number of records that matched the query.

##### Query More

`queryMore`

Retrieves more results (in case of large number of results) using result link returned from the `query` and `queryAll` operations. If neither `sObjectClass` nor `sObjectName` are set, Camel will attempt to determine the correct `AbstractQueryRecordsBase` sublcass based on the response.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body or `sObjectQuery` | `String` | `nextRecords` value. Can be found in a prior query result in the `AbstractQueryRecordsBase.nextRecordsUrl` property |  | X |
| `sObjectClass` | `String` | Fully qualified name of class to deserialize response to. Usually a subclass of `AbstractQueryRecordsBase`, e.g. `org.my.dto.QueryRecordsAccount` |  |  |
| `sObjectName` | `String` | Simple name of class to deserialize response to. Usually a subclass of `AbstractQueryRecordsBase`, e.g. `QueryRecordsAccount`. Requires the `package` option be set. |  |  |

**Output**

Type: Instance of class supplied in `sObjectClass`

##### Query All

`queryAll`

Executes the specified SOQL query. Unlike the `query` operation , `queryAll` returns records that are deleted because of a merge or delete. It also returns information about archived task and event records. If neither `sObjectClass` nor `sObjectName` are set, Camel will attempt to determine the correct `AbstractQueryRecordsBase` sublcass based on the response.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body or `sObjectQuery` | `String` | SOQL query |  | x |
| streamQueryResult | `Boolean` | If true, returns a streaming `Iterable` and transparently retrieves all pages as needed. The `sObjectClass` option must reference an `AbstractQueryRecordsBase` subclass. | false |  |
| `sObjectClass` | `String` | Fully qualified name of class to deserialize response to. Usually a subclass of `AbstractQueryRecordsBase`, e.g. `org.my.dto.QueryRecordsAccount` |  |  |
| `sObjectName` | `String` | Simple name of class to deserialize response to. Usually a subclass of `AbstractQueryRecordsBase`, e.g. `QueryRecordsAccount`. Requires the `package` option be set. |  |  |

**Output**

Type: Instance of class supplied in `sObjectClass`, or `Iterator<SomeSObject>` if `streamQueryResult` is true.

##### Search

`search`

Runs a Salesforce SOSL search

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body or `sObjectSearch` | `String` | Name of field to retrieve |  | x |

**Output**

Type: `SearchResult2`

##### Submit Approval

`approval`

Submit a record or records (batch) for approval process.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `ApprovalRequest` or `List<ApprovalRequest>` | `ApprovalRequest`(s) to process |  |  |
| `Approval.` | Prefixed headers or endpoint options in lieu of passing an `ApprovalRequest` in the body. |  |  |  |

**Output**

Type: `ApprovalResult`

**Additional usage information**

All the properties are named exactly the same as in the Salesforce REST API prefixed with `approval.`. You can set approval properties by setting `approval.PropertyName` of the Endpoint these will be used as template — meaning that any property not present in either body or header will be taken from the Endpoint configuration. Or you can set the approval template on the Endpoint by assigning `approval` property to a reference onto a bean in the Registry.

You can also provide header values using the same `approval.PropertyName` in the incoming message headers.

And finally body can contain one `AprovalRequest` or an `Iterable` of `ApprovalRequest` objects to process as a batch.

The important thing to remember is the priority of the values specified in these three mechanisms:

1.  value in body takes precedence before any other
    
2.  value in message header takes precedence before template value
    
3.  value in template is set if no other value in header or body was given
    

For example, to send one record for approval using values in headers use:

Given a route:

```java
from("direct:example1")//
        .setHeader("approval.ContextId", simple("${body['contextId']}"))
        .setHeader("approval.NextApproverIds", simple("${body['nextApproverIds']}"))
        .to("salesforce:approval?"//
            + "approval.actionType=Submit"//
            + "&approval.comments=this is a test"//
            + "&approval.processDefinitionNameOrId=Test_Account_Process"//
            + "&approval.skipEntryCriteria=true");
```

You could send a record for approval using:

```java
final Map<String, String> body = new HashMap<>();
body.put("contextId", accountIds.iterator().next());
body.put("nextApproverIds", userId);

final ApprovalResult result = template.requestBody("direct:example1", body, ApprovalResult.class);
```

##### Get Approvals

`approvals`

Returns a list of all approval processes.

**Output**

Type: `Approvals`

##### Composite

`composite`

Executes up to 25 REST API requests in a single call. You can use the output of one request as the input to a subsequent request. The response bodies and HTTP statuses of the requests are returned in a single response body. The entire series of requests counts as a single call toward your API limits. Use Salesforce Composite API to submit multiple chained requests. Individual requests and responses are linked with the provided _reference_.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `SObjectComposite` | Contains REST API sub-requests to be executed. |  | x |
| `rawPayload` | `Boolean` | Any (un)marshaling of requests and responses are assumed to be handled by the route | false | x |
| `compositeMethod` | `String` | HTTP method to use for rawPayload requests. | `POST` |  |

**Output**

Type: `SObjectCompositeResponse`

> **Note**
> Composite API supports only JSON payloads.

> **Note**
> As with the batch API, the results can vary from API to API so the body of each `SObjectCompositeResult` instance is given as a `java.lang.Object`. In most cases the result will be a `java.util.Map` with string keys and values or other `java.util.Map` as value. Requests are made in JSON format hold some type information (i.e., it is known what values are strings and what values are numbers).

Let’s look at an example:

```java
SObjectComposite composite = new SObjectComposite("38.0", true);

// first insert operation via an external id
final Account updateAccount = new TestAccount();
updateAccount.setName("Salesforce");
updateAccount.setBillingStreet("Landmark @ 1 Market Street");
updateAccount.setBillingCity("San Francisco");
updateAccount.setBillingState("California");
updateAccount.setIndustry(Account_IndustryEnum.TECHNOLOGY);
composite.addUpdate("Account", "001xx000003DIpcAAG", updateAccount, "UpdatedAccount");

final Contact newContact = new TestContact();
newContact.setLastName("John Doe");
newContact.setPhone("1234567890");
composite.addCreate(newContact, "NewContact");

final AccountContactJunction__c junction = new AccountContactJunction__c();
junction.setAccount__c("001xx000003DIpcAAG");
junction.setContactId__c("@{NewContact.id}");
composite.addCreate(junction, "JunctionRecord");

final SObjectCompositeResponse response = template.requestBody("salesforce:composite", composite, SObjectCompositeResponse.class);
final List<SObjectCompositeResult> results = response.getCompositeResponse();

final SObjectCompositeResult accountUpdateResult = results.stream().filter(r -> "UpdatedAccount".equals(r.getReferenceId())).findFirst().get()
final int statusCode = accountUpdateResult.getHttpStatusCode(); // should be 200
final Map<String, ?> accountUpdateBody = accountUpdateResult.getBody();

final SObjectCompositeResult contactCreationResult = results.stream().filter(r -> "JunctionRecord".equals(r.getReferenceId())).findFirst().get()
```

**Using the `rawPayload` option**

It’s possible to directly call Salesforce composite by preparing the Salesforce JSON request in the route thanks to the `rawPayload` option.

For instance, you can have the following route:

from("timer:fire?period=2000").setBody(constant("{\\n" +
     " \\"allOrNone\\" : true,\\n" +
     " \\"records\\" : \[ { \\n" +
     "   \\"attributes\\" : {\\"type\\" : \\"FOO\\"},\\n" +
     "   \\"Name\\" : \\"123456789\\",\\n" +
     "   \\"FOO\\" : \\"XXXX\\",\\n" +
     "   \\"ACCOUNT\\" : 2100.0\\n" +
     "   \\"ExternalID\\" : \\"EXTERNAL\\"\\n"
     " }\]\\n" +
     "}")
   .to("salesforce:composite?rawPayload=true")
   .log("${body}");

The route directly creates the body as JSON and directly submit to salesforce endpoint using `rawPayload=true` option.

With this approach, you have complete control on the Salesforce request.

`POST` is the default HTTP method used to send raw Composite requests to salesforce. Use the `compositeMethod` option to override to the other supported value, `GET`, which returns a list of other available composite resources.

##### Composite Tree

`composite-tree`

Create up to 200 records with parent-child relationships (up to 5 levels) in one go.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `SObjectTree` | Contains REST API sub-requests to be executed. |  | x |

**Output**

Type: `SObjectTree`

To create up to 200 records including parent-child relationships use `salesforce:composite-tree` operation. This requires an instance of `org.apache.camel.component.salesforce.api.dto.composite.SObjectTree` in the input message and returns the same tree of objects in the output message. The `org.apache.camel.component.salesforce.api.dto.AbstractSObjectBase` instances within the tree get updated with the identifier values (`Id` property) or their corresponding `org.apache.camel.component.salesforce.api.dto.composite.SObjectNode` is populated with `errors` on failure.

Note that for some records operation can succeed and for some it can fail — so you need to manually check for errors.

The easiest way to use this functionality is to use the DTOs generated by the `camel-salesforce-maven-plugin`, but you also have the option of customizing the references that identify each object in the tree, for instance primary keys from your database.

Let’s look at an example:

```java
Account account = ...
Contact president = ...
Contact marketing = ...

Account anotherAccount = ...
Contact sales = ...
Asset someAsset = ...

// build the tree
SObjectTree request = new SObjectTree();
request.addObject(account).addChildren(president, marketing);
request.addObject(anotherAccount).addChild(sales).addChild(someAsset);

final SObjectTree response = template.requestBody("salesforce:composite-tree", tree, SObjectTree.class);
final Map<Boolean, List<SObjectNode>> result = response.allNodes()
                                                   .collect(Collectors.groupingBy(SObjectNode::hasErrors));

final List<SObjectNode> withErrors = result.get(true);
final List<SObjectNode> succeeded = result.get(false);

final String firstId = succeeded.get(0).getId();
```

##### Composite Batch

`composite-batch`

Submit a composition of requests in batch. Executes up to 25 sub-requests in a single request.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `SObjectBatch` | Contains sub-requests to be executed. |  | x |

**Output**

Type: `SObjectBatchResponse`

The Composite API batch operation allows you to accumulate multiple requests in a batch and then submit them in one go, saving the round trip cost of multiple individual requests. Each response is then received in a list of responses with the order preserved, so that the n-th requests response is in the n-th place of the response.

> **Note**
> The results can vary from API to API so the result of each sub-request (`SObjectBatchResult.result`) is given as a `java.lang.Object`. In most cases the result will be a `java.util.Map` with string keys and values or other `java.util.Map` as value. Requests are made in JSON format and hold some type information (i.e., it is known what values are strings and what values are numbers).

Let’s look at an example:

```java
final String acountId = ...
final SObjectBatch batch = new SObjectBatch("53.0");

final Account updates = new Account();
updates.setName("NewName");
batch.addUpdate("Account", accountId, updates);

final Account newAccount = new Account();
newAccount.setName("Account created from Composite batch API");
batch.addCreate(newAccount);

batch.addGet("Account", accountId, "Name", "BillingPostalCode");

batch.addDelete("Account", accountId);

final SObjectBatchResponse response = template.requestBody("salesforce:composite-batch", batch, SObjectBatchResponse.class);

boolean hasErrors = response.hasErrors(); // if any of the requests has resulted in either 4xx or 5xx HTTP status
final List<SObjectBatchResult> results = response.getResults(); // results of three operations sent in batch

final SObjectBatchResult updateResult = results.get(0); // update result
final int updateStatus = updateResult.getStatusCode(); // probably 204
final Object updateResultData = updateResult.getResult(); // probably null

final SObjectBatchResult createResult = results.get(1); // create result
@SuppressWarnings("unchecked")
final Map<String, Object> createData = (Map<String, Object>) createResult.getResult();
final String newAccountId = createData.get("id"); // id of the new account, this is for JSON, for XML it would be createData.get("Result").get("id")

final SObjectBatchResult retrieveResult = results.get(2); // retrieve result
@SuppressWarnings("unchecked")
final Map<String, Object> retrieveData = (Map<String, Object>) retrieveResult.getResult();
final String accountName = retrieveData.get("Name"); // Name of the retrieved account, this is for JSON, for XML it would be createData.get("Account").get("Name")
final String accountBillingPostalCode = retrieveData.get("BillingPostalCode"); // Name of the retrieved account, this is for JSON, for XML it would be createData.get("Account").get("BillingPostalCode")

final SObjectBatchResult deleteResult = results.get(3); // delete result
final int updateStatus = deleteResult.getStatusCode(); // probably 204
final Object updateResultData = deleteResult.getResult(); // probably null
```

##### Retrieve Multiple Records with Fewer Round-Trips

`compositeRetrieveSObjectCollections`

Retrieve one or more records of the same object type.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| sObjectIds | List of String or comma-separated string | A list of one or more IDs of the objects to return. All IDs must belong to the same object type. |  | x |
| sObjectFields | List of String or comma-separated string | A list of fields to include in the response. The field names you specify must be valid, and you must have read-level permissions to each field. |  | x |
| sObjectName | String | Type of SObject, e.g. `Account` |  | x |
| sObjectClass | String | Fully qualified class name of DTO class to use for deserializing the response. |  | Required if `sObjectName` parameter does not resolve to a class that exists in the package specified by the `package` option. |

**Output**

Type: `List` of class determined by `sObjectName` or `sObjectClass` header

##### Create SObject Collections

`compositeCreateSObjectCollections`

Add up to 200 records. Mixed SObject types is supported.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | List of `SObject` | A list of SObjects to create |  | x |
| `allOrNone` | boolean | Indicates whether to roll back the entire request when the creation of any object fails (true) or to continue with the independent creation of other objects in the request. | false |  |

**Output**

Type: `List<SaveSObjectResult>`

##### Update SObject Collections

`compositeUpdateSObjectCollections`

Update up to 200 records. Mixed SObject types is supported.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | List of `SObject` | A list of SObjects to update |  | x |
| `allOrNone` | `boolean` | Indicates whether to roll back the entire request when the update of any object fails (true) or to continue with the independent update of other objects in the request. | false |  |

**Output**

Type: `List<SaveSObjectResult>`

##### Upsert SObject Collections

`compositeUpsertSObjectCollections`

Create or update (upsert) up to 200 records based on an external ID field. Mixed SObject types is not supported.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | List of `SObject` | A list of SObjects to upsert |  | x |
| `allOrNone` | `boolean` | Indicates whether to roll back the entire request when the upsert of any object fails (true) or to continue with the independent upsert of other objects in the request. | false |  |
| `sObjectName` | `String` | Type of SObject, e.g. `Account` |  | x |
| `sObjectIdName` | `String` | Name of External ID field |  | x |

**Output**

Type: `List<UpsertSObjectResult>`

##### Delete SObject Collections

`compositeDeleteSObjectCollections`

Delete up to 200 records. Mixed SObject types is supported.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `sObjectIds` or request body | List of String or comma-separated string | A list of up to 200 IDs of objects to be deleted. |  | x |
| `allOrNone` | boolean | Indicates whether to roll back the entire request when the deletion of any object fails (true) or to continue with the independent deletion of other objects in the request. | false |  |

**Output**

Type: `List<DeleteSObjectResult>`

##### Get Event Schema

`getEventSchema`

Gets the definition of a Platform Event in JSON format. Other types of events such as Change Data Capture events or custom events are also supported. This operation is available in REST API version 40.0 and later.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `eventName` | String | Name of event |  | `eventName` or `eventSchemaId` is required |
| `eventSchemaId` | String | ID of a schema |  | `eventName` or `eventSchemaId` is required |
| `eventSchemaFormat` | EventSchemaFormatEnum | `EXPANDED`: Apache Avro format but doesn’t strictly adhere to the record complex type. `COMPACT`: Apache Avro, adheres to the specification for the record complex type. This parameter is available in API version 43.0 and later. | `EXPANDED` |  |

**Output**

Type: `InputStream`

#### Binary Fields and Multipart Requests

The Salesforce component provides automatic support for handling binary fields (blob fields) in SObjects without requiring manual base64 encoding. This feature works with both `createSObject` and `updateSObject` operations.

##### Binary Field Pattern

For any SObject with blob fields, you can use binary fields that follow the naming pattern `***Binary`, where `***` is the original field name. For example:

-   `VersionData` field → `VersionDataBinary` field
    
-   `Body` field → `BodyBinary` field
    
-   `ContentData` field → `ContentDataBinary` field
    

##### Automatic Multipart Detection

When you populate a `***Binary` field with an `InputStream`, the component automatically detects this and switches to multipart encoding for the request. This means that the binary data is sent directly as a stream, avoiding the overhead of base64 encoding.:

##### Usage Examples

**Creating a ContentVersion with binary data:**

```java
// Create ContentVersion with binary field
ContentVersion cv = new ContentVersion();
cv.setTitle("My Document");
cv.setPathOnClient("document.pdf");

// Use binary field instead of base64 encoded string
InputStream fileData = new FileInputStream("document.pdf");
cv.setVersionDataBinary(fileData);  // Automatically triggers multipart request

// Send to Salesforce
template.requestBody("salesforce:createSObject", cv);
```

**Updating a Document with binary content:**

```java
// Update Document with binary field
Document doc = new Document();
doc.setId("01234567890123456");
doc.setName("Updated Document");

// Use binary field for efficient upload
InputStream content = getClass().getResourceAsStream("/updated-content.pdf");
doc.setBodyBinary(content);  // Automatically triggers multipart request

// Send to Salesforce
template.requestBody("salesforce:updateSObject", doc);
```

##### DTO Generation

When using the [Camel Salesforce Maven Plugin](#MavenPlugin), binary fields are automatically generated for blob fields:

```java
public class ContentVersion extends AbstractSObjectBase {

    // Standard base64 field (for backward compatibility)
    private String VersionData;

    // Generated binary field (new efficient approach)
    @JsonIgnore
    private InputStream VersionDataBinary;

    // Getters and setters for both fields...
}
```

##### Field Priority

When both the standard field and binary field are populated:

-   **Binary field takes precedence** - The `***Binary` field is used and a multipart request is made
    
-   **Standard field is ignored** - The base64 string field is not sent in the multipart request
    
-   **Automatic cleanup** - Binary field names are automatically removed from the JSON payload
    

##### Performance Benefits

Using binary fields provides significant performance improvements:

-   **No base64 encoding** required on the client side
    
-   **Direct streaming** of binary data to Salesforce
    
-   **Reduced memory usage** for large files
    
-   **Faster upload times** especially for large documents
    
-   **Higher salesforce limits** for multipart requests compared to base64 strings. Salesforce limits base64 strings to 50 MB of text data or 37.5 MB of base64–encoded data. Multipart uploads can handle 2 GB for ContentVersion records, and 500 MB for all other objects.
    

##### Backward Compatibility

The existing base64 string approach continues to work:

```java
// Still supported - base64 approach
ContentVersion cv = new ContentVersion();
cv.setVersionData(base64EncodedString);  // Uses standard JSON request
```

However, using binary fields is recommended for better performance when working with binary data.

#### Apex REST API

##### Invoke an Apex REST Web Service method

`apexCall`

You can [expose your Apex class and methods](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_rest_intro.htm) so that external applications can access your code and your application through the REST architecture.

The URI format for invoking Apex REST is:

salesforce:apexCall\[/yourApexRestUrl\]\[?options\]

You can supply the apexUrl either in the endpoint (see above), or as the `apexUrl` option as listed in the table below. In either case the Apex URL can contain placeholders in the format of `{headerName}`. E.g., for the Apex URL `MyApexClass/{id}`, the value of the header named `id` will be used to replace the placeholder. If `rawPayload` is false and neither `sObjectClass` nor `sObjectName` are set, Camel will attempt to determine the correct `AbstractQueryRecordsBase` sublcass based on the response.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `Map<String, Object>` if `GET`, otherwise `String` or `InputStream` | In the case of a `GET`, the body (`Map` instance) is transformed into query parameters. For other HTTP methods, the body is used for the HTTP body. |  |  |
| `apexUrl` | `String` | The portion of the endpoint URL after `[https://instance.salesforce.com/services/apexrest/](https://instance.salesforce.com/services/apexrest/)`, e.g., 'MyApexClass/' |  | Yes, unless supplied in endpoint |
| `apexMethod` | `String` | The HTTP method (e.g. `GET`, `POST`) to use. | `GET` |  |
| `rawPayload` | `Boolean` | If true, Camel will not serialize the request or response bodies. | false |  |
| Header: `apexQueryParam.[paramName]` | Object | Headers that override apex parameters passed in the endpoint. |  |  |
| `sObjectName` | `String` | Name of sObject (e.g. `Merchandise__c`) used to deserialize the response |  |  |
| `sObjectClass` | `String` | Fully qualified class name used to deserialize the response |  |  |

**Output**

Type: Instance of class supplied in `sObjectClass` input header.

#### Bulk 2.0 API

The Bulk 2.0 API has a simplified model over the original Bulk API. Use it to quickly load a large amount of data into salesforce, or query a large amount of data out of salesforce. Data must be provided in CSV format, usually via an `InputStream` instance. PK chunking is performed automatically. The minimum API version for Bulk 2.0 is v41.0. The minimum API version for Bulk Queries is v47.0. DTO classes mentioned below are from the `org.apache.camel.component.salesforce.api.dto.bulkv2` package. The following operations are supported:

-   [bulk2CreateJob](#bulk2CreateJob) - Creates a bulk ingest job.
    
-   [bulk2CreateBatch](#bulk2CreateBatch) - Adds a batch of data to an ingest job.
    
-   [bulk2CloseJob](#bulk2CloseJob) - Closes an ingest job.
    
-   [bulk2AbortJob](#bulk2AbortJob) - Aborts an ingest job.
    
-   [bulk2DeleteJob](#bulk2DeleteJob) - Deletes an ingest job.
    
-   [bulk2GetSuccessfulResults](#bulk2GetSuccessfulResults) - Gets successful results for an ingest job.
    
-   [bulk2GetFailedResults](#bulk2GetFailedResults) - Gets failed results for an ingest job.
    
-   [bulk2GetUnprocessedRecords](#bulk2GetUnprocessedRecords) - Gets unprocessed records for an ingest job.
    
-   [bulk2GetJob](#bulk2GetJob) - Gets an ingest Job.
    
-   [bulk2GetAllJobs](#bulk2GetAllJobs) - Gets all ingest jobs.
    
-   [bulk2CreateQueryJob](#bulk2CreateQueryJob) - Creates a query job.
    
-   [bulk2GetQueryJobResults](#bulk2GetQueryJobResults) - Gets query job results.
    
-   [bulk2AbortQueryJob](#bulk2AbortQueryJob) - Aborts a query job.
    
-   [bulk2DeleteQueryJob](#bulk2DeleteQueryJob) - Deletes a query job.
    
-   [bulk2GetQueryJob](#bulk2GetQueryJob) - Gets a query job.
    
-   [bulk2GetAllQueryJobs](#bulk2GetAllQueryJobs) - Gets all query jobs.
    

##### Create a Job

`bulk2CreateJob` Creates a bulk ingest job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `Job` | Job to create |  | x |

**Output**

Type: `Job`

##### Upload a Batch of Job Data

`bulk2CreateBatch`

Adds a batch of data to an ingest job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `InputStream` or `String` | CSV data. The first row must contain headers. |  | Required if `jobId` not supplied |
| `jobId` | `String` | Id of Job to create batch under |  | x |

##### Close a Job

`bulk2CloseJob`

Closes an ingest job. You must close the job in order for it to be processed or aborted/deleted.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to close |  | x |

**Output**

Type: `Job`

##### Abort a Job

`bulk2AbortJob`

Aborts an ingest job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to abort |  | x |

**Output**

Type: `Job`

##### Delete a Job

`bulk2DeleteJob`

Deletes an ingest job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to delete |  | x |

##### Get Job Successful Record Results

`bulk2GetSuccessfulResults`

Gets successful results for an ingest job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to get results for |  | x |

**Output**

Type: `InputStream`  
Contents: CSV data

##### Get Job Failed Record Results

`bulk2GetFailedResults`

Gets failed results for an ingest job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to get results for |  | x |

**Output**

Type: `InputStream`  
Contents: CSV data

##### Get Job Unprocessed Record Results

`bulk2GetUnprocessedRecords`

Gets unprocessed records for an ingest job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to get records for |  | x |

**Output**

Type: `InputStream` Contents: CSV data

##### Get Job Info

`bulk2GetJob`

Gets an ingest Job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `Job` | Will use Id of supplied Job to retrieve Job |  | Required if `jobId` not supplied |
| `jobId` | `String` | Id of Job to retrieve |  | Required if `Job` not supplied in body |

**Output**

Type: `Job`

##### Get All Jobs

`bulk2GetAllJobs`

Gets all ingest jobs.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `queryLocator` | `String` | Used in subsequent calls if results span multiple pages |  |  |

**Output**

Type: `Jobs`

If the `done` property of the `Jobs` instance is false, there are additional pages to fetch, and the `nextRecordsUrl` property contains the value to be set in the `queryLocator` parameter on subsequent calls.

##### Create a Query Job

`bulk2CreateQueryJob`

Gets a query job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `QueryJob` | QueryJob to create |  | x |

**Output**

Type: `QueryJob`

##### Get Results for a Query Job

`bulk2GetQueryJobResults`

Get bulk query job results. `jobId` parameter is required. Accepts `maxRecords` and `locator` parameters.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to get results for |  | x |
| `maxRecords` | `Integer` | The maximum number of records to retrieve per set of results for the query. The request is still subject to the size limits. If you are working with a very large number of query results, you may experience a timeout before receiving all the data from Salesforce. To prevent a timeout, specify the maximum number of records your client is expecting to receive in the maxRecords parameter. This splits the results into smaller sets with this value as the maximum size. |  |  |
| `locator` | `locator` | A string that identifies a specific set of query results. Providing a value for this parameter returns only that set of results. Omitting this parameter returns the first set of results. |  |  |

**Output**

Type: `InputStream` Contents: CSV data

Response message headers include `Sforce-NumberOfRecords` and `Sforce-Locator` headers. The value of `Sforce-Locator` can be passed into subsequent calls via the `locator` parameter.

##### Abort a Query Job

`bulk2AbortQueryJob`

Aborts a query job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to abort |  | x |

**Output**

Type: `QueryJob`

##### Delete a Query Job

`bulk2DeleteQueryJob`

Deletes a query job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to delete |  | x |

##### Get Information About a Query Job

`bulk2GetQueryJob`

Gets a query job.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to retrieve |  | x |

**Output**

Type: `QueryJob`

##### Get Information About All Query Jobs

`bulk2GetAllQueryJobs`

Gets all query jobs.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `queryLocator` | `String` | Used in subsequent calls if results span multiple pages |  |  |

**Output**

Type: `QueryJobs`

If the `done` property of the `QueryJobs` instance is false, there are additional pages to fetch, and the `nextRecordsUrl` property contains the value to be set in the `queryLocator` parameter on subsequent calls.

#### Bulk (original) API

Producer endpoints can use the following APIs. All Job data formats, i.e. xml, csv, zip/xml, and zip/csv are supported.  
The request and response have to be marshalled/unmarshalled by the route. Usually the request will be some stream source like a CSV file, and the response may also be saved to a file to be correlated with the request.

The following operations are supported:

-   [createJob](#createJob) - Creates a Salesforce Bulk Job.
    
-   [getJob](#getJob) - Gets a Job using its Salesforce Id
    
-   [closeJob](#closeJob) - Closes a Job
    
-   [abortJob](#abortJob) - Aborts a Job
    
-   [createBatch](#createBatch) - Submits a Batch within a Bulk Job
    
-   [getBatch](#getBatch) - Gets a Batch using Id
    
-   [getAllBatches](#getAllBatches) - Gets all Batches for a Bulk Job Id
    
-   [getRequest](#getRequest) - Gets Request data (XML/CSV) for a Batch
    
-   [getResults](#getResults) - Gets the results of the Batch when its complete
    
-   [createBatchQuery](#createBatchQuery) - Creates a Batch from an SOQL query
    
-   [getQueryResultIds](#getQueryResultIds) - Gets a list of Result Ids for a Batch Query
    
-   [getQueryResult](#getQueryResult) - Gets results for a Result Id
    

##### Create a Job

`createJob`

Creates a Salesforce Bulk Job. PK Chunking is supported via the pkChunking\* options. See an explanation [here](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/async_api_headers_enable_pk_chunking.htm).

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `JobInfo` | Job to create |  | x |
| `pkChunking` | `Boolean` | Whether to use PK Chunking | false |  |
| `pkChunkingChunkSize` | `Integer` |  |  |  |
| `pkChunkingStartRow` | `Integer` |  |  |  |
| `pkChunkingParent` | `String` |  |  |  |

**Output**

Type: `JobInfo`

##### Get Job Details

`getJob`

Gets a Job

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job to get |  | Required if body not supplied |
| Body | `JobInfo` | `JobInfo` instance from which Id will be used |  | Required if `jobId` not supplied |

**Output**

Type: `JobInfo`

##### Close a Job

`closeJob`

Closes a Job

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | Required if body not supplied |
| Body | `JobInfo` | `JobInfo` instance from which Id will be used |  | Required if `jobId` not supplied |

**Output**

Type: `JobInfo`

##### Abort a Job

`abortJob`

Aborts a Job

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | Required if body not supplied |
| Body | `JobInfo` | `JobInfo` instance from which Id will be used |  | Required if `jobId` not supplied |

**Output**

Type: `JobInfo`

##### Add a Batch to a Job

`createBatch`

Submits a Batch within a Bulk Job

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | x |
| `contentType` | `String` | Content type of body. Can be XML, CSV, ZIP\_XML or ZIP\_CSV |  | x |
| `Body` | `InputStream` or `String` | Batch data |  | x |

**Output**

Type: `BatchInfo`

##### Get Information for a Batch

`getBatch`

Get a Batch

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | Required if body not supplied |
| `batchId` | `String` | Id of Batch |  | Required if body not supplied |
| Body | `BatchInfo` | `JobInfo` instance from which `jobId` and `batchId` will be used |  | Required if `jobId` and `BatchId` not supplied |

**Output**

Type: `BatchInfo`

##### Get Information for All Batches in a Job

`getAllBatches`

Gets all Batches for a Bulk Job Id

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | Required if body not supplied |
| Body | `JobInfo` | `JobInfo` instance from which Id will be used |  | Required if `jobId` not supplied |

**Output**

Type: `List<JobInfo>`

##### Get a Batch Request

`getRequest`

Gets Request data (XML/CSV) for a Batch

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | Required if body not supplied |
| `batchId` | `String` | Id of Batch |  | Required if body not supplied |
| Body | `BatchInfo` | `JobInfo` instance from which `jobId` and `batchId` will be used |  | Required if `jobId` and `BatchId` not supplied |

**Output**

Type: `InputStream`

##### Get Batch Results

`getResults`

Gets the results of the Batch when it’s complete

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | Required if body not supplied |
| `batchId` | `String` | Id of Batch |  | Required if body not supplied |
| Body | `BatchInfo` | `JobInfo` instance from which `jobId` and `batchId` will be used |  | Required if `jobId` and `BatchId` not supplied |

**Output**

Type: `InputStream`

##### Create Bulk Query Batch

`createBatchQuery`

Creates a Batch from an SOQL query

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | Required if body not supplied |
| `contentType` | `String` | Content type of body. Can be XML, CSV, ZIP\_XML or ZIP\_CSV |  | Required if `JobInfo` instance not supplied in body |
| `sObjectQuery` | `String` | SOQL query to be used for this batch |  | Required if not supplied in body |
| Body | `JobInfo` or `String` | Either `JobInfo` instance from which `jobId` and `contentType` will be used, or `String` to be used as the Batch query |  | Required `JobInfo` if `jobId` and `contentType` not supplied. |

**Output**

Type: `BatchInfo`

##### Get Batch Results

`getQueryResultIds`

Gets a list of Result Ids for a Batch Query

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | Required if body not supplied |
| `batchId` | `String` | Id of Batch |  | Required if body not supplied |
| Body | `BatchInfo` | `JobInfo` instance from which `jobId` and `batchId` will be used |  | Required if `jobId` and `BatchId` not supplied |

**Output**

Type: `List<String>`

##### Get Bulk Query Results

`getQueryResult`

Gets results for a Result Id

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `jobId` | `String` | Id of Job |  | Required if body not supplied |
| `batchId` | `String` | Id of Batch |  | Required if body not supplied |
| `resultId` | `String` | Id of Result |  | If not passed in body |
| Body | `BatchInfo` or `String` | `JobInfo` instance from which `jobId` and `batchId` will be used. Otherwise, can be a `String` containing the `resultId` |  | `BatchInfo` Required if `jobId` and `BatchId` not supplied |

**Output**

Type: `InputStream`

For example, the following producer endpoint uses the createBatch API to create a Job Batch. The in message must contain a body that can be converted into an `InputStream` (usually UTF-8 CSV or XML content from a file, etc.) and header fields 'jobId' for the Job and 'contentType' for the Job content type, which can be XML, CSV, ZIP\_XML or ZIP\_CSV. The put message body will contain `BatchInfo` on success, or throw a `SalesforceException` on error.

```java
...to("salesforce:createBatch")..
```

#### Pub/Sub API

The Pub/Sub API allows you to publish and subscribe to platform events, including real-time event monitoring events, and change data capture events. This API is based on gRPC and HTTP/2, and event payloads are delivered in Apache Avro format.

##### Publishing Events

The URI format for publishing events is:

salesforce:pubSubPublish:<topic\_name>

For example:

.to("salesforce:pubsubPublish:/event/MyCustomPlatformEvent\_\_e")

##### Publish an Event

`pubSubPublish`

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `List`. List can contained mixed types (see description below). | Event payloads to be published |  |  |

Because The Pub/Sub API requires that event payloads be serialized in Apache Avro format, Camel will attempt to serialize event payloads from the following input types:

-   Avro `GenericRecord`. Camel fetches the Avro schema in order to serialize `GenericRecord` instances. This option doesn’t require ahead-of-time generation of Event classes.
    
-   Avro `SpecificRecord`. Subclasses of `SpecificRecord` contain properties that are specific to an event type. The [maven plugin](#MavenPlugin) can generate the subclasses automatically.
    
-   POJO. Camel fetches the Avro schema in order to serialize POJO instances. The POJO’s field names must match event field names exactly, including case.
    
-   `String`. Camel will treat the `String` value as JSON and serialize to Avro. Note that the JSON value does not have to be Avro-encoded JSON. It can be arbitrary JSON, but it must be serializable to Avro based on the Schema associated with the topic you’re publishing to. The JSON object’s field names must match event field names exactly, including case.
    
-   `byte[]`. Camel will not perform any serialization. Value must be the Avro-encoded event payload.
    
-   `com.salesforce.eventbus.protobuf.ProducerEvent`. Providing a `ProducerEvent` allows full control, e.g., setting the `id` property, which can be tied back to the `PublishResult.CorrelationKey`.
    

**Output**

Type: `List<org.apache.camel.component.salesforce.api.dto.pubsub.PublishResult>`

The order of the items in the returned `List` correlates to the order of the items in the input `List`.

##### Subscribing

The URI format for subscribing to a Pub/Sub topic is:

salesforce:pubSubSubscribe:<topic\_name>

For example:

from("salesforce:pubSubSubscribe:/event/BatchApexErrorEvent")

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `replayPreset` | `ReplayPreset` | Values: `LATEST`, `EARLIEST`, `CUSTOM`. | `LATEST` |  |
| `pubSubReplayId` | `String` | When `replayPreset` is set to `CUSTOM`, the replayId to use when subscribing to a topic. |  |  |
| `pubSubBatchSize` | int | Max number of events to receive at a time. Values >100 will be normalized to 100 by salesforce. | 100 | X |
| `pubSubDeserializeType` | `PubSubDeserializeType` | Values: `AVRO`, `SPECIFIC_RECORD`, `GENERIC_RECORD`, `POJO`, `JSON`. `AVRO` will try a `SpecificRecord` subclass if found, otherwise `GenericRecord` | `AVRO` | X |
| `pubSubPojoClass` | Fully qualified class name to deserialize Pub/Sub API event to. |  |  | If `pubSubDeserializeType` is `POJO` |

**Output**

Type: Determined by the `pubSubDeserializeType` option.

Headers: `CamelSalesforcePubSubReplayId`

#### Streaming API

The Streaming API enables streaming of events using push technology and provides a subscription mechanism for receiving events in near real time. The Streaming API subscription mechanism supports multiple types of events, including PushTopic events, generic events, platform events, and Change Data Capture events.

##### Push Topics

The URI format for consuming Push Topics is:

salesforce:subscribe:<topic\_name>\[?options\]

To create and subscribe to a topic

```java
from("salesforce:subscribe:CamelTestTopic?notifyForFields=ALL&notifyForOperations=ALL&sObjectName=Merchandise__c&updateTopic=true&sObjectQuery=SELECT Id, Name FROM Merchandise__c")...
```

To subscribe to an existing topic

```java
from("salesforce:subscribe:CamelTestTopic&sObjectName=Merchandise__c")...
```

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `sObjectName` | `String` | SObject to monitor |  | x |
| `sObjectQuery` | `String` | SOQL query used to create Push Topic |  | Required for creating new topics |
| `updateTopic` | `Boolean` | Whether to update an existing Push Topic if exists | false |  |
| `notifyForFields` | `NotifyForFieldsEnum` | Specifies how the record is evaluated against the PushTopic query. | Referenced |  |
| `notifyForOperationCreate` | `Boolean` | Whether a create operation should generate a notification. | false |  |
| `notifyForOperationDelete` | `Boolean` | Whether a delete operation should generate a notification. | false |  |
| `notifyForOperationUndelete` | `Boolean` | Whether an undelete operation should generate a notification. | false |  |
| `notifyForOperationUpdate` | `Boolean` | Whether an update operation should generate a notification. | false |  |
| `notifyForOperations` | `NotifyForOperationsEnum` | Whether an update operation should generate a notification. Only for use in API version < 29.0 | All |  |
| `replayId` | `int` | The replayId value to use when subscribing. |  |  |
| `defaultReplayId` | `int` | Default replayId setting if no value is found in initialReplayIdMap. | \-1 |  |
| `fallBackReplayId` | `int` | ReplayId to fall back to after an Invalid Replay Id response. | \-1 |  |

##### Parallel processing received events

You can turn on `consumerWorkerPoolEnabled=true` on the salesforce endpoint to let Camel use a thread-pool to process the received events, which allows to process these events in parallel.

> **Note**
> It has been reported that when receiving from PUSH\_TOPIC events and then later sending a message to salesforce (via producer) via the same thread could cause Salesforce to block. Enabling the worker pool can help with this. See more in [CAMEL-22332](https://issues.apache.org/jira/browse/CAMEL-22332).

**Output**

Type: Class passed via `sObjectName` parameter

##### Platform Events

To emit a platform event use the [createSObject](#createSObject) operation, passing an instance of a platform event, e.g. `Order_Event__e`.

The URI format for consuming platform events is:

salesforce:subscribe:event/<event\_name>

For example, to receive platform events use for the event type `Order_Event__e`:

```java
from("salesforce:subscribe:event/Order_Event__e")
```

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `rawPayload` | `Boolean` | If false, operation returns a `PlatformEvent`, otherwise returns the raw Bayeux Message | false |  |
| `replayId` | `int` | The replayId value to use when subscribing. |  |  |
| `defaultReplayId` | `int` | Default replayId setting if no value is found in initialReplayIdMap. | \-1 |  |
| `fallBackReplayId` | `int` | ReplayId to fall back to after an Invalid Replay Id response. | \-1 |  |

**Output**

Type: `PlatformEvent` or `org.cometd.bayeux.Message`

##### Change Data Capture Events

Change Data Capture (CDC) allows you to receive near-real-time changes of Salesforce records, and synchronize corresponding records in an external data store. Change Data Capture publishes change events, which represent changes to Salesforce records. Changes include the creation of a new record, updates to an existing record, deletion of a record, and undeletion of a record.

The URI format to consume CDC events is as follows:

All Selected Entities

salesforce:subscribe:data/ChangeEvents

Standard Objects

salesforce:subscribe:data/<Standard\_Object\_Name>ChangeEvent

Custom Objects

salesforce:subscribe:data/<Custom\_Object\_Name>\_\_ChangeEvent

Here are a few examples

```java
from("salesforce:subscribe:data/ChangeEvents?replayId=-1").log("being notified of all change events")
from("salesforce:subscribe:data/AccountChangeEvent?replayId=-1").log("being notified of change events for Account records")
from("salesforce:subscribe:data/Employee__ChangeEvent?replayId=-1").log("being notified of change events for Employee__c custom object")
```

More details about how to use the Camel Salesforce component change data capture capabilities could be found in the [ChangeEventsConsumerIntegrationTest](https://github.com/apache/camel/tree/main/components/camel-salesforce/camel-salesforce-component/src/test/java/org/apache/camel/component/salesforce/ChangeEventsConsumerIntegrationTest.java).

The [Salesforce developer guide](https://developer.salesforce.com/docs/atlas.en-us.change_data_capture.meta/change_data_capture/cdc_intro.htm) is a good fit to better know the subtleties of implementing a change data capture integration application. The dynamic nature of change event body fields, high level replication steps as well as security considerations could be of interest.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `rawPayload` | `Boolean` | If false, operation returns a `Map<String, Object>`, otherwise returns the raw Bayeux `Message` | false |  |
| `replayId` | `int` | The replayId value to use when subscribing. |  |  |
| `defaultReplayId` | `int` | Default replayId setting if no value is found in initialReplayIdMap. | \-1 |  |
| `fallBackReplayId` | `int` | ReplayId to fall back to after an Invalid Replay Id response. | \-1 |  |

**Output**

Type: `Map<String, Object>` or `org.cometd.bayeux.Message`

Headers

 
| Name | Description |
| --- | --- |
| `CamelSalesforceChangeType` | `CREATE`, `UPDATE`, `DELETE` or `UNDELETE` |

#### Reports API

-   [getRecentReports](#getRecentReports) - Gets up to 200 of the reports you most recently viewed.
    
-   [getReportDescription](#getReportDescription) - Retrieves report description.
    
-   [executeSyncReport](#executeSyncReport) - Runs a report synchronously.
    
-   [executeAsyncReport](#executeAsyncReport) - Runs a report asynchronously.
    
-   [getReportInstances](#getReportInstances) - Returns a list of instances for a report that you requested to be run asynchronously.
    
-   [getReportResults](#getReportResults) - Retrieves results for an instance of a report run asynchronously.
    

##### Report List

`getRecentReports`

Gets up to 200 of the reports you most recently viewed.

**Output**

Type: `List<RecentReport>`

##### Describe Report

`getReportDescription`

Retrieves the report, report type, and related metadata for a report, either in a tabular or summary or matrix format.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `reportId` | `String` | Id of Report |  | Required if not supplied in body |
| Body | `String` | Id of Report |  | Required if not supplied in `reportId` parameter |

**Output**

Type: `ReportDescription`

##### Execute Sync

`executeSyncReport`

Runs a report synchronously with or without changing filters and returns the latest summary data.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `reportId` | `String` | Id of Report |  | Required if not supplied in body |
| `includeDetails` | `Boolean` | Whether to include details | false |  |
| `reportMetadata` | `ReportMetadata` | Optionally, pass ReportMetadata here instead of body |  |  |
| Body | `ReportMetadata` | If supplied, will use instead of `reportId` |  | Required if not supplied in `reportId` parameter |

**Output**

Type: `AbstractReportResultsBase`

##### Execute Async

`executeAsyncReport`

Runs an instance of a report asynchronously with or without filters and returns the summary data with or without details.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `reportId` | `String` | Id of Report |  | Required if not supplied in body |
| `includeDetails` | `Boolean` | Whether to include details | false |  |
| `reportMetadata` | `ReportMetadata` | Optionally, pass ReportMetadata here instead of body |  |  |
| Body | `ReportMetadata` | If supplied, will use instead of `reportId` parameter |  | Required if not supplied in `reportId` parameter |

**Output**

Type: `ReportInstance`

##### Instances List

`getReportInstances`

Returns a list of instances for a report that you requested to be run asynchronously. Each item in the list is treated as a separate instance of the report.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `reportId` | `String` | Id of Report |  | Required if not supplied in body |
| Body | `String` | If supplied, will use instead of `reportId` parameter |  | Required if not supplied in `reportId` parameter |

**Output**

Type: `List<ReportInstance>`

##### Instance Results

`getReportResults`

Contains the results of running a report.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `reportId` | `String` | Id of Report |  | Required if not supplied in body |
| `instanceId` | `String` | Id of Report instance |  | x |
| Body | `String` | If supplied, will use instead of `reportId` parameter |  | Required if not supplied in `reportId` parameter |

**Output**

Type: `AbstractReportResultsBase`

### Miscellaneous Operations

-   [raw](#raw) - Send requests to salesforce and have full, raw control over endpoint, parameters, body, etc.
    

#### Raw

`raw`

Sends HTTP requests to salesforce with full, raw control of all aspects of the call. Any serialization or deserialization of request and response bodies must be performed in the route. The `Content-Type` HTTP header will be automatically set based on the `format` option, but this can be overridden with the `rawHttpHeaders` option.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `String` or `InputStream` | Body of the HTTP request |  |  |
| `rawPath` | `String` | The portion of the endpoint URL after the domain name, e.g., '/services/data/v51.0/sobjects/Account/' |  | x |
| `rawMethod` | `String` | The HTTP method |  | x |
| `rawQueryParameters` | `String` | Comma separated list of message headers to include as query parameters. Do not url-encode values as this will be done automatically. |  |  |
| `rawHttpHeaders` | `String` | Comma separated list of message headers to include as HTTP headers |  |  |

**Output**

Type: `InputStream`

##### Query example

In this example we’ll send a query to the REST API. The query must be passed in a URL parameter called "q", so we’ll create a message header called q and tell the raw operation to include that message header as a URL parameter:

from("direct:queryExample")
  .setHeader("q", "SELECT Id, LastName FROM Contact")
  .to("salesforce:raw?format=JSON&rawMethod=GET&rawQueryParameters=q&rawPath=/services/data/v51.0/query")
  // deserialize JSON results or handle in some other way

##### SObject example

In this example, we’ll pass a Contact the REST API in a `create` operation. Since the `raw` operation does not perform any serialization, we make sure to pass XML in the message body

from("direct:createAContact")
  .setBody(constant("<Contact><LastName>TestLast</LastName></Contact>"))
  .to("salesforce:raw?format=XML&rawMethod=POST&rawPath=/services/data/v51.0/sobjects/Contact")

The response is:

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<Result>
    <id>0034x00000RnV6zAAF</id>
    <success>true</success>
</Result>

### Uploading a document to a ContentWorkspace

#### Using Binary Fields (Recommended)

For efficient document uploads without base64 encoding overhead, use the binary field approach:

```java
public class ContentProcessor implements Processor {
    public void process(Exchange exchange) throws Exception {
        Message message = exchange.getIn();

        ContentVersion cv = new ContentVersion();
        ContentWorkspace cw = getWorkspace(exchange);
        cv.setFirstPublishLocationId(cw.getId());
        cv.setTitle("test document");
        cv.setPathOnClient("test_doc.html");

        // Use binary field for efficient upload - no base64 encoding needed
        InputStream document = message.getBody(InputStream.class);
        cv.setVersionDataBinary(document);  // Automatically triggers multipart request
        message.setBody(cv);
    }

    protected ContentWorkspace getWorkSpace(Exchange exchange) {
        // Look up the content workspace somehow, maybe use enrich() to add it to a
        // header that can be extracted here
        ....
    }
}
```

Give the output from the processor to the Salesforce component:

```java
from("file:///home/camel/library")
    .to(new ContentProcessor())     // convert file stream into a ContentVersion SObject
                                    // with binary field for efficient upload
    .to("salesforce:createSObject");
```

#### Using Base64 Encoding (Legacy)

The traditional base64 encoding approach is still supported for backward compatibility:

```java
public class ContentProcessor implements Processor {
    public void process(Exchange exchange) throws Exception {
        Message message = exchange.getIn();

        ContentVersion cv = new ContentVersion();
        ContentWorkspace cw = getWorkspace(exchange);
        cv.setFirstPublishLocationId(cw.getId());
        cv.setTitle("test document");
        cv.setPathOnClient("test_doc.html");
        byte[] document = message.getBody(byte[].class);
        ObjectMapper mapper = new ObjectMapper();
        String enc = mapper.convertValue(document, String.class);
        cv.setVersionData(enc);  // Uses base64 encoding and standard JSON request
        message.setBody(cv);
    }

    protected ContentWorkspace getWorkSpace(Exchange exchange) {
        // Look up the content workspace somehow, maybe use enrich() to add it to a
        // header that can be extracted here
        ....
    }
}
```

### Generating SOQL query strings

`org.apache.camel.component.salesforce.api.utils.QueryHelper` contains helper methods to generate SOQL queries. For instance, to fetch all custom fields from _Account_ SObject, you can generate the SOQL SELECT by invoking:

```java
String allCustomFieldsQuery = QueryHelper.queryToFetchFilteredFieldsOf(new Account(), SObjectField::isCustom);
```

### Camel Salesforce Maven Plugin

The Maven plugin generates Java DTOs to represent salesforce objects.

Please refer to [README.md](https://github.com/apache/camel/tree/main/components/camel-salesforce/camel-salesforce-maven-plugin) for details on how to use the plugin.

## Spring Boot Auto-Configuration

When using salesforce with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-salesforce-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 109 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.salesforce.all-or-none** | Composite API option to indicate to rollback all records if any are not successful. | false | Boolean |
| **camel.component.salesforce.apex-method** | APEX method name. |  | String |
| **camel.component.salesforce.apex-query-params** | Query params for APEX method. |  | Map |
| **camel.component.salesforce.apex-url** | APEX method URL. |  | String |
| **camel.component.salesforce.api-version** | Salesforce API version. | 56.0 | String |
| **camel.component.salesforce.authentication-type** | Explicit authentication method to be used, one of USERNAME\_PASSWORD, REFRESH\_TOKEN, CLIENT\_CREDENTIALS, or JWT. Salesforce component can auto-determine the authentication method to use from the properties set, set this property to eliminate any ambiguity. |  | AuthenticationType |
| **camel.component.salesforce.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.salesforce.backoff-increment** | Backoff interval increment for Streaming connection restart attempts for failures beyond CometD auto-reconnect. The option is a long type. | 1000 | Long |
| **camel.component.salesforce.batch-id** | Bulk API Batch ID. |  | String |
| **camel.component.salesforce.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.salesforce.client-id** | OAuth Consumer Key of the connected app configured in the Salesforce instance setup. Typically a connected app needs to be configured but one can be provided by installing a package. |  | String |
| **camel.component.salesforce.client-secret** | OAuth Consumer Secret of the connected app configured in the Salesforce instance setup. |  | String |
| **camel.component.salesforce.composite-method** | Composite (raw) method. |  | String |
| **camel.component.salesforce.config** | Global endpoint configuration - use to set values that are common to all endpoints. The option is a org.apache.camel.component.salesforce.SalesforceEndpointConfig type. |  | SalesforceEndpointConfig |
| **camel.component.salesforce.consumer-worker-pool-enabled** | Use thread pool for processing received Salesforce events, for example to process events in parallel. | false | Boolean |
| **camel.component.salesforce.consumer-worker-pool-executor-service** | To use a custom thread pool for processing received Salesforce events, for example to process events in parallel. The option is a java.util.concurrent.ExecutorService type. |  | ExecutorService |
| **camel.component.salesforce.consumer-worker-pool-max-size** | Maximum thread pool size size for consumer worker pool. | 20 | Integer |
| **camel.component.salesforce.consumer-worker-pool-size** | Core thread pool size size for consumer worker pool. | 10 | Integer |
| **camel.component.salesforce.content-type** | Bulk API content type, one of XML, CSV, ZIP\_XML, ZIP\_CSV. |  | ContentType |
| **camel.component.salesforce.default-replay-id** | Default replayId setting if no value is found in initialReplayIdMap. | \-1 | Long |
| **camel.component.salesforce.enabled** | Whether to enable auto configuration of the salesforce component. This is enabled by default. |  | Boolean |
| **camel.component.salesforce.event-name** | Name of Platform Event, Change Data Capture Event, custom event, etc. |  | String |
| **camel.component.salesforce.event-schema-format** | EXPANDED: Apache Avro format but doesn’t strictly adhere to the record complex type. COMPACT: Apache Avro, adheres to the specification for the record complex type. This parameter is available in API version 43.0 and later. |  | EventSchemaFormatEnum |
| **camel.component.salesforce.event-schema-id** | The ID of the event schema. |  | String |
| **camel.component.salesforce.fall-back-replay-id** | ReplayId to fall back to after an Invalid Replay Id response. | \-1 | Long |
| **camel.component.salesforce.fallback-to-latest-replay-id** | Whether the pub/sub consumer needs to fallback to the latest replay id when the provided id is not valid. If set to false, the component will keep retrying; in order to treat this as an exception you can use BridgeExceptionHandlerToErrorHandler and handle the exception in the route. | false | Boolean |
| **camel.component.salesforce.format** | Payload format to use for Salesforce API calls, either JSON or XML, defaults to JSON. As of Camel 3.12, this option only applies to the Raw operation. |  | PayloadFormat |
| **camel.component.salesforce.http-client** | Custom Jetty Http Client to use to connect to Salesforce. The option is a org.apache.camel.component.salesforce.SalesforceHttpClient type. |  | SalesforceHttpClient |
| **camel.component.salesforce.http-client-connection-timeout** | Connection timeout used by the HttpClient when connecting to the Salesforce server. | 60000 | Long |
| **camel.component.salesforce.http-client-idle-timeout** | Timeout used by the HttpClient when waiting for response from the Salesforce server. | 10000 | Long |
| **camel.component.salesforce.http-client-properties** | Used to set any properties that can be configured on the underlying HTTP client. Have a look at properties of SalesforceHttpClient and the Jetty HttpClient for all available options. |  | Map |
| **camel.component.salesforce.http-max-content-length** | Max content length of an HTTP response. |  | Integer |
| **camel.component.salesforce.http-proxy-auth-uri** | Used in authentication against the HTTP proxy server, needs to match the URI of the proxy server in order for the httpProxyUsername and httpProxyPassword to be used for authentication. |  | String |
| **camel.component.salesforce.http-proxy-excluded-addresses** | A list of addresses for which HTTP proxy server should not be used. |  | Set |
| **camel.component.salesforce.http-proxy-host** | Hostname of the HTTP proxy server to use. |  | String |
| **camel.component.salesforce.http-proxy-included-addresses** | A list of addresses for which HTTP proxy server should be used. |  | Set |
| **camel.component.salesforce.http-proxy-password** | Password to use to authenticate against the HTTP proxy server. |  | String |
| **camel.component.salesforce.http-proxy-port** | Port number of the HTTP proxy server to use. |  | Integer |
| **camel.component.salesforce.http-proxy-realm** | Realm of the proxy server, used in preemptive Basic/Digest authentication methods against the HTTP proxy server. |  | String |
| **camel.component.salesforce.http-proxy-secure** | If set to false disables the use of TLS when accessing the HTTP proxy. | true | Boolean |
| **camel.component.salesforce.http-proxy-socks4** | If set to true the configures the HTTP proxy to use as a SOCKS4 proxy. | false | Boolean |
| **camel.component.salesforce.http-proxy-use-digest-auth** | If set to true Digest authentication will be used when authenticating to the HTTP proxy, otherwise Basic authorization method will be used. | false | Boolean |
| **camel.component.salesforce.http-proxy-username** | Username to use to authenticate against the HTTP proxy server. |  | String |
| **camel.component.salesforce.http-request-buffer-size** | HTTP request buffer size. May need to be increased for large SOQL queries. | 8192 | Integer |
| **camel.component.salesforce.http-request-timeout** | Timeout value for HTTP requests. | 60000 | Long |
| **camel.component.salesforce.include-details** | Include details in Salesforce1 Analytics report, defaults to false. | false | Boolean |
| **camel.component.salesforce.initial-replay-id-map** | Replay IDs to start from per channel name. |  | Map |
| **camel.component.salesforce.initial-reply-id-timeout** | Timeout in seconds to validate when a custom pubSubReplayId has been configured, when starting the Camel Salesforce consumer. | 30 | Integer |
| **camel.component.salesforce.instance-id** | Salesforce1 Analytics report execution instance ID. |  | String |
| **camel.component.salesforce.instance-url** | URL of the Salesforce instance used after authentication, by default received from Salesforce on successful authentication. |  | String |
| **camel.component.salesforce.job-id** | Bulk API Job ID. |  | String |
| **camel.component.salesforce.jwt-audience** | Value to use for the Audience claim (aud) when using OAuth JWT flow. If not set, the login URL will be used, which is appropriate in most cases. |  | String |
| **camel.component.salesforce.keystore** | KeyStore parameters to use in OAuth JWT flow. The KeyStore should contain only one entry with private key and certificate. Salesforce does not verify the certificate chain, so this can easily be a selfsigned certificate. Make sure that you upload the certificate to the corresponding connected app. The option is a org.apache.camel.support.jsse.KeyStoreParameters type. |  | KeyStoreParameters |
| **camel.component.salesforce.lazy-login** | If set to true prevents the component from authenticating to Salesforce with the start of the component. You would generally set this to the (default) false and authenticate early and be immediately aware of any authentication issues. Lazy login is not supported by salesforce consumers. | false | Boolean |
| **camel.component.salesforce.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.salesforce.limit** | Limit on number of returned records. Applicable to some of the API, check the Salesforce documentation. |  | Integer |
| **camel.component.salesforce.locator** | Locator provided by salesforce Bulk 2.0 API for use in getting results for a Query job. |  | String |
| **camel.component.salesforce.login-config** | All authentication configuration in one nested bean, all properties set there can be set directly on the component as well. The option is a org.apache.camel.component.salesforce.SalesforceLoginConfig type. |  | SalesforceLoginConfig |
| **camel.component.salesforce.login-url** | URL of the Salesforce instance used for authentication, by default set to [https://login.salesforce.com](https://login.salesforce.com). | [https://login.salesforce.com](https://login.salesforce.com) | String |
| **camel.component.salesforce.long-polling-transport-properties** | Used to set any properties that can be configured on the LongPollingTransport used by the BayeuxClient (CometD) used by the streaming api. |  | Map |
| **camel.component.salesforce.max-backoff** | Maximum backoff interval for Streaming connection restart attempts for failures beyond CometD auto-reconnect. The option is a long type. | 30000 | Long |
| **camel.component.salesforce.max-records** | The maximum number of records to retrieve per set of results for a Bulk 2.0 Query. The request is still subject to the size limits. If you are working with a very large number of query results, you may experience a timeout before receiving all the data from Salesforce. To prevent a timeout, specify the maximum number of records your client is expecting to receive in the maxRecords parameter. This splits the results into smaller sets with this value as the maximum size. |  | Integer |
| **camel.component.salesforce.not-found-behaviour** | Sets the behaviour of 404 not found status received from Salesforce API. Should the body be set to NULL NotFoundBehaviour#NULL or should a exception be signaled on the exchange NotFoundBehaviour#EXCEPTION - the default. | exception | NotFoundBehaviour |
| **camel.component.salesforce.notify-for-fields** | Notify for fields, options are ALL, REFERENCED, SELECT, WHERE. |  | NotifyForFieldsEnum |
| **camel.component.salesforce.notify-for-operation-create** | Notify for create operation, defaults to false (API version >= 29.0). | false | Boolean |
| **camel.component.salesforce.notify-for-operation-delete** | Notify for delete operation, defaults to false (API version >= 29.0). | false | Boolean |
| **camel.component.salesforce.notify-for-operation-undelete** | Notify for un-delete operation, defaults to false (API version >= 29.0). | false | Boolean |
| **camel.component.salesforce.notify-for-operation-update** | Notify for update operation, defaults to false (API version >= 29.0). | false | Boolean |
| **camel.component.salesforce.notify-for-operations** | Notify for operations, options are ALL, CREATE, EXTENDED, UPDATE (API version < 29.0). |  | NotifyForOperationsEnum |
| **camel.component.salesforce.object-mapper** | Custom Jackson ObjectMapper to use when serializing/deserializing Salesforce objects. The option is a com.fasterxml.jackson.databind.ObjectMapper type. |  | ObjectMapper |
| **camel.component.salesforce.packages** | In what packages are the generated DTO classes. Typically the classes would be generated using camel-salesforce-maven-plugin. Set it if using the generated DTOs to gain the benefit of using short SObject names in parameters/header values. Multiple packages can be separated by comma. |  | String |
| **camel.component.salesforce.password** | Password used in OAuth flow to gain access to access token. It’s easy to get started with password OAuth flow, but in general one should avoid it as it is deemed less secure than other flows. Make sure that you append security token to the end of the password if using one. |  | String |
| **camel.component.salesforce.pk-chunking** | Use PK Chunking. Only for use in original Bulk API. Bulk 2.0 API performs PK chunking automatically, if necessary. | false | Boolean |
| **camel.component.salesforce.pk-chunking-chunk-size** | Chunk size for use with PK Chunking. If unspecified, salesforce default is 100,000. Maximum size is 250,000. |  | Integer |
| **camel.component.salesforce.pk-chunking-parent** | Specifies the parent object when you’re enabling PK chunking for queries on sharing objects. The chunks are based on the parent object’s records rather than the sharing object’s records. For example, when querying on AccountShare, specify Account as the parent object. PK chunking is supported for sharing objects as long as the parent object is supported. |  | String |
| **camel.component.salesforce.pk-chunking-start-row** | Specifies the 15-character or 18-character record ID to be used as the lower boundary for the first chunk. Use this parameter to specify a starting ID when restarting a job that failed between batches. |  | String |
| **camel.component.salesforce.pub-sub-batch-size** | Max number of events to receive in a batch from the Pub/Sub API. | 100 | Integer |
| **camel.component.salesforce.pub-sub-deserialize-type** | How to deserialize events consume from the Pub/Sub API. AVRO will try a SpecificRecord subclass if found, otherwise GenericRecord. | avro | PubSubDeserializeType |
| **camel.component.salesforce.pub-sub-host** | Pub/Sub host. | api.pubsub.salesforce.com | String |
| **camel.component.salesforce.pub-sub-pojo-class** | Fully qualified class name to deserialize Pub/Sub API event to. |  | String |
| **camel.component.salesforce.pub-sub-port** | Pub/Sub port. | 7443 | Integer |
| **camel.component.salesforce.pubsub-allow-use-system-proxy** | Allow the Pub/Sub API client to use the proxy detected by java.net.ProxySelector. If false then no proxy server will be used. | true | Boolean |
| **camel.component.salesforce.query-locator** | Query Locator provided by salesforce for use when a query results in more records than can be retrieved in a single call. Use this value in a subsequent call to retrieve additional records. |  | String |
| **camel.component.salesforce.raw-http-headers** | Comma separated list of message headers to include as HTTP parameters for Raw operation. |  | String |
| **camel.component.salesforce.raw-method** | HTTP method to use for the Raw operation. |  | String |
| **camel.component.salesforce.raw-path** | The portion of the endpoint URL after the domain name. E.g., '/services/data/v52.0/sobjects/Account/'. |  | String |
| **camel.component.salesforce.raw-payload** | Use raw payload String for request and response (either JSON or XML depending on format), instead of DTOs, false by default. | false | Boolean |
| **camel.component.salesforce.raw-query-parameters** | Comma separated list of message headers to include as query parameters for Raw operation. Do not url-encode values as this will be done automatically. |  | String |
| **camel.component.salesforce.refresh-token** | Refresh token already obtained in the refresh token OAuth flow. One needs to setup a web application and configure a callback URL to receive the refresh token, or configure using the builtin callback at [https://login.salesforce.com/services/oauth2/success](https://login.salesforce.com/services/oauth2/success) or [https://test.salesforce.com/services/oauth2/success](https://test.salesforce.com/services/oauth2/success) and then retrive the refresh\_token from the URL at the end of the flow. Note that in development organizations Salesforce allows hosting the callback web application at localhost. |  | String |
| **camel.component.salesforce.replay-preset** | Replay preset for Pub/Sub API. | latest | ReplayPreset |
| **camel.component.salesforce.report-id** | Salesforce1 Analytics report Id. |  | String |
| **camel.component.salesforce.report-metadata** | Salesforce1 Analytics report metadata for filtering. The option is a org.apache.camel.component.salesforce.api.dto.analytics.reports.ReportMetadata type. |  | ReportMetadata |
| **camel.component.salesforce.result-id** | Bulk API Result ID. |  | String |
| **camel.component.salesforce.s-object-blob-field-name** | SObject blob field name. |  | String |
| **camel.component.salesforce.s-object-class** | Fully qualified SObject class name, usually generated using camel-salesforce-maven-plugin. |  | String |
| **camel.component.salesforce.s-object-fields** | SObject fields to retrieve. |  | String |
| **camel.component.salesforce.s-object-id** | SObject ID if required by API. |  | String |
| **camel.component.salesforce.s-object-id-name** | SObject external ID field name. |  | String |
| **camel.component.salesforce.s-object-id-value** | SObject external ID field value. |  | String |
| **camel.component.salesforce.s-object-name** | SObject name if required or supported by API. |  | String |
| **camel.component.salesforce.s-object-query** | Salesforce SOQL query string. |  | String |
| **camel.component.salesforce.s-object-search** | Salesforce SOSL search string. |  | String |
| **camel.component.salesforce.ssl-context-parameters** | SSL parameters to use, see SSLContextParameters class for all available options. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.salesforce.stream-query-result** | If true, streams SOQL query result and transparently handles subsequent requests if there are multiple pages. Otherwise, results are returned one page at a time. | false | Boolean |
| **camel.component.salesforce.update-topic** | Whether to update an existing Push Topic when using the Streaming API, defaults to false. | false | Boolean |
| **camel.component.salesforce.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.salesforce.user-name** | Username used in OAuth flow to gain access to access token. It’s easy to get started with password OAuth flow, but in general one should avoid it as it is deemed less secure than other flows. |  | String |
| **camel.component.salesforce.worker-pool-max-size** | Maximum size of the thread pool used to handle HTTP responses. | 20 | Integer |
| **camel.component.salesforce.worker-pool-size** | Size of the thread pool used to handle HTTP responses. | 10 | Integer |