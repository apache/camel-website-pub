# ![xml schema validator action](_images/kamelets/xml-schema-validator-action.svg) XML Schema Validator Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Checks that each XML message matches an XML Schema (XSD), and fails the messages that do not.

Use it to stop bad data early, for example to reject the orders that miss a required element or carry a wrong value before they reach another system. For JSON, use `json-schema-validator-action`; to change the XML, use `xslt-action`.

Input: XML as text, bytes or a stream.

Output: the same message, unchanged, when it matches the schema: text stays text and bytes stay bytes.

Good to know: a message that does not match the schema, or that is not XML, fails with an error that lists what is wrong, such as `cvc-datatype-valid.1.2.1: 'abc' is not a valid value for 'decimal'.`; it is not dropped silently, so the error handling of the integration decides what happens to it. A message whose DOCTYPE has an entity that points to a file or URL fails, and so does one with entities nested so deep that they pass the entity expansion limit of Java. The schema is loaded from the `template` location; it cannot come from the message.

## Configuration Options

The following table summarizes the configuration options available for the `xml-schema-validator-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Schema Location | **Required** Where to load the XML Schema (XSD) from, not the XML Schema itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. | string |  | file:///etc/camel/order.xsd |

## Dependencies

At runtime, the `xml-schema-validator-action` Kamelet relies upon the presence of the following dependencies:

-   camel:validator
    
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
            uri: "kamelet:xml-schema-validator-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/xml-schema-validator-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/xml-schema-validator-action.kamelet.yaml)