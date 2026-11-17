# ![jolt transformation action](_images/kamelets/jolt-transformation-action.svg) Jolt Transformation Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reshapes each JSON message into other JSON, as a Jolt specification describes: moves, renames, removes fields or adds defaults.

Use it to map the JSON of one system to the JSON another system expects, for example to rename fields or move them into a nested object, when you already have Jolt specifications. `jslt-action` does the same with a query language, and is often easier to write.

Input: parsed JSON, a Map (or a List). Since Camel 4.24, JSON text, bytes and a stream work too. With older versions they do not fail but give an empty body, and so does the parsed JSON of `json-deserialize-action`.

Output: the body is the result as parsed JSON, a Map (or a List), not JSON text. Add `json-serialize-action` after it to get JSON text. The headers are kept.

Good to know: the specification cannot read headers, only the body. It is loaded from a file, the classpath or a URL given by the `template` option; it cannot come from the message.

## Configuration Options

The following table summarizes the configuration options available for the `jolt-transformation-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Template | **Required** Where to load the Jolt specification from, not the Jolt specification itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. With the default `transform`, the file holds a JSON array of steps, such as `[\{"operation": "shift", "spec": \{"name": "customer.fullName"}}]`. | string |  | file:///opt/templates/order-spec.json |
| **transform** | Transform DSL | The kind of Jolt specification in the `template` file. `Chainr`, the default, is a list of steps, each with an `operation` (such as `shift`, `default` or `remove`) and a `spec`. The others take the spec of one operation alone: `Shiftr` moves and renames fields, `Defaultr` adds default values, `Removr` removes fields, and `Sortr` sorts the fields by name. Enum values: \* Chainr \* Shiftr \* Defaultr \* Removr \* Sortr | string | Chainr |  |

## Dependencies

At runtime, the `jolt-transformation-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jolt
    
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
            uri: "kamelet:jolt-transformation-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jolt-transformation-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jolt-transformation-action.kamelet.yaml)