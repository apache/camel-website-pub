# ![oracle database source](_images/kamelets/oracle-database-source.svg) Oracle Database Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs an SQL query in an Oracle Database database again and again, and sends each row it returns as a message, as a JSON object.

Use it to pick up the rows that another application adds to a table, such as new orders or events, and pass them on to another system. To write rows, use `oracle-database-sink`.

Output: the body is one row as JSON text, an object with the column names as keys, such as `{"ID":1,"USERNAME":"oscerd","CITY":"Rome"}` (Oracle gives the names in upper case). The `Content-Type` header is `application/json`.

Good to know: the query runs again half a second after the previous run, so the same rows are sent again and again, unless `consumedQuery` marks or deletes each row once it is sent and `query` leaves such rows out: for example `SELECT * FROM accounts WHERE processed = false` with `UPDATE accounts SET processed = true WHERE id = :#id`. When the next step fails for a row, `consumedQuery` is not run for it, and the row is read again. A query that finds no rows sends nothing. `query` cannot contain `?`. The format of date and time columns in the JSON depends on the Camel version. The JDBC driver of Oracle Database is not included: add `mvn:com.oracle.database.jdbc:ojdbc17` to the dependencies of the integration. Camel JBang (`camel run`) adds it by itself.

## Configuration Options

The following table summarizes the configuration options available for the `oracle-database-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The service name of the database to connect to, such as `FREEPDB1` or `ORCLPDB1`. It is a service name, not a SID. | string |  | ORCLPDB1 |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **query** | Query | **Required** The SQL query to run on each poll, usually a SELECT. Each row it returns becomes a message. | string |  | SELECT \* FROM accounts WHERE processed = false |
| **serverName** | Server Name | **Required** The host name or IP address of the Oracle Database server, without the port. | string |  | db.example.com |
| **username** | Username | **Required** The database user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **consumedQuery** | Consumed Query | An SQL statement to run after each row has been sent on, to mark the row as read or to delete it, so that `query` does not return it again. Write `:#column` where the value of a column of that row goes, such as `:#id`. When it is not set, nothing is changed, and the same rows are read on every poll. | string |  | UPDATE accounts SET processed = true WHERE id = :#id |
| **serverPort** | Server Port | The port of the Oracle listener on the server. Oracle uses 1521 unless it was set up otherwise. | string | 1521 |  |

## Dependencies

At runtime, the `oracle-database-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:oracle-database-source"
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

## Oracle Database Source Kamelet Description

### Authentication methods

This Kamelet connects to Oracle Database with the user name and password of a database user, set in `username` and `password`.

### Output format

The Kamelet runs `query` again every half second, and sends each row it returns as a message: a JSON object with the column names as keys. Without `consumedQuery`, the same rows are read again on every run.

### Configuration

The Kamelet requires database connection parameters:

-   `serverName` and `serverPort` (1521 by default): where the Oracle listener runs
    
-   `databaseName`: the service name of the database, such as `ORCLPDB1`
    
-   `username` and `password`: the database user to log in as
    
-   `query`: the SQL query to run, such as `SELECT * FROM accounts WHERE processed = false`
    
-   `consumedQuery` (optional): an SQL statement run for each row once it is sent, to mark the row as read or delete it, such as `UPDATE accounts SET processed = true WHERE id = :#id`
    

### Usage example

The route below logs each account that is not processed yet, and marks it as processed.

```yaml
- route:
    from:
      uri: "kamelet:oracle-database-source"
      parameters:
        serverName: "db.example.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "ORCLPDB1"
        query: "SELECT * FROM accounts WHERE processed = false"
        consumedQuery: "UPDATE accounts SET processed = true WHERE id = :#id"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/oracle-database-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/oracle-database-source.kamelet.yaml)