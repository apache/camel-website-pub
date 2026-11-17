# ![sqlserver sink](_images/kamelets/sqlserver-sink.svg) Microsoft SQL Server Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL statement, such as an INSERT, in a Microsoft SQL Server database for each message, with values taken from the fields of the JSON object in the body.

Use it to store records from another system as rows of a table, such as each order that arrives on a Kafka topic, or to update or delete rows. To read rows, use `sqlserver-source`.

Input: the body is one JSON object, as text, such as `{"username":"oscerd","city":"Rome"}`. In `query`, write `:#username` where the value of the field `username` goes. When the object has no field of that name, the header of that name is used instead. Fields that `query` does not name are ignored.

Output: the body afterwards is the JSON object as a Map, and the `CamelSqlUpdateCount` header holds the number of rows the statement changed. When `query` is a SELECT, the body is instead a List of the rows found, each a Map, and the `CamelSqlRowCount` header holds their number.

Good to know: a message fails when its body is not a JSON object (a JSON array or plain text, for example), or when it has no value for a parameter of `query`. The values are sent to the database apart from the SQL text, so the content of a message cannot change the statement. Do not write `?` in `query`, not even in a quoted string: the Kamelet then fails to start. The connection is encrypted and the certificate of the server is checked: for a self-signed certificate, as a new installation has, set `trustServerCertificate` to true. The JDBC driver of SQL Server is not included: add `mvn:com.microsoft.sqlserver:mssql-jdbc` to the dependencies of the integration. Camel JBang (`camel run`) adds it by itself.

## Configuration Options

The following table summarizes the configuration options available for the `sqlserver-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database to connect to on the SQL Server server. | string |  | shop |
| **password** | Password | **Required** The password of the SQL Server login `username`. | string |  |  |
| **query** | Query | **Required** The SQL statement to run for each message, such as an INSERT, UPDATE or DELETE. Write `:#name` where the value of the field `name` of the JSON body goes. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The host name or IP address of the SQL Server server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The SQL Server login to connect with, using SQL Server authentication (a user name and password, not Windows authentication). It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **encrypt** | Encrypt Connection | Whether the connection to SQL Server is encrypted with TLS. When true, the certificate of the server must be trusted by Java, or `trustServerCertificate` must be true. | boolean | true |  |
| **serverPort** | Server Port | The port the SQL Server server listens on. SQL Server uses 1433 unless it was set up otherwise. | string | 1433 |  |
| **trustServerCertificate** | Trust Server Certificate | Whether to accept the certificate of the server without checking it, as needed for a server with a self-signed certificate. Only for development and tests: the connection can then be intercepted. | boolean | false |  |

## Dependencies

At runtime, the `sqlserver-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:sqlserver-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Microsoft SQL Server Sink Kamelet Description

### Enterprise Database Platform

This Kamelet integrates with Microsoft SQL Server, a comprehensive database platform that provides enterprise-class data management and business intelligence capabilities.

### JDBC Driver

Uses the Microsoft SQL Server JDBC driver for optimal connectivity and performance. The driver supports modern SQL Server features and security protocols.

### Security Configuration

Provides configurable encryption and certificate trust options:

-   Connection encryption can be enabled/disabled based on security requirements
    
-   Server certificate trust settings can be configured for different deployment scenarios
    

### Data Processing

Processes JSON input data through unmarshalling before SQL execution. This enables integration with modern JSON-based applications and data pipelines.

### Parameterized Queries

Supports secure SQL query execution using named parameters (e.g., `:#username`, `:#city`) that map to JSON data fields, preventing SQL injection vulnerabilities.

### Connection Management

Utilizes Apache Commons DBCP2 for efficient connection pooling, ensuring optimal resource utilization and performance in enterprise environments.

### Default Port Configuration

Uses SQL Server’s default port 1433, with configurable port settings for custom installations and security configurations.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/sqlserver-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/sqlserver-sink.kamelet.yaml)