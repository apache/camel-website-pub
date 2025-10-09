# ![sqlserver sink](_images/kamelets/sqlserver-sink.svg) Microsoft SQL Server Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to a Microsoft SQL Server Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

## Configuration Options

The following table summarizes the configuration options available for the `sqlserver-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the SQL Server Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured SQL Server Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the SQL Server Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured SQL Server Database. | string |  |  |
| **encrypt** | Encrypt Connection | Encrypt the connection to SQL Server. | boolean | false |  |
| **serverPort** | Server Port | The server port for the data source. | string | 1433 |  |
| **trustServerCertificate** | Trust Server Certificate | Trust Server Certificate. | boolean | true |  |

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