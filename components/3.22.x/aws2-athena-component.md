# AWS Athena

**Since Camel 3.4**

**Only producer is supported**

The AWS2 Athena component supports running queries with [AWS Athena](https://aws.amazon.com/athena/) and working with results.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Athena. More information is available at [AWS Athena](https://aws.amazon.com/athena/).

## URI Format

aws2-athena://label\[?options\]

You can append query options to the URI in the following format, ?options=value&option2=value&…​

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

The AWS Athena component supports 30 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accessKey** (producer) | Amazon AWS Access Key. |  | String |
| **amazonAthenaClient** (producer) | **Autowired** The AmazonAthena instance to use as the client. |  | AthenaClient |
| **configuration** (producer) | The component configuration. |  | Athena2Configuration |
| **database** (producer) | The Athena database to use. |  | String |
| **delay** (producer) | Milliseconds before the next poll for query execution status. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 2000 | long |
| **encryptionOption** (producer) | 
The encryption type to use when storing query results in S3. One of SSE\_S3, SSE\_KMS, or CSE\_KMS.

Enum values:

-   SSE\_S3
    
-   SSE\_KMS
    
-   CSE\_KMS
    
-   null
    





 |  | EncryptionOption |
| **includeTrace** (producer) | Include useful trace information at the beginning of queries as an SQL comment (prefixed with --). | false | boolean |
| **initialDelay** (producer) | Milliseconds before the first poll for query execution status. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 1000 | long |
| **kmsKey** (producer) | For SSE-KMS and CSE-KMS, this is the KMS key ARN or ID. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxAttempts** (producer) | Maximum number of times to attempt a query. Set to 1 to disable retries. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 1 | int |
| **maxResults** (producer) | Max number of results to return for the given operation (if supported by the Athena API endpoint). If not set, will use the Athena API default for the given operation. |  | Integer |
| **nextToken** (producer) | Pagination token to use in the case where the response from the previous request was truncated. |  | String |
| **operation** (producer) | 

The Athena API function to call.

Enum values:

-   getQueryExecution
    
-   getQueryResults
    
-   listQueryExecutions
    
-   startQueryExecution
    





 | startQueryExecution | Athena2Operations |
| **outputLocation** (producer) | The location in Amazon S3 where query results are stored, such as s3://path/to/query/bucket/. Ensure this value ends with a forward slash ('/'). |  | String |
| **outputType** (producer) | 

How query results should be returned. One of StreamList (default - return a GetQueryResultsIterable that can page through all results), SelectList (returns at most 1,000 rows at a time, plus a NextToken value as a header than can be used for manual pagination of results), S3Pointer (return an S3 path pointing to the results).

Enum values:

-   StreamList
    
-   SelectList
    
-   S3Pointer
    





 | StreamList | Athena2OutputType |
| **proxyHost** (producer) | To define a proxy host when instantiating the Athena client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Athena client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Athena client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **queryExecutionId** (producer) | The unique ID identifying the query execution. |  | String |
| **queryString** (producer) | The SQL query to run. Except for simple queries, prefer setting this as the body of the Exchange or as a header using Athena2Constants.QUERY\_STRING to avoid having to deal with URL encoding issues. |  | String |
| **region** (producer) | The region in which Athena client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1). You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **resetWaitTimeoutOnRetry** (producer) | Reset the waitTimeout countdown in the event of a query retry. If set to true, potential max time spent waiting for queries is equal to waitTimeout x maxAttempts. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | true | boolean |
| **retry** (producer) | 

Optional comma separated list of error types to retry the query for. Use 'retryable' to retry all retryable failure conditions (e.g. generic errors and resources exhausted), 'generic' to retry 'GENERIC\_INTERNAL\_ERROR' failures, 'exhausted' to retry queries that have exhausted resource limits, 'always' to always retry regardless of failure condition, or 'never' or null to never retry (default). See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more.

Enum values:

-   never
    
-   always
    
-   retryable
    
-   exhausted
    
-   generic
    





 | never | String |
