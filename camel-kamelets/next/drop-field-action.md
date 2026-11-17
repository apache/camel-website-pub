# ![drop field action](_images/kamelets/drop-field-action.svg) Drop Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Removes one field, chosen by its name, from each message that is a JSON object.

Use it to take out a field that the next system does not accept or should not see, such as an internal ID or a password. To remove several fields, or to keep only some, use `replace-field-action`; to keep the field but hide its value, use `mask-field-action`.

Input: a JSON object, as JSON text or as parsed JSON (a Map or a Jackson `JsonNode`). Only the fields at the top level of the object are looked at. A JSON array is passed on unchanged; a body that is not JSON fails.

Output: the same object without the field. When the `Content-Type` header is `application/json`, the body is JSON text again; otherwise it is parsed JSON (a Jackson `JsonNode`), which `json-serialize-action` turns into JSON text.

Good to know: a message without the field is passed on unchanged. A field of the same name inside a nested object is not removed.

## Configuration Options

The following table summarizes the configuration options available for the `drop-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **field** | Field | **Required** The name of the top-level field to remove from the JSON object. | string |  | password |

## Dependencies

At runtime, the `drop-field-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
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
            uri: "kamelet:drop-field-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-field-action.kamelet.yaml)