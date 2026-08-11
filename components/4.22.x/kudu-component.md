# Kudu

**Since Camel 3.0**

**Only producer is supported**

The Kudu component supports storing and retrieving data from/to [Apache Kudu](https://kudu.apache.org/), a free and open source column-oriented data store of the Apache Hadoop ecosystem.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-kudu</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Prerequisites

You must have a valid Kudu instance running. More information is available at [Apache Kudu](https://kudu.apache.org/).

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

The Kudu component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **kuduClient** (advanced) | **Autowired** To use an existing Kudu client instance, instead of creating a client per endpoint. This allows you to customize various aspects to the client configuration. |  | KuduClient |

## Endpoint Options

The Kudu endpoint is configured using URI syntax:

kudu:host:port/tableName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** Host of the server to connect to. |  | String |
| **port** (common) | **Required** Port of the server to connect to. |  | String |
| **tableName** (common) | Table to connect to. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
Operation to perform.

Enum values:

-   INSERT
    
-   DELETE
    
-   UPDATE
    
-   UPSERT
    
-   CREATE\_TABLE
    
-   SCAN
    





 |  | KuduOperations |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Kudu component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelKuduSchema** (producer) Constant: [`CAMEL_KUDU_SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-kudu/latest/org/apache/camel/component/kudu/KuduConstants.html#CAMEL_KUDU_SCHEMA) | The schema. |  | Schema |
| **CamelKuduTableOptions** (producer) Constant: [`CAMEL_KUDU_TABLE_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-kudu/latest/org/apache/camel/component/kudu/KuduConstants.html#CAMEL_KUDU_TABLE_OPTIONS) | The create table options. |  | CreateTableOptions |
| **CamelKuduScanColumnNames** (producer) Constant: [`CAMEL_KUDU_SCAN_COLUMN_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-kudu/latest/org/apache/camel/component/kudu/KuduConstants.html#CAMEL_KUDU_SCAN_COLUMN_NAMES) | The projected column names for scan operation. |  | List |
| **CamelKuduScanPredicate** (producer) Constant: [`CAMEL_KUDU_SCAN_PREDICATE`](https://javadoc.io/doc/org.apache.camel/camel-kudu/latest/org/apache/camel/component/kudu/KuduConstants.html#CAMEL_KUDU_SCAN_PREDICATE) | The predicate for scan operation. |  | KuduPredicate |
| **CamelKuduScanLimit** (producer) Constant: [`CAMEL_KUDU_SCAN_LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-kudu/latest/org/apache/camel/component/kudu/KuduConstants.html#CAMEL_KUDU_SCAN_LIMIT) | The limit on the number of rows for scan operation. |  | long |

## Usage

### Input Body formats

#### Insert, delete, update, and upsert

The input body format has to be a `java.util.Map<String, Object>`. This map will represent a row of the table whose elements are columns, where the key is the column name and the value is the value of the column.

### Output Body formats

#### Scan

The output body format will be a `java.util.List<java.util.Map<String, Object>>`. Each element of the list will be a different row of the table. Each row is a `Map<String, Object>` whose elements will be each pair of column name and column value for that row.