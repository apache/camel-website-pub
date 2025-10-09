# ![twitter timeline source](_images/kamelets/twitter-timeline-source.svg) Twitter Timeline Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Allows to get tweets from the timeline of a specific user from Twitter.

## Configuration Options

The following table summarizes the configuration options available for the `twitter-timeline-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** The Access Token from the Twitter application in the developer portal. | string |  |  |
| **accessTokenSecret** | Access Token Secret | **Required** The Access Token Secret from the Twitter application in the developer portal. | string |  |  |
| **apiKey** | API Key | **Required** The API Key from the Twitter application in the developer portal. | string |  |  |
| **apiKeySecret** | API Key Secret | **Required** The API Key Secret from the Twitter application in the developer portal. | string |  |  |
| **user** | User | **Required** The user we want to read the timeline. | string |  | ApacheCamel |

## Dependencies

At runtime, the `twitter-timeline-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:twitter-timeline-source"
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

## Twitter Timeline Source Kamelet Description

### Authentication methods

This Kamelet connects to Twitter Timeline using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Twitter Timeline and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Twitter Timeline:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: twitter-timeline-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: twitter-timeline-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-timeline-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-timeline-source.kamelet.yaml)