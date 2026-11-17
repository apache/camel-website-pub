# ![predicate filter action](_images/kamelets/predicate-filter-action.svg) Predicate Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Keeps only the JSON messages that match a condition, written as a JSONPath expression, and drops all others.

Use it to pass on only the messages you care about, for example only the orders above a certain amount, or only the events of one customer. To keep or drop messages by a header, use `header-matches-filter-action` or `has-header-filter-action` instead.

Input: a JSON object, as JSON text or as parsed JSON.

Output: the same message, unchanged, when the condition is true. When it is false, the message is dropped and nothing is sent on.

Good to know: a message that does not have the field the condition looks at is dropped too.

## Configuration Options

The following table summarizes the configuration options available for the `predicate-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **expression** | Expression | **Required** The condition a message must meet to be kept, as a JSONPath filter without the surrounding `[?( )]`. `@` is the message. For example, `@.foo =~ /.*John/` keeps the messages whose `foo` field contains `John`, and `@.amount > 100` keeps those whose `amount` is more than 100. | string |  | @.foo =~ /.\*John/ |

## Dependencies

At runtime, the `predicate-filter-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:jsonpath
    

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
            uri: "kamelet:predicate-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/predicate-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/predicate-filter-action.kamelet.yaml)