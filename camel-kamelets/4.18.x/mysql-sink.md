# ![mysql sink](_images/kamelets/mysql-sink.svg) MySQL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to a MySQL Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

## Configuration Options

The following table summarizes the configuration options available for the `mysql-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the MySQL Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured MySQL Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the MySQL Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured MySQL Database. | string |  |  |
| **serverPort** | Server Port | The server port for the data source. | string | 3306 |  |

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

This Kamelet connects to MySQL databases using the MySQL Connector/J JDBC driver. MySQL is one of the world’s most popular open-source relational database management systems.

### Data Processing

The Kamelet expects JSON input data which is automatically unmarshalled before executing the SQL query. This allows for seamless integration with JSON-based data sources.

### Parameterized Queries

SQL queries use named parameters (e.g., `:#username`, `:#city`) that map to fields in the incoming JSON data. This approach provides protection against SQL injection attacks while maintaining query flexibility.

### Connection Management

Uses Apache Commons DBCP2 for efficient database connection pooling. This provides optimal resource utilization and connection lifecycle management.

### Authentication and Security

Requires username and password authentication for database access. The Kamelet uses the latest MySQL JDBC driver which supports modern security features and protocols.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-sink.kamelet.yaml)