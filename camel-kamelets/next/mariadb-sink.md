# ![mariadb sink](_images/kamelets/mariadb-sink.svg) MariaDB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL statement, such as an INSERT, in a MariaDB database for each message, with values taken from the fields of the JSON object in the body.

Use it to store records from another system as rows of a table, such as each order that arrives on a Kafka topic, or to update or delete rows. To read rows, use `mariadb-source`.

Input: the body is one JSON object, as text, such as `{"username":"oscerd","city":"Rome"}`. In `query`, write `:#username` where the value of the field `username` goes. When the object has no field of that name, the header of that name is used instead. Fields that `query` does not name are ignored.

Output: the body afterwards is the JSON object as a Map, and the `CamelSqlUpdateCount` header holds the number of rows the statement changed. When `query` is a SELECT, the body is instead a List of the rows found, each a Map, and the `CamelSqlRowCount` header holds their number.

Good to know: a message fails when its body is not a JSON object (a JSON array or plain text, for example), or when it has no value for a parameter of `query`. The values are sent to the database apart from the SQL text, so the content of a message cannot change the statement. Do not write `?` in `query`, not even in a quoted string: the Kamelet then fails to start. The JDBC driver of MariaDB is not included: add `mvn:org.mariadb.jdbc:mariadb-java-client` to the dependencies of the integration. Camel JBang (`camel run`) adds it by itself. Whether the connection uses TLS when `connectionProperties` is not set depends on the version of the MariaDB driver: set `sslMode=trust` in `connectionProperties` to insist on TLS.

## Configuration Options

The following table summarizes the configuration options available for the `mariadb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database to connect to on the MariaDB server. | string |  | shop |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **query** | Query | **Required** The SQL statement to run for each message, such as an INSERT, UPDATE or DELETE. Write `:#name` where the value of the field `name` of the JSON body goes. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The host name or IP address of the MariaDB server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The database user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **connectionProperties** | Connection Properties | Extra settings for the MariaDB JDBC driver (MariaDB Connector/J), as `name=value` pairs separated by `;`, such as `sslMode=trust;connectTimeout=10000`. Use it for TLS: `sslMode=trust` makes the connection use TLS without checking the certificate of the server, and `sslMode=disable` turns TLS off. When it is not set, the default of the driver applies, and it depends on its version: Connector/J 3 connects without TLS, Connector/J 4 with TLS. The value is not hidden like a password, and it can show in the log when the integration starts, so do not put a password in it. | string |  | sslMode=trust |
| **serverPort** | Server Port | The port the MariaDB server listens on. MariaDB uses 3306 unless it was set up otherwise. | string | 3306 |  |

## Dependencies

At runtime, the `mariadb-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:mariadb-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## MariaDB Sink Kamelet Description

### Database Connection

This Kamelet connects to MariaDB databases using JDBC. MariaDB is a popular open-source relational database management system that is a compatible drop-in replacement for MySQL.

### Data Processing

The Kamelet expects JSON input data which is unmarshalled before executing the SQL query. The input data fields can be referenced in the SQL query using named parameters.

### Query Configuration

The SQL query should use named parameters (e.g., `:#username`, `:#city`) that correspond to fields in the incoming JSON data. This allows for safe parameterized queries that prevent SQL injection attacks.

### Connection Pooling

The Kamelet uses Apache Commons DBCP2 for connection pooling, providing efficient database connection management and resource optimization.

### Authentication

Requires username and password authentication for secure database access. These credentials should be properly managed and secured.

### Connecting with TLS

Set `connectionProperties` to pass settings to the MariaDB JDBC driver (MariaDB Connector/J), as `name=value` pairs separated by `;`. Without it, the default of the driver applies, and it depends on its version: Connector/J 3 connects without TLS, Connector/J 4 with TLS. Set `sslMode=trust` to always use TLS, without checking the certificate of the server.

```yaml
connectionProperties: "sslMode=trust"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mariadb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mariadb-sink.kamelet.yaml)