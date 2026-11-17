# ![mysql sink](_images/kamelets/mysql-sink.svg) MySQL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL statement, such as an INSERT, in a MySQL database for each message, with values taken from the fields of the JSON object in the body.

Use it to store records from another system as rows of a table, such as each order that arrives on a Kafka topic, or to update or delete rows. To read rows, use `mysql-source`.

Input: the body is one JSON object, as text, such as `{"username":"oscerd","city":"Rome"}`. In `query`, write `:#username` where the value of the field `username` goes. When the object has no field of that name, the header of that name is used instead. Fields that `query` does not name are ignored.

Output: the body afterwards is the JSON object as a Map, and the `CamelSqlUpdateCount` header holds the number of rows the statement changed. When `query` is a SELECT, the body is instead a List of the rows found, each a Map, and the `CamelSqlRowCount` header holds their number.

Good to know: a message fails when its body is not a JSON object (a JSON array or plain text, for example), or when it has no value for a parameter of `query`. The values are sent to the database apart from the SQL text, so the content of a message cannot change the statement. Do not write `?` in `query`, not even in a quoted string: the Kamelet then fails to start. The JDBC driver of MySQL is not included: add `mvn:com.mysql:mysql-connector-j` to the dependencies of the integration. Camel JBang (`camel run`) adds it by itself.

## Configuration Options

The following table summarizes the configuration options available for the `mysql-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database to connect to on the MySQL server. | string |  | shop |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **query** | Query | **Required** The SQL statement to run for each message, such as an INSERT, UPDATE or DELETE. Write `:#name` where the value of the field `name` of the JSON body goes. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The host name or IP address of the MySQL server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The database user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **serverPort** | Server Port | The port the MySQL server listens on. MySQL uses 3306 unless it was set up otherwise. | string | 3306 |  |

## Dependencies

At runtime, the `mysql-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
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
            uri: "kamelet:mysql-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## MySQL Sink Kamelet Description

### Database Connection

This Kamelet connects to MySQL databases using the MySQL Connector/J JDBC driver, which is not a dependency of the Kamelet: add `mvn:com.mysql:mysql-connector-j` to the integration (Camel JBang adds it by itself). MySQL is one of the world’s most popular open-source relational database management systems.

### Data Processing

The Kamelet expects JSON input data which is automatically unmarshalled before executing the SQL query. This allows for seamless integration with JSON-based data sources.

### Parameterized Queries

SQL queries use named parameters (e.g., `:#username`, `:#city`) that map to fields in the incoming JSON data. This approach provides protection against SQL injection attacks while maintaining query flexibility.

### Connection Management

Uses Apache Commons DBCP2 for efficient database connection pooling. This provides optimal resource utilization and connection lifecycle management.

### Authentication and Security

Requires username and password authentication for database access.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-sink.kamelet.yaml)