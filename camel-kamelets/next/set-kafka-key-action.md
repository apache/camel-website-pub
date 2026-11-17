# ![set kafka key action](_images/kamelets/set-kafka-key-action.svg) Set Kafka Key Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sets the key of the Kafka record to the value of a header of the message.

Use it before `kafka-sink` when the records need a key, for example so that all the records of one customer go to the same partition and stay in order.

Input: any message with the header named by `headerName`.

Output: the same body. The `CamelKafkaKey` header, which `kafka-sink` uses as the record key, is set to the value of that header.

Good to know: to build the key from fields of the body instead, use `value-to-key-action`.

## Configuration Options

The following table summarizes the configuration options available for the `set-kafka-key-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **headerName** | Header Name | **Required** The name of the header whose value becomes the key of the Kafka record. | string |  | customerId |
| **forceHeaderDeletion** | Force Header Deletion | If true, the header named by `headerName` is removed from the message after its value is copied to the key. | boolean | false |  |

## Dependencies

At runtime, the `set-kafka-key-action` Kamelet relies upon the presence of the following dependencies:

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