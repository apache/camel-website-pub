# ![oracle database sink](_images/kamelets/oracle-database-sink.svg) Oracle Database Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to an Oracle Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

## Configuration Options

The following table summarizes the configuration options available for the `oracle-database-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the Oracle Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured Oracle Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the Oracle Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured Oracle Database. | string |  |  |
| **serverPort** | Server Port | The server port for the data source. | string | 1521 |  |

## Dependencies

At runtime, the `oracle-database-sink` Kamelet relies upon the presence of the following dependencies:

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