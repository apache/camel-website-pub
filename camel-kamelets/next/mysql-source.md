# ![mysql source](_images/kamelets/mysql-source.svg) MySQL Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL query in a MySQL database again and again, and sends each row it returns as a message, as a JSON object.

Use it to pick up the rows that another application adds to a table, such as new orders or events, and pass them on to another system. To write rows, use `mysql-sink`.

Output: the body is one row as JSON text, an object with the column names as keys, such as `{"id":1,"username":"oscerd","city":"Rome"}`. The `Content-Type` header is `application/json`.

Good to know: the query runs again `delay` milliseconds after the previous run, so the same rows are sent again and again, unless `consumedQuery` marks or deletes each row once it is sent and `query` leaves such rows out: for example `SELECT * FROM accounts WHERE processed = false` with `UPDATE accounts SET processed = true WHERE id = :#id`. When the next step fails for a row, `consumedQuery` is not run for it, and the row is read again. A query that finds no rows sends nothing. `query` cannot contain `?`. The format of date and time columns in the JSON depends on the Camel version. The JDBC driver of MySQL is not included: add `mvn:com.mysql:mysql-connector-j` to the dependencies of the integration. Camel JBang (`camel run`) adds it by itself.

## Configuration Options

The following table summarizes the configuration options available for the `mysql-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database to connect to on the MySQL server. | string |  | shop |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **query** | Query | **Required** The SQL query to run on each poll, usually a SELECT. Each row it returns becomes a message. | string |  | SELECT \* FROM accounts WHERE processed = false |
| **serverName** | Server Name | **Required** The host name or IP address of the MySQL server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The database user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **consumedQuery** | Consumed Query | An SQL statement to run after each row has been sent on, to mark the row as read or to delete it, so that `query` does not return it again. Write `:#column` where the value of a column of that row goes, such as `:#id`. When it is not set, nothing is changed, and the same rows are read on every poll. | string |  | UPDATE accounts SET processed = true WHERE id = :#id |
| **delay** | Delay | How long to wait after one run of `query` before the next, in milliseconds. | integer | 500 |  |
| **serverPort** | Server Port | The port the MySQL server listens on. MySQL uses 3306 unless it was set up otherwise. | string | 3306 |  |

## Dependencies

At runtime, the `mysql-source` Kamelet relies upon the presence of the following dependencies:

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
    
-   **Delay**: How long to wait after one run of the query before the next, in milliseconds (default: 500)
    
-   **Consumed Query**: An SQL statement run for each row once it is sent, to mark the row as read or delete it, so that it is not read again
    

### Output Format

The Kamelet sends one message per row of the query result. Each row is a JSON object with the column names as keys. Without `consumedQuery`, the same rows are read again on every run of the query.

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
        delay: 30000
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
        delay: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with a Filter

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
        delay: 120000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Connection Management

The kamelet manages database connections automatically, including connection pooling and reconnection on failures. Query execution is scheduled at the specified interval.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-source.kamelet.yaml)