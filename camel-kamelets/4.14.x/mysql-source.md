# ![mysql source](_images/kamelets/mysql-source.svg) MySQL Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Query data from a MySQL Database.

## Configuration Options

The following table summarizes the configuration options available for the `mysql-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the MySQL Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured MySQL Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the MySQL Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured MySQL Database. | string |  |  |
| **consumedQuery** | Consumed Query | A query to run on a tuple consumed. | string |  | DELETE FROM accounts where user\_id = :#user\_id |
| **delay** | Delay | The number of milliseconds before the next poll. | integer | 500 |  |
| **serverPort** | Server Port | The server port for the data source. | string | 3306 |  |

## Dependencies

At runtime, the `mysql-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:mysql-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## MySQL Source Kamelet Description

### Authentication

This Kamelet requires username and password authentication to connect to a MySQL database. The credentials are configured through the `username` and `password` properties.

### Configuration

The MySQL Source Kamelet supports the following configurations:

-   **Server Name**: The hostname or IP address of the MySQL server (required)
    
-   **Username**: Username for database authentication (required)
    
-   **Password**: Password for database authentication (required)
    
-   **Query**: SQL query to execute (required)
    
-   **Database Name**: Name of the MySQL database (required)
    
-   **Server Port**: Port number for the MySQL server (default: 3306)
    
-   **Period**: Interval between query executions in milliseconds
    
-   **Connection Properties**: Additional JDBC connection properties
    

### Output Format

The Kamelet outputs query results as JSON objects. Each row from the result set is converted to a JSON object with column names as keys.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:mysql-source"
      parameters:
        serverName: "mysql.example.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "orders"
        query: "SELECT * FROM orders WHERE status = 'PENDING'"
        period: 30000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Custom Port

```yaml
- route:
    from:
      uri: "kamelet:mysql-source"
      parameters:
        serverName: "mysql.example.com"
        serverPort: "3307"
        username: "dbuser"
        password: "dbpass"
        databaseName: "analytics"
        query: "SELECT id, name, created_at FROM users WHERE created_at > NOW() - INTERVAL 1 HOUR"
        period: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Parameterized Query

```yaml
- route:
    from:
      uri: "kamelet:mysql-source"
      parameters:
        serverName: "mysql.example.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "inventory"
        query: "SELECT * FROM products WHERE stock_level < 10"
        period: 120000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Connection Management

The kamelet manages database connections automatically, including connection pooling and reconnection on failures. Query execution is scheduled at the specified interval.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-source.kamelet.yaml)