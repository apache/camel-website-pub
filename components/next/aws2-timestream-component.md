# AWS Timestream

**Since Camel 4.1**

**Only producer is supported**

The AWS2 Timestream component supports the following operations on [AWS Timestream](https://aws.amazon.com/timestream/):

-   Write Operations
    
    -   Describe Write Endpoints
        
    -   Create, Describe, Resume, List Batch Load Tasks
        
    -   Create, Delete, Update, Describe, List Databases
        
    -   Create, Delete, Update, Describe, List Tables
        
    -   Write Records
        
    
-   Query Operations
    
    -   Describe Query Endpoints
        
    -   Prepare Query, Query, Cancel Query
        
    -   Create, Delete, Execute, Update, Describe, List Scheduled Queries
        
    

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Timestream. More information is available at [AWS Timestream](https://aws.amazon.com/timestream/).

## URI Format

aws2-timestream://clientType:label\[?options\]

You can append query options to the URI in the following format:

`?options=value&option2=value&…​`

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

The AWS Timestream component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | Timestream2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform. It can be describeEndpoints,createBatchLoadTask,describeBatchLoadTask, resumeBatchLoadTask,listBatchLoadTasks,createDatabase,deleteDatabase,describeDatabase,updateDatabase, listDatabases,createTable,deleteTable,describeTable,updateTable,listTables,writeRecords, createScheduledQuery,deleteScheduledQuery,executeScheduledQuery,updateScheduledQuery, describeScheduledQuery,listScheduledQueries,prepareQuery,query,cancelQuery.

Enum values:

-   describeEndpoints
    
-   createBatchLoadTask
    
-   describeBatchLoadTask
    
-   resumeBatchLoadTask
    
-   listBatchLoadTasks
    
-   createDatabase
    
-   deleteDatabase
    
-   describeDatabase
    
-   updateDatabase
    
-   listDatabases
    
-   createTable
    
-   deleteTable
    
-   describeTable
    
-   updateTable
    
-   listTables
    
-   writeRecords
    
-   createScheduledQuery
    
-   deleteScheduledQuery
    
-   executeScheduledQuery
    
-   updateScheduledQuery
    
-   describeScheduledQuery
    
-   listScheduledQueries
    
-   prepareQuery
    
-   query
    
-   cancelQuery
    





 |  | Timestream2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which the Timestream client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   eu-isoe-west-1
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   ca-west-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Timestream client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Timestream client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **awsTimestreamQueryClient** (advanced) | **Autowired** To use an existing configured AwsTimestreamQueryClient client. |  | TimestreamQueryClient |
| **awsTimestreamWriteClient** (advanced) | **Autowired** To use an existing configured AwsTimestreamWriteClient client. |  | TimestreamWriteClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Timestream client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Timestream client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Timestream client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **useSessionCredentials** (security) | Set whether the Timestream client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Timestream. | false | boolean |

## Endpoint Options

The AWS Timestream endpoint is configured using URI syntax:

aws2-timestream:clientType:label

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientType** (producer) | 
**Required** Type of client - write/query.

Enum values:

-   write
    
-   query
    





 |  | Timestream2ClientType |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform. It can be describeEndpoints,createBatchLoadTask,describeBatchLoadTask, resumeBatchLoadTask,listBatchLoadTasks,createDatabase,deleteDatabase,describeDatabase,updateDatabase, listDatabases,createTable,deleteTable,describeTable,updateTable,listTables,writeRecords, createScheduledQuery,deleteScheduledQuery,executeScheduledQuery,updateScheduledQuery, describeScheduledQuery,listScheduledQueries,prepareQuery,query,cancelQuery.

Enum values:

-   describeEndpoints
    
-   createBatchLoadTask
    
-   describeBatchLoadTask
    
-   resumeBatchLoadTask
    
-   listBatchLoadTasks
    
-   createDatabase
    
-   deleteDatabase
    
-   describeDatabase
    
-   updateDatabase
    
-   listDatabases
    
-   createTable
    
-   deleteTable
    
-   describeTable
    
-   updateTable
    
-   listTables
    
-   writeRecords
    
-   createScheduledQuery
    
-   deleteScheduledQuery
    
-   executeScheduledQuery
    
-   updateScheduledQuery
    
-   describeScheduledQuery
    
-   listScheduledQueries
    
-   prepareQuery
    
-   query
    
-   cancelQuery
    





 |  | Timestream2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which the Timestream client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   eu-isoe-west-1
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   ca-west-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Timestream client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Timestream client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **awsTimestreamQueryClient** (advanced) | **Autowired** To use an existing configured AwsTimestreamQueryClient client. |  | TimestreamQueryClient |
| **awsTimestreamWriteClient** (advanced) | **Autowired** To use an existing configured AwsTimestreamWriteClient client. |  | TimestreamWriteClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Timestream client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Timestream client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Timestream client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **useSessionCredentials** (security) | Set whether the Timestream client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Timestream. | false | boolean |

## Message Headers

The AWS Timestream component supports 38 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsTimestreamOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsTimestreamRecord** (producer) Constant: [`RECORD`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#RECORD) | Represents a time-series data point being written into Timestream. |  | Record |
| **CamelAwsTimestreamRecordList** (producer) Constant: [`RECORD_LIST`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#RECORD_LIST) | List of Records. |  | List |
| **CamelAwsTimestreamTaskStatus** (producer) Constant: [`TASK_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#TASK_STATUS) | Status of Batch Load Task. |  | String |
| **CamelAwsTimestreamTaskId** (producer) Constant: [`TASK_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#TASK_ID) | The ID of the batch load task to resume. |  | String |
| **CamelAwsTimestreamDatabaseName** (producer) Constant: [`DATABASE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#DATABASE_NAME) | Name of Database. |  | String |
| **CamelAwsTimestreamTableName** (producer) Constant: [`TABLE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#TABLE_NAME) | Name of Table. |  | String |
| **CamelAwsTimestreamTargetDatabaseName** (producer) Constant: [`TARGET_DATABASE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#TARGET_DATABASE_NAME) | Name of Target Database. |  | String |
| **CamelAwsTimestreamTargetTableName** (producer) Constant: [`TARGET_TABLE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#TARGET_TABLE_NAME) | Name of Target Table. |  | String |
| **CamelAwsTimestreamRecordVersion** (producer) Constant: [`RECORD_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#RECORD_VERSION) | Record version. |  | String |
| **CamelAwsTimestreamDataModelConfiguration** (producer) Constant: [`DATA_MODEL_CONFIGURATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#DATA_MODEL_CONFIGURATION) | Configuration of Data Model. |  | DataModelConfiguration |
| **CamelAwsTimestreamDataSourceConfiguration** (producer) Constant: [`DATA_SOURCE_CONFIGURATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#DATA_SOURCE_CONFIGURATION) | Configuration of Data Source. |  | DataSourceConfiguration |
| **CamelAwsTimestreamReportConfiguration** (producer) Constant: [`REPORT_CONFIGURATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#REPORT_CONFIGURATION) | Reporting Configuration. |  | ReportConfiguration |
| **CamelAwsTimestreamTableSchema** (producer) Constant: [`SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#SCHEMA) | Timestream Table Schema. |  | Schema |
| **CamelAwsTimestreamRetentionProperties** (producer) Constant: [`RETENTION_PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#RETENTION_PROPERTIES) | Timestream Table Retention Properties. |  | RetentionProperties |
| **CamelAwsTimestreamMagneticStoreWriteProperties** (producer) Constant: [`MAGNETIC_STORE_WRITE_PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#MAGNETIC_STORE_WRITE_PROPERTIES) | Timestream Table Magentic Store Write properties. |  | MagneticStoreWriteProperties |
| **CamelAwsTimestreamTimeColumn** (producer) Constant: [`TIME_COLUMN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#TIME_COLUMN) | Name of Time column. |  | String |
| **CamelAwsTimestreamMeasureColumnName** (producer) Constant: [`MEASURE_NAME_COLUMN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#MEASURE_NAME_COLUMN) | Name of the measure column. |  | String |
| **CamelAwsTimestreamDimensionMappingList** (producer) Constant: [`DIMENSION_MAPPING_LIST`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#DIMENSION_MAPPING_LIST) | This is to allow mapping column(s) from the query result to the dimension in the destination table. |  | List |
| **CamelAwsTimestreamMultiMeasureMappings** (producer) Constant: [`MULTI_MEASURE_MAPPINGS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#MULTI_MEASURE_MAPPINGS) | Multi-measure mappings. |  | MultiMeasureMappings |
| **CamelAwsTimestreamMixedMeasureMappingList** (producer) Constant: [`MIXED_MEASURE_MAPPING_LIST`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#MIXED_MEASURE_MAPPING_LIST) | Specifies how to map measures to multi-measure records. |  | List |
| **CamelAwsTimestreamScheduledQueryName** (producer) Constant: [`SCHEDULED_QUERY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#SCHEDULED_QUERY_NAME) | Name of scheduled query. |  | String |
| **CamelAwsTimestreamScheduledQueryArn** (producer) Constant: [`SCHEDULED_QUERY_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#SCHEDULED_QUERY_ARN) | Arn of scheduled query. |  | String |
| **CamelAwsTimestreamScheduledQueryState** (producer) Constant: [`SCHEDULED_QUERY_STATE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#SCHEDULED_QUERY_STATE) | State of scheduled query. |  | String |
| **CamelAwsTimestreamScheduledQueryInvocationTime** (producer) Constant: [`SCHEDULED_QUERY_INVOCATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#SCHEDULED_QUERY_INVOCATION_TIME) | Invocation Time for scheduled query execution. |  | Instant |
| **CamelAwsTimestreamQueryString** (producer) Constant: [`QUERY_STRING`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#QUERY_STRING) | The query string to run. |  | String |
| **CamelAwsTimestreamQueryId** (producer) Constant: [`QUERY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#QUERY_ID) | ID of query. |  | String |
| **CamelAwsTimestreamQueryValidateOnly** (producer) Constant: [`QUERY_VALIDATE_ONLY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#QUERY_VALIDATE_ONLY) | Validates the prepared query, but does not store for later execution. |  | Boolean |
| **CamelAwsTimestreamQueryMaxRows** (producer) Constant: [`QUERY_MAX_ROWS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#QUERY_MAX_ROWS) | The total number of rows to be returned in the Query output. |  | Integer |
| **CamelAwsTimestreamMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#MAX_RESULTS) | Max Results to be returned in output. |  | Integer |
| **CamelAwsTimestreamScheduleExpression** (producer) Constant: [`SCHEDULE_EXPRESSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#SCHEDULE_EXPRESSION) | The schedule expression for the query. |  | String |
| **CamelAwsTimestreamNotificationTopicArn** (producer) Constant: [`NOTIFICATION_TOPIC_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#NOTIFICATION_TOPIC_ARN) | Notification Topic Arn for the scheduled query. |  | String |
| **CamelAwsTimestreamErrorReportS3BucketName** (producer) Constant: [`ERROR_REPORT_S3_BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#ERROR_REPORT_S3_BUCKET_NAME) | S3 Bucket name for error reporting. |  | String |
| **CamelAwsTimestreamErrorReportS3ObjectKeyPrefix** (producer) Constant: [`ERROR_REPORT_S3_OBJECT_KEY_PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#ERROR_REPORT_S3_OBJECT_KEY_PREFIX) | S3 object key prefix for error reporting. |  | String |
| **CamelAwsTimestreamErrorReportS3EncryptionOption** (producer) Constant: [`ERROR_REPORT_S3_ENCRYPTION_OPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#ERROR_REPORT_S3_ENCRYPTION_OPTION) | S3 encryption option for error reporting. |  | String |
| **CamelAwsTimestreamScheduledQueryExecutionRoleArn** (producer) Constant: [`SCHEDULED_QUERY_EXECUTION_ROLE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#SCHEDULED_QUERY_EXECUTION_ROLE_ARN) | he ARN for the IAM role that Timestream will assume when running the scheduled query. |  | String |
| **CamelAwsTimestreamClientToken** (producer) Constant: [`CLIENT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#CLIENT_TOKEN) | Using a ClientToken makes the call to CreateScheduledQuery idempotent. |  | String |
| **CamelAwsTimestreamKmsKeyId** (producer) Constant: [`KMS_KEY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-timestream/latest/org/apache/camel/component/aws2/timestream/Timestream2Constants.html#KMS_KEY_ID) | The Amazon KMS key used to encrypt the scheduled query resource, at-rest. |  | String |

Required Timestream component options

Based on the type of operation to be performed, the type of client (write/query) needs to be provided as clientType URI path parameter

You have to provide either the awsTimestreamWriteClient(for write operations) or awsTimestreamQueryClient(for query operations) in the Registry or your accessKey and secretKey to access the [AWS Timestream](https://aws.amazon.com/timestream/) service.

## Usage

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Timestream Producer operations

Camel-AWS Timestream component provides the following operation on the producer side:

-   Write Operations
    
    -   describeEndpoints
        
    -   createBatchLoadTask
        
    -   describeBatchLoadTask
        
    -   resumeBatchLoadTask
        
    -   listBatchLoadTasks
        
    -   createDatabase
        
    -   deleteDatabase
        
    -   describeDatabase
        
    -   updateDatabase
        
    -   listDatabases
        
    -   createTable
        
    -   deleteTable
        
    -   describeTable
        
    -   updateTable
        
    -   listTables
        
    -   writeRecords
        
    
-   Query Operations
    
    -   describeEndpoints
        
    -   createScheduledQuery
        
    -   deleteScheduledQuery
        
    -   executeScheduledQuery
        
    -   updateScheduledQuery
        
    -   describeScheduledQuery
        
    -   listScheduledQueries
        
    -   prepareQuery
        
    -   query
        
    -   cancelQuery
        
    

## Examples

### Producer Examples

-   Write Operation
    
    -   createDatabase: this operation will create a timestream database
        
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createDatabase")
    .setHeader(Timestream2Constants.DATABASE_NAME, constant("testDb"))
    .setHeader(Timestream2Constants.KMS_KEY_ID, constant("testKmsKey"))
    .to("aws2-timestream://write:test?awsTimestreamWriteClient=#awsTimestreamWriteClient&operation=createDatabase");
```

```xml
<route>
    <from uri="direct:createDatabase"/>
    <setHeader name="CamelAwsTimestreamDatabaseName">
        <constant>testDb</constant>
    </setHeader>
    <setHeader name="CamelAwsTimestreamKmsKeyId">
        <constant>testKmsKey</constant>
    </setHeader>
    <to uri="aws2-timestream://write:test?awsTimestreamWriteClient=#awsTimestreamWriteClient&amp;operation=createDatabase"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createDatabase
    steps:
      - setHeader:
          name: CamelAwsTimestreamDatabaseName
          constant: testDb
      - setHeader:
          name: CamelAwsTimestreamKmsKeyId
          constant: testKmsKey
      - to:
          uri: aws2-timestream://write:test
          parameters:
            awsTimestreamWriteClient: "#awsTimestreamWriteClient"
            operation: createDatabase
```

-   Query Operation
    
    -   query: this operation will execute a timestream query
        
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:query")
    .setHeader(Timestream2Constants.QUERY_STRING, constant("SELECT * FROM testDb.testTable ORDER BY time DESC LIMIT 10"))
    .to("aws2-timestream://query:test?awsTimestreamQueryClient=#awsTimestreamQueryClient&operation=query");
```

```xml
<route>
    <from uri="direct:query"/>
    <setHeader name="CamelAwsTimestreamQueryString">
        <constant>SELECT * FROM testDb.testTable ORDER BY time DESC LIMIT 10</constant>
    </setHeader>
    <to uri="aws2-timestream://query:test?awsTimestreamQueryClient=#awsTimestreamQueryClient&amp;operation=query"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:query
    steps:
      - setHeader:
          name: CamelAwsTimestreamQueryString
          constant: "SELECT * FROM testDb.testTable ORDER BY time DESC LIMIT 10"
      - to:
          uri: aws2-timestream://query:test
          parameters:
            awsTimestreamQueryClient: "#awsTimestreamQueryClient"
            operation: query
```

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as the body. In AWS Timestream there are multiple operations you can submit, as an example for Create state machine request, you can do something like:

-   Write Operation
    
    -   createDatabase: this operation will create a timestream database
        
    

_Java-only: uses AWS SDK POJO request builder as message body_

```java
from("direct:start")
  .setBody(CreateDatabaseRequest.builder().database(Database.builder().databaseName("testDb").kmsKeyId("testKmsKey").build()).build())
  .to("aws2-timestream://write:test?awsTimestreamWriteClient=#awsTimestreamWriteClient&operation=createDatabase&pojoRequest=true")
```

-   Query Operation
    
    -   query: this operation will execute a timestream query
        
    

_Java-only: uses AWS SDK POJO request builder as message body_

```java
from("direct:query")
    .setBody(QueryRequest.builder().queryString("SELECT * FROM testDb.testTable ORDER BY time DESC LIMIT 10").build())
    .to("aws2-timestream://query:test?awsTimestreamQueryClient=#awsTimestreamQueryClient&operation=query&pojoRequest=true")
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-timestream</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.