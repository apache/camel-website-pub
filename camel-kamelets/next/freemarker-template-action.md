# ![freemarker template action](_images/kamelets/freemarker-template-action.svg) Freemarker Template Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Builds a new message body from a FreeMarker template, filling in values from the incoming message.

Use it to turn data into text for people or for another system, such as an email, a report or a small XML or JSON document, when you already have FreeMarker templates or need its loops and conditions. For simple templates, `mustache-template-action` is an alternative; to reshape JSON into other JSON, `jslt-action` is often simpler.

Input: any body. The template sees the body as `${body}` and a header as `${headers.name}`, for example `Dear ${headers.customer}, your order ${body} has shipped.`

Output: the body is the text the template produced. The headers are kept.

Good to know: a value the template uses that is missing, such as a header that is not set, fails the message; give a default with `${headers.customer!""}`. A template file that cannot be found fails the message too. The template is loaded from a file, the classpath or a URL given by the `template` option; it cannot come from the message. Headers that start with `CamelFreemarker` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `freemarker-template-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Template | **Required** Where to load the FreeMarker template from, not the FreeMarker template itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. | string |  | file:///opt/templates/order.ftl |

## Dependencies

At runtime, the `freemarker-template-action` Kamelet relies upon the presence of the following dependencies:

-   camel:freemarker
    
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
            uri: "kamelet:freemarker-template-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/freemarker-template-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/freemarker-template-action.kamelet.yaml)