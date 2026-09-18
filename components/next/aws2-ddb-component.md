# AWS DynamoDB

**Since Camel 3.1**

**Only producer is supported**

The AWS2 DynamoDB component supports storing and retrieving data from/to [Amazon’s DynamoDB](https://aws.amazon.com/dynamodb) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon DynamoDB. More information is available at [Amazon DynamoDB](https://aws.amazon.com/dynamodb).

## URI Format

aws2-ddb://domainName\[?options\]

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

The AWS DynamoDB component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The component configuration. |  | Ddb2Configuration |
| **consistentRead** (producer) | Determines whether strong consistency should be enforced when data is read. | false | boolean |
| **enabledInitialDescribeTable** (producer) | Set whether the initial Describe table operation in the DDB Endpoint must be done, or not. | true | boolean |
| **keyAttributeName** (producer) | Attribute name when creating table. |  | String |
| **keyAttributeType** (producer) | Attribute type when creating table. |  | String |
| **keyScalarType** (producer) | The key scalar type, it can be S (String), N (Number) and B (Bytes). |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
What operation to perform.

Enum values:

-   BatchGetItems
    
-   BatchWriteItems
    
-   BatchExecuteStatement
    
-   DeleteItem
    
-   DeleteTable
    
-   DescribeTable
    
-   ExecuteStatement
    
-   GetItem
    
-   PutItem
    
-   Query
    
-   Scan
    
-   TransactGetItems
    
-   TransactWriteItems
    
-   UpdateItem
    
-   UpdateTable
    





 | PutItem | Ddb2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **readCapacity** (producer) | The provisioned throughput to reserve for reading resources from your table. |  | Long |
| **region** (producer) | 

The region in which DDB client needs to work.

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
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **writeCapacity** (producer) | The provisioned throughput to reserved for writing resources to your table. |  | Long |
| **amazonDDBClient** (advanced) | **Autowired** To use the AmazonDynamoDB as the client. |  | DynamoDbClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the DDB client. |  | String |
| **proxyPort** (proxy) | The region in which DynamoDB client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the DDB client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the DDB client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the DDB client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in DDB. | false | boolean |

## Endpoint Options

The AWS DynamoDB endpoint is configured using URI syntax:

aws2-ddb:tableName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **tableName** (producer) | **Required** The name of the table currently worked with. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **consistentRead** (producer) | Determines whether strong consistency should be enforced when data is read. | false | boolean |
| **enabledInitialDescribeTable** (producer) | Set whether the initial Describe table operation in the DDB Endpoint must be done, or not. | true | boolean |
| **keyAttributeName** (producer) | Attribute name when creating table. |  | String |
| **keyAttributeType** (producer) | Attribute type when creating table. |  | String |
| **keyScalarType** (producer) | The key scalar type, it can be S (String), N (Number) and B (Bytes). |  | String |
| **operation** (producer) | 
What operation to perform.

Enum values:

-   BatchGetItems
    
-   BatchWriteItems
    
-   BatchExecuteStatement
    
-   DeleteItem
    
-   DeleteTable
    
-   DescribeTable
    
-   ExecuteStatement
    
-   GetItem
    
-   PutItem
    
-   Query
    
-   Scan
    
-   TransactGetItems
    
-   TransactWriteItems
    
-   UpdateItem
    
-   UpdateTable
    





 | PutItem | Ddb2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **readCapacity** (producer) | The provisioned throughput to reserve for reading resources from your table. |  | Long |
| **region** (producer) | 

The region in which DDB client needs to work.

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
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **writeCapacity** (producer) | The provisioned throughput to reserved for writing resources to your table. |  | Long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **amazonDDBClient** (advanced) | **Autowired** To use the AmazonDynamoDB as the client. |  | DynamoDbClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the DDB client. |  | String |
| **proxyPort** (proxy) | The region in which DynamoDB client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the DDB client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the DDB client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the DDB client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in DDB. | false | boolean |

## Message Headers

The AWS DynamoDB component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsDdbAttributes** (DeleteItem GetItem PutItem UpdateItem) Constant: [`ATTRIBUTES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#ATTRIBUTES) | The list of attributes returned by the operation. |  | Map |
| **CamelAwsDdbAttributeNames** (producer) Constant: [`ATTRIBUTE_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#ATTRIBUTE_NAMES) | If attribute names are not specified then all attributes will be returned. |  | Collection |
| **CamelAwsDdbBatchItems** (producer) Constant: [`BATCH_ITEMS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#BATCH_ITEMS) | A map of the table name and corresponding items to get by primary key. |  | Map |
| **CamelAwsDdbBatchResponse** (BatchGetItems) Constant: [`BATCH_RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#BATCH_RESPONSE) | Table names and the respective item attributes from the tables. |  | Map |
| **CamelAwsDdbConsistentRead** (producer) Constant: [`CONSISTENT_READ`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#CONSISTENT_READ) | If set to true, then a consistent read is issued, otherwise eventually consistent is used. |  | Boolean |
| **CamelAwsDdbConsumedCapacity** (Query Scan) Constant: [`CONSUMED_CAPACITY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#CONSUMED_CAPACITY) | The number of Capacity Units of the provisioned throughput of the table consumed during the operation. |  | Double |
| **CamelAwsDdbCount** (Query Scan) Constant: [`COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#COUNT) | Number of items in the response. |  | Integer |
| **CamelAwsDdbCreationDate** (DeleteTable DescribeTable) Constant: [`CREATION_DATE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#CREATION_DATE) | Creation DateTime of this table. |  | Date |
| **CamelAwsDdbIndexName** (producer) Constant: [`INDEX_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#INDEX_NAME) | If set will be used as Secondary Index for Query operation. |  | String |
| **CamelAwsDdbItem** (producer) Constant: [`ITEM`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#ITEM) | A map of the attributes for the item, and must include the primary key values that define the item. |  | Map |
| **CamelAwsDdbItems** (Query Scan) Constant: [`ITEMS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#ITEMS) | The list of attributes returned by the operation. |  | List |
| **CamelAwsDdbTableItemCount** (DeleteTable DescribeTable) Constant: [`ITEM_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#ITEM_COUNT) | Item count for this table. |  | Long |
| **CamelAwsDdbKey** (producer) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#KEY) | The primary key that uniquely identifies each item in a table. |  | Map |
| **CamelAwsDdbKeyConditions** (producer) Constant: [`KEY_CONDITIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#KEY_CONDITIONS) | This header specify the selection criteria for the query, and merge together the two old headers CamelAwsDdbHashKeyValue and CamelAwsDdbScanRangeKeyCondition. |  | Map |
| **CamelAwsDdbKeySchema** (DeleteTable DescribeTable) Constant: [`KEY_SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#KEY_SCHEMA) | The KeySchema that identifies the primary key for this table. From Camel 2.16.0 the type of this header is List and not KeySchema. |  | List |
| **CamelAwsDdbLastEvaluatedKey** (Query Scan) Constant: [`LAST_EVALUATED_KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#LAST_EVALUATED_KEY) | Primary key of the item where the query operation stopped, inclusive of the previous result set. |  | Key |
| **CamelAwsDdbIsTruncated** (Query Scan) Constant: [`IS_TRUNCATED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#IS_TRUNCATED) | Whether the response has more results (is truncated). If true, use LAST\_EVALUATED\_KEY as START\_KEY for the next page. |  | Boolean |
| **CamelAwsDdbLimit** (producer) Constant: [`LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#LIMIT) | The maximum number of items to return. |  | Integer |
| **CamelAwsDdbOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#OPERATION) | 
The operation to perform.

Enum values:

-   BatchGetItems
    
-   BatchWriteItems
    
-   BatchExecuteStatement
    
-   DeleteItem
    
-   DeleteTable
    
-   DescribeTable
    
-   ExecuteStatement
    
-   GetItem
    
-   PutItem
    
-   Query
    
-   Scan
    
-   TransactGetItems
    
-   TransactWriteItems
    
-   UpdateItem
    
-   UpdateTable
    





 |  | Ddb2Operations |
| **CamelAwsDdbProvisionedThroughput** (DeleteTable DescribeTable) Constant: [`PROVISIONED_THROUGHPUT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#PROVISIONED_THROUGHPUT) | The value of the ProvisionedThroughput property for this table. |  | ProvisionedThroughputDescription |
| **CamelAwsDdbReadCapacity** (UpdateTable DescribeTable) Constant: [`READ_CAPACITY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#READ_CAPACITY) | ReadCapacityUnits property of this table. |  | Long |
| **CamelAwsDdbReturnValues** (producer) Constant: [`RETURN_VALUES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#RETURN_VALUES) | Use this parameter if you want to get the attribute name-value pairs before or after they are modified(NONE, ALL\_OLD, UPDATED\_OLD, ALL\_NEW, UPDATED\_NEW). |  | String |
| **CamelAwsDdbScannedCount** (Scan) Constant: [`SCANNED_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#SCANNED_COUNT) | Number of items in the complete scan before any filters are applied. |  | Integer |
| **CamelAwsDdbScanIndexForward** (producer) Constant: [`SCAN_INDEX_FORWARD`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#SCAN_INDEX_FORWARD) | Specifies forward or backward traversal of the index. |  | Boolean |
| **CamelAwsDdbScanFilter** (producer) Constant: [`SCAN_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#SCAN_FILTER) | Evaluates the scan results and returns only the desired values. |  | Map |
| **CamelAwsDdbStartKey** (producer) Constant: [`START_KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#START_KEY) | Primary key of the item from which to continue an earlier query. |  | Map |
| **CamelAwsDdbTableName** (producer) Constant: [`TABLE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#TABLE_NAME) | Table Name for this operation. |  | String |
| **CamelAwsDdbTableSize** (DeleteTable DescribeTable) Constant: [`TABLE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#TABLE_SIZE) | The table size in bytes. |  | Long |
| **CamelAwsDdbTableStatus** (DeleteTable DescribeTable) Constant: [`TABLE_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#TABLE_STATUS) | The status of the table: CREATING, UPDATING, DELETING, ACTIVE. |  | String |
| **CamelAwsDdbUpdateCondition** (producer) Constant: [`UPDATE_CONDITION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#UPDATE_CONDITION) | Designates an attribute for a conditional modification. |  | Map |
| **CamelAwsDdbUpdateValues** (producer) Constant: [`UPDATE_VALUES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#UPDATE_VALUES) | Map of attribute name to the new value and action for the update. |  | Map |
| **CamelAwsDdbUnprocessedKeys** (BatchGetItems) Constant: [`UNPROCESSED_KEYS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#UNPROCESSED_KEYS) | Contains a map of tables and their respective keys that were not processed with the current response. |  | Map |
| **CamelAwsDdbWriteCapacity** (UpdateTable DescribeTable) Constant: [`WRITE_CAPACITY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#WRITE_CAPACITY) | WriteCapacityUnits property of this table. |  | Long |
| **CamelAwsDdbStatement** (ExecuteStatement) Constant: [`STATEMENT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#STATEMENT) | A PartiQL statement that uses parameters. |  | String |
| **CamelAwsDdbStatementParameters** (ExecuteStatement) Constant: [`STATEMENT_PARAMETERS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#STATEMENT_PARAMETERS) | The parameters for the PartiQL statement, if any. |  | List |
| **CamelAwsDdbBatchStatements** (BatchExecuteStatement) Constant: [`BATCH_STATEMENTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#BATCH_STATEMENTS) | The list of PartiQL statements representing the batch to run. |  | List |
| **CamelAwsDdbExecuteStatementItems** (ExecuteStatement) Constant: [`EXECUTE_STATEMENT_ITEMS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#EXECUTE_STATEMENT_ITEMS) | The response items from an ExecuteStatement operation. |  | List |
| **CamelAwsDdbBatchStatementResponse** (BatchExecuteStatement) Constant: [`BATCH_STATEMENT_RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#BATCH_STATEMENT_RESPONSE) | The response to each PartiQL statement in the batch. |  | List |
| **CamelAwsDdbTransactWriteItems** (TransactWriteItems) Constant: [`TRANSACT_WRITE_ITEMS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#TRANSACT_WRITE_ITEMS) | The list of TransactWriteItem objects for a transactional write. |  | List |
| **CamelAwsDdbTransactClientRequestToken** (TransactWriteItems) Constant: [`TRANSACT_CLIENT_REQUEST_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#TRANSACT_CLIENT_REQUEST_TOKEN) | A unique client request token for idempotent TransactWriteItems calls. |  | String |
| **CamelAwsDdbTransactWriteConsumedCapacity** (TransactWriteItems) Constant: [`TRANSACT_WRITE_CONSUMED_CAPACITY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#TRANSACT_WRITE_CONSUMED_CAPACITY) | The consumed capacity from a TransactWriteItems operation. |  | List |
| **CamelAwsDdbTransactWriteItemCollectionMetrics** (TransactWriteItems) Constant: [`TRANSACT_WRITE_ITEM_COLLECTION_METRICS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#TRANSACT_WRITE_ITEM_COLLECTION_METRICS) | The item collection metrics from a TransactWriteItems operation. |  | Map |
| **CamelAwsDdbTransactGetItems** (TransactGetItems) Constant: [`TRANSACT_GET_ITEMS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#TRANSACT_GET_ITEMS) | The list of TransactGetItem objects for a transactional read. |  | List |
| **CamelAwsDdbTransactGetResponse** (TransactGetItems) Constant: [`TRANSACT_GET_RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#TRANSACT_GET_RESPONSE) | The response from a TransactGetItems operation. |  | List |
| **CamelAwsDdbBatchWriteItems** (BatchWriteItems) Constant: [`BATCH_WRITE_ITEMS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#BATCH_WRITE_ITEMS) | A map of table names to lists of WriteRequest objects for batch writes. |  | Map |
| **CamelAwsDdbBatchWriteUnprocessedItems** (BatchWriteItems) Constant: [`BATCH_WRITE_UNPROCESSED_ITEMS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#BATCH_WRITE_UNPROCESSED_ITEMS) | A map of tables and their respective unprocessed items after a BatchWriteItems operation. |  | Map |
| **CamelAwsDdbFilterExpression** (Query Scan) Constant: [`FILTER_EXPRESSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#FILTER_EXPRESSION) | The Filter Expression. |  | String |
| **CamelAwsDdbFilterExpressionAttributeNames** (Query Scan) Constant: [`FILTER_EXPRESSION_ATTRIBUTE_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#FILTER_EXPRESSION_ATTRIBUTE_NAMES) | The Filter Expression Attribute Names. |  | Map |
| **CamelAwsDdbFilterExpressionAttributeValues** (Query Scan) Constant: [`FILTER_EXPRESSION_ATTRIBUTE_VALUES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#FILTER_EXPRESSION_ATTRIBUTE_VALUES) | The Filter Expression Attribute Values. |  | Map |
| **CamelAwsDdbProjectExpression** (Query Scan) Constant: [`PROJECT_EXPRESSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#PROJECT_EXPRESSION) | The Project Expression. |  | String |

Required DDB component options

You have to provide the amazonDDBClient in the Registry or your accessKey and secretKey to access the [Amazon’s DynamoDB](https://aws.amazon.com/dynamodb).

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

### Advanced AmazonDynamoDB configuration

If you need more control over the `AmazonDynamoDB` instance configuration you can create your own instance and refer to it from the URI:

_Java-only: programmatic `DynamoDbClient` configuration and registry binding_

```java
DynamoDbClient client = DynamoDbClient.builder()
    .region(Region.AP_SOUTHEAST_2)
    .credentialsProvider(StaticCredentialsProvider.create(AwsBasicCredentials.create(accessKey, secretKey)))
    .build();

getCamelContext().getRegistry().bind("client", client);

from("direct:start")
    .to("aws2-ddb://domainName?amazonDDBClient=#client");
```

The `#client` refers to a `DynamoDbClient` in the Registry.

### Supported producer operations

-   BatchGetItems
    
-   BatchWriteItems
    
-   BatchExecuteStatement
    
-   DeleteItem
    
-   DeleteTable
    
-   DescribeTable
    
-   ExecuteStatement
    
-   GetItem
    
-   PutItem
    
-   Query
    
-   Scan
    
-   TransactGetItems
    
-   TransactWriteItems
    
-   UpdateItem
    
-   UpdateTable
    

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-ddb</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Examples

### Producer Examples

-   PutItem: this operation will create an entry into DynamoDB
    

_Java-only: uses AWS SDK `AttributeValue` builders and variable table name_

```java
Map<String, AttributeValue> attributeMap = new HashMap<>();
attributeMap.put("partitionKey", AttributeValue.builder().s("3000").build());
attributeMap.put("id", AttributeValue.builder().s("1001").build());
attributeMap.put("barcode", AttributeValue.builder().s("9002811220001").build());

from("direct:start")
  .setHeader("CamelAwsDdbOperation",  constant("PutItem"))
  .setHeader("CamelAwsDdbConsistentRead", constant("true"))
  .setHeader("CamelAwsDdbReturnValues", constant("ALL_OLD"))
  .setHeader("CamelAwsDdbItem", constant(attributeMap))
  .setHeader("CamelAwsDdbAttributeNames", constant(attributeMap.keySet()))
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client");
```

-   UpdateItem: this operation will update an entry into DynamoDB
    

_Java-only: uses AWS SDK `AttributeValue` and `AttributeValueUpdate` builders_

```java
Map<String, AttributeValueUpdate> attributeMap = new HashMap<>();
attributeMap.put("partitionKey", AttributeValueUpdate.builder().value(AttributeValue.builder().s("3000").build()).build());
attributeMap.put("sortKey",  AttributeValueUpdate.builder().value(AttributeValue.builder().s("1001").build()).build());
attributeMap.put("borcode",  AttributeValueUpdate.builder().value(AttributeValue.builder().s("900281122").build()).build());

Map<String, AttributeValue> keyMap = new HashMap<>();
keyMap.put("partitionKey", AttributeValue.builder().s("3000").build());
keyMap.put("sortKey", AttributeValue.builder().s("1001").build());

from("direct:start")
  .setHeader("CamelAwsDdbOperation",  constant("UpdateItem"))
  .setHeader("CamelAwsDdbUpdateValues",  constant(attributeMap))
  .setHeader("CamelAwsDdbKey",  constant(keyMap))
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client");
```

-   GetItem: this operation will retrieve an entry from DynamoDB
    

_Java-only: uses `Processor` with AWS SDK `AttributeValue` builders_

```java
from("direct:get")
  .process(exchange -> {
      final Map<String, AttributeValue> keyMap = new HashMap<>();
      keyMap.put("table-key", AttributeValue.builder().s("1").build());

      exchange.getIn().setHeader("CamelAwsDdbOperation", "GetItem");
      exchange.getIn().setHeader("CamelAwsDdbAttributeNames", constant(List.of("table-key", "message")));
      exchange.getIn().setHeader("CamelAwsDdbKey", keyMap);
  })
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client&consistentRead=true");
```

-   DeleteItem: this operation will delete an entry from DynamoDB
    

_Java-only: uses `Processor` with AWS SDK `AttributeValue` builders_

```java
from("direct:delete")
  .process(exchange -> {
      final Map<String, AttributeValue> keyMap = new HashMap<>();
      keyMap.put("table-key", AttributeValue.builder().s("1").build());

      exchange.getIn().setHeader("CamelAwsDdbOperation", "DeleteItem");
      exchange.getIn().setHeader("CamelAwsDdbKey", keyMap);
  })
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client&consistentRead=true");
```

-   ExecuteStatement (PartiQL): this operation runs a PartiQL statement against DynamoDB
    

_Java-only: uses `Processor` with AWS SDK `AttributeValue` builders_

```java
from("direct:partiql")
  .process(exchange -> {
      exchange.getIn().setHeader("CamelAwsDdbOperation", "ExecuteStatement");
      exchange.getIn().setHeader("CamelAwsDdbStatement",
          "SELECT * FROM \"MyTable\" WHERE \"key\" = ?");
      exchange.getIn().setHeader("CamelAwsDdbStatementParameters",
          List.of(AttributeValue.builder().s("myKeyValue").build()));
      exchange.getIn().setHeader("CamelAwsDdbConsistentRead", true);
  })
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client");
```

-   BatchExecuteStatement (PartiQL batch): this operation runs multiple PartiQL statements in a batch
    

_Java-only: uses `Processor` with AWS SDK `BatchStatementRequest` builders_

```java
from("direct:batchPartiql")
  .process(exchange -> {
      exchange.getIn().setHeader("CamelAwsDdbOperation", "BatchExecuteStatement");
      exchange.getIn().setHeader("CamelAwsDdbBatchStatements", List.of(
          BatchStatementRequest.builder()
              .statement("INSERT INTO \"MyTable\" VALUE {'key': 'k1', 'data': 'v1'}")
              .build(),
          BatchStatementRequest.builder()
              .statement("INSERT INTO \"MyTable\" VALUE {'key': 'k2', 'data': 'v2'}")
              .build()));
  })
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client");
```

-   TransactWriteItems: this operation performs a transactional write across one or more tables
    

_Java-only: uses `Processor` with AWS SDK `TransactWriteItem` builders_

```java
Map<String, AttributeValue> item = new HashMap<>();
item.put("key", AttributeValue.builder().s("txKey").build());
item.put("data", AttributeValue.builder().s("txValue").build());

from("direct:transactWrite")
  .process(exchange -> {
      exchange.getIn().setHeader("CamelAwsDdbOperation", "TransactWriteItems");
      exchange.getIn().setHeader("CamelAwsDdbTransactWriteItems", List.of(
          TransactWriteItem.builder()
              .put(Put.builder().tableName("MyTable").item(item).build())
              .build()));
  })
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client");
```

-   TransactGetItems: this operation performs a transactional read across one or more tables
    

_Java-only: uses `Processor` with AWS SDK `TransactGetItem` builders_

```java
Map<String, AttributeValue> key = new HashMap<>();
key.put("key", AttributeValue.builder().s("txKey").build());

from("direct:transactGet")
  .process(exchange -> {
      exchange.getIn().setHeader("CamelAwsDdbOperation", "TransactGetItems");
      exchange.getIn().setHeader("CamelAwsDdbTransactGetItems", List.of(
          TransactGetItem.builder()
              .get(Get.builder().tableName("MyTable").key(key).build())
              .build()));
  })
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client");
```

-   BatchWriteItems: this operation puts or deletes multiple items in one or more tables in a single batch
    

_Java-only: uses AWS SDK `WriteRequest` and `PutRequest` builders_

```java
Map<String, AttributeValue> item1 = new HashMap<>();
item1.put("key", AttributeValue.builder().s("bk1").build());
item1.put("data", AttributeValue.builder().s("bv1").build());

Map<String, List<WriteRequest>> requestItems = new HashMap<>();
requestItems.put("MyTable", List.of(
    WriteRequest.builder()
        .putRequest(PutRequest.builder().item(item1).build())
        .build()));

from("direct:batchWrite")
  .process(exchange -> {
      exchange.getIn().setHeader("CamelAwsDdbOperation", "BatchWriteItems");
      exchange.getIn().setHeader("CamelAwsDdbBatchWriteItems", requestItems);
  })
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client");
```