# ![databricks source](_images/kamelets/databricks-source.svg) Databricks Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Query data from a Databricks Database. For Unity Catalog workspaces, specify catalog and schema parameters.

## Configuration Options

The following table summarizes the configuration options available for the `databricks-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** The personal access token to access Databricks. | string |  |  |
| **httpPath** | HTTP Path | **Required** The HTTP path to the Databricks SQL Warehouse or cluster. | string |  | /sql/1.0/warehouses/abc123def456 |
| **query** | Query | **Required** The query to execute against the Databricks Database. | string |  | SELECT \* FROM accounts |
| **serverHostname** | Server Hostname | **Required** The Databricks server hostname. | string |  | adb-1234567890123456.7.azuredatabricks.net |
| **consumedQuery** | Consumed Query | A query to run on a tuple consumed. | string |  | DELETE FROM accounts where user\_id = :#user\_id |
| **delay** | Delay | The number of milliseconds before the next poll from the Databricks database. | integer | 500 |  |
| **extraOptions** | Extra Options | Additional JDBC connection options (e.g., ConnCatalog=main;ConnSchema=default). | string |  |  |
| **serverPort** | Server Port | The server port for the Databricks data source. | string | 443 |  |

## Dependencies

At runtime, the `databricks-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:com.databricks:databricks-jdbc:3.3.1
    
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