# ![message timestamp router action](_images/kamelets/message-timestamp-router-action.svg) Message Timestamp Router Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Changes the topic that `kafka-sink` writes a record to, to a name made of the original topic name and a date read from a field of the JSON body.

Use it to spread the records over one topic per day or per month by a date in the data, such as the date of an order, in a flow from `kafka-source` to `kafka-sink`. To use the time the record was written to Kafka instead use `timestamp-router-action`.

Input: a JSON object as JSON text, with the `Content-Type` header set to `application/json`. The name of the topic is read from the `CamelKafkaTopic` header, which `kafka-source` sets.

Output: the same JSON object, as JSON text in a stream, with `Content-Type` set to `application/json`. When one of the `timestampKeys` fields is found, the `CamelKafkaOverrideTopic` header is set to the new name, and `kafka-sink` writes the record to that topic instead of its own `topic`.

Good to know: a field value that cannot be read as a date with `timestampKeyFormat` makes the message fail. The default `topicFormat` of `topic-$[timestamp]` gives names such as `topic-20240703`, without the original name: set it to `$[topic]-$[timestamp]` to keep it. The date is in UTC.

## Configuration Options

The following table summarizes the configuration options available for the `message-timestamp-router-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **timestampKeys** | Timestamp Keys | **Required** The names of the top-level fields of the JSON body that may hold the date, separated by commas. The first one present is used; when none is, the topic is not changed. | string |  | orderDate,createdAt |
| **timestampFormat** | Timestamp Format | How to write the time in the topic name, as a Java `SimpleDateFormat` pattern, in UTC: `yyyyMMdd` gives `20240703`, and `yyyy-MM` gives `2024-07`. | string | yyyyMMdd | yyyy-MM-dd |
| **timestampKeyFormat** | Timestamp Keys Format | How the date is written in the field: `timestamp` for a number of milliseconds since 1970, or a Java `SimpleDateFormat` pattern, read in UTC. | string | timestamp | yyyy-MM-dd |
| **topicFormat** | Topic Format | The name of the new topic. `$[topic]` is replaced by the name of the original topic, and `$[timestamp]` by the time, written with `timestampFormat`. The default writes to topics named `topic-` and the date, without the original name. | string | topic-$\[timestamp\] | $\[topic\]-$\[timestamp\] |

## Dependencies

At runtime, the `message-timestamp-router-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:message-timestamp-router-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/message-timestamp-router-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/message-timestamp-router-action.kamelet.yaml)