# ![mariadb sink](_images/kamelets/mariadb-sink.svg) MariaDB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to a MariaDB Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

## Configuration Options

The following table summarizes the configuration options available for the `mariadb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the MariaDB Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured MariaDB Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the MariaDB Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured MariaDB Database. | string |  |  |
| **serverPort** | Server Port | The server port for the data source. | string | 3306 |  |

## Dependencies

At runtime, the `mariadb-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:sql
    
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mariadb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mariadb-sink.kamelet.yaml)