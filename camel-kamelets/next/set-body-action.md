# ![set body action](_images/kamelets/set-body-action.svg) Set Body Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Replaces the body of each message with a text you write, which can include values from the message, such as a header.

Use it to send a fixed text or a small JSON document, such as a status message, or to build a short text from headers and the old body. For longer texts, a template Kamelet such as `mustache-template-action` is easier to maintain.

Input: any message. In the text, `${body}` is the old body and `${header.name}` the value of a header.

Output: the body is the text, with the values filled in. The headers are kept as they were, `Content-Type` too, so set it to match the new body when needed, for example with `insert-header-action`.

Good to know: up to Camel 4.23, two closing braces in a row are read as the end of a placeholder and make the Kamelet fail to start, so write nested JSON with a space between them, as `} }`.

## Configuration Options

The following table summarizes the configuration options available for the `set-body-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **value** | Value | **Required** The new body, as text. `$\{body}` is replaced by the old body, `$\{header.name}` by the value of the header `name`, and `$\{date:now:yyyy-MM-dd}` by the current date. | string |  | Order ${header.orderId} received |

## Dependencies

At runtime, the `set-body-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:set-body-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/set-body-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/set-body-action.kamelet.yaml)