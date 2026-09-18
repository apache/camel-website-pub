# ![solr source](_images/kamelets/solr-source.svg) Solr Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Query for documents to Solr Collection.

## Configuration Options

The following table summarizes the configuration options available for the `solr-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | Collection | **Required** Solr Collection name. | string |  |  |
| **period** | Period between Polls | **Required** The interval between fetches to the Solr collection. | integer | 10000 |  |
| **query** | Query | **Required** The query to submit to Solr. | string |  |  |
| **servers** | Servers | **Required** Comma separated list of Solr Servers and ports. | string |  |  |
| **password** | Password | Password to connect to Solr. | string |  |  |
| **username** | Username | Username to connect to Solr. | string |  |  |

## Dependencies

At runtime, the `solr-source` Kamelet relies upon the presence of the following dependencies:

-   camel:solr
    
-   camel:core
    
-   camel:timer
    
-   camel:jackson
    
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
      uri: "kamelet:solr-source"
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

## Solr Source Kamelet Description

### Authentication methods

This Kamelet connects to Solr using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Solr and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Solr:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: solr-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: solr-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/solr-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/solr-source.kamelet.yaml)