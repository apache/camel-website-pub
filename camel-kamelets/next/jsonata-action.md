# ![jsonata action](_images/kamelets/jsonata-action.svg) Jsonata Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Transforms each JSON message with a JSONata expression, to reshape it, pick out fields, or compute new values.

Use it to turn the JSON of one system into the JSON another system expects, for example to rename fields, join a first and a last name, or add up the lines of an order. For other ways to reshape JSON, see `jslt-action` and `jolt-transformation-action`; to build text, such as an email, from a template, use `mustache-template-action`.

Input: parsed JSON, such as a Map, a List, or the output of `json-deserialize-action`.

Output: the body is the result of the expression, as parsed JSON (a Jackson `JsonNode`), not as text: add `json-serialize-action` after it to get JSON text. The headers are kept.

Good to know: put `json-deserialize-action` before it when the body is JSON text, as depending on the Camel version the expression sees JSON text as one string rather than as an object, and bytes or a stream fail. The expression is loaded from the `template` location; it cannot come from the message. Headers that start with `CamelJsonata` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `jsonata-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Expression Location | **Required** Where to load the JSONata expression from, not the JSONata expression itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. | string |  | file:///etc/camel/order.jsonata |

## Dependencies

At runtime, the `jsonata-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jsonata
    
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
            uri: "kamelet:jsonata-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jsonata-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jsonata-action.kamelet.yaml)