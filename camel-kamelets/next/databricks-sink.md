# ![databricks sink](_images/kamelets/databricks-sink.svg) Databricks Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Send data to a Databricks Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters. For Unity Catalog workspaces, specify catalog and schema parameters.

## Configuration Options

The following table summarizes the configuration options available for the `databricks-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** The personal access token to access Databricks. | string |  |  |
| **httpPath** | HTTP Path | **Required** The HTTP path to the Databricks SQL Warehouse or cluster. | string |  | /sql/1.0/warehouses/abc123def456 |
| **query** | Query | **Required** The query to execute against the Databricks Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverHostname** | Server Hostname | **Required** The Databricks server hostname. | string |  | adb-1234567890123456.7.azuredatabricks.net |
| **extraOptions** | Extra Options | Additional JDBC connection options (e.g., ConnCatalog=main;ConnSchema=default). | string |  |  |
| **serverPort** | Server Port | The server port for the Databricks data source. | string | 443 |  |

## Dependencies

At runtime, the `databricks-sink` Kamelet relies upon the presence of the following dependencies:

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