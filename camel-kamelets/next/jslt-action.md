# ![jslt action](_images/kamelets/jslt-action.svg) JSLT Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns each JSON message into new JSON with a JSLT transformation, a query language for JSON that picks, renames and computes fields.

Use it to map the JSON of one system to the JSON another system expects, for example to keep only some fields, rename them or count the items of an order. To build text rather than JSON, use `mustache-template-action`; `jolt-transformation-action` reshapes JSON with Jolt specifications instead.

Input: JSON text, as text, bytes or a stream, or parsed JSON as a Jackson `JsonNode`, such as the output of `json-deserialize-action`. The transformation sees the body as `.` and a header as `$headers.name`, for example `{"customer": .name, "items": size(.items), "source": $headers.origin}`.

Output: the body is the result as JSON text in bytes, and the `Content-Type` header is set to `application/json`. The other headers are kept.

Good to know: a Map fails the message: give the JSON as text. A field whose value is missing, such as a header that is not set, is left out of the result. The transformation is loaded from a file, the classpath or a URL given by the `template` option; it cannot come from the message. Headers that start with `CamelJslt` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `jslt-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Template | **Required** Where to load the JSLT transformation from, not the JSLT transformation itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. | string |  | file:///opt/templates/order.jslt |

## Dependencies

At runtime, the `jslt-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:jslt
    
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
            uri: "kamelet:jslt-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jslt-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jslt-action.kamelet.yaml)