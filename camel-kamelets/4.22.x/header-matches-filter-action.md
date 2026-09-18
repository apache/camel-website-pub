# ![header matches filter action](_images/kamelets/header-matches-filter-action.svg) Header Matches Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Filter based on header value compared to regex.

## Configuration Options

The following table summarizes the configuration options available for the `header-matches-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **regex** | Regex | **Required** The Regex to Evaluate against the Kafka topic name. | string |  |  |
| **headerName** | Header Name | The header name to get the value to compare. | string |  | headerName |

## Dependencies

At runtime, the `header-matches-filter-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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
            uri: "kamelet:header-matches-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/header-matches-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/header-matches-filter-action.kamelet.yaml)