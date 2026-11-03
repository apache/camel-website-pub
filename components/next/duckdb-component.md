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
| **query** (producer) | Static SQL for the execute and query operations. When set, it is used instead of the message body; the CamelDuckDbQuery header takes precedence over it. |  | String |
| **readOnly** (producer) | Open the embedded database file in read-only mode. Only applies to connections created by this endpoint from databasePath or jdbcUrl, and requires an existing database file. | false | boolean |
| **resultFormat** (producer) | 

How query results are returned: LIST\_MAP (List of Map) or JSON array string.

Enum values:

-   LIST\_MAP
    
-   JSON
    





 | LIST\_MAP | DuckDbResultFormat |
| **table** (producer) | Target table for insert and copy operations. Can be overridden per message with the CamelDuckDbTable header. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **allowDatabasePathFromHeader** (security) | Whether to allow overriding the database of the endpoint with the CamelDuckDbDatabasePath header, which opens a short-lived connection to the DuckDB file at that path (DuckDB creates the file when it does not exist) instead of using the databasePath, jdbcUrl or DataSource of the endpoint. Disabled by default; enable it only when the header source is trusted, since it lets a message choose the database file. | false | boolean |

## Message Headers

The DuckDB component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDuckDbOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#OPERATION) | Overrides the operation configured on the endpoint. |  | String |
| **CamelDuckDbDatabasePath** (producer) Constant: [`DATABASE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#DATABASE_PATH) | Overrides the database of the endpoint for one message: a short-lived connection to the DuckDB file at this path is opened, and DuckDB creates the file when it does not exist. This header is ignored unless the endpoint enables allowDatabasePathFromHeader=true (disabled by default). |  | String |
| **CamelDuckDbTable** (producer) Constant: [`TABLE`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#TABLE) | Overrides the target table configured on the endpoint. |  | String |
| **CamelDuckDbQuery** (producer) Constant: [`QUERY`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#QUERY) | Overrides the SQL for query or execute operations. Takes precedence over the query option and the message body. |  | String |
| **CamelDuckDbRowsWritten** (producer) Constant: [`ROWS_WRITTEN`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#ROWS_WRITTEN) | The number of rows written or affected. |  | long |
| **CamelDuckDbRowsRead** (producer) Constant: [`ROWS_READ`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#ROWS_READ) | The number of rows returned by a query. |  | long |
| **CamelDuckDbPingOk** (producer) Constant: [`PING_OK`](https://javadoc.io/doc/org.apache.camel/camel-duckdb/latest/org/apache/camel/component/duckdb/DuckDbConstants.html#PING_OK) | The boolean result of a ping operation. |  | boolean |

## Message Body

The message body at each side of the DuckDB component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `text`, `bytes`, `stream` or `file` | The SQL statement as text, or bytes, a stream or a file of it; the query option or the CamelDuckDbQuery header takes its place. Insert takes a List of Maps of the column names and their values (a Map alone fails), copy a File, a Path or the path (as text or bytes) of the csv, parquet or json file to load.
-   With `operation=INSERT`: `list`
    
-   With `operation=COPY`: `file`, `text` or `bytes`
    
-   With `operation=PING`: `any`
    

Not known when `query` is set.

 |
| **Producer output** | `value` (`java.lang.Long`) | 

The count of rows written or affected as a Long, also in the CamelDuckDbRowsWritten header. Query gives the rows as a List of Maps of the column names and their values (a JSON array String with resultFormat=JSON), ping a Boolean. The CamelDuckDbOperation header overrides the operation.

-   With `operation=QUERY`: `list` (`java.util.List<java.util.Map<String, Object>>`)
    
-   With `operation=PING`: `value` (`java.lang.Boolean`)
    
-   With `resultFormat=JSON`: `text` or `value`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Operations

The producer supports:

-   `execute` (default) — run DDL/DML that returns no rows
    
-   `query` — run a SELECT and return rows as `List<Map>` (default) or JSON (`resultFormat=JSON`)
    
-   `insert` — insert a `List` of `Map` rows into `table`
    
-   `copy` — bulk load from a `File`, a `Path` or a path as `String` (or bytes) using DuckDB `read_csv` / `read_parquet` / `read_json`
    
-   `ping` — `SELECT 1` connectivity check; sets `CamelDuckDbPingOk`
    

The SQL for `execute` and `query` is taken from the `CamelDuckDbQuery` header, else from the `query` option, else from the message body. So when the `query` option is set, the message body is not used as SQL.

A statement that returns rows fails with `execute`, and a statement that returns no rows (such as DDL) fails with `query`; the error says which operation to use instead. DuckDB has run the statement when the error is raised.

The endpoint reuses one JDBC connection for its configured `databasePath` / `jdbcUrl` and serializes access for thread safety. Prefer a shared `DataSource` when you need concurrent producers.

## Headers that override the endpoint

These headers take the place of an endpoint option for one message:

-   `CamelDuckDbOperation` replaces the `operation` option.
    
-   `CamelDuckDbQuery` replaces the `query` option and the message body as the SQL of `execute` and `query`.
    
-   `CamelDuckDbTable` replaces the `table` option of `insert` and `copy`.
    

So a message that carries them chooses the operation, the SQL that runs and the table that is written to.

The `CamelDuckDbDatabasePath` header is ignored unless the endpoint sets `allowDatabasePathFromHeader=true`. With that option, the header opens a short-lived connection to the DuckDB file at that path for one message, instead of the `databasePath`, `jdbcUrl` or `DataSource` of the endpoint, and DuckDB creates the file when it does not exist.

When the messages come from an untrusted producer through a consumer that does not filter out `Camel*` headers, remove these headers with `removeHeaders("CamelDuckDb*")` before the `duckdb` endpoint.

## Example

-   Java
    
-   YAML
    

```java
from("direct:metrics")
    .to("duckdb:local.db?operation=insert&table=metrics&batchSize=500");
```

```yaml
- route:
    from:
      uri: direct:metrics
      steps:
        - to:
            uri: duckdb:local.db
            parameters:
              operation: insert
              table: metrics
              batchSize: 500
```

-   Java
    
-   YAML
    

```java
from("file:incoming?include=.*\\.csv")
    .to("duckdb:warehouse.db?operation=copy&table=staging&format=csv");
```

```yaml
- route:
    from:
      uri: file:incoming
      parameters:
        include: ".*\\.csv"
      steps:
        - to:
            uri: duckdb:warehouse.db
            parameters:
              operation: copy
              table: staging
              format: csv
```

A query returns the rows as a `List` of `Map`, or as a JSON array with `resultFormat=JSON`:

```yaml
- route:
    from:
      uri: timer:report
      parameters:
        period: 60000
      steps:
        - to:
            uri: duckdb:warehouse.db
            parameters:
              operation: query
              query: "SELECT region, sum(amount) AS total FROM staging GROUP BY region"
              resultFormat: JSON
        - log:
            message: "${body}"
```