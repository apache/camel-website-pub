# ![sqlserver source](_images/kamelets/sqlserver-source.svg) Microsoft SQL Server Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL query in a Microsoft SQL Server database again and again, and sends each row it returns as a message, as a JSON object.

Use it to pick up the rows that another application adds to a table, such as new orders or events, and pass them on to another system. To write rows, use `sqlserver-sink`.

Output: the body is one row as JSON text, an object with the column names as keys, such as `{"id":1,"username":"oscerd","city":"Rome"}`. The `Content-Type` header is `application/json`.

Good to know: the query runs again `delay` milliseconds after the previous run, so the same rows are sent again and again, unless `consumedQuery` marks or deletes each row once it is sent and `query` leaves such rows out: for example `SELECT * FROM accounts WHERE processed = false` with `UPDATE accounts SET processed = true WHERE id = :#id`. When the next step fails for a row, `consumedQuery` is not run for it, and the row is read again. A query that finds no rows sends nothing. `query` cannot contain `?`. The format of date and time columns in the JSON depends on the Camel version. The connection is encrypted and the certificate of the server is checked: for a self-signed certificate, as a new installation has, set `trustServerCertificate` to true. The JDBC driver of SQL Server is not included: add `mvn:com.microsoft.sqlserver:mssql-jdbc` to the dependencies of the integration. Camel JBang (`camel run`) adds it by itself.

## Configuration Options

The following table summarizes the configuration options available for the `sqlserver-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database to connect to on the SQL Server server. | string |  | shop |
| **password** | Password | **Required** The password of the SQL Server login `username`. | string |  |  |
| **query** | Query | **Required** The SQL query to run on each poll, usually a SELECT. Each row it returns becomes a message. | string |  | SELECT \* FROM accounts WHERE processed = false |
| **serverName** | Server Name | **Required** The host name or IP address of the SQL Server server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The SQL Server login to connect with, using SQL Server authentication (a user name and password, not Windows authentication). It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **consumedQuery** | Consumed Query | An SQL statement to run after each row has been sent on, to mark the row as read or to delete it, so that `query` does not return it again. Write `:#column` where the value of a column of that row goes, such as `:#id`. When it is not set, nothing is changed, and the same rows are read on every poll. | string |  | UPDATE accounts SET processed = true WHERE id = :#id |
| **delay** | Delay | How long to wait after one run of `query` before the next, in milliseconds. | integer | 500 |  |
| **encrypt** | Encrypt Connection | Whether the connection to SQL Server is encrypted with TLS. When true, the certificate of the server must be trusted by Java, or `trustServerCertificate` must be true. | boolean | true |  |
| **serverPort** | Server Port | The port the SQL Server server listens on. SQL Server uses 1433 unless it was set up otherwise. | string | 1433 |  |
| **trustServerCertificate** | Trust Server Certificate | Whether to accept the certificate of the server without checking it, as needed for a server with a self-signed certificate. Only for development and tests: the connection can then be intercepted. | boolean | false |  |

## Dependencies

At runtime, the `sqlserver-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:sqlserver-source"
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

## Microsoft SQL Server Source Kamelet Description

### Authentication methods

This Kamelet connects to SQL Server with the user name and password of a SQL Server login, set in `username` and `password`. The connection is encrypted with TLS by default (`encrypt`); for a server with a self-signed certificate, set `trustServerCertificate` to true, in development and tests only.

### Output format

The Kamelet runs `query` again every `delay` milliseconds, and sends each row it returns as a message: a JSON object with the column names as keys. Without `consumedQuery`, the same rows are read again on every run.

### Configuration

The Kamelet requires database connection parameters:

-   `serverName` and `serverPort` (1433 by default): where the SQL Server runs
    
-   `databaseName`: the database to connect to
    
-   `username` and `password`: the SQL Server login to use
    
-   `query`: the SQL query to run, such as `SELECT * FROM accounts WHERE processed = false`
    
-   `consumedQuery` (optional): an SQL statement run for each row once it is sent, to mark the row as read or delete it, such as `UPDATE accounts SET processed = true WHERE id = :#id`
    

### Usage example

The route below logs each account that is not processed yet, and marks it as processed.

```yaml
- route:
    from:
      uri: "kamelet:sqlserver-source"
      parameters:
        serverName: "db.example.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "shop"
        query: "SELECT * FROM accounts WHERE processed = false"
        consumedQuery: "UPDATE accounts SET processed = true WHERE id = :#id"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/sqlserver-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/sqlserver-source.kamelet.yaml)