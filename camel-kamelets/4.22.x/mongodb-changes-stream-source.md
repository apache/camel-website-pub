# ![mongodb changes stream source](_images/kamelets/mongodb-changes-stream-source.svg) MongoDB Changes Stream Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume Changes from MongoDB Collection in streaming mode.

## Configuration Options

The following table summarizes the configuration options available for the `mongodb-changes-stream-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | MongoDB Collection | **Required** Sets the name of the MongoDB collection to bind to this endpoint. | string |  |  |
| **database** | MongoDB Database | **Required** Sets the name of the MongoDB database to target. | string |  |  |
| **hosts** | MongoDB Hosts | **Required** Comma separated list of MongoDB Host Addresses in host:port format. | string |  |  |
| **password** | MongoDB Password | User password for accessing MongoDB. | string |  |  |
| **ssl** | Enable Ssl for Mongodb Connection | whether to enable ssl connection to mongodb. | boolean | true |  |
| **sslValidationEnabled** | Enables Ssl Certificates Validation and Host name checks. | IMPORTANT this should be disabled only in test environment since can pose security issues. | boolean | true |  |
| **streamFilter** | Stream Filter | Filter condition for change streams consumer. | string |  | { '$match':{'$or':\[{'fullDocument.stringValue': 'specificValue'}\]} } |
| **username** | MongoDB Username | Username for accessing MongoDB. The username must be present in the MongoDB’s authentication database (authenticationDatabase). By default, the MongoDB authenticationDatabase is 'admin'. | string |  |  |

## Dependencies

At runtime, the `mongodb-changes-stream-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:mongodb
    
-   camel:jackson
    

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
      uri: "kamelet:mongodb-changes-stream-source"
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

## Mongodb Changes Stream Source Kamelet Description

### Authentication methods

This Kamelet connects to Mongodb Changes Stream using:

-   Database-specific connection credentials
    
-   Username and password authentication
    
-   Connection URL/string configuration
    

### Output format

The Kamelet monitors Mongodb Changes Stream for changes and produces the data in JSON format.

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
  name: mongodb-changes-stream-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: mongodb-changes-stream-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-changes-stream-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-changes-stream-source.kamelet.yaml)