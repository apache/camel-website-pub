# ![drop headers action](_images/kamelets/drop-headers-action.svg) Drop Headers Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Removes from each message all the headers whose names match a pattern, such as `Camel*`.

Use it to remove the internal `Camel*` headers that came with a message from outside before it reaches a sink, or to clear many headers at once before a message goes to another system. To remove a single header by its name, `drop-header-action` is enough.

Input: any message.

Output: the same body, without the headers that match `pattern`. The headers that match `excludePattern` are kept.

Good to know: a pattern is compared with each header name first as an exact name, then as a wildcard when it ends with **(`x-`** matches every name that starts with `x-`), and then as a Java regular expression, such as `x-(one|two)`. None of these comparisons is case-sensitive.

## Configuration Options

The following table summarizes the configuration options available for the `drop-headers-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **pattern** | Header Pattern | **Required** The headers to remove: an exact header name, a text that ends with `*` to match every name that starts with the text before it, or a regular expression. Upper and lower case do not matter. | string |  | Camel\* |
| **excludePattern** | Exclusion Pattern | The headers to keep even when they match `pattern`, written in the same way. When it is not set, every header that matches `pattern` is removed. | string |  | CamelKafkaKey |

## Dependencies

At runtime, the `drop-headers-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:drop-headers-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-headers-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-headers-action.kamelet.yaml)