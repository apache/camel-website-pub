# ![hoist field action](_images/kamelets/hoist-field-action.svg) Hoist Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Wraps the body of each message in a new JSON object, as the value of the one field you name.

Use it to nest the whole message under one name, for example to turn `{"id":1}` into `{"order":{"id":1}}` for a system that expects that shape. To do the opposite, and take the value out of a field, use `extract-field-action`.

Input: any body. JSON is nested as a JSON object or array when it is parsed JSON (a Map or a Jackson `JsonNode`), or JSON text with the `Content-Type` header `application/json`. Any other text, including JSON text with another `Content-Type`, becomes a text value: `hello` gives `{"order":"hello"}`.

Output: the body is the new JSON object, as JSON text in bytes, and the `Content-Type` header is set to `application/json`.

## Configuration Options

The following table summarizes the configuration options available for the `hoist-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **field** | Field | **Required** The name of the field that holds the body in the new JSON object. | string |  | order |

## Dependencies

At runtime, the `hoist-field-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:hoist-field-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/hoist-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/hoist-field-action.kamelet.yaml)