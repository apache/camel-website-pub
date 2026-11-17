# ![simple filter action](_images/kamelets/simple-filter-action.svg) Simple Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Drops the messages for which a condition, written in the Camel Simple language, is true, and passes on all others.

Use it to leave out the messages you do not want, for example the test events, with the condition `${header.type} == 'test'`. To keep only the messages that match a condition instead, use `predicate-filter-action` (a condition on a JSON body), `has-header-filter-action` or `header-matches-filter-action`.

Input: any message.

Output: the same message, unchanged, when the condition is false. When it is true, the message is dropped and nothing is sent on.

Good to know: this is the opposite of the other filter actions of the catalog, which keep the messages that match. A condition on a header the message does not have is false, so such a message is passed on.

## Configuration Options

The following table summarizes the configuration options available for the `simple-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **expression** | Condition | **Required** The condition, in the Camel Simple language, that makes a message be dropped. `$\{body}` is the body and `$\{header.name}` the value of a header. For example, `$\{header.type} == 'test'` drops the messages whose `type` header is `test`, and `$\{header.amount} > 100` those whose `amount` header is more than 100. | string |  | ${header.type} == 'test' |

## Dependencies

At runtime, the `simple-filter-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:simple-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/simple-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/simple-filter-action.kamelet.yaml)