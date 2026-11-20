# ![value to key action](_images/kamelets/value-to-key-action.svg) Value to Key Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sets the key of the Kafka record to some fields of the JSON body, so that records with the same values in those fields get the same key.

Use it to take the key of the record from the data, before `kafka-sink`, for example the customer of an order, so that all the records of one customer go to the same partition and stay in order. To take the key from a header instead use `set-kafka-key-action`.

Input: a JSON object as JSON text, with the `Content-Type` header set to `application/json`.

Output: the same JSON object, as JSON text in bytes, with `Content-Type` set to `application/json`. The `CamelKafkaKey` header, which `kafka-sink` uses as the key of the record, is set to a Map of the fields named in `fields` and their values.

Good to know: `kafka-sink` writes the key as text such as `{id=7, customer=acme}`, not as JSON, and not necessarily with the fields in the order of `fields`. A field that is not in the body is left out of the key.

## Configuration Options

The following table summarizes the configuration options available for the `value-to-key-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **fields** | Fields | **Required** The names of the top-level fields of the JSON body that make up the key, separated by commas. | string |  | id,customer |

## Dependencies

At runtime, the `value-to-key-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
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
            uri: "kamelet:value-to-key-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/value-to-key-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/value-to-key-action.kamelet.yaml)