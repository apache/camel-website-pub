# ![mask field action](_images/kamelets/mask-field-action.svg) Mask Fields Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Replaces the values of the fields you name in each message that is a JSON object with a fixed value, such as `XXXX`.

Use it to hide card numbers, passwords or personal data before the messages are logged or sent to another system. To remove a field entirely, use `drop-field-action`, or `replace-field-action` for several fields.

Input: a JSON object, as JSON text or as parsed JSON (a Map or a Jackson `JsonNode`). Only the fields at the top level of the object are masked; nested objects are left as they are. A JSON array, or a body that is not JSON, fails.

Output: the object with the masked values; the order of its fields can change. When the `Content-Type` header is `application/json`, the body is JSON text again; otherwise it is parsed JSON (a Jackson `JsonNode`), which `json-serialize-action` turns into JSON text.

Good to know: the replacement must suit the value it replaces. A text value takes any replacement, but a number takes only a number, such as `0`, and a true or false value, an object or a list cannot be masked: such a message fails. A named field that the object does not have is ignored.

## Configuration Options

The following table summarizes the configuration options available for the `mask-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **fields** | Fields | **Required** The names of the top-level fields to mask, separated by commas. | string |  | card,password |
| **replacement** | Replacement | **Required** The value that replaces the value of each masked field. Any text works for a text value; a number value needs a number, such as `0`. | string |  | **\***\* |

## Dependencies

At runtime, the `mask-field-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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
            uri: "kamelet:mask-field-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mask-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mask-field-action.kamelet.yaml)