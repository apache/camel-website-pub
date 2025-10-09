# ![snowflake source](_images/kamelets/snowflake-source.svg) Snowflake Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Query data from a Snowflake Database.

## Configuration Options

The following table summarizes the configuration options available for the `snowflake-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **instanceUrl** | Instance URL | **Required** The Instance url. | string |  | instance.snowflakecomputing.com |
| **password** | Password | **Required** The password to access a secured Snowflake Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the Snowflake Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **username** | Username | **Required** The username to access a secured Snowflake Database. | string |  |  |
| **consumedQuery** | Consumed Query | A query to run on a tuple consumed. | string |  | DELETE FROM accounts where user\_id = :#user\_id |
| **databaseName** | Database Name | The name of the Snowflake Database. | string |  |  |
| **delay** | Delay | The number of milliseconds before the next poll. | integer | 500 |  |

## Dependencies

At runtime, the `snowflake-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:net.snowflake:snowflake-jdbc:3.24.2
    
-   mvn:org.apache.commons:commons-dbcp2:2.13.0
    

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

This Kamelet connects to Snowflake using:

-   Database-specific connection credentials
    
-   Username and password authentication
    
-   Connection URL/string configuration
    

### Output format

The Kamelet monitors Snowflake for changes and produces the data in JSON format.

### Configuration

The Kamelet requires database connection parameters:

-   Database connection URL/server information
    
-   Username and password for authentication
    
-   Query or monitoring configuration
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: snowflake-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: snowflake-source
    properties:
      serverName: "database-server"
      username: "{{username}}"
      password: "{{password}}"
      databaseName: "mydb"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/snowflake-source.kamelet.yaml)