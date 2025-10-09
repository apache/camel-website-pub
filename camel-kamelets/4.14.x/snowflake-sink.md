# ![snowflake sink](_images/kamelets/snowflake-sink.svg) Snowflake Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Send data to a Snowflake Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

## Configuration Options

The following table summarizes the configuration options available for the `snowflake-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **instanceUrl** | Instance URL | **Required** The Instance url. | string |  | instance.snowflakecomputing.com |
| **password** | Password | **Required** The password to access a secured Snowflake Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the Snowflake Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **username** | Username | **Required** The username to access a secured Snowflake Database. | string |  |  |
| **databaseName** | Database Name | The name of the Snowflake Database. | string |  |  |

## Dependencies

At runtime, the `snowflake-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:net.snowflake:snowflake-jdbc:3.24.2
    
-   mvn:org.apache.commons:commons-dbcp2:2.13.0
    

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
            uri: "kamelet:snowflake-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Snowflake Sink Kamelet Description

### Cloud Data Warehouse

This Kamelet integrates with Snowflake, a cloud-based data warehouse platform that provides scalable data storage and analytics capabilities. Snowflake is designed for modern data architecture and cloud-native applications.

### JDBC Connectivity

Uses the Snowflake JDBC driver for native connectivity to Snowflake instances. The driver provides optimized performance and supports Snowflake-specific features and data types.

### Instance Configuration

Requires configuration of the Snowflake instance URL (e.g., `instance.snowflakecomputing.com`) which uniquely identifies your Snowflake account and region.

### Data Processing

Processes JSON input data through unmarshalling before executing SQL queries. This enables seamless integration with JSON-based data pipelines and streaming applications.

### Query Execution

Supports parameterized SQL queries using named parameters that map to JSON data fields. This ensures secure and efficient data insertion into Snowflake tables.

### Cloud-Native Features

Snowflake’s cloud-native architecture provides automatic scaling, performance optimization, and enterprise-grade security, making this Kamelet suitable for large-scale data operations.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-sink.kamelet.yaml)