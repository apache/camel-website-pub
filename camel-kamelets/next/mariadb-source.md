# ![mariadb source](_images/kamelets/mariadb-source.svg) MariaDB Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Query data from a MariaDB Database.

## Configuration Options

The following table summarizes the configuration options available for the `mariadb-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the MariaDB Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured MariaDB Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the MariaDB Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured MariaDB Database. | string |  |  |
| **consumedQuery** | Consumed Query | A query to run on a tuple consumed. | string |  | DELETE FROM accounts where user\_id = :#user\_id |
| **delay** | Delay | The number of milliseconds before the next poll. | integer | 500 |  |
| **serverPort** | Server Port | The server port for the data source. | string | 3306 |  |

## Dependencies

At runtime, the `mariadb-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:mariadb-source"
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

## Mariadb Source Kamelet Description

### Authentication methods

This Kamelet connects to Mariadb using:

-   Database-specific connection credentials
    
-   Username and password authentication
    
-   Connection URL/string configuration
    

### Output format

The Kamelet monitors Mariadb for changes and produces the data in JSON format.

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
  name: mariadb-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: mariadb-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mariadb-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mariadb-source.kamelet.yaml)