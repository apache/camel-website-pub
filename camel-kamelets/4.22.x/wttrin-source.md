# ![wttrin source](_images/kamelets/wttrin-source.svg) wttr.in Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Get weather forecasts from the wttr.in weather forecast service

## Configuration Options

The following table summarizes the configuration options available for the `wttrin-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **output** | Output Type | The type of output. | string | current | current, weather, full |
| **period** | Period | The interval between fetches to the wttr.in service in milliseconds. | integer | 60000 |  |
| **wttrLanguage** | Language | The language to use for displaying weather forecasts. | string |  | am ar af be bn ca da de el et fr fa hi hu ia id it lt mg nb nl oc pl pt-br ro ru ta tr th uk vi zh-cn zh-tw |
| **wttrLocation** | Location | The location to get weather forecasts. | string |  | "paris", "~Eiffel+tower", "Москва", "muc", "@stackoverflow.com", "94107", "-78.46,106.79" |

## Dependencies

At runtime, the `wttrin-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:http
    
-   camel:jackson
    
-   camel:jsonpath
    
-   camel:kamelet
    
-   camel:timer
    

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
      uri: "kamelet:wttrin-source"
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

## Wttrin Source Kamelet Description

### Authentication methods

This Kamelet connects to Wttrin using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Wttrin and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Wttrin:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: wttrin-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: wttrin-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/wttrin-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/wttrin-source.kamelet.yaml)