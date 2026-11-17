# ![regex router action](_images/kamelets/regex-router-action.svg) Regex Router Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Changes the topic that `kafka-sink` writes a record to, by applying a regular expression and a replacement to the name of the topic it was read from.

Use it to copy records, in a flow from `kafka-source` to `kafka-sink`, to topics with related names, for example from `orders-eu` to `archive-eu`. To add the date to the name use `timestamp-router-action`.

Input: a message from `kafka-source`, with the name of the topic in the `CamelKafkaTopic` header. The same expression is also applied to the `ce-type` header, when there is one.

Output: the same body. When `regex` matches the whole topic name, the `CamelKafkaOverrideTopic` header is set to the name with the match replaced by `replacement`, and `kafka-sink` writes the record to that topic instead of its own `topic`. When `regex` matches the whole `ce-type` header, that header is replaced in the same way.

Good to know: the expression must match the whole name, not a part of it. When it does not match, nothing changes.

## Configuration Options

The following table summarizes the configuration options available for the `regex-router-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **regex** | Regular Expression | **Required** A Java regular expression that the whole topic name must match. Groups in parentheses capture parts of the name for `replacement`. | string |  | orders-(.\*) |
| **replacement** | Replacement | **Required** The new topic name. `$1`, `$2` and so on insert the text that the groups of `regex` captured. | string |  | archive-$1 |

## Dependencies

At runtime, the `regex-router-action` Kamelet relies upon the presence of the following dependencies:

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