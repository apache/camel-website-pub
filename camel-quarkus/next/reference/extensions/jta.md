# JTA

JVM since1.0.0 Native since1.0.0

Enclose Camel routes in transactions using Java Transaction API (JTA) and Narayana transaction manager

## What’s inside

-   [JTA](../../../../components/4.18.x/others/jta.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jta)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jta</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

This extension should be added when you need to use the `transacted()` EIP in the router. It leverages the transaction capabilities provided by the narayana-jta extension in Quarkus.

Refer to the [Quarkus Transaction guide](https://quarkus.io/guides/transaction) for the more details about transaction support. For a simple usage:

```java
from("direct:transaction")
    .transacted()
    .to("sql:INSERT INTO A TABLE ...?dataSource=#ds1")
    .to("sql:INSERT INTO A TABLE ...?dataSource=#ds2")
    .log("All data committed to DataSources ds1 and ds2")
```

You can use a specific transaction policy by referring to its name.

```java
from("direct:transaction")
    .transacted("PROPAGATION_REQUIRED")
    .to("sql:INSERT INTO A TABLE ...?dataSource=#ds1");
    .to("sql:INSERT INTO A TABLE ...?dataSource=#ds2")
    .log("All data committed to DataSources ds1 and ds2")
```

Support is provided for the following transaction policies.

 
| Policy | Description |
| --- | --- |
| `PROPAGATION_MANDATORY` | Support a current transaction; throw an exception if no current transaction exists. |
| `PROPAGATION_NEVER` | Do not support a current transaction; throw an exception if a current transaction exists. |
| `PROPAGATION_NOT_SUPPORTED` | Do not support a current transaction; rather always execute non-transactionally. |
| `PROPAGATION_REQUIRED` | Support a current transaction; create a new one if none exists. |
| `PROPAGATION_REQUIRES_NEW` | Create a new transaction, suspending the current transaction if one exists. |
| `PROPAGATION_SUPPORTS` | Support a current transaction; execute non-transactionally if none exists. |