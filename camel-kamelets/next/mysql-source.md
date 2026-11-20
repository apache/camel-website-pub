# ![mysql source](_images/kamelets/mysql-source.svg) MySQL Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL query in a MySQL database again and again, and sends each row it returns as a message, as a JSON object.

Use it to pick up the rows that another application adds to a table, such as new orders or events, and pass them on to another system. To write rows, use `mysql-sink`.

Output: the body is one row as JSON text (a stream), an object with the column names as keys, such as `{"id":1,"username":"oscerd","city":"Rome"}`. When `useIterator` is false, the body is instead one JSON array with all the rows of a poll. The `Content-Type` header is `application/json`.

Good to know: the query runs again `delay` milliseconds after the previous run, so the same rows are sent again and again, unless `consumedQuery` marks or deletes each row once it is sent and `query` leaves such rows out: for example `SELECT * FROM accounts WHERE processed = false` with `UPDATE accounts SET processed = true WHERE id = :#id`. When the next step fails for a row, `consumedQuery` is not run for it, and the row is read again, unless `onConsumeFailed` marks it. A query that finds no rows sends nothing. `maxMessagesPerPoll` limits how many rows one poll sends. `query` cannot contain `?`. The format of date and time columns in the JSON depends on the Camel version. The JDBC driver of MySQL is not included: add `mvn:com.mysql:mysql-connector-j` to the dependencies of the integration. Camel JBang (`camel run`) adds it by itself. Without `connectionProperties`, the connection uses TLS only when the server offers it, and the certificate of the server is not checked: set `sslMode=REQUIRED` in `connectionProperties` to insist on TLS.

## Configuration Options

The following table summarizes the configuration options available for the `mysql-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database to connect to on the MySQL server. | string |  | shop |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **query** | Query | **Required** The SQL query to run on each poll, usually a SELECT. Each row it returns becomes a message. | string |  | SELECT \* FROM accounts WHERE processed = false |
| **serverName** | Server Name | **Required** The host name or IP address of the MySQL server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The database user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **connectionProperties** | Connection Properties | Extra settings for the MySQL JDBC driver (Connector/J), as `name=value` pairs separated by `;`, such as `sslMode=REQUIRED;connectTimeout=10000`. Use it for TLS: `sslMode=REQUIRED` makes the connection use TLS, and `sslMode=DISABLED` turns TLS off. When it is not set, the driver uses TLS when the server offers it, without checking the certificate. The value is not hidden like a password, and it can show in the log when the integration starts, so do not put a password in it. | string |  | sslMode=REQUIRED |
| **consumedQuery** | Consumed Query | An SQL statement to run after each row has been sent on, to mark the row as read or to delete it, so that `query` does not return it again. Write `:#column` where the value of a column of that row goes, such as `:#id`. When it is not set, nothing is changed, and the same rows are read on every poll. | string |  | UPDATE accounts SET processed = true WHERE id = :#id |
| **delay** | Delay | How long to wait after one run of `query` before the next, in milliseconds. | integer | 500 |  |
| **initialDelay** | Initial Delay | How long to wait after the start before the first run of `query`, in milliseconds. When it is not set, the first run is one second after the start. | integer |  | 10000 |
| **maxIdle** | Max Idle Connections | The most unused connections to keep open for later. A connection that is given back when this many are unused already is closed. When it is not set, up to 8 are kept open. | integer |  | 2 |
| **maxMessagesPerPoll** | Max Rows Per Poll | The most rows to read in one poll. The other rows are read by the next polls, as long as `consumedQuery` marks the rows that were sent and `query` leaves them out. When it is not set, every row that `query` returns is sent. | integer |  | 100 |
| **maxTotal** | Max Connections | The most connections to the database that the Kamelet opens at the same time. While it sends the rows of a poll, the Kamelet keeps one connection, and `consumedQuery`, `onConsumeFailed` and `onConsumeBatchComplete` each need a second one, so do not set it to 1 when you use them. When all of them are in use, the next message waits for one to be free, as long as `maxWaitMillis` allows. When it is not set, the limit is 8. | integer |  | 20 |
| **maxWaitMillis** | Max Wait | How long to wait for a free connection when `maxTotal` connections are in use, in milliseconds. After that, the message fails. When it is not set, it waits as long as it takes. | integer |  | 5000 |
| **onConsumeBatchComplete** | Poll Complete Query | An SQL statement to run once after all the rows of one poll have been sent on, such as an UPDATE that marks them all at once. It cannot use `:#column`. It does not run when the query finds no rows. A row added after `query` ran is not sent in this poll, so make sure the statement does not mark it. | string |  | UPDATE poll\_status SET last\_poll = CURRENT\_TIMESTAMP |
| **onConsumeFailed** | Failed Row Query | An SQL statement to run instead of `consumedQuery` when the next step fails for a row, to mark the row as failed so that `query` leaves it out. Write `:#column` where the value of a column of that row goes, such as `:#id`. When it is not set, nothing is changed for a failed row, and it is read again on the next poll. | string |  | UPDATE accounts SET failed = true WHERE id = :#id |
| **routeEmptyResultSet** | Send Empty Result | Whether to send a message with an empty JSON array, `[]`, when `query` finds no rows. Only used when `useIterator` is false. When it is not set, nothing is sent when no rows are found. | boolean |  |  |
| **serverPort** | Server Port | The port the MySQL server listens on. MySQL uses 3306 unless it was set up otherwise. | string | 3306 |  |
| **useIterator** | One Message Per Row | Whether to send each row as a message of its own. When false, all the rows of one poll are sent as one message, a JSON array of objects, such as `[\{"id":1},\{"id":2}]`. `consumedQuery` and `onConsumeFailed` then cannot use `:#column`, but `onConsumeBatchComplete` can mark all the rows at once. When it is not set, each row is a message. | boolean |  |  |

