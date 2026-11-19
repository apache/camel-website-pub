# ![extract field action](_images/kamelets/extract-field-action.svg) Extract Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Replaces the body of each message that is a JSON object with the value of one of its fields, or copies that value into a header.

Use it to keep only the part of a message you need, such as the `payload` of an event or the `email` of a customer, or, with `headerOutput`, to have that value in a header for a later step while the body stays as it is. To do the opposite, and wrap a body in a field, use `hoist-field-action`.

Input: a JSON object, as JSON text or as parsed JSON (a Map or a Jackson `JsonNode`). The field must be at the top level of the object. A JSON array, or a body that is not JSON, fails.

Output: the body is the value of the field. A text, a number or a boolean is the plain value as text, such as `Ann` or `42`, with `Content-Type: text/plain`. An object or an array is JSON text, such as `{"name":"Ann"}`, with `Content-Type: application/json`. When `headerOutput` is true, the value goes into the header `CamelKameletsExtractFieldName`, or the header named by `headerOutputName`, as it is in the JSON: a text, a number, a boolean, or a Java `Map` or `List` for an object or an array. The body and its `Content-Type` are then left as they were.

Good to know: when the object does not have the field, or the field is `null`, the body is empty and the `Content-Type` header is removed, or with `headerOutput` the header is empty; the message does not fail. The `Content-Type` of the incoming message does not change how the body is read.

## Configuration Options

The following table summarizes the configuration options available for the `extract-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **field** | Field | **Required** The name of the top-level field whose value to take. | string |  | email |
| **headerOutput** | Header Output | If true, the value is put in a header, `CamelKameletsExtractFieldName` unless `headerOutputName` is set, and the body is left as it was. If false, the value replaces the body. | boolean | false |  |
| **headerOutputName** | Header Output Name | The name of the header to put the value in. Only used when `headerOutput` is true. The default, `none`, means the header `CamelKameletsExtractFieldName`. | string | none | customerEmail |
| **strictHeaderCheck** | Strict Header Check | Only used when `headerOutput` is true. If true, and the message already has the header, the header keeps its old value and the value of the field replaces the body instead. | boolean | false |  |
| **trimField** | Trim Field | **Deprecated** Deprecated and ignored. A text value now always comes out as the plain value, such as `Ann`, and an object or an array as JSON text. Kept so that a configuration that sets it still starts. | boolean | false |  |

## Dependencies

At runtime, the `extract-field-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:jackson3
    
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
            uri: "kamelet:extract-field-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/extract-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/extract-field-action.kamelet.yaml)