# ![json schema validator action](_images/kamelets/json-schema-validator-action.svg) Json Schema Validator Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Checks that each JSON message matches a JSON Schema, and fails the messages that do not.

Use it to stop bad data early, for example to reject the orders that miss a required field before they reach a database or another system. To keep or drop messages by a condition instead of failing them, use `predicate-filter-action`.

Input: JSON text, as text, bytes or a stream, or parsed JSON from `json-deserialize-action`. A Map fails.

Output: the same message, unchanged, when it matches the schema.

Good to know: a message that does not match the schema, or that is not JSON, fails with an error that lists what is wrong; it is not dropped silently, so the error handling of the integration decides what happens to it. The schema is loaded from the `template` location; it cannot come from the message.

## Configuration Options

The following table summarizes the configuration options available for the `json-schema-validator-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Schema Location | **Required** Where to load the JSON Schema from, not the JSON Schema itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. | string |  | file:///etc/camel/order-schema.json |

## Dependencies

At runtime, the `json-schema-validator-action` Kamelet relies upon the presence of the following dependencies:

-   camel:json-validator
    
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
            uri: "kamelet:json-schema-validator-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/json-schema-validator-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/json-schema-validator-action.kamelet.yaml)