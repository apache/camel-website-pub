# ![sqlserver source](_images/kamelets/sqlserver-source.svg) Microsoft SQL Server Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Query data from a Microsoft SQL Server Database.

## Configuration Options

The following table summarizes the configuration options available for the `sqlserver-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured SQL Server Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the SQL Server Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured SQL Server Database. | string |  |  |
| **consumedQuery** | Consumed Query | A query to run on a tuple consumed. | string |  | DELETE FROM accounts where user\_id = :#user\_id |
| **delay** | Delay | The number of milliseconds before the next poll. | integer | 500 |  |
| **encrypt** | Encrypt Connection | Encrypt the connection to SQL Server. | boolean | true |  |
| **serverPort** | Server Port | The server port for the data source. | string | 1433 |  |
| **trustServerCertificate** | Trust Server Certificate | Trust the server certificate without validating it against a certificate authority. Intended for development and test environments only. | boolean | false |  |

## Dependencies

At runtime, the `sqlserver-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
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

## Sqlserver Source Kamelet Description

### Authentication methods

This Kamelet connects to Sqlserver using:

-   Database-specific connection credentials
    
-   Username and password authentication
    
-   Connection URL/string configuration
    

### Output format

The Kamelet monitors Sqlserver for changes and produces the data in JSON format.

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
  name: sqlserver-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: sqlserver-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/sqlserver-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/sqlserver-source.kamelet.yaml)