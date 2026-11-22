# ![xslt action](_images/kamelets/xslt-action.svg) XSLT Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Transforms each XML message with an XSLT stylesheet, for example to map the XML of one system to the XML or text that another system expects.

Use it to rename, pick, reorder or compute the elements of XML documents, such as the totals of an order, with a stylesheet you write. The stylesheet can use XSLT 3.0, which Saxon runs. To convert between XML and JSON, use `xj-identity-action` or `xj-template-action`; to check XML against an XML Schema, use `xml-schema-validator-action`.

Input: XML as text, bytes or a stream. A header whose name is a parameter of the stylesheet sets that parameter: with `<xsl:param name="channel" select="'web'"/>`, a `channel` header with the value `shop` makes `$channel` give `shop`; without the header it gives `web`.

Output: the body is the result as text (a String): XML, or plain text when the `xsl:output` of the stylesheet says `method="text"`. The `Content-Type` header is not set. The other headers are kept.

Good to know: a body that is not XML fails the message. The DOCTYPE of the message is not used: its entities are not expanded and an entity that points to a file or URL is not read, so an entity reference in the body gives nothing. A message can set every parameter of the stylesheet with a header, so do not let a parameter choose which resource the stylesheet reads. The stylesheet is code you write and trust: XSLT functions such as `document()` can read other resources, such as XML from the classpath. The stylesheet is loaded from a file, the classpath or a URL given by the `template` option; it cannot come from the message. Headers that start with `CamelXslt` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `xslt-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **template** | Template | **Required** Where to load the XSLT stylesheet from, not the stylesheet itself: `file://` followed by the path of a file, `classpath://` followed by a resource in the application, or an `http://` or `https://` URL. | string |  | file:///opt/templates/order.xsl |

## Dependencies

At runtime, the `xslt-action` Kamelet relies upon the presence of the following dependencies:

-   camel:xslt-saxon
    
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
            uri: "kamelet:xslt-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/xslt-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/xslt-action.kamelet.yaml)