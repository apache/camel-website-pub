# ![opensearch search source](_images/kamelets/opensearch-search-source.svg) OpenSearch Search Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Search data on OpenSearch.

## Configuration Options

The following table summarizes the configuration options available for the `opensearch-search-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | OpenSearch Cluster Name | **Required** The name of the cluster. | string |  |  |
| **hostAddresses** | Host Addresses | **Required** Comma separated list with ip:port formatted remote transport addresses to use. | string |  |  |
| **indexName** | Index in OpenSearch | **Required** The name of the index to act against. | string |  |  |
| **query** | Query | **Required** The query we want to use to search on OpenSearch. | string |  |  |
| **certificate** | Certificate | The Certificate for accessing the Opensearch cluster. You must encode this value in base64. | string |  |  |
| **enableSSL** | Enable SSL | Do we want to connect using SSL?. | boolean | true |  |
| **password** | Password | Password to connect to OpenSearch. | string |  |  |
| **period** | Period | The time interval between two searches. | integer | 1000 |  |
| **user** | Username | Username to connect to OpenSearch. | string |  |  |

## Dependencies

At runtime, the `opensearch-search-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kamelet
    
-   camel:timer
    
-   camel:opensearch
    
-   camel:gson
    

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
      uri: "kamelet:opensearch-search-source"
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

## Opensearch Search Source Kamelet Description

### Authentication methods

This Kamelet connects to Opensearch Search using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Opensearch Search and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Opensearch Search:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: opensearch-search-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: opensearch-search-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-search-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-search-source.kamelet.yaml)