# AWS DynamoDB

**Since Camel 3.1**

**Only producer is supported**

The AWS2 DynamoDB component supports storing and retrieving data from/to [Amazon’s DynamoDB](https://aws.amazon.com/dynamodb) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon DynamoDB. More information is available at [Amazon DynamoDB](https://aws.amazon.com/dynamodb).

## URI Format

aws2-ddb://domainName\[?options\]

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

The AWS DynamoDB component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonDDBClient** (producer) | **Autowired** To use the AmazonDynamoDB as the client. |  | DynamoDbClient |
| **configuration** (producer) | The component configuration. |  | Ddb2Configuration |
| **consistentRead** (producer) | Determines whether or not strong consistency should be enforced when data is read. | false | boolean |
| **enabledInitialDescribeTable** (producer) | Set whether the initial Describe table operation in the DDB Endpoint must be done, or not. | true | boolean |
| **keyAttributeName** (producer) | Attribute name when creating table. |  | String |
| **keyAttributeType** (producer) | Attribute type when creating table. |  | String |
| **keyScalarType** (producer) | The key scalar type, it can be S (String), N (Number) and B (Bytes). |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
What operation to perform.

Enum values:

-   BatchGetItems
    
-   DeleteItem
    
-   DeleteTable
    
-   DescribeTable
    
-   GetItem
    
-   PutItem
    
-   Query
    
-   Scan
    
-   UpdateItem
    
-   UpdateTable
    





 | PutItem | Ddb2Operations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the DDB client. |  | String |
| **proxyPort** (producer) | The region in which DynamoDB client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the DDB client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **readCapacity** (producer) | The provisioned throughput to reserve for reading resources from your table. |  | Long |
| **region** (producer) | The region in which DDB client needs to work. |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **writeCapacity** (producer) | The provisioned throughput to reserved for writing resources to your table. |  | Long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS DynamoDB endpoint is configured using URI syntax:

aws2-ddb:tableName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **tableName** (producer) | **Required** The name of the table currently worked with. |  | String |

### Query Parameters (20 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonDDBClient** (producer) | **Autowired** To use the AmazonDynamoDB as the client. |  | DynamoDbClient |
| **consistentRead** (producer) | Determines whether or not strong consistency should be enforced when data is read. | false | boolean |
| **enabledInitialDescribeTable** (producer) | Set whether the initial Describe table operation in the DDB Endpoint must be done, or not. | true | boolean |
| **keyAttributeName** (producer) | Attribute name when creating table. |  | String |
| **keyAttributeType** (producer) | Attribute type when creating table. |  | String |
| **keyScalarType** (producer) | The key scalar type, it can be S (String), N (Number) and B (Bytes). |  | String |
| **operation** (producer) | 
What operation to perform.

Enum values:

-   BatchGetItems
    
-   DeleteItem
    
-   DeleteTable
    
-   DescribeTable
    
-   GetItem
    
-   PutItem
    
-   Query
    
-   Scan
    
-   UpdateItem
    
-   UpdateTable
    





 | PutItem | Ddb2Operations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the DDB client. |  | String |
| **proxyPort** (producer) | The region in which DynamoDB client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the DDB client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **readCapacity** (producer) | The provisioned throughput to reserve for reading resources from your table. |  | Long |
| **region** (producer) | The region in which DDB client needs to work. |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **writeCapacity** (producer) | The provisioned throughput to reserved for writing resources to your table. |  | Long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

Required DDB component options

You have to provide the amazonDDBClient in the Registry or your accessKey and secretKey to access the [Amazon’s DynamoDB](https://aws.amazon.com/dynamodb).

## Usage

### Static credentials vs Default Credential Provider

You have the possibility of avoiding the usage of explicit static credentials, by specifying the useDefaultCredentialsProvider option and set it to true.

-   Java system properties - aws.accessKeyId and aws.secretKey
    
-   Environment variables - AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable AWS\_CONTAINER\_CREDENTIALS\_RELATIVE\_URI is set.
    
-   Amazon EC2 Instance profile credentials.
    

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

## Message Headers

The AWS DynamoDB component supports 32 message header(s), which is/are listed below:

   
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
| **CamelAwsDdbLimit** (producer) Constant: [`LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#LIMIT) | The maximum number of items to return. |  | Integer |
| **CamelAwsDdbOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ddb/latest/org/apache/camel/component/aws2/ddb/Ddb2Constants.html#OPERATION) | 
The operation to perform.

Enum values:

-   BatchGetItems
    
-   DeleteItem
    
-   DeleteTable
    
-   DescribeTable
    
-   GetItem
    
-   PutItem
    
-   Query
    
-   Scan
    
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

### Advanced AmazonDynamoDB configuration

If you need more control over the `AmazonDynamoDB` instance configuration you can create your own instance and refer to it from the URI:

```java
public class MyRouteBuilder extends RouteBuilder {

    private String accessKey = "myaccessKey";
    private String secretKey = "secretKey";

    @Override
    public void configure() throws Exception {

        DynamoDbClient client = DynamoDbClient.builder()
        .region(Region.AP_SOUTHEAST_2)
        .credentialsProvider(StaticCredentialsProvider.create(AwsBasicCredentials.create(accessKey, secretKey)))
        .build();

        getCamelContext().getRegistry().bind("client", client);

    	from("direct:start")
        .to("aws2-ddb://domainName?amazonDDBClient=#client");
    }
}
```

The `#client` refers to a `DynamoDbClient` in the Registry.

## Supported producer operations

-   BatchGetItems
    
-   DeleteItem
    
-   DeleteTable
    
-   DescribeTable
    
-   GetItem
    
-   PutItem
    
-   Query
    
-   Scan
    
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
    

```java
Map<String, AttributeValue> attributeMap = new HashMap<>();
attributeMap.put("partitionKey", AttributeValue.builder().s("3000").build());
attributeMap.put("id", AttributeValue.builder().s("1001").build());
attributeMap.put("barcode", AttributeValue.builder().s("9002811220001").build());

from("direct:start")
  .setHeader(Ddb2Constants.OPERATION,  constant(Ddb2Operations.PutItem))
  .setHeader(Ddb2Constants.CONSISTENT_READ, constant("true"))
  .setHeader(Ddb2Constants.RETURN_VALUES, constant("ALL_OLD"))
  .setHeader(Ddb2Constants.ITEM, constant(attributeMap))
  .setHeader(Ddb2Constants.ATTRIBUTE_NAMES, constant(attributeMap.keySet()))
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client");
```

-   UpdateItem: this operation will update an entry into DynamoDB
    

```java
Map<String, AttributeValueUpdate> attributeMap = new HashMap<>();
attributeMap.put("partitionKey", AttributeValueUpdate.builder().value(AttributeValue.builder().s("3000").build()).build());
attributeMap.put("sortKey",  AttributeValueUpdate.builder().value(AttributeValue.builder().s("1001").build()).build());
attributeMap.put("borcode",  AttributeValueUpdate.builder().value(AttributeValue.builder().s("900281122").build()).build());

Map<String, AttributeValue> keyMap = new HashMap<>();
keyMap.put("partitionKey", AttributeValue.builder().s("3000").build());
keyMap.put("sortKey", AttributeValue.builder().s("1001").build());

from("direct:start")
  .setHeader(Ddb2Constants.OPERATION,  constant(Ddb2Operations.UpdateItem))
  .setHeader(Ddb2Constants.ITEM,  constant(attributeMap))
  .setHeader(Ddb2Constants.KEY,  constant(keyMap))
  .to("aws2-ddb://" + tableName + "?amazonDDBClient=#client");
```

-   GetItem: this operation will retrieve an entry from DynamoDB
    

```java
from("direct:get")
  .process(exchange -> {
      final Map<String, AttributeValue> keyMap = new HashMap<>();
      keyMap.put("table-key", AttributeValue.builder().s("1").build());

      exchange.getIn().setHeader(Ddb2Constants.OPERATION, Ddb2Operations.GetItem);
      exchange.getIn().setHeader(Ddb2Constants.ATTRIBUTE_NAMES, constant(List.of("table-key", "message")));
      exchange.getIn().setHeader(Ddb2Constants.KEY, keyMap);
  })
  .toF("aws2-ddb://%s?amazonDDBClient=#client&consistentRead=true", tableName);
```

-   DeleteItem: this operation will delete an entry from DynamoDB
    

```java
from("direct:delete")
  .process(exchange -> {
      final Map<String, AttributeValue> keyMap = new HashMap<>();
      keyMap.put("table-key", AttributeValue.builder().s("1").build());

      exchange.getIn().setHeader(Ddb2Constants.OPERATION, Ddb2Operations.DeleteItem);
      exchange.getIn().setHeader(Ddb2Constants.KEY, keyMap);
  })
  .toF("aws2-ddb://%s?amazonDDBClient=#client&consistentRead=true", tableName);
```

## Spring Boot Auto-Configuration

When using aws2-ddb with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-ddb-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 40 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-ddb.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-ddb.amazon-d-d-b-client** | To use the AmazonDynamoDB as the client. The option is a software.amazon.awssdk.services.dynamodb.DynamoDbClient type. |  | DynamoDbClient |
| **camel.component.aws2-ddb.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-ddb.configuration** | The component configuration. The option is a org.apache.camel.component.aws2.ddb.Ddb2Configuration type. |  | Ddb2Configuration |
| **camel.component.aws2-ddb.consistent-read** | Determines whether or not strong consistency should be enforced when data is read. | false | Boolean |
| **camel.component.aws2-ddb.enabled** | Whether to enable auto configuration of the aws2-ddb component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-ddb.enabled-initial-describe-table** | Set whether the initial Describe table operation in the DDB Endpoint must be done, or not. | true | Boolean |
| **camel.component.aws2-ddb.key-attribute-name** | Attribute name when creating table. |  | String |
| **camel.component.aws2-ddb.key-attribute-type** | Attribute type when creating table. |  | String |
| **camel.component.aws2-ddb.key-scalar-type** | The key scalar type, it can be S (String), N (Number) and B (Bytes). |  | String |
| **camel.component.aws2-ddb.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-ddb.operation** | What operation to perform. |  | Ddb2Operations |
| **camel.component.aws2-ddb.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-ddb.proxy-host** | To define a proxy host when instantiating the DDB client. |  | String |
| **camel.component.aws2-ddb.proxy-port** | The region in which DynamoDB client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | Integer |
| **camel.component.aws2-ddb.proxy-protocol** | To define a proxy protocol when instantiating the DDB client. |  | Protocol |
| **camel.component.aws2-ddb.read-capacity** | The provisioned throughput to reserve for reading resources from your table. |  | Long |
| **camel.component.aws2-ddb.region** | The region in which DDB client needs to work. |  | String |
| **camel.component.aws2-ddb.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-ddb.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-ddb.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-ddb.use-default-credentials-provider** | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-ddb.write-capacity** | The provisioned throughput to reserved for writing resources to your table. |  | Long |
| **camel.component.aws2-ddbstream.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-ddbstream.amazon-dynamo-db-streams-client** | Amazon DynamoDB client to use for all requests for this endpoint. The option is a software.amazon.awssdk.services.dynamodb.streams.DynamoDbStreamsClient type. |  | DynamoDbStreamsClient |
| **camel.component.aws2-ddbstream.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-ddbstream.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws2-ddbstream.configuration** | The component configuration. The option is a org.apache.camel.component.aws2.ddbstream.Ddb2StreamConfiguration type. |  | Ddb2StreamConfiguration |
| **camel.component.aws2-ddbstream.enabled** | Whether to enable auto configuration of the aws2-ddbstream component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-ddbstream.max-results-per-request** | Maximum number of records that will be fetched in each poll. |  | Integer |
| **camel.component.aws2-ddbstream.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-ddbstream.proxy-host** | To define a proxy host when instantiating the DDBStreams client. |  | String |
| **camel.component.aws2-ddbstream.proxy-port** | To define a proxy port when instantiating the DDBStreams client. |  | Integer |
| **camel.component.aws2-ddbstream.proxy-protocol** | To define a proxy protocol when instantiating the DDBStreams client. |  | Protocol |
| **camel.component.aws2-ddbstream.region** | The region in which DDBStreams client needs to work. |  | String |
| **camel.component.aws2-ddbstream.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-ddbstream.stream-iterator-type** | Defines where in the DynamoDB stream to start getting records. Note that using FROM\_START can cause a significant delay before the stream has caught up to real-time. |  | Ddb2StreamConfiguration$StreamIteratorType |
| **camel.component.aws2-ddbstream.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-ddbstream.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-ddbstream.use-default-credentials-provider** | Set whether the DynamoDB Streams client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |