# ![xj identity action](_images/kamelets/xj-identity-action.svg) XJ Identity Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Converts each message from XML to JSON, or from JSON to XML, with a fixed mapping and no template to write.

Use it to pass XML to a system that expects JSON, or the other way round, when the default mapping is good enough. To control the result, such as the names of the elements or which fields to keep, use `xj-template-action` with an XSLT stylesheet.

Input: XML or JSON as text, bytes or a stream, as `direction` says. Parsed JSON, such as a Map, fails the message.

Output: the body is JSON text or XML text. From XML, the root element is dropped, its attributes and child elements become fields, repeated elements become an array, and all values are text: `<order id="7"><qty>2</qty></order>` gives `{"id":"7","qty":"2"}`. To XML, each JSON value becomes an `object` element that keeps its name and type in `xj:name` and `xj:type` attributes, such as `<object xj:name="qty" xj:type="int">2</object>`. The headers are kept.

Good to know: Headers that start with `CamelXslt` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `xj-identity-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **direction** | Direction | **Required** Which way to convert: `XML2JSON` turns XML into JSON, and `JSON2XML` turns JSON into XML. Enum values: \* XML2JSON \* JSON2XML | string |  |  |

## Dependencies

At runtime, the `xj-identity-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:xj-identity-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/xj-identity-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/xj-identity-action.kamelet.yaml)