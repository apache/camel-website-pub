# AWS RedshiftData

**Since Camel 4.1**

**Only producer is supported**

The AWS2 Redshift Data component supports the following operations on [AWS Redshift](https://aws.amazon.com/redshift/):

-   listDatabases, listSchemas, listStatements, listTables, describeTable, executeStatement, batchExecuteStatement, cancelStatement, describeStatement, getStatementResult
    

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Redshift. More information is available at [AWS Redshift](https://aws.amazon.com/redshift/).

## URI Format

aws2-redshift-data://label\[?options\]

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

The AWS RedshiftData component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | RedshiftData2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform. It can be batchExecuteStatement, cancelStatement, describeStatement, describeTable, executeStatement, getStatementResult, listDatabases, listSchemas, listStatements or listTables.

Enum values:

-   listDatabases
    
-   listSchemas
    
-   listStatements
    
-   listTables
    
-   describeTable
    
-   executeStatement
    
-   batchExecuteStatement
    
-   cancelStatement
    
-   describeStatement
    
-   getStatementResult
    





 |  | RedshiftData2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which RedshiftData client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useDefaultCredentialsProvider** (producer) | Set whether the RedshiftData client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the RedshiftData client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **awsRedshiftDataClient** (advanced) | **Autowired** To use an existing configured AwsRedshiftDataClient client. |  | RedshiftDataClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the RedshiftData client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the RedshiftData client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the RedshiftData client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **useSessionCredentials** (security) | Set whether the Redshift client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Redshift. | false | boolean |

## Endpoint Options

The AWS RedshiftData endpoint is configured using URI syntax:

aws2-redshift-data:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform. It can be batchExecuteStatement, cancelStatement, describeStatement, describeTable, executeStatement, getStatementResult, listDatabases, listSchemas, listStatements or listTables.

Enum values:

-   listDatabases
    
-   listSchemas
    
-   listStatements
    
-   listTables
    
-   describeTable
    
-   executeStatement
    
-   batchExecuteStatement
    
-   cancelStatement
    
-   describeStatement
    
-   getStatementResult
    





 |  | RedshiftData2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which RedshiftData client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useDefaultCredentialsProvider** (producer) | Set whether the RedshiftData client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the RedshiftData client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **awsRedshiftDataClient** (advanced) | **Autowired** To use an existing configured AwsRedshiftDataClient client. |  | RedshiftDataClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the RedshiftData client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the RedshiftData client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the RedshiftData client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **useSessionCredentials** (security) | Set whether the Redshift client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Redshift. | false | boolean |

## Message Headers

The AWS RedshiftData component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsRedshiftDataOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsRedshiftDataClusterIdentifier** (producer) Constant: [`CLUSTER_IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#CLUSTER_IDENTIFIER) | The cluster identifier. |  | String |
| **CamelAwsRedshiftDataSecretArn** (producer) Constant: [`SECRET_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#SECRET_ARN) | The name or ARN of the secret that enables access to the database. |  | String |
| **CamelAwsRedshiftDataDatabase** (producer) Constant: [`DATABASE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#DATABASE) | The name of the database. |  | String |
| **CamelAwsRedshiftDataWorkGroupName** (producer) Constant: [`WORKGROUP_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#WORKGROUP_NAME) | The serverless workgroup name or Amazon Resource Name (ARN). |  | String |
| **CamelAwsRedshiftDataDatabasesMaxResults** (producer) Constant: [`LIST_DATABASES_MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#LIST_DATABASES_MAX_RESULTS) | The maximum number of databases to return in the response. |  | Integer |
| **CamelAwsRedshiftDataDbUser** (producer) Constant: [`DB_USER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#DB_USER) | The database user name. |  | String |
| **CamelAwsRedshiftDataConnectedDatabase** (producer) Constant: [`CONNECTED_DATABASE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#CONNECTED_DATABASE) | A database name. |  | String |
| **CamelAwsRedshiftDataSchemaPattern** (producer) Constant: [`SCHEMA_PATTERN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#SCHEMA_PATTERN) | A pattern to filter results by schema name. |  | String |
| **CamelAwsRedshiftDataSchemasMaxResults** (producer) Constant: [`LIST_SCHEMAS_MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#LIST_SCHEMAS_MAX_RESULTS) | The maximum number of schemas to return in the response. |  | Integer |
| **CamelAwsRedshiftDataStatementsMaxResults** (producer) Constant: [`LIST_STATEMENTS_MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#LIST_STATEMENTS_MAX_RESULTS) | The maximum number of SQL statements to return in the response. |  | Integer |
| **CamelAwsRedshiftDataStatementName** (producer) Constant: [`STATEMENT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#STATEMENT_NAME) | The name of the SQL statement specified as input to BatchExecuteStatement or ExecuteStatement to identify the query. |  | String |
| **CamelAwsRedshiftDataStatus** (producer) Constant: [`STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#STATUS) | The status of the SQL statement to list. |  | String |
| **CamelAwsRedshiftDataRoleLevel** (producer) Constant: [`ROLE_LEVEL`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#ROLE_LEVEL) | A value that filters which statements to return in the response. |  | Boolean |
| **CamelAwsRedshiftDataTablesMaxResults** (producer) Constant: [`LIST_TABLES_MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#LIST_TABLES_MAX_RESULTS) | The maximum number of tables to return in the response. |  | Integer |
| **CamelAwsRedshiftDataTablePattern** (producer) Constant: [`TABLE_PATTERN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#TABLE_PATTERN) | A pattern to filter results by table name. |  | String |
| **CamelAwsRedshiftDataTable** (producer) Constant: [`TABLE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#TABLE) | The name of the table. |  | String |
| **CamelAwsRedshiftDataSchema** (producer) Constant: [`SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#SCHEMA) | The schema that contains the table. |  | String |
| **CamelAwsRedshiftDataDescribeTableMaxResults** (producer) Constant: [`DESCRIBE_TABLE_MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#DESCRIBE_TABLE_MAX_RESULTS) | The maximum number of tables to return in the response. |  | Integer |
| **CamelAwsRedshiftDataStatementId** (producer) Constant: [`STATEMENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#STATEMENT_ID) | ID of the statement. |  | String |
| **CamelAwsRedshiftDataWithEvent** (producer) Constant: [`WITH_EVENT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#WITH_EVENT) | A value that indicates whether to send an event to the Amazon EventBridge event bus after the SQL statement runs. |  | Boolean |
| **CamelAwsRedshiftDataClientToken** (producer) Constant: [`CLIENT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#CLIENT_TOKEN) | A unique, case-sensitive identifier that you provide to ensure the idempotency of the request. |  | String |
| **CamelAwsRedshiftDataSqlStatement** (producer) Constant: [`SQL_STATEMENT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#SQL_STATEMENT) | The SQL statement text to run. |  | String |
| **CamelAwsRedshiftDataSqlParameterList** (producer) Constant: [`SQL_PARAMETER_LIST`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#SQL_PARAMETER_LIST) | The parameters for the SQL statement. |  | List |
| **CamelAwsRedshiftDataSqlStatementList** (producer) Constant: [`SQL_STATEMENT_LIST`](https://javadoc.io/doc/org.apache.camel/camel-aws2-redshift/latest/org/apache/camel/component/aws2/redshift/data/RedshiftData2Constants.html#SQL_STATEMENT_LIST) | The List of SQL statements text to run. |  | List |

Required Redshift Data component options

You have to provide the awsRedshiftDataClient in the Registry or your accessKey and secretKey to access the [AWS Redshift](https://aws.amazon.com/redshift/) service.

## Usage

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Redshift Producer operations

Camel-AWS Redshift Data component provides the following operation on the producer side:

-   listDatabases
    
-   listSchemas
    
-   listStatements
    
-   listTables
    
-   describeTable
    
-   executeStatement
    
-   batchExecuteStatement
    
-   cancelStatement
    
-   describeStatement
    
-   getStatementResult
    

## Examples

### Producer Examples

-   listDatabases: this operation will list redshift databases
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listDatabases")
    .to("aws2-redshift-data://test?awsRedshiftDataClient=#awsRedshiftDataClient&operation=listDatabases");
```

```xml
<route>
  <from uri="direct:listDatabases"/>
  <to uri="aws2-redshift-data://test?awsRedshiftDataClient=#awsRedshiftDataClient&amp;operation=listDatabases"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:listDatabases
      steps:
        - to:
            uri: aws2-redshift-data://test
            parameters:
              awsRedshiftDataClient: "#awsRedshiftDataClient"
              operation: listDatabases
```

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as body. In AWS Redshift Data there are multiple operations you can submit, as an example for List Databases request, you can do something like:

_Java-only: using a POJO request body with the AWS SDK builder_

```java
from("direct:start")
  .setBody(ListDatabases.builder().database("database1").build())
  .to("aws2-redshift-data://test?awsRedshiftDataClient=#awsRedshiftDataClient&operation=listDatabases&pojoRequest=true")
```

In this way you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-redshift-data</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.