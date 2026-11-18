# ![oracle database sink](_images/kamelets/oracle-database-sink.svg) Oracle Database Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL statement, such as an INSERT, in an Oracle Database database for each message, with values taken from the fields of the JSON object in the body.

Use it to store records from another system as rows of a table, such as each order that arrives on a Kafka topic, or to update or delete rows. To read rows, use `oracle-database-source`.

Input: the body is one JSON object, as text, such as `{"username":"oscerd","city":"Rome"}`. In `query`, write `:#username` where the value of the field `username` goes. When the object has no field of that name, the header of that name is used instead. Fields that `query` does not name are ignored.

Output: the body afterwards is the JSON object as a Map, and the `CamelSqlUpdateCount` header holds the number of rows the statement changed. When `query` is a SELECT, the body is instead a List of the rows found, each a Map, and the `CamelSqlRowCount` header holds their number.

Good to know: a message fails when its body is not a JSON object (a JSON array or plain text, for example), or when it has no value for a parameter of `query`. The values are sent to the database apart from the SQL text, so the content of a message cannot change the statement. Do not write `?` in `query`, not even in a quoted string: the Kamelet then fails to start. The JDBC driver of Oracle Database is not included: add `mvn:com.oracle.database.jdbc:ojdbc17` to the dependencies of the integration. Camel JBang (`camel run`) adds it by itself.

## Configuration Options

The following table summarizes the configuration options available for the `oracle-database-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The service name of the database to connect to, such as `FREEPDB1` or `ORCLPDB1`. It is a service name, not a SID. | string |  | ORCLPDB1 |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **query** | Query | **Required** The SQL statement to run for each message, such as an INSERT, UPDATE or DELETE. Write `:#name` where the value of the field `name` of the JSON body goes. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The host name or IP address of the Oracle Database server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The database user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **serverPort** | Server Port | The port of the Oracle listener on the server. Oracle uses 1521 unless it was set up otherwise. | string | 1521 |  |

## Dependencies

At runtime, the `oracle-database-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:org.apache.commons:commons-dbcp2:2.14.0
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:oracle-database-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Oracle Database Sink Kamelet Description

### Enterprise Database Integration

This Kamelet provides integration with Oracle Database, a leading enterprise-grade relational database management system known for its performance, reliability, and advanced features.

### JDBC Connectivity

Uses Oracle’s thin JDBC driver for efficient database connectivity. The thin driver provides a pure Java implementation that doesn’t require Oracle client software installation.

### Data Processing

Expects JSON input data which is unmarshalled before SQL execution. The JSON data fields can be referenced in SQL queries using named parameters for secure data binding.

### Query Parameterization

Supports named parameters in SQL queries (e.g., `:#username`, `:#city`) that correspond to incoming JSON data fields. This provides secure, injection-resistant query execution.

### Connection Pooling

Utilizes Apache Commons DBCP2 for connection pooling, ensuring efficient resource management and optimal database performance in enterprise environments.

### Enterprise Features

Oracle Database supports advanced features like transactions, stored procedures, and complex data types, making this Kamelet suitable for enterprise-level applications.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/oracle-database-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/oracle-database-sink.kamelet.yaml)