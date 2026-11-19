# ![xj template action](_images/kamelets/xj-template-action.svg) XJ Template Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Converts each message from XML to JSON, or from JSON to XML, with an XSLT stylesheet that decides what the result looks like.

Use it to map the XML of one system to the JSON of another, or the other way round, when the fixed mapping of `xj-identity-action` does not give the shape you need.

Input: XML or JSON as text, bytes or a stream, as `direction` says. With `JSON2XML` the stylesheet sees the JSON as XML in which each value is an `object` element with its name and type in `xj:name` and `xj:type` attributes, such as `<object xj:name="qty" xj:type="int">2</object>`; select a field with `object[@xj:name='qty']`.

Output: the body is JSON text or XML text. With `XML2JSON` the stylesheet must write that same form, which becomes JSON: `<object xj:type="object"><object xj:name="qty" xj:type="int">2</object></object>` gives `{"qty":2}`. The prefix `xj` stands for the namespace `[http://camel.apache.org/component/xj](http://camel.apache.org/component/xj)`. The headers are kept.

Good to know: the stylesheet is loaded from a file, the classpath or a URL given by the `template` option; it cannot come from the message. Headers that start with `CamelXslt` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `xj-template-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **direction** | Direction | **Required** Which way to convert: `XML2JSON` turns XML into JSON, and `JSON2XML` turns JSON into XML. Enum values: \* XML2JSON \* JSON2XML | string |  |  |
| **template** | Template | **Required** Where to load the XSLT stylesheet from, not the stylesheet itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. | string |  | file:///opt/templates/order.xsl |

## Dependencies

At runtime, the `xj-template-action` Kamelet relies upon the presence of the following dependencies:

-   camel:xj
    
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
            uri: "kamelet:xj-template-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/xj-template-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/xj-template-action.kamelet.yaml)