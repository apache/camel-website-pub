# SQL

JVM since1.0.0 Native since1.0.0

Perform SQL queries.

## What’s inside

-   [SQL component](../../../../components/4.18.x/sql-component.md), URI syntax: `sql:query`
    
-   [SQL Stored Procedure component](../../../../components/4.18.x/sql-stored-component.md), URI syntax: `sql-stored:template`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-sql)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-sql</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Configuring a DataSource

This extension leverages [Quarkus Agroal](https://quarkus.io/guides/datasource) for `DataSource` support. Setting up a `DataSource` can be achieved via configuration properties.

```properties
quarkus.datasource.db-kind=postgresql
quarkus.datasource.username=your-username
quarkus.datasource.password=your-password
quarkus.datasource.jdbc.url=jdbc:postgresql://localhost:5432/your-database
quarkus.datasource.jdbc.max-size=16
```

The Camel SQL component will automatically resolve the `DataSource` bean from the registry. When configuring multiple datasources, you can specify which one is to be used on an SQL endpoint via the URI options `datasource` or `dataSourceRef`. Refer to the SQL component documentation for more details.

#### Zero configuration with Quarkus Dev Services

In dev and test mode you can take advantage of [Configuration Free Databases](https://quarkus.io/guides/datasource#dev-services-configuration-free-databases). The Camel SQL component will be automatically configured to use a `DataSource` that points to a local containerized instance of the database matching the JDBC driver type that you have selected.

### SQL scripts

When configuring `sql` or `sql-stored` endpoints to reference script files from the classpath, set the following configuration property to ensure that they are available in native mode.

```properties
quarkus.native.resources.includes = queries.sql, sql/*.sql
```

### SQL aggregation repository in native mode

In order to use SQL aggregation repositories like `JdbcAggregationRepository` in native mode, you must [enable native serialization support](core.html#quarkus-camel-native-reflection-serialization-enabled).

In addition, if your exchange bodies are custom types, they must be registered for serialization by annotating their class declaration with `@RegisterForReflection(serialization = true)`.