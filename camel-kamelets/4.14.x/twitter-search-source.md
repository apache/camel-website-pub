# ![twitter search source](_images/kamelets/twitter-search-source.svg) Twitter Search Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Allows to get all tweets on particular keywords from Twitter.

## Configuration Options

The following table summarizes the configuration options available for the `twitter-search-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** The Access Token from the Twitter application in the developer portal. | string |  |  |
| **accessTokenSecret** | Access Token Secret | **Required** The Access Token Secret from the Twitter application in the developer portal. | string |  |  |
| **apiKey** | API Key | **Required** The API Key from the Twitter application in the developer portal. | string |  |  |
| **apiKeySecret** | API Key Secret | **Required** The API Key Secret from the Twitter application in the developer portal. | string |  |  |
| **keywords** | Keywords | **Required** The keywords to use in the Twitter search (Supports Twitter standard operators). | string |  | Apache Camel |

## Dependencies

At runtime, the `twitter-search-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:twitter
    
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
      uri: "kamelet:twitter-search-source"
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

## Twitter Search Source Kamelet Description

### Authentication methods

This Kamelet connects to Twitter Search using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Twitter Search and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Twitter Search:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: twitter-search-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: twitter-search-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-search-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-search-source.kamelet.yaml)