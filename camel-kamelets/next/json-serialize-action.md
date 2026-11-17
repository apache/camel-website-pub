# ![json serialize action](_images/kamelets/json-serialize-action.svg) Json Serialize Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Turns a body of parsed data, such as a Map, a List or parsed JSON, into JSON text.

Use it to send parsed data to a sink that needs JSON text, for example after `jsonata-action` or `json-deserialize-action`, whose output is parsed JSON. To do the opposite, use `json-deserialize-action`.

Input: parsed data: a Map, a List, or parsed JSON (a Jackson `JsonNode`).

Output: the body is JSON text, as a stream of bytes. The `Content-Type` header is set to `application/json`.

Good to know: a body that is already text becomes one JSON string, in quotes: `hello` becomes `"hello"`, and JSON text is quoted the same way. Do not use it on a body that is already JSON text.

## Configuration Options

The `json-serialize-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `json-serialize-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:jackson
    

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
            uri: "kamelet:json-serialize-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/json-serialize-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/json-serialize-action.kamelet.yaml)