## Dependencies

At runtime, the `mysql-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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
    
-   **Connection Properties**: Extra settings for the MySQL JDBC driver, such as `sslMode=REQUIRED` to always use TLS
    

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

### Connecting with TLS

Set `connectionProperties` to pass settings to the MySQL JDBC driver (Connector/J), as `name=value` pairs separated by `;`. Without it, the driver uses TLS only when the server offers it, and does not check the certificate of the server. Set `sslMode=REQUIRED` to always use TLS.

```yaml
connectionProperties: "sslMode=REQUIRED"
```

### Reading Rows in Batches

`maxMessagesPerPoll` limits how many rows one poll sends. The other rows are read by the next polls, because `consumedQuery` marks the rows that were sent and `query` leaves them out. `onConsumeFailed` marks a row when the next step fails for it, so that it is not read again and again. `initialDelay` sets how long to wait before the first poll, in milliseconds (one second when not set).

```yaml
- route:
    from:
      uri: "kamelet:mysql-source"
      parameters:
        serverName: "db.example.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "shop"
        query: "SELECT * FROM accounts WHERE processed = 0 AND failed = 0"
        consumedQuery: "UPDATE accounts SET processed = 1 WHERE id = :#id"
        onConsumeFailed: "UPDATE accounts SET failed = 1 WHERE id = :#id"
        maxMessagesPerPoll: 100
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### All the Rows of a Poll in One Message

With `useIterator` set to false, each poll that finds rows sends one message: a JSON array with all of them. Set `routeEmptyResultSet` to true to also get a message, `[]`, from a poll that finds none.

`consumedQuery` and `onConsumeFailed` cannot use `:#column` in this mode. `onConsumeBatchComplete` runs once after the message is sent, and can mark all the rows at once. A row added after `query` ran is not in the message, so such a statement must not mark it: the example below is only safe when nothing adds rows while the Kamelet polls.

```yaml
- route:
    from:
      uri: "kamelet:mysql-source"
      parameters:
        serverName: "db.example.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "shop"
        query: "SELECT * FROM accounts WHERE processed = 0"
        useIterator: false
        onConsumeBatchComplete: "UPDATE accounts SET processed = 1 WHERE processed = 0"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Connection Pool

The Kamelet keeps a pool of connections to the database:

-   `maxTotal`: the most connections it opens at the same time, 8 when not set.
    
-   `maxIdle`: the most unused connections it keeps open, 8 when not set.
    
-   `maxWaitMillis`: how long a message waits for a free connection when `maxTotal` are in use, in milliseconds, before it fails. When not set, it waits as long as it takes.
    

While it sends the rows of a poll, the source keeps one connection, and `consumedQuery`, `onConsumeFailed` and `onConsumeBatchComplete` each need a second one. Do not set `maxTotal` to 1 when you use them: they then wait for a connection for ever, or fail after `maxWaitMillis`.

```yaml
maxTotal: 4
maxIdle: 2
maxWaitMillis: 5000
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mysql-source.kamelet.yaml)