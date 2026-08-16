# JDBC

JVM since0.0.1 Native since0.0.1

Access databases through SQL and JDBC.

## What’s inside

-   [JDBC component](../../../../components/4.22.x/jdbc-component.md), URI syntax: `jdbc:dataSourceName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jdbc)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jdbc</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Configuring a DataSource

This extension leverages [Quarkus Agroal](https://quarkus.io/guides/datasource) for `DataSource` support. Setting up a `DataSource` can be achieved via configuration properties. It is recommended that you explicitly name the datasource so that it can be referenced in the JDBC endpoint URI. E.g. like `to("jdbc:camel")`.

```properties
quarkus.datasource.camel.db-kind=postgresql
quarkus.datasource.camel.username=your-username
quarkus.datasource.camel.password=your-password
quarkus.datasource.camel.jdbc.url=jdbc:postgresql://localhost:5432/your-database
quarkus.datasource.camel.jdbc.max-size=16
```

If you choose to not name the datasource, you can resolve the default `DataSource` by defining your endpoint like `to("jdbc:default")`.

#### Zero configuration with Quarkus Dev Services

In dev and test mode you can take advantage of [Configuration Free Databases](https://quarkus.io/guides/datasource#dev-services-configuration-free-databases). All you need to do is reference the default database in your routes. E.g `to("jdbc:default")`.