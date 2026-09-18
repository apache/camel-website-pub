# DuckDB

**Since Camel 4.22**

**Only producer is supported**

This component integrates with [DuckDB](https://duckdb.org/) using the official JDBC driver (`org.duckdb:duckdb_jdbc`). It focuses on embedded databases (`:memory:` or file paths), SQL `execute`/`query`, structured batch `insert`, file `copy` (CSV, Parquet, JSON), and `ping`.

While DuckDB can be used through [JDBC](jdbc-component.md) and [SQL](sql-component.md), this component exposes DuckDB-oriented URI options and headers without hand-wiring JDBC URLs in every route.

Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-duckdb</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

duckdb:databasePath?\[options\]

Configure `databasePath` as `:memory:` or a file path, either relative (`analytics.db`) or absolute (`/data/analytics.db`). The default table for `insert` and `copy` is set with the `table` option. Alternatively set `jdbcUrl=jdbc:duckdb:…​` to override the built URL, or autowire a shared `javax.sql.DataSource`.

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

The DuckDB component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **databasePath** (producer) | Embedded database path (:memory: or a file path). Used when jdbcUrl is not set. | :memory: | String |
| **dataSource** (producer) | **Autowired** Shared JDBC DataSource for all endpoints. |  | DataSource |
| **jdbcUrl** (producer) | Full JDBC URL override (for example jdbc:duckdb:/path/to/db). When set, databasePath is ignored. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The DuckDB endpoint is configured using URI syntax:

duckdb:databasePath

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **databasePath** (producer) | Database path, either :memory: or a relative or absolute file path. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **batchSize** (producer) | Batch size for insert when the body is a List. 0 inserts all rows in one JDBC batch. | 0 | int |
| **format** (producer) | File format for copy: csv, parquet, json or auto (inferred from the file extension). | auto | String |
| **jdbcUrl** (producer) | Full JDBC URL override. When set, databasePath is not used to build the URL. |  | String |
| **operation** (producer) | 
The operation to perform: execute, query, insert, copy or ping.

Enum values:

-   EXECUTE
    
-   QUERY
    
-   INSERT
    
-   COPY
    
-   PING
    





 | EXECUTE | DuckDbOperation |
| **query** (producer) | Static SQL for query when the message body is empty. |  | String |
| **readOnly** (producer) | Open the embedded database file in read-only mode. Only applies to connections created by this endpoint from databasePath or jdbcUrl, and requires an existing database file. | false | boolean |
| **resultFormat** (producer) | 

How query results are returned: LIST\_MAP (List of Map) or JSON array string.

Enum values:

-   LIST\_MAP
    
-   JSON
    





 | LIST\_MAP | DuckDbResultFormat |
| **table** (producer) | Target table for insert and copy operations. Can be overridden per message with the CamelDuckDbTable header. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The DuckDB component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDuckDbOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#OPERATION) | Overrides the operation configured on the endpoint. |  | String |
| **CamelDuckDbDatabasePath** (producer) Constant: [`DATABASE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#DATABASE_PATH) | Overrides the database path configured on the endpoint. |  | String |
| **CamelDuckDbTable** (producer) Constant: [`TABLE`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#TABLE) | Overrides the target table configured on the endpoint. |  | String |
| **CamelDuckDbQuery** (producer) Constant: [`QUERY`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#QUERY) | Overrides the SQL for query or execute operations. |  | String |
| **CamelDuckDbRowsWritten** (producer) Constant: [`ROWS_WRITTEN`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#ROWS_WRITTEN) | The number of rows written or affected. |  | long |
| **CamelDuckDbRowsRead** (producer) Constant: [`ROWS_READ`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#ROWS_READ) | The number of rows returned by a query. |  | long |
| **CamelDuckDbPingOk** (producer) Constant: [`PING_OK`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#PING_OK) | The boolean result of a ping operation. |  | boolean |

## Operations

The producer supports:

-   `execute` (default) — run DDL/DML from the message body (or `query` option / `CamelDuckDbQuery` header)
    
-   `query` — run a SELECT and return rows as `List<Map>` (default) or JSON (`resultFormat=JSON`)
    
-   `insert` — insert a `List` of `Map` rows into `table`
    
-   `copy` — bulk load from a `File` or path `String` using DuckDB `read_csv` / `read_parquet` / `read_json`
    
-   `ping` — `SELECT 1` connectivity check; sets `CamelDuckDbPingOk`
    

The endpoint reuses one JDBC connection for its configured `databasePath` / `jdbcUrl` and serializes access for thread safety. Prefer a shared `DataSource` when you need concurrent producers. Set the `CamelDuckDbDatabasePath` header to open a short-lived connection to a different database file for a single message.

## Example

```java
from("direct:metrics")
    .to("duckdb:local.db?operation=insert&table=metrics&batchSize=500");
```

```java
from("file:incoming?include=.*\\.csv")
    .to("duckdb:warehouse.db?operation=copy&table=staging&format=csv");
```