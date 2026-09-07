# ![couchbase source](_images/kamelets/couchbase-source.svg) Couchbase Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Poll a Couchbase bucket and emit the results.

By default the bucket is queried with the N1QL statement given in the statement property. Set useView to true to poll a MapReduce view instead, selected with designDocumentName and viewName.

## Configuration Options

The following table summarizes the configuration options available for the `couchbase-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucket** | Bucket | **Required** The bucket to use. | string |  |  |
| **couchbaseHostname** | Hostname | **Required** The hostname to use. | string |  |  |
| **protocol** | Protocol | **Required** The protocol to use. | string |  |  |
| **connectionString** | Connection String | The full Couchbase SDK connection string (e.g. couchbase://host:port). When set, it takes precedence over hostname extraction for the KV service port. | string |  |  |
| **couchbasePort** | Port | The port to use. | integer | 8091 |  |
| **delay** | Delay | The number of milliseconds between each poll. | integer | 500 |  |
| **descending** | Descending | Return the results in descending order. | boolean | false |  |
| **designDocumentName** | Design Document Name | The design document to query. Only used when useView is true. | string | beer |  |
| **fullDocument** | Full Document | Emit the whole document rather than only the fields the query or view returns. | boolean | false |  |
| **limit** | Limit | The maximum number of documents to return per poll. A negative value means no limit. | integer | \-1 |  |
| **password** | Password | Password to connect to Couchbase. | string |  |  |
| **skip** | Skip | How many documents to skip before returning results. A negative value means none. | integer | \-1 |  |
| **statement** | N1QL Statement | The N1QL query to run against the bucket on each poll. Used unless useView is true. | string |  | SELECT \* FROM `travel-sample` LIMIT 10 |
| **useView** | Use View | Poll a MapReduce view instead of running the N1QL statement. | boolean | false |  |
| **username** | Username | Username to connect to Couchbase. | string |  |  |
| **viewName** | View Name | The view to query. Only used when useView is true. | string | brewery\_beers |  |

## Dependencies

At runtime, the `couchbase-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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
      uri: "kamelet:couchbase-source"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-source.kamelet.yaml)