| **secretKey** (producer) | Amazon AWS Secret Key. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Athena client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **waitTimeout** (producer) | Optional max wait time in millis to wait for a successful query completion. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 0 | long |
| **workGroup** (producer) | The workgroup to use for running the query. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientRequestToken** (advanced) | A unique string to ensure issues queries are idempotent. It is unlikely you will need to set this. |  | String |

## Endpoint Options

The AWS Athena endpoint is configured using URI syntax:

aws2-athena:label

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (28 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accessKey** (producer) | Amazon AWS Access Key. |  | String |
| **amazonAthenaClient** (producer) | **Autowired** The AmazonAthena instance to use as the client. |  | AthenaClient |
| **database** (producer) | The Athena database to use. |  | String |
| **delay** (producer) | Milliseconds before the next poll for query execution status. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 2000 | long |
| **encryptionOption** (producer) | 
The encryption type to use when storing query results in S3. One of SSE\_S3, SSE\_KMS, or CSE\_KMS.

Enum values:

-   SSE\_S3
    
-   SSE\_KMS
    
-   CSE\_KMS
    
-   null
    





 |  | EncryptionOption |
| **includeTrace** (producer) | Include useful trace information at the beginning of queries as an SQL comment (prefixed with --). | false | boolean |
| **initialDelay** (producer) | Milliseconds before the first poll for query execution status. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 1000 | long |
| **kmsKey** (producer) | For SSE-KMS and CSE-KMS, this is the KMS key ARN or ID. |  | String |
| **maxAttempts** (producer) | Maximum number of times to attempt a query. Set to 1 to disable retries. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 1 | int |
| **maxResults** (producer) | Max number of results to return for the given operation (if supported by the Athena API endpoint). If not set, will use the Athena API default for the given operation. |  | Integer |
| **nextToken** (producer) | Pagination token to use in the case where the response from the previous request was truncated. |  | String |
| **operation** (producer) | 

The Athena API function to call.

Enum values:

-   getQueryExecution
    
-   getQueryResults
    
-   listQueryExecutions
    
-   startQueryExecution
    





 | startQueryExecution | Athena2Operations |
| **outputLocation** (producer) | The location in Amazon S3 where query results are stored, such as s3://path/to/query/bucket/. Ensure this value ends with a forward slash ('/'). |  | String |
| **outputType** (producer) | 

How query results should be returned. One of StreamList (default - return a GetQueryResultsIterable that can page through all results), SelectList (returns at most 1,000 rows at a time, plus a NextToken value as a header than can be used for manual pagination of results), S3Pointer (return an S3 path pointing to the results).

Enum values:

-   StreamList
    
-   SelectList
    
-   S3Pointer
    





 | StreamList | Athena2OutputType |
| **proxyHost** (producer) | To define a proxy host when instantiating the Athena client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Athena client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Athena client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **queryExecutionId** (producer) | The unique ID identifying the query execution. |  | String |
| **queryString** (producer) | The SQL query to run. Except for simple queries, prefer setting this as the body of the Exchange or as a header using Athena2Constants.QUERY\_STRING to avoid having to deal with URL encoding issues. |  | String |
| **region** (producer) | The region in which Athena client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1). You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **resetWaitTimeoutOnRetry** (producer) | Reset the waitTimeout countdown in the event of a query retry. If set to true, potential max time spent waiting for queries is equal to waitTimeout x maxAttempts. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | true | boolean |
| **retry** (producer) | 

Optional comma separated list of error types to retry the query for. Use 'retryable' to retry all retryable failure conditions (e.g. generic errors and resources exhausted), 'generic' to retry 'GENERIC\_INTERNAL\_ERROR' failures, 'exhausted' to retry queries that have exhausted resource limits, 'always' to always retry regardless of failure condition, or 'never' or null to never retry (default). See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more.

Enum values:

-   never
    
-   always
    
-   retryable
    
-   exhausted
    
-   generic
    





 | never | String |
