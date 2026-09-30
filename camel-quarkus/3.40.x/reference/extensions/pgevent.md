# PostgresSQL Event

JVM since1.1.0 Native since1.2.0

Send and receive PostgreSQL events via LISTEN and NOTIFY commands.

## What’s inside

-   [PostgreSQL Event component](../../../../components/4.22.x/pgevent-component.md), URI syntax: `pgevent:host:port/database/channel`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-pgevent)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-pgevent</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

You can use pgevent extension with Agroal Datasource.

Add the quarkus-agroal dependency :

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-agroal</artifactId>
</dependency>
```

Set Agroal properties, example for named DataSource `pgDatasource` :

quarkus.datasource.pgDatasource.db-kind=pgsql
quarkus.datasource.pgDatasource.jdbc.url=jdbc:pgsql://localhost:5432/myDB
quarkus.datasource.pgDatasource.username=postgres
quarkus.datasource.pgDatasource.password=mysecretpassword
quarkus.datasource.pgDatasource.jdbc.max-size=16

Inject the DataSource name in the camel Route, example :

pgevent:///postgres/testchannel?datasource=#pgDatasource