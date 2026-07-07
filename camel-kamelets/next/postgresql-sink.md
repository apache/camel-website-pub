# ![postgresql sink](_images/kamelets/postgresql-sink.svg) PostgreSQL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to a PostgreSQL Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

## Configuration Options

The following table summarizes the configuration options available for the `postgresql-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the PostgreSQL Database. | string |  |  |
| **password** | Password | **Required** The password to access a secured PostgreSQL Database. | string |  |  |
| **query** | Query | **Required** The query to execute against the PostgreSQL Database. | string |  | INSERT INTO accounts (username,city) VALUES (:#username,:#city) |
| **serverName** | Server Name | **Required** The server name for the data source. | string |  | localhost |
| **username** | Username | **Required** The username to access a secured PostgreSQL Database. | string |  |  |
| **serverPort** | Server Port | The server port for the data source. | string | 5432 |  |

## Dependencies

At runtime, the `postgresql-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:sql
    
-   mvn:org.postgresql:postgresql:42.7.13
    
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
            uri: "kamelet:postgresql-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## PostgreSQL Sink Kamelet Description

### Input Format

This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

### Query Example

Here is an example query:

```sql
INSERT INTO accounts (username,city) VALUES (:#username,:#city)
```

Here is example input for the example query:

```json
{ "username":"oscerd", "city":"Rome"}
```

### Authentication

The Kamelet requires username and password authentication to connect to the PostgreSQL database.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/postgresql-sink.kamelet.yaml)