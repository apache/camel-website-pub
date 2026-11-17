# ![has header filter action](_images/kamelets/has-header-filter-action.svg) Has Header Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Keeps only the messages that have a given header, optionally with a given value, and drops all others.

Use it to pass on only the messages that carry a marker, such as a `priority` header, or only those of one kind, such as the events whose `type` header is `order`. To match the value of a header against a pattern, use `header-matches-filter-action`, and to keep or drop messages by the content of a JSON body, use `predicate-filter-action`.

Input: any message. The header named by `name` is read.

Output: the same message, unchanged, when it has the header and, when `value` is set, when the header has exactly that value. Otherwise the message is dropped and nothing is sent on.

Good to know: the comparison with `value` is case-sensitive: `order` does not match `Order`. A header with an empty value counts as present when `value` is not set.

## Configuration Options

The following table summarizes the configuration options available for the `has-header-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **name** | Header Name | **Required** The name of the header the message must have to be kept, such as `priority`. The header must already be on the message, for example set by the source. With Knative, the name of a CloudEvent attribute starts with `ce-`, such as `ce-type`. | string |  | priority |
| **value** | Header Value | The value the header must have, exactly, for the message to be kept, such as `high`. When it is not set, any value is enough, as long as the header is there. | string |  | high |

## Dependencies

At runtime, the `has-header-filter-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:has-header-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/has-header-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/has-header-filter-action.kamelet.yaml)