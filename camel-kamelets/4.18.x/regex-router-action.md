# ![regex router action](_images/kamelets/regex-router-action.svg) Regex Router Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Update the destination using the configured regular expression and replacement string.

## Configuration Options

The following table summarizes the configuration options available for the `regex-router-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **regex** | Regex | **Required** Regular Expression for destination. | string |  |  |
| **replacement** | Replacement | **Required** Replacement when matching. | string |  |  |

## Dependencies

At runtime, the `regex-router-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
-   camel:kafka
    

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
            uri: "kamelet:regex-router-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/regex-router-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/regex-router-action.kamelet.yaml)