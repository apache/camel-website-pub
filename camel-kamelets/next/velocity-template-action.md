# ![velocity template action](_images/kamelets/velocity-template-action.svg) Velocity Template Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Builds a new message body from an Apache Velocity template, filling in values from the incoming message.

Use it to turn data into text for people or for another system, such as an email, a report or a small XML or JSON document, when you already have Velocity templates or need its loops and conditions. For simple templates, `mustache-template-action` is an alternative; to reshape JSON into other JSON, `jslt-action` is often simpler.

Input: any body. The template sees the body as `${body}` and a header as `${headers.name}`, for example `Dear ${headers.customer}, your order ${body} has shipped.`

Output: the body is the text the template produced. The headers are kept.

Good to know: a value the template uses that is missing, such as a header that is not set, stays in the text as written, for example `${headers.customer}`; write `$!{headers.customer}` to get nothing instead. A template file that cannot be found fails the message. The template is loaded from a file, the classpath or a URL given by the `template` option; it cannot come from the message.

## Configuration Options

The following table summarizes the configuration options available for the `velocity-template-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Template | **Required** Where to load the Velocity template from, not the Velocity template itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. | string |  | file:///opt/templates/order.vm |

## Dependencies

At runtime, the `velocity-template-action` Kamelet relies upon the presence of the following dependencies:

-   camel:velocity
    
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
            uri: "kamelet:velocity-template-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/velocity-template-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/velocity-template-action.kamelet.yaml)