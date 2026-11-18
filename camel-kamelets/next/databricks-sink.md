# ![databricks sink](_images/kamelets/databricks-sink.svg) Databricks Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Runs an SQL statement, such as an INSERT, on a Databricks SQL warehouse or cluster for each message, with values taken from the fields of the JSON object in the body.

Use it to store records from another system as rows of a table, such as each order that arrives on a Kafka topic, or to update or delete rows. To read rows, use `databricks-source`.

Input: the body is one JSON object, as text, such as `{"username":"oscerd","city":"Rome"}`. In `query`, write `:#username` where the value of the field `username` goes. When the object has no field of that name, the header of that name is used instead. Fields that `query` does not name are ignored.

Output: the body afterwards is the JSON object as a Map, and the `CamelSqlUpdateCount` header holds the number of rows the statement changed. When `query` is a SELECT, the body is instead a List of the rows found, each a Map, and the `CamelSqlRowCount` header holds their number.

Good to know: a message fails when its body is not a JSON object (a JSON array or plain text, for example), or when it has no value for a parameter of `query`. The values are sent to the database apart from the SQL text, so the content of a message cannot change the statement. Do not write `?` in `query`, not even in a quoted string: the Kamelet then fails to start.

## Configuration Options

The following table summarizes the configuration options available for the `databricks-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** A Databricks personal access token, created in the Developer part of the settings of your Databricks user. The Kamelet runs the queries as the user who created it. | string |  |  |
| **httpPath** | HTTP Path | **Required** The path of the SQL warehouse or cluster to run the queries on. Find it as HTTP path in the Connection details of the SQL warehouse or cluster. | string |  | /sql/1.0/warehouses/abc123def456 |
| **query** | Query | **Required** The SQL statement to run for each message, such as an INSERT, UPDATE or DELETE. Write `:#name` where the value of the field `name` of the JSON body goes. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverHostname** | Server Hostname | **Required** The host name of your Databricks workspace, without `https://`. Find it as Server hostname in the Connection details of the SQL warehouse or cluster. | string |  | adb-1234567890123456.7.azuredatabricks.net |
| **extraOptions** | Extra Options | More settings of the Databricks JDBC driver, added to the end of the connection string as they are. Start with `;` and separate the settings with `;`, such as `;ConnCatalog=main;ConnSchema=default` to choose the catalog and schema of Unity Catalog that `query` uses. | string |  | ;ConnCatalog=main;ConnSchema=default |
| **serverPort** | Server Port | The port to connect to. Databricks uses 443 (HTTPS). | string | 443 |  |

## Dependencies

At runtime, the `databricks-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:databricks-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/databricks-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/databricks-sink.kamelet.yaml)