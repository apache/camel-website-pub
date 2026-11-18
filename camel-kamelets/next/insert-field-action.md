# ![insert field action](_images/kamelets/insert-field-action.svg) Insert Field Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Adds a field with a value you choose to each message that is a JSON object, or replaces the value when the field is already there.

Use it to tag records with where they come from or which environment they passed through, or to add a value from a header or the current date. To add a header instead of a field, use `insert-header-action`.

Input: a JSON object, as JSON text or as parsed JSON (a Map or a Jackson `JsonNode`). When the body is a JSON array, the value is added at the end of the array and `field` is not used. A body that is not JSON fails.

Output: the object with the field. When the `Content-Type` header is `application/json`, the body is JSON text again; otherwise it is parsed JSON (a Jackson `JsonNode`), which `json-serialize-action` turns into JSON text.

Good to know: the value is always added as a JSON text value, in quotes, even when it looks like a number. The field is added at the top level of the object.

## Configuration Options

The following table summarizes the configuration options available for the `insert-field-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **field** | Field | **Required** The name of the top-level field to add. When the object already has a field of this name, its value is replaced. | string |  | source |
| **value** | Value | **Required** The value of the new field, as text. It can include values from the message: `$\{header.name}` is the value of a header, `$\{date:now:yyyy-MM-dd}` the current date. | string |  | shop-${header.region} |

## Dependencies

At runtime, the `insert-field-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:insert-field-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/insert-field-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/insert-field-action.kamelet.yaml)