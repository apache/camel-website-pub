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

## Message Body

The message body at each side of the Kudu component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `map` | 
For insert, update, upsert and delete: a Map of the column names and their values, one row, each value of the Java type of its column (a String for an INT32 column fails); delete uses only the key columns. Text such as JSON, a List or a POJO fails: unmarshal it into a Map first. Scan and create\_table do not read the body: they take the CamelKuduScan\* and the CamelKuduSchema and CamelKuduTableOptions headers. The operation must be set.

-   With `operation=SCAN`: `any`
    
-   With `operation=CREATE_TABLE`: `any`
    





 |
| **Producer output** | `unchanged` | 

Scan gives a List of the rows, each a Map of the column names and their values, an empty List for no rows. The other operations leave the body unchanged.

-   With `operation=SCAN`: `list` (`java.util.List<java.util.Map<String, Object>>`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Input Body formats

#### Insert, delete, update, and upsert

The input body format has to be a `java.util.Map<String, Object>`. This map will represent a row of the table whose elements are columns, where the key is the column name and the value is the value of the column.

### Output Body formats

#### Scan

The output body format will be a `java.util.List<java.util.Map<String, Object>>`. Each element of the list will be a different row of the table. Each row is a `Map<String, Object>` whose elements will be each pair of column name and column value for that row.

### Example

The first route inserts a row from a JSON message, which the JSON data format turns into a `Map`. The second route scans the table:

```yaml
- route:
    from:
      uri: direct:insertOrder
      steps:
        - unmarshal:
            json: {}
        - to:
            uri: kudu:localhost:7051/orders
            parameters:
              operation: insert
- route:
    from:
      uri: timer:scan
      parameters:
        repeatCount: 1
      steps:
        - to:
            uri: kudu:localhost:7051/orders
            parameters:
              operation: scan
        - log:
            message: "Rows: ${body}"
```

### Row errors

The producer fails the exchange with a `KuduRowErrorException` when the answer to an insert, delete, update or upsert carries a row error. Its `getRowError()` returns the row error of the Kudu client, whose status tells the kind of error. There are two cases:

-   a row that Kudu rejected: an insert of a row whose key is already in the table, or an update or a delete of a row that is not in the table. The row was not written. Use the `upsert` operation to write a row whether it exists or not.
    
-   a request that failed, for example because it timed out or because no tablet server could be reached. The Kudu client reports it the same way. In this case it is not known whether the row was written.