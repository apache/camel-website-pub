# ![mustache template action](_images/kamelets/mustache-template-action.svg) Mustache Template Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Builds a new message body from a Mustache template, filling in values from the incoming message.

Use it to turn data into text for people or for another system, such as the text of an email or a chat message, or a small JSON or XML document, without writing code. To reshape JSON into other JSON, `jsonata-action` or `jslt-action` is often simpler.

Input: any body. The template sees the body as `{{body}}` and a header as `{{headers.name}}`.

Output: the body is the text the template produced. The headers are kept.

Good to know: the template is loaded from a file, the classpath or a URL given by the `template` option; it cannot come from the message.

## Configuration Options

The following table summarizes the configuration options available for the `mustache-template-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Template | **Required** Where to load the Mustache template from, not the Mustache template itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. | string |  | file:////template.mustache |

## Dependencies

At runtime, the `mustache-template-action` Kamelet relies upon the presence of the following dependencies:

-   camel:mustache
    
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
            uri: "kamelet:mustache-template-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mustache-template-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mustache-template-action.kamelet.yaml)