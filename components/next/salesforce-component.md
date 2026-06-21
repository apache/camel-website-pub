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

The Salesforce component supports 23 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSalesforceReplayId** (consumer) Constant: [`HEADER_SALESFORCE_REPLAY_ID`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_REPLAY_ID) | The Streaming API replayId. |  | Object |
| **CamelSalesforceEventUuid** (consumer) Constant: [`HEADER_SALESFORCE_EVENT_UUID`](https://javadoc.io/doc/org.apache.camel/camel-salesforce/latest/org/apache/camel/component/salesforce/SalesforceConstants.html#HEADER_SALESFORCE_EVENT_UUID) | The Streaming API eventUuid. |  | Object |
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

_Java-only: endpoint URI snippet_

```java
...to("salesforce:upsertSObject?sObjectIdName=Name")...
```

#### Supplying operation parameters as message headers

The operation parameters described in the per-operation tables below (such as `sObjectQuery`, `sObjectName`, `sObjectId`, `sObjectSearch`, `apexUrl`, `apexMethod`, the `apexQueryParam.` prefix and the Bulk/Analytics/RAW parameters) can be supplied either as endpoint options or as message headers.

> **Important**
> Starting with Camel 4.21, when these parameters are supplied as **message headers**, the header names follow the standard `CamelSalesforce` naming convention so that they are governed by the default `HeaderFilterStrategy` (which only filters `Camel`/`camel`\-prefixed headers). For example, set the `CamelSalesforceSObjectQuery` header instead of `sObjectQuery`, `CamelSalesforceApexUrl` instead of `apexUrl`, and use the `CamelSalesforceApexQueryParam.` prefix instead of `apexQueryParam.`. The **endpoint option** spelling is unchanged (for example `salesforce:query?sObjectQuery=…​` still works).
>
> Prefer referencing the constants in `SalesforceEndpointConfig` (for example `SalesforceEndpointConfig.SOBJECT_QUERY`) when setting these headers, so route code is unaffected by the value change. See the Camel 4.21 upgrade guide for the full list of renamed header names.

### Passing in Salesforce headers and fetching Salesforce response headers

There is support to pass [Salesforce headers](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/headers.htm) via inbound message headers, header names that start with `Sforce` or `x-sfdc` on the Camel message will be passed on in the request, and response headers that start with `Sforce` will be present in the outbound message headers.

For example, to fetch API limits, you can specify:

_Java-only: uses custom `Processor` implementation to read response headers_

```java
// in your Camel route set the header before Salesforce endpoint
  .setHeader("Sforce-Limit-Info", constant("api-usage"))
  .to("salesforce:getGlobalObjects")
  .to(myProcessor);

// myProcessor will receive `Sforce-Limit-Info` header on the outbound message
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

_Java-only: programmatic SObject field manipulation_

```java
accountSObject.getFieldsToNull().add("Site");
```

### Supported Salesforce APIs

Camel supports the following Salesforce APIs:

-   [REST API](others/salesforce-rest-api.md)
    
-   [Apex REST API](#ApexRESTAPI)
    
-   [Bulk 2 API](others/salesforce-bulk-api.md)
    
-   [Bulk API](others/salesforce-bulk-api.html#BulkAPI)
    
-   [Pub/Sub API](others/salesforce-streaming.html#PubSubAPI)
    
-   [Streaming API](others/salesforce-streaming.html#StreamingAPI)
    
-   [Reports API](others/salesforce-reports.md)
    

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

## Sub-Pages

For more details on specific Salesforce APIs, see:

-   [REST API](others/salesforce-rest-api.md) - CRUD operations, queries, composite requests, approvals, and more
    
-   [Bulk API](others/salesforce-bulk-api.md) - Bulk 2.0 and original Bulk API for large data operations
    
-   [Streaming and Pub/Sub](others/salesforce-streaming.md) - Platform events, push topics, change data capture, and Pub/Sub API
    
-   [Reports API](others/salesforce-reports.md) - Report execution, instances, and results
    

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

_Java-only: Processor implementation with Salesforce DTO and binary fields_

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

_Java-only: inline Processor instantiation_

```java
from("file:///home/camel/library")
    .to(new ContentProcessor())     // convert file stream into a ContentVersion SObject
                                    // with binary field for efficient upload
    .to("salesforce:createSObject");
```

#### Using Base64 Encoding (Legacy)

The traditional base64 encoding approach is still supported for backward compatibility:

_Java-only: Processor implementation with base64 encoding_

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

_Java-only: QueryHelper API_

```java
String allCustomFieldsQuery = QueryHelper.queryToFetchFilteredFieldsOf(new Account(), SObjectField::isCustom);
```

### Camel Salesforce Maven Plugin

The Maven plugin generates Java DTOs to represent salesforce objects.

Please refer to [README.md](https://github.com/apache/camel/tree/main/components/camel-salesforce/camel-salesforce-maven-plugin) for details on how to use the plugin.