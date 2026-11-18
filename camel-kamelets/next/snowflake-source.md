# ![snowflake source](_images/kamelets/snowflake-source.svg) Snowflake Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Runs an SQL query in a Snowflake database again and again, and sends each row it returns as a message, as a JSON object.

Use it to pick up the rows that another application adds to a table, such as new orders or events, and pass them on to another system. To write rows, use `snowflake-sink`.

Output: the body is one row as JSON text, an object with the column names as keys, such as `{"id":1,"username":"oscerd","city":"Rome"}`. The `Content-Type` header is `application/json`.

Good to know: the query runs again `delay` milliseconds after the previous run, so the same rows are sent again and again, unless `consumedQuery` marks or deletes each row once it is sent and `query` leaves such rows out: for example `SELECT * FROM accounts WHERE processed = false` with `UPDATE accounts SET processed = true WHERE id = :#id`. When the next step fails for a row, `consumedQuery` is not run for it, and the row is read again. A query that finds no rows sends nothing. `query` cannot contain `?`. The format of date and time columns in the JSON depends on the Camel version.

## Configuration Options

The following table summarizes the configuration options available for the `snowflake-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **instanceUrl** | Account Host Name | **Required** The host name of your Snowflake account, without `https://`: your account identifier followed by `.snowflakecomputing.com`, as in the address you open Snowflake at. | string |  | myorg-myaccount.snowflakecomputing.com |
| **password** | Password | **Required** The password of the Snowflake user `username`. | string |  |  |
| **query** | Query | **Required** The SQL query to run on each poll, usually a SELECT. Each row it returns becomes a message. | string |  | SELECT \* FROM accounts WHERE processed = false |
| **username** | Username | **Required** The Snowflake user to log in as. It needs the rights to run the queries of this Kamelet on their tables. | string |  |  |
| **consumedQuery** | Consumed Query | An SQL statement to run after each row has been sent on, to mark the row as read or to delete it, so that `query` does not return it again. Write `:#column` where the value of a column of that row goes, such as `:#id`. When it is not set, nothing is changed, and the same rows are read on every poll. | string |  | UPDATE accounts SET processed = true WHERE id = :#id |
| **databaseName** | Database Name | The Snowflake database that holds the tables `query` names. | string |  | SHOP |
| **delay** | Delay | How long to wait after one run of `query` before the next, in milliseconds. | integer | 500 |  |

## Dependencies

At runtime, the `snowflake-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:net.snowflake:snowflake-jdbc:4.3.4
    
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
      uri: "kamelet:snowflake-source"
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

## Snowflake Source Kamelet Description

### Authentication methods

This Kamelet connects to Snowflake with the user name and password of a Snowflake user, set in `username` and `password`.

### Output format

The Kamelet runs `query` again every `delay` milliseconds, and sends each row it returns as a message: a JSON object with the column names as keys. Without `consumedQuery`, the same rows are read again on every run.

### Configuration

The Kamelet requires database connection parameters:

-   `instanceUrl`: the host name of your Snowflake account, such as `myorg-myaccount.snowflakecomputing.com`
    
-   `databaseName` (optional): the Snowflake database that holds the tables
    
-   `username` and `password`: the Snowflake user to log in as
    
-   `query`: the SQL query to run, such as `SELECT * FROM accounts WHERE processed = false`
    
-   `consumedQuery` (optional): an SQL statement run for each row once it is sent, to mark the row as read or delete it, such as `UPDATE accounts SET processed = true WHERE id = :#id`
    

### Usage example

The route below logs each account that is not processed yet, and marks it as processed.

```yaml
- route:
    from:
      uri: "kamelet:snowflake-source"
      parameters:
        instanceUrl: "myorg-myaccount.snowflakecomputing.com"
        username: "dbuser"
        password: "dbpass"
        databaseName: "SHOP"
        query: "SELECT * FROM accounts WHERE processed = false"
        consumedQuery: "UPDATE accounts SET processed = true WHERE id = :#id"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-source.kamelet.yaml)