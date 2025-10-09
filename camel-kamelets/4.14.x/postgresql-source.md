# ![postgresql source](_images/kamelets/postgresql-source.svg) PostgreSQL Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Query data from a PostgreSQL Database.

## Configuration Options

The following table summarizes the configuration options available for the `postgresql-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the PostgreSQL Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured PostgreSQL Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the PostgreSQL Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured PostgreSQL Database. | string |  |  |
| **consumedQuery** | Consumed Query | A query to run on a tuple consumed. | string |  | DELETE FROM accounts where user\_id = :#user\_id |
| **delay** | Delay | The number of milliseconds before the next poll. | integer | 500 |  |
| **serverPort** | Server Port | The server port for the data source. | string | 5432 |  |

## Dependencies

At runtime, the `postgresql-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:org.postgresql:postgresql:42.7.7
    
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
      uri: "kamelet:postgresql-source"
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

## PostgreSQL Source Kamelet Description

### Authentication

This Kamelet requires username and password authentication to connect to a PostgreSQL database. The credentials are configured through the `username` and `password` properties.

### Configuration

The PostgreSQL Source Kamelet supports the following configurations:

-   **Server Name**: The hostname or IP address of the PostgreSQL server (required)
    
-   **Username**: Username for database authentication (required)
    
-   **Password**: Password for database authentication (required)
    
-   **Query**: SQL query to execute (required)
    
-   **Database Name**: Name of the PostgreSQL database (required)
    
-   **Server Port**: Port number for the PostgreSQL server (default: 5432)
    
-   **Period**: Interval between query executions in milliseconds
    
-   **Connection Properties**: Additional JDBC connection properties
    

### Output Format

The Kamelet outputs query results as JSON objects. Each row from the result set is converted to a JSON object with column names as keys.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:postgresql-source"
      parameters:
        serverName: "postgres.example.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "analytics"
        query: "SELECT * FROM events WHERE created_at > NOW() - INTERVAL '1 hour'"
        period: 30000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Complex Query

```yaml
- route:
    from:
      uri: "kamelet:postgresql-source"
      parameters:
        serverName: "postgres.example.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "ecommerce"
        query: "SELECT o.id, o.total, u.email FROM orders o JOIN users u ON o.user_id = u.id WHERE o.status = 'PENDING'"
        period: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Connection Management

The kamelet manages PostgreSQL connections automatically, including connection pooling and reconnection on failures. Query execution is scheduled at the specified interval with robust error handling.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-source.kamelet.yaml)