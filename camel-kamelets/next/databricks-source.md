# ![databricks source](_images/kamelets/databricks-source.svg) Databricks Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Runs an SQL query on a Databricks SQL warehouse or cluster again and again, and sends each row it returns as a message, as a JSON object.

Use it to pick up the rows that another application adds to a table, such as new orders or events, and pass them on to another system. To write rows, use `databricks-sink`.

Output: the body is one row as JSON text, an object with the column names as keys, such as `{"id":1,"username":"oscerd","city":"Rome"}`. The `Content-Type` header is `application/json`.

Good to know: the query runs again `delay` milliseconds after the previous run, so the same rows are sent again and again, unless `consumedQuery` marks or deletes each row once it is sent and `query` leaves such rows out: for example `SELECT * FROM accounts WHERE processed = false` with `UPDATE accounts SET processed = true WHERE id = :#id`. When the next step fails for a row, `consumedQuery` is not run for it, and the row is read again. A query that finds no rows sends nothing. `query` cannot contain `?`. The format of date and time columns in the JSON depends on the Camel version.

## Configuration Options

The following table summarizes the configuration options available for the `databricks-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** A Databricks personal access token, created in the Developer part of the settings of your Databricks user. The Kamelet runs the queries as the user who created it. | string |  |  |
| **httpPath** | HTTP Path | **Required** The path of the SQL warehouse or cluster to run the queries on. Find it as HTTP path in the Connection details of the SQL warehouse or cluster. | string |  | /sql/1.0/warehouses/abc123def456 |
| **query** | Query | **Required** The SQL query to run on each poll, usually a SELECT. Each row it returns becomes a message. | string |  | SELECT \* FROM accounts WHERE processed = false |
| **serverHostname** | Server Hostname | **Required** The host name of your Databricks workspace, without `https://`. Find it as Server hostname in the Connection details of the SQL warehouse or cluster. | string |  | adb-1234567890123456.7.azuredatabricks.net |
| **consumedQuery** | Consumed Query | An SQL statement to run after each row has been sent on, to mark the row as read or to delete it, so that `query` does not return it again. Write `:#column` where the value of a column of that row goes, such as `:#id`. When it is not set, nothing is changed, and the same rows are read on every poll. | string |  | UPDATE accounts SET processed = true WHERE id = :#id |
| **delay** | Delay | How long to wait after one run of `query` before the next, in milliseconds. | integer | 500 |  |
| **extraOptions** | Extra Options | More settings of the Databricks JDBC driver, added to the end of the connection string as they are. Start with `;` and separate the settings with `;`, such as `;ConnCatalog=main;ConnSchema=default` to choose the catalog and schema of Unity Catalog that `query` uses. | string |  | ;ConnCatalog=main;ConnSchema=default |
| **serverPort** | Server Port | The port to connect to. Databricks uses 443 (HTTPS). | string | 443 |  |

## Dependencies

At runtime, the `databricks-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:com.databricks:databricks-jdbc:3.4.5
    
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
      uri: "kamelet:databricks-source"
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/databricks-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/databricks-source.kamelet.yaml)