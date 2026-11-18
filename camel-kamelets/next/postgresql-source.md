# ![postgresql source](_images/kamelets/postgresql-source.svg) PostgreSQL Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL query in a PostgreSQL database again and again, and sends each row it returns as a message, as a JSON object.

Use it to pick up the rows that another application adds to a table, such as new orders or events, and pass them on to another system. To write rows, use `postgresql-sink`.

Output: the body is one row as JSON text, an object with the column names as keys, such as `{"id":1,"username":"oscerd","city":"Rome"}`. The `Content-Type` header is `application/json`.

Good to know: the query runs again `delay` milliseconds after the previous run, so the same rows are sent again and again, unless `consumedQuery` marks or deletes each row once it is sent and `query` leaves such rows out: for example `SELECT * FROM accounts WHERE processed = false` with `UPDATE accounts SET processed = true WHERE id = :#id`. When the next step fails for a row, `consumedQuery` is not run for it, and the row is read again. A query that finds no rows sends nothing. `query` cannot contain `?`. The format of date and time columns in the JSON depends on the Camel version. Without `connectionProperties`, the connection uses TLS only when the server offers it, and the certificate of the server is not checked: set `sslmode=require` or `sslmode=verify-full` in `connectionProperties` to insist on TLS.

## Configuration Options

The following table summarizes the configuration options available for the `postgresql-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database to connect to on the PostgreSQL server. | string |  | shop |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **query** | Query | **Required** The SQL query to run on each poll, usually a SELECT. Each row it returns becomes a message. | string |  | SELECT \* FROM accounts WHERE processed = false |
| **serverName** | Server Name | **Required** The host name or IP address of the PostgreSQL server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The database user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **connectionProperties** | Connection Properties | Extra settings for the PostgreSQL JDBC driver, as `name=value` pairs separated by `;`, such as `sslmode=require;connectTimeout=10`. Use it for TLS: `sslmode=require` refuses a server that does not offer TLS, and `sslmode=verify-full` also checks the certificate of the server against the CA certificate in the file named by `sslrootcert`. When it is not set, the driver uses TLS when the server offers it, without checking the certificate. The value is not hidden like a password, and it can show in the log when the integration starts, so do not put a password in it. | string |  | sslmode=require |
| **consumedQuery** | Consumed Query | An SQL statement to run after each row has been sent on, to mark the row as read or to delete it, so that `query` does not return it again. Write `:#column` where the value of a column of that row goes, such as `:#id`. When it is not set, nothing is changed, and the same rows are read on every poll. | string |  | UPDATE accounts SET processed = true WHERE id = :#id |
| **delay** | Delay | How long to wait after one run of `query` before the next, in milliseconds. | integer | 500 |  |
| **serverPort** | Server Port | The port the PostgreSQL server listens on. PostgreSQL uses 5432 unless it was set up otherwise. | string | 5432 |  |

## Dependencies

At runtime, the `postgresql-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:org.postgresql:postgresql:42.7.14
    
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
    
-   **Delay**: How long to wait after one run of the query before the next, in milliseconds (default: 500)
    
-   **Consumed Query**: An SQL statement run for each row once it is sent, to mark the row as read or delete it, so that it is not read again
    
-   **Connection Properties**: Extra settings for the PostgreSQL JDBC driver, such as `sslmode=require` to always use TLS
    

### Output Format

The Kamelet sends one message per row of the query result. Each row is a JSON object with the column names as keys. Without `consumedQuery`, the same rows are read again on every run of the query.

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
        delay: 30000
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
        delay: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Connection Management

The kamelet manages PostgreSQL connections automatically, including connection pooling and reconnection on failures. Query execution is scheduled at the specified interval with robust error handling.

### Connecting with TLS

Set `connectionProperties` to pass settings to the PostgreSQL JDBC driver, as `name=value` pairs separated by `;`. Without it, the driver uses TLS only when the server offers it, and does not check the certificate of the server.

-   `sslmode=require`: always use TLS, and fail when the server does not offer it.
    
-   `sslmode=verify-full;sslrootcert=/etc/certs/root.crt`: also check the certificate of the server against the CA certificate in that file.
    

```yaml
connectionProperties: "sslmode=require"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-source.kamelet.yaml)