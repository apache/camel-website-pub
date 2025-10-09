# ![couchbase sink](_images/kamelets/couchbase-sink.svg) Couchbase Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send documents to Couchbase.

## Configuration Options

The following table summarizes the configuration options available for the `couchbase-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucket** | Bucket | **Required** The bucket to use. | string |  |  |
| **couchbaseHostname** | Hostname | **Required** The hostname to use. | string |  |  |
| **protocol** | Protocol | **Required** The protocol to use. | string |  |  |
| **autoStartId** | Auto Start Id | Auto Start Id or not. | boolean | true |  |
| **connectionString** | Connection String | The full Couchbase SDK connection string (e.g. couchbase://host:port). When set, it takes precedence over hostname extraction for the KV service port. | string |  |  |
| **couchbasePort** | Port | The port to use. | integer | 8091 |  |
| **password** | Password | Password to connect to Couchbase. | string |  |  |
| **startingId** | Starting Id | The starting id. | integer | 1 |  |
| **username** | Username | Username to connect to Couchbase. | string |  |  |

## Dependencies

At runtime, the `couchbase-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:couchbase
    
-   camel:kamelet
    

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
            uri: "kamelet:couchbase-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Couchbase Sink Kamelet Description

### Authentication

This Kamelet uses username and password authentication to connect to Couchbase.

### Configuration

This Kamelet requires configuration of: - Protocol (e.g., http or https) - Hostname of the Couchbase server - Bucket name to store documents - Username and password credentials

Optional settings include: - Port (defaults to 8091) - Starting ID for document inserts (defaults to 1) - Auto start ID flag (defaults to true)

### Document Storage

Documents are stored in the specified Couchbase bucket. The Kamelet can automatically generate document IDs starting from a configurable starting point.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-sink.kamelet.yaml)