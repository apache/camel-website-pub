# ![json deserialize action](_images/kamelets/json-deserialize-action.svg) Json Deserialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns a body of JSON text into parsed JSON, a Jackson `JsonNode`, so that the next steps can work with its fields.

Use it to prepare a message for a step that needs parsed JSON rather than text, such as `jsonata-action`, or to make sure that a body is well-formed JSON. To turn parsed data back into JSON text, use `json-serialize-action`, and to check JSON against a schema, use `json-schema-validator-action`.

Input: JSON text, as text or bytes: a JSON object or a JSON array.

Output: the body is parsed JSON, a Jackson `JsonNode`: an object node for a JSON object, an array node for a JSON array. The `Content-Type` header is removed.

Good to know: a body that is not valid JSON fails the message.

## Configuration Options

The `json-deserialize-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `json-deserialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:jackson3
    

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
            uri: "kamelet:json-deserialize-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/json-deserialize-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/json-deserialize-action.kamelet.yaml)