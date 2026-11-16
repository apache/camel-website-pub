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
| **allowGlobCopySource** (security) | Whether the copy operation accepts a source with glob pattern characters (asterisk, question mark, square bracket or curly brace), which DuckDB expands to all the matching files. Disabled by default, so copy loads a single file. | false | boolean |
| **allowUrlCopySource** (security) | Whether the copy operation accepts a source that starts with a URL scheme (such as https:// or s3://), which DuckDB reads as a remote file. Disabled by default, so copy loads a local file only; enable it only when the source of the message body is trusted. | false | boolean |
| **copyBaseDirectory** (security) | A directory that the local source of the copy operation must be inside, after resolving symbolic links. A relative source is resolved against this directory. For a glob pattern, the directory before the first glob character must be inside it. Not set by default, so copy loads a file from any directory. |  | String |

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
    
-   `copy` — bulk load one local file, from a `File` or a path `String`, using DuckDB `read_csv` / `read_parquet` / `read_json`
    
-   `ping` — `SELECT 1` connectivity check; sets `CamelDuckDbPingOk`
    

The endpoint reuses one JDBC connection for its configured `databasePath` / `jdbcUrl` and serializes access for thread safety. Prefer a shared `DataSource` when you need concurrent producers. Set the `CamelDuckDbDatabasePath` header to open a short-lived connection to a different database file for a single message.

## Copy sources

The `copy` operation gives the path from the message body to the DuckDB `read_csv`, `read_parquet` or `read_json` function. DuckDB reads a value that starts with a URL scheme (such as `https://` or `s3://`) as a remote file, and expands a value with glob pattern characters (`*`, `?`, `[` or `{`) to all the matching files. So by default `copy` loads a single local file, and fails with an `IllegalArgumentException` that names the option to set otherwise:

-   `allowUrlCopySource=true` passes a source with a URL scheme to DuckDB as it is.
    
-   `allowGlobCopySource=true` loads all the files that a glob pattern matches. This also applies to a `File` body whose name has one of these characters.
    
-   `copyBaseDirectory` sets the directory that a local source must be inside, after resolving symbolic links. A relative source is resolved against this directory, and for a glob pattern the directory before the first glob character must be inside it.
    

-   Java
    
-   YAML
    

```java
from("direct:load")
    .to("duckdb:warehouse.db?operation=copy&table=staging&allowGlobCopySource=true&copyBaseDirectory=/data/incoming");
```

```yaml
- route:
    from:
      uri: direct:load
      steps:
        - to:
            uri: duckdb:warehouse.db
            parameters:
              operation: copy
              table: staging
              allowGlobCopySource: true
              copyBaseDirectory: /data/incoming
```

These options apply to `copy` only. The SQL of `execute` and `query` can call the read functions itself; to have DuckDB restrict file and network access for every statement, configure the DuckDB settings `enable_external_access`, `allowed_directories` and `autoinstall_known_extensions` (see the DuckDB documentation).

## Example

```java
from("direct:metrics")
    .to("duckdb:local.db?operation=insert&table=metrics&batchSize=500");
```

```java
from("file:incoming?include=.*\\.csv")
    .to("duckdb:warehouse.db?operation=copy&table=staging&format=csv");
```