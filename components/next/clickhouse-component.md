# ClickHouse

**Since Camel 4.22**

**Only producer is supported**

This component allows you to interact with [ClickHouse](https://clickhouse.com/), the high-performance columnar OLAP database, using the official ClickHouse Java client (client-v2).

While ClickHouse can be reached through the generic [JDBC](jdbc-component.md) and [SQL](sql-component.md) components, this dedicated component exposes ClickHouse’s native capabilities as first-class endpoint options: native format streaming inserts (RowBinary, JSONEachRow, CSV, TSV, Parquet), server-side asynchronous inserts, OLAP queries and health checks.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-clickhouse</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

clickhouse://database\[.table\]?\[options\]

The producer can either use a shared `com.clickhouse.client.api.Client` bean (autowired from the registry) or build its own client from the `serverUrl`, `username`, `password` and `ssl` options. Connection settings can also be configured once on the **component** (for example `camel.component.clickhouse.serverUrl`) and inherited by every endpoint, so they do not need to be repeated in each URI.

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

The ClickHouse component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **client** (producer) | **Autowired** The shared ClickHouse client to use for all endpoints, of type com.clickhouse.client.api.Client. When set, the endpoint-level connection options (serverUrl, username, password, ssl) are ignored. |  | Client |
| **compression** (producer) | Whether to compress the insert request payload sent to the server (LZ4). | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **serverUrl** (producer) | The ClickHouse HTTP endpoint URL, e.g. [http://localhost:8123](http://localhost:8123). Can be overridden per endpoint. Required unless a shared Client bean is autowired or configured on the component. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **password** (security) | The password used to authenticate to ClickHouse. |  | String |
| **ssl** (security) | Whether to connect to ClickHouse over a secure (HTTPS) connection. | false | boolean |
| **username** (security) | The username used to authenticate to ClickHouse. | default | String |

## Endpoint Options

The ClickHouse endpoint is configured using URI syntax:

clickhouse:database

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **database** (producer) | **Required** The ClickHouse database. A table may also be provided using the database.table syntax. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **asyncInsert** (producer) | Whether to use ClickHouse server-side asynchronous inserts (async\_insert=1). | false | boolean |
| **batchSize** (producer) | The client-side batch size for insert operations when the message body is a List. When greater than 0, the list is split into batches of this size and each batch is sent as a separate insert. A value of 0 (default) inserts the whole list in a single call. | 0 | int |
| **compression** (producer) | Whether to compress the insert request payload sent to the server (LZ4). | false | boolean |
| **format** (producer) | The ClickHouse data format used for insert and query operations, e.g. JSONEachRow, RowBinary, CSV, TSV or Parquet. | JSONEachRow | String |
| **operation** (producer) | 
The operation to perform: insert, query or ping.

Enum values:

-   INSERT
    
-   QUERY
    
-   PING
    





 | INSERT | ClickHouseOperation |
| **serverUrl** (producer) | The ClickHouse HTTP endpoint URL, e.g. [http://localhost:8123](http://localhost:8123). Required unless a shared Client bean is autowired or configured on the component. |  | String |
| **table** (producer) | The target table for insert operations. Can also be given in the path as database.table or overridden per message with the CamelClickHouseTable header. |  | String |
| **waitForAsyncInsert** (producer) | When asyncInsert is enabled, whether the server should wait for the async insert to be flushed before acknowledging (wait\_for\_async\_insert). | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **password** (security) | The password used to authenticate to ClickHouse. |  | String |
| **ssl** (security) | Whether to connect to ClickHouse over a secure (HTTPS) connection. | false | boolean |
| **username** (security) | The username used to authenticate to ClickHouse. | default | String |

## Message Headers

The ClickHouse component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelClickHouseOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-clickhouse/latest/org/apache/camel/component/clickhouse/ClickHouseConstants.html#OPERATION) | Overrides the operation configured on the endpoint (insert, query or ping). |  | String |
| **CamelClickHouseDatabase** (producer) Constant: [`DATABASE`](https://javadoc.io/doc/org.apache.camel/camel-clickhouse/latest/org/apache/camel/component/clickhouse/ClickHouseConstants.html#DATABASE) | Overrides the target database configured on the endpoint. |  | String |
| **CamelClickHouseTable** (producer) Constant: [`TABLE`](https://javadoc.io/doc/org.apache.camel/camel-clickhouse/latest/org/apache/camel/component/clickhouse/ClickHouseConstants.html#TABLE) | Overrides the target table configured on the endpoint. |  | String |
| **CamelClickHouseFormat** (producer) Constant: [`FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-clickhouse/latest/org/apache/camel/component/clickhouse/ClickHouseConstants.html#FORMAT) | Overrides the data format configured on the endpoint. |  | String |
| **CamelClickHouseWrittenRows** (producer) Constant: [`WRITTEN_ROWS`](https://javadoc.io/doc/org.apache.camel/camel-clickhouse/latest/org/apache/camel/component/clickhouse/ClickHouseConstants.html#WRITTEN_ROWS) | The number of rows written by an insert operation. |  | long |
| **CamelClickHouseReadRows** (producer) Constant: [`READ_ROWS`](https://javadoc.io/doc/org.apache.camel/camel-clickhouse/latest/org/apache/camel/component/clickhouse/ClickHouseConstants.html#READ_ROWS) | The number of rows read by a query operation. |  | long |
| **CamelClickHousePingOk** (producer) Constant: [`PING_OK`](https://javadoc.io/doc/org.apache.camel/camel-clickhouse/latest/org/apache/camel/component/clickhouse/ClickHouseConstants.html#PING_OK) | The boolean result of a ping operation. |  | boolean |

## Operations

The component is producer-only and supports the following operations, selected with the `operation` option or the `CamelClickHouseOperation` header:

 
| Operation | Description |
| --- | --- |
| `insert` (default) | Streams the message body into the target table using the configured `format`. Accepted body types are `InputStream`, `byte[]`, `String`, `java.io.File` (matched to the `format`), or a `List` of objects whose class has been registered on the shared `Client`. When the body is a `List` and `batchSize` is greater than 0, the list is split into batches of that size, each sent as a separate insert. The number of written rows is set on the `CamelClickHouseWrittenRows` header. |
| `query` | Runs the SQL statement contained in the message body and returns the result set (in the configured `format`) as a `String` body. The number of read rows is set on the `CamelClickHouseReadRows` header. |
| `ping` | Pings the ClickHouse server and sets the boolean result on both the message body and the `CamelClickHousePingOk` header. |

## Examples

### High-throughput event ingestion

Batch-insert aggregated events into ClickHouse using the native `RowBinary` format:

```java
from("kafka:events?groupId=analytics")
    .aggregate(constant(true), new GroupedBodyAggregationStrategy())
        .completionSize(5000).completionTimeout(2000)
    .to("clickhouse://analytics.events?operation=insert&format=RowBinary")
    .log("Inserted ${header.CamelClickHouseWrittenRows} rows");
```

### Server-side asynchronous inserts

Let ClickHouse buffer and flush inserts server-side, ideal for many concurrent producers sending small payloads:

```java
from("platform-http:/ingest")
    .to("clickhouse://metrics.samples?operation=insert&asyncInsert=true&waitForAsyncInsert=false");
```

### Scheduled OLAP query

Run an aggregation query on a timer and route the result set downstream:

```java
from("timer:rollup?period=60000")
    .setBody(constant("SELECT count() FROM analytics.events"))
    .to("clickhouse://analytics?operation=query&format=JSONEachRow")
    .to("kafka:rollup-metrics");
```

### Health check

Verify connectivity to the ClickHouse server:

```java
from("timer:health?period=30000")
    .to("clickhouse://default?operation=ping")
    .choice()
        .when(header("CamelClickHousePingOk").isEqualTo(true))
            .to("direct:markHealthy")
        .otherwise()
            .to("direct:alertOps")
    .end();
```