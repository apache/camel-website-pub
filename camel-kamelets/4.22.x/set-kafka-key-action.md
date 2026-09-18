# ![set kafka key action](_images/kamelets/set-kafka-key-action.svg) Set Kafka Key Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Set Kafka Key based on a specific incoming header value from the message body.

## Configuration Options

The following table summarizes the configuration options available for the `set-kafka-key-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **headerName** | Field | **Required** The name of the header to set as Kafka Key. | string |  |  |
| **forceHeaderDeletion** | Force Header Deletion | If true, it will remove the header with name headerName from the Exchange after setting it as Kafka Key. | boolean | false |  |

## Dependencies

At runtime, the `set-kafka-key-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    

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
            uri: "kamelet:set-kafka-key-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/set-kafka-key-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/set-kafka-key-action.kamelet.yaml)