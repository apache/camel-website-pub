# ![topic name matches filter action](_images/kamelets/topic-name-matches-filter-action.svg) Kafka Topic Name Matches Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Filter based on kafka topic value compared to regex.

## Configuration Options

The following table summarizes the configuration options available for the `topic-name-matches-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **regex** | Regex | **Required** The Regex to Evaluate against the Kafka topic name. | string |  |  |

## Dependencies

At runtime, the `topic-name-matches-filter-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:topic-name-matches-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/topic-name-matches-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/topic-name-matches-filter-action.kamelet.yaml)