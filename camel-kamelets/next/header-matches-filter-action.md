# ![header matches filter action](_images/kamelets/header-matches-filter-action.svg) Header Matches Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Keeps only the messages whose value of a given header matches a regular expression, and drops all others.

Use it to pass on only some messages, for example only the events whose `type` header has the form `order-` followed by a number, or only the messages of some customers by a `customerId` header. To check only that a header is there, or has one exact value, `has-header-filter-action` is simpler, and to filter Kafka records by their topic, use `topic-name-matches-filter-action`.

Input: any message. The header named by `headerName` is read.

Output: the same message, unchanged, when the value of the header matches `regex`. Otherwise, and when the message does not have the header, the message is dropped and nothing is sent on.

Good to know: the expression must match the whole value, not only a part of it: `order-[0-9]+` matches `order-1` but not `x-order-1`, and it is case-sensitive. `headerName` must be set: the Kamelet does not start without it.

## Configuration Options

The following table summarizes the configuration options available for the `header-matches-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **headerName** | Header Name | **Required** The name of the header whose value is matched, such as `type`. It must be set: the Kamelet does not start without it. | string |  | type |
| **regex** | Regular Expression | **Required** A Java regular expression that the whole value of the header must match for the message to be kept. For example, `order-[0-9]+` keeps the values `order-1` and `order-55`. | string |  | order-\[0-9\]+ |

## Dependencies

At runtime, the `header-matches-filter-action` Kamelet relies upon the presence of the following dependencies:

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