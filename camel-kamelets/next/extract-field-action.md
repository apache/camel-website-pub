# ![extract field action](_images/kamelets/extract-field-action.svg) Extract Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Replaces the body of each message that is a JSON object with the value of one of its fields, or copies that value into a header.

Use it to keep only the part of a message you need, such as the `payload` of an event or the `email` of a customer, or, with `headerOutput`, to have that value in a header for a later step while the body stays as it is. To do the opposite, and wrap a body in a field, use `hoist-field-action`.

Input: a JSON object, as JSON text or as parsed JSON (a Map or a Jackson `JsonNode`). The field must be at the top level of the object. A JSON array, or a body that is not JSON, fails.

Output: the body is the value of the field. When the `Content-Type` header is `application/json`, it is JSON text, so a text value keeps its quotes (`"Ann"`) unless `trimField` is true; otherwise it is the value itself, such as the text `Ann`. When `headerOutput` is true, the value goes into the header `CamelKameletsExtractFieldName`, or the header named by `headerOutputName`, and the body is left as it was.

Good to know: when the object does not have the field, the body or the header is empty (the JSON text `null` when the `Content-Type` header is `application/json`); the message does not fail.

## Configuration Options

The following table summarizes the configuration options available for the `extract-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **field** | Field | **Required** The name of the top-level field whose value to take. | string |  | email |
| **headerOutput** | Header Output | If true, the value is put in a header, `CamelKameletsExtractFieldName` unless `headerOutputName` is set, and the body is left as it was. If false, the value replaces the body. | boolean | false |  |
| **headerOutputName** | Header Output Name | The name of the header to put the value in. Only used when `headerOutput` is true. The default, `none`, means the header `CamelKameletsExtractFieldName`. | string | none | customerEmail |
| **strictHeaderCheck** | Strict Header Check | Only used when `headerOutput` is true. If true, and the message already has the header, the header keeps its old value and the value of the field replaces the body instead. | boolean | false |  |
| **trimField** | Trim Field | If true, the body is the plain value, such as `Ann`, instead of JSON text such as `"Ann"`. It changes something only when the `Content-Type` header is `application/json`, and that header is then left as it is. | boolean | false |  |

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