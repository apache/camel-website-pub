# ![topic name matches filter action](_images/kamelets/topic-name-matches-filter-action.svg) Kafka Topic Name Matches Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Keeps only the Kafka records whose topic name matches a regular expression, and drops all others.

Use it to handle the records of only some topics, after a `kafka-source` whose `topic` lists several topics or is a pattern, for example only those of `orders-eu`. To keep or drop messages by another header use `header-matches-filter-action`.

Input: a message from `kafka-source`, with the name of the topic in the `CamelKafkaTopic` header.

Output: the same message, unchanged, when `regex` matches the whole topic name. Otherwise the message is dropped and nothing is sent on.

Good to know: the expression must match the whole name: `orders` does not keep the records of `orders-eu`, but `orders.*` does. A message without the `CamelKafkaTopic` header is dropped.

## Configuration Options

The following table summarizes the configuration options available for the `topic-name-matches-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **regex** | Regular Expression | **Required** A Java regular expression that the whole name of the topic must match for the record to be kept. | string |  | orders-.\* |

## Dependencies

At runtime, the `topic-name-matches-filter-action` Kamelet relies upon the presence of the following dependencies:

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