# ![timestamp router action](_images/kamelets/timestamp-router-action.svg) Timestamp Router Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Changes the topic that `kafka-sink` writes a record to, to a name made of the original topic name and the date of the record, such as `orders-20240703`.

Use it to spread the records over one topic per day or per month, in a flow from `kafka-source` to `kafka-sink`, for example to keep or delete them by period. To take the date from a field of a JSON body instead use `message-timestamp-router-action`.

Input: a message from `kafka-source`, with the name of the topic in the `CamelKafkaTopic` header and the time of the record, in milliseconds since 1970, in the `CamelKafkaTimestamp` header. `topicHeaderName` and `timestampHeaderName` choose other headers.

Output: the same body. The `CamelKafkaOverrideTopic` header is set to the new name, and `kafka-sink` writes the record to that topic instead of its own `topic`.

Good to know: the default `topicFormat` of `topic-$[timestamp]` gives names such as `topic-20240703`, without the original name: set it to `$[topic]-$[timestamp]` to keep it. The date is in UTC. Without a time header, nothing changes.

## Configuration Options

The following table summarizes the configuration options available for the `timestamp-router-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **timestampFormat** | Timestamp Format | How to write the time in the topic name, as a Java `SimpleDateFormat` pattern, in UTC: `yyyyMMdd` gives `20240703`, and `yyyy-MM` gives `2024-07`. | string | yyyyMMdd | yyyy-MM-dd |
| **timestampHeaderName** | Timestamp Header Name | The header that holds the time of the record, in milliseconds since 1970, as a number or as text. `kafka-source` sets `CamelKafkaTimestamp`. | string | CamelKafkaTimestamp | kafka-timestamp |
| **topicFormat** | Topic Format | The name of the new topic. `$[topic]` is replaced by the name of the original topic, and `$[timestamp]` by the time, written with `timestampFormat`. The default writes to topics named `topic-` and the date, without the original name. | string | topic-$\[timestamp\] | $\[topic\]-$\[timestamp\] |
| **topicHeaderName** | Topic Header Name | The header that holds the name of the original topic. When it is not set, `CamelKafkaTopic`, which `kafka-source` sets, is used. | string |  | kafka-topic |

## Dependencies

At runtime, the `timestamp-router-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:timestamp-router-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/timestamp-router-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/timestamp-router-action.kamelet.yaml)