| **secretKey** (producer) | Amazon AWS Secret Key. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Athena client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **waitTimeout** (producer) | Optional max wait time in millis to wait for a successful query completion. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 0 | long |
| **workGroup** (producer) | The workgroup to use for running the query. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **clientRequestToken** (advanced) | A unique string to ensure issues queries are idempotent. It is unlikely you will need to set this. |  | String |

Required Athena component options

You have to provide the amazonAthenaClient in the Registry or your accessKey and secretKey to access the [AWS Athena](https://aws.amazon.com/athena/) service.

## Examples

### Producer Examples

For example, to run a simple query, wait up to 60 seconds for completion, and log the results:

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?waitTimeout=60000&outputLocation=s3://bucket/path/")
    .to("aws2-athena://label?operation=getQueryResults&outputType=StreamList")
    .split(body()).streaming()
    .to("log:out")
    .to("mock:result");
```

Similarly, running the query and returning a path to the results in S3:

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?waitTimeout=60000&outputLocation=s3://bucket/path/")
    .to("aws2-athena://label?operation=getQueryResults&outputType=S3Pointer")
    .to("mock:result");
```

## Message Headers

The AWS Athena component supports 22 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsAthenaOperation** (all) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#OPERATION) | 
The operation to perform. Permitted values are getQueryExecution, getQueryResults, listQueryExecutions, startQueryExecution.

Enum values:

-   getQueryExecution
    
-   getQueryResults
    
-   listQueryExecutions
    
-   startQueryExecution
    





 | startQueryExecution | Athena2Operations |
| **CamelAwsAthenaDatabase** (startQueryExecution) Constant: [`DATABASE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#DATABASE) | The Athena database to use. |  | String |
| **CamelAwsAthenaQueryExecutionId** (getQueryExecution getQueryResults startQueryExecution) Constant: [`QUERY_EXECUTION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#QUERY_EXECUTION_ID) | The unique ID identifying the query execution. |  | String |
| **CamelAwsAthenaWorkGroup** (listQueryExecutions startQueryExecution) Constant: [`WORK_GROUP`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#WORK_GROUP) | The workgroup to use for running the query. |  | String |
| **CamelAwsAthenaNextToken** (getQueryResults listQueryExecutions) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#NEXT_TOKEN) | Pagination token to use in the case where the response from the previous request was truncated. |  | String |
| **CamelAwsAthenaMaxResults** (getQueryResults listQueryExecutions) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#MAX_RESULTS) | Max number of results to return for the given operation (if supported by the Athena API endpoint). If not set, will use the Athena API default for the given operation. |  | Integer |
| **CamelAwsAthenaIncludeTrace** (startQueryExecution) Constant: [`INCLUDE_TRACE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#INCLUDE_TRACE) | Include useful trace information at the beginning of queries as an SQL comment (prefixed with --). |  | boolean |
| **CamelAwsAthenaOutputLocation** (getQueryExecution getQueryResults startQueryExecution) Constant: [`OUTPUT_LOCATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#OUTPUT_LOCATION) | The location in Amazon S3 where query results are stored, such as s3://path/to/query/bucket/. Ensure this value ends with a forward slash ('/'). |  | String |
| **CamelAwsAthenaOutputType** (getQueryResults) Constant: [`OUTPUT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#OUTPUT_TYPE) | 

How query results should be returned. One of StreamList (default - return a GetQueryResultsIterable that can page through all results), SelectList (returns at most 1,000 rows at a time, plus a NextToken value as a header than can be used for manual pagination of results), S3Pointer (return an S3 path pointing to the results).

Enum values:

-   StreamList
    
-   SelectList
    
-   S3Pointer
    





 |  | Athena2OutputType |
| **CamelAwsAthenaQueryExecutionState** (getQueryExecution getQueryResults startQueryExecution) Constant: [`QUERY_EXECUTION_STATE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#QUERY_EXECUTION_STATE) | 

The state of the query execution.

Enum values:

-   QUEUED
    
-   RUNNING
    
-   SUCCEEDED
    
-   FAILED
    
-   CANCELLED
    
-   null
    





 |  | QueryExecutionState |
| **CamelAwsAthenaClientRequestToken** (startQueryExecution) Constant: [`CLIENT_REQUEST_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#CLIENT_REQUEST_TOKEN) | A unique string to ensure issues queries are idempotent. It is unlikely you will need to set this. |  | String |
| **CamelAwsAthenaQueryString** (startQueryExecution) Constant: [`QUERY_STRING`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#QUERY_STRING) | The SQL query to run. Except for simple queries, prefer setting this as the body of the Exchange or as this header to avoid having to deal with URL encoding issues. |  | String |
| **CamelAwsAthenaEncryptionOption** (startQueryExecution) Constant: [`ENCRYPTION_OPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#ENCRYPTION_OPTION) | 

The encryption type to use when storing query results in S3.

Enum values:

-   SSE\_S3
    
-   SSE\_KMS
    
-   CSE\_KMS
    
-   null
    





 |  | EncryptionOption |
| **CamelAwsAthenaKmsKey** (startQueryExecution) Constant: [`KMS_KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#KMS_KEY) | For SSE-KMS and CSE-KMS, this is the KMS key ARN or ID. |  | String |
| **CamelAwsAthenaWaitTimeout** (startQueryExecution) Constant: [`WAIT_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#WAIT_TIMEOUT) | Optional max wait time in millis to wait for a successful query completion. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. |  | long |
| **CamelAwsAthenaInitialDelay** (startQueryExecution) Constant: [`INITIAL_DELAY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#INITIAL_DELAY) | Milliseconds before the first poll for query execution status. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. |  | long |
| **CamelAwsAthenaDelay** (startQueryExecution) Constant: [`DELAY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#DELAY) | Milliseconds before the next poll for query execution status. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. |  | long |
| **CamelAwsAthenaMaxAttempts** (startQueryExecution) Constant: [`MAX_ATTEMPTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#MAX_ATTEMPTS) | Maximum number of times to attempt a query. Set to 1 to disable retries. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. |  | int |
| **CamelAwsAthenaRetry** (startQueryExecution) Constant: [`RETRY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#RETRY) | Optional comma separated list of error types to retry the query for. Use 'retryable' to retry all retryable failure conditions (e.g. generic errors and resources exhausted), 'generic' to retry 'GENERIC\_INTERNAL\_ERROR' failures, 'exhausted' to retry queries that have exhausted resource limits, 'always' to always retry regardless of failure condition, or 'never' or null to never retry (default). See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. |  | String |
| **CamelAwsAthenaResetWaitTimeoutOnRetry** (startQueryExecution) Constant: [`RESET_WAIT_TIMEOUT_ON_RETRY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#RESET_WAIT_TIMEOUT_ON_RETRY) | Reset the waitTimeout countdown in the event of a query retry. If set to true, potential max time spent waiting for queries is equal to waitTimeout x maxAttempts. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. |  | boolean |
| **CamelAwsAthenaStartQueryExecutionAttempts** (startQueryExecution) Constant: [`START_QUERY_EXECUTION_ATTEMPTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#START_QUERY_EXECUTION_ATTEMPTS) | Total number of attempts made to run the query. Will be greater than 1 if the query is retried. |  | int |
| **CamelAwsAthenaStartQueryExecutionElapsedMillis** (startQueryExecution) Constant: [`START_QUERY_EXECUTION_ELAPSED_MILLIS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-athena/latest/org/apache/camel/component/aws2/athena/Athena2Constants.html#START_QUERY_EXECUTION_ELAPSED_MILLIS) | Total time in millis taken in startQueryExecution (mostly relevant when waiting for query completion within startQueryExecution). |  | long |

### Static credentials vs Default Credential Provider

You have the possibility of avoiding the usage of explicit static credentials, by specifying the useDefaultCredentialsProvider option and set it to true.

-   Java system properties - aws.accessKeyId and aws.secretKey
    
-   Environment variables - AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable AWS\_CONTAINER\_CREDENTIALS\_RELATIVE\_URI is set.
    
-   Amazon EC2 Instance profile credentials.
    

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Athena Producer operations

The Camel-AWS Athena component provides the following operation on the producer side:

-   getQueryExecution
    
-   getQueryResults
    
-   listQueryExecutions
    
-   startQueryExecution
    

### Advanced AmazonAthena configuration

If your Camel Application is running behind a firewall or if you need to have more control over the `AthenaClient` instance configuration, you can create your own instance and refer to it in your Camel aws2-athena component configuration:

```java
from("aws2-athena://MyQuery?amazonAthenaClient=#client&...")
.to("mock:result");
```

### Overriding query parameters with message headers

Message headers listed in "Message headers evaluated by the Athena producer" override the corresponding query parameters listed in "Query Parameters".

For example:

```java
from("direct:start")
     .setHeader(Athena2Constants.OUTPUT_LOCATION, constant("s3://other/location/"))
     .to("aws2-athena:label?outputLocation=s3://foo/bar/")
     .to("mock:result");
```

Will cause the output location to be `s3://other/location/`.

### Athena Producer Operation examples

-   getQueryExecution: this operation returns information about a query given its query execution ID
    

```java
from("direct:start")
    .to("aws2-athena://label?operation=getQueryExecution&queryExecutionId=11111111-1111-1111-1111-111111111111")
    .to("mock:result");
```

The preceding example will yield an [Athena QueryExecution](https://docs.aws.amazon.com/athena/latest/APIReference/API_QueryExecution.md) in the body.

The getQueryExecution operation also supports retreiving the query execution ID from a header (`CamelAwsAthenaQueryExecutionId`), and since startQueryExecution sets the same header upon starting a query, these operations can be used together:

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?operation=startQueryExecution&outputLocation=s3://bucket/path/")
    .to("aws2-athena://label?operation=getQueryExecution")
    .to("mock:result");
```

The preceding example will yield an Athena QueryExecution in the body for the query that was just started.

-   getQueryResults: this operation returns the results of a query that has succeeded. The results are returned in the body in one of three formats.
    

`StreamList` - the default - returns a [GetQueryResultsIterable](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/services/athena/paginators/GetQueryResultsIterable.md) in the body that can page through all results:

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?operation=startQueryExecution&waitTimeout=60000&outputLocation=s3://bucket/path/")
    .to("aws2-athena://label?operation=getQueryResults&outputType=StreamList")
    .to("mock:result");
```

The output of StreamList can be processed in various ways:

```java
from("direct:start")
    .setBody(constant(
        "SELECT * FROM ("
            + "    VALUES"
            + "        (1, 'a'),"
            + "        (2, 'b')"
            + ") AS t (id, name)"))
    .to("aws2-athena://label?operation=startQueryExecution&waitTimeout=60000&outputLocation=s3://bucket/path/")
    .to("aws2-athena://label?operation=getQueryResults&outputType=StreamList")
    .split(body()).streaming()
    .process(new Processor() {

      @Override
      public void process(Exchange exchange) {
        GetQueryResultsResponse page = exchange
                                        .getMessage()
                                        .getBody(GetQueryResultsResponse.class);
        for (Row row : page.resultSet().rows()) {
          String line = row.data()
                          .stream()
                          .map(Datum::varCharValue)
                          .collect(Collectors.joining(","));
          System.out.println(line);
        }
      }
    })
    .to("mock:result");
```

The preceding example will print the results of the query as CSV to the console.

`SelectList` - returns a [GetQueryResponse](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/services/athena/model/GetQueryResultsResponse.md) in the body containing at most 1,000 rows, plus the NextToken value as a header (`CamelAwsAthenaNextToken`), which can be used for manual pagination of results:

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?operation=startQueryExecution&waitTimeout=60000&outputLocation=s3://bucket/path/")
    .to("aws2-athena://label?operation=getQueryResults&outputType=SelectList")
    .to("mock:result");
```

The preceding example will return a [GetQueryResponse](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/services/athena/model/GetQueryResultsResponse.md) in the body plus the NextToken value as a header (`CamelAwsAthenaNextToken`), which can be used to manually page through the results 1,000 rows at a time.

`S3Pointer` - return an S3 path (e.g. `s3://bucket/path/`) pointing to the results:

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?operation=startQueryExecution&waitTimeout=60000&outputLocation=s3://bucket/path/")
    .to("aws2-athena://label?operation=getQueryResults&outputType=S3Pointer")
    .to("mock:result");
```

The preceding example will return an S3 path (e.g. `s3://bucket/path/`) in the body pointing to the results. The path will also be set in a header (`CamelAwsAthenaOutputLocation`).

-   listQueryExecutions: this operation returns a list of query execution IDs
    

```java
from("direct:start")
    .to("aws2-athena://label?operation=listQueryExecutions")
    .to("mock:result");
```

The preceding example will return a list of query executions in the body, plus the NextToken value as a header (`CamelAwsAthenaNextToken`) than can be used for manual pagination of results.

-   startQueryExecution: this operation starts the execution of a query. It supports waiting for the query to complete before proceeding, and retrying the query based on a set of configurable failure conditions:
    

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?operation=startQueryExecution&outputLocation=s3://bucket/path/")
    .to("mock:result");
```

The preceding example will start the query `SELECT 1` and configure the results to be saved to `s3://bucket/path/`, but will not wait for the query to complete.

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?operation=startQueryExecution&waitTimeout=60000&outputLocation=s3://bucket/path/")
    .to("mock:result");
```

The preceding example will start a query and wait up to 60 seconds for it to reach a status that indicates it is complete (one of SUCCEEDED, FAILED, CANCELLED, or UNKNOWN\_TO\_SDK\_VERSION). Upon failure, the query would not be retried.

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?operation=startQueryExecution&waitTimeout=60000&initialDelay=10000&delay=1000&maxAttempts=3&retry=retryable&outputLocation=s3://bucket/path/")
    .to("mock:result");
```

The preceding example will start a query and wait up to 60 seconds for it to reach a status that indicates it is complete (one of SUCCEEDED, FAILED, CANCELLED, or UNKNOWN\_TO\_SDK\_VERSION). Upon failure, the query would be automatically retried up to 2 more times if the failure state indicates the query may succeed upon retry (Athena queries that fail with states such as `GENERIC_INTERNAL_ERROR` or "resource limit exhaustion" will sometimes succeed if retried). While waiting for the query to complete, the query status would first be checked after an initial delay of 10 seconds, and subsequently every 1 second until the query completes.

### Putting it all together

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?waitTimeout=60000&&maxAttempts=3&retry=retryable&outputLocation=s3://bucket/path/")
    .to("aws2-athena://label?operation=getQueryResults&outputType=StreamList")
    .to("mock:result");
```

The preceding example will start the query and wait up to 60 seconds for it to complete. Upon completion, getQueryResults put the results of the query into the body of the message for further processing.

For the sake of completeness, a similar outcome could be achieved with the following:

```java
from("direct:start")
    .setBody(constant("SELECT 1"))
    .to("aws2-athena://label?operation=startQueryExecution&outputLocation=s3://bucket/path/")
    .loopDoWhile(simple("${header." + Athena2Constants.QUERY_EXECUTION_STATE + "} != 'SUCCEEDED'"))
      .delay(1_000)
      .to("aws2-athena://label?operation=getQueryExecution")
    .end()
    .to("aws2-athena://label?operation=getQueryResults&outputType=StreamList")
    .to("mock:result");
```

Caution: the preceding example would block indefinitely, however, if the query did not complete with a status of SUCCEEDED.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-athena</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-athena with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-athena-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 31 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-athena.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-athena.amazon-athena-client** | The AmazonAthena instance to use as the client. The option is a software.amazon.awssdk.services.athena.AthenaClient type. |  | AthenaClient |
| **camel.component.aws2-athena.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-athena.client-request-token** | A unique string to ensure issues queries are idempotent. It is unlikely you will need to set this. |  | String |
| **camel.component.aws2-athena.configuration** | The component configuration. The option is a org.apache.camel.component.aws2.athena.Athena2Configuration type. |  | Athena2Configuration |
| **camel.component.aws2-athena.database** | The Athena database to use. |  | String |
| **camel.component.aws2-athena.delay** | Milliseconds before the next poll for query execution status. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 2000 | Long |
| **camel.component.aws2-athena.enabled** | Whether to enable auto configuration of the aws2-athena component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-athena.encryption-option** | The encryption type to use when storing query results in S3. One of SSE\_S3, SSE\_KMS, or CSE\_KMS. |  | EncryptionOption |
| **camel.component.aws2-athena.include-trace** | Include useful trace information at the beginning of queries as an SQL comment (prefixed with --). | false | Boolean |
| **camel.component.aws2-athena.initial-delay** | Milliseconds before the first poll for query execution status. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 1000 | Long |
| **camel.component.aws2-athena.kms-key** | For SSE-KMS and CSE-KMS, this is the KMS key ARN or ID. |  | String |
| **camel.component.aws2-athena.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-athena.max-attempts** | Maximum number of times to attempt a query. Set to 1 to disable retries. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 1 | Integer |
| **camel.component.aws2-athena.max-results** | Max number of results to return for the given operation (if supported by the Athena API endpoint). If not set, will use the Athena API default for the given operation. |  | Integer |
| **camel.component.aws2-athena.next-token** | Pagination token to use in the case where the response from the previous request was truncated. |  | String |
| **camel.component.aws2-athena.operation** | The Athena API function to call. |  | Athena2Operations |
| **camel.component.aws2-athena.output-location** | The location in Amazon S3 where query results are stored, such as s3://path/to/query/bucket/. Ensure this value ends with a forward slash ('/'). |  | String |
| **camel.component.aws2-athena.output-type** | How query results should be returned. One of StreamList (default - return a GetQueryResultsIterable that can page through all results), SelectList (returns at most 1,000 rows at a time, plus a NextToken value as a header than can be used for manual pagination of results), S3Pointer (return an S3 path pointing to the results). |  | Athena2OutputType |
| **camel.component.aws2-athena.proxy-host** | To define a proxy host when instantiating the Athena client. |  | String |
| **camel.component.aws2-athena.proxy-port** | To define a proxy port when instantiating the Athena client. |  | Integer |
| **camel.component.aws2-athena.proxy-protocol** | To define a proxy protocol when instantiating the Athena client. |  | Protocol |
| **camel.component.aws2-athena.query-execution-id** | The unique ID identifying the query execution. |  | String |
| **camel.component.aws2-athena.query-string** | The SQL query to run. Except for simple queries, prefer setting this as the body of the Exchange or as a header using Athena2Constants.QUERY\_STRING to avoid having to deal with URL encoding issues. |  | String |
| **camel.component.aws2-athena.region** | The region in which Athena client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1). You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-athena.reset-wait-timeout-on-retry** | Reset the waitTimeout countdown in the event of a query retry. If set to true, potential max time spent waiting for queries is equal to waitTimeout x maxAttempts. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | true | Boolean |
| **camel.component.aws2-athena.retry** | Optional comma separated list of error types to retry the query for. Use 'retryable' to retry all retryable failure conditions (e.g. generic errors and resources exhausted), 'generic' to retry 'GENERIC\_INTERNAL\_ERROR' failures, 'exhausted' to retry queries that have exhausted resource limits, 'always' to always retry regardless of failure condition, or 'never' or null to never retry (default). See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | never | String |
| **camel.component.aws2-athena.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-athena.use-default-credentials-provider** | Set whether the Athena client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-athena.wait-timeout** | Optional max wait time in millis to wait for a successful query completion. See the section 'Waiting for Query Completion and Retrying Failed Queries' to learn more. | 0 | Long |
| **camel.component.aws2-athena.work-group** | The workgroup to use for running the query. |  | String |