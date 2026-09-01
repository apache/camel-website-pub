# XML Tokenize

**Since Camel 2.14**

The XML Tokenize language (xtokenize) is a tokenizer specifically designed for XML documents. Unlike the conventional [Tokenize language](tokenize-language.md), which is primarily a text-based tokenizer, XML Tokenize uses a StAX parser to interpret the XML structure while producing tokens.

The conventional Tokenize language also provides an xml option for XML-aware tokenization (xml=true). This should not be confused with XML Tokenize: xtokenize uses different tokenization semantics and is intended for different use cases.

Use xtokenize when XML structure or namespaces are important, or when you want a tokenizer specifically designed for XML documents. Use the conventional Tokenize language when you primarily need text-based tokenization and XML awareness is sufficient for your use case.

Maven users will need to add the following dependency to their `pom.xml` for this language:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-stax</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## XML Tokenizer Options

The XML Tokenize language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **mode** (common) | `i` | `Enum` | 
The extraction mode. The available extraction modes are: i - injecting the contextual namespace bindings into the extracted token (default), w - wrapping the extracted token in its ancestor context, u - unwrapping the extracted token to its child content, t - extracting the text content of the specified element.

Enum values:

-   i
    
-   w
    
-   u
    
-   t
    





 |
| **group** (common) |  | `Integer` | To group N parts together. |
| **source** (common) |  | `String` | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Example

Suppose the input XML contains multiple orders:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<orders xmlns="urn:shop">
    <order>
        <id>1001</id>
        <customer>John</customer>
    </order>
    <order>
        <id>1002</id>
        <customer>Jane</customer>
    </order>
</orders>
```

The XML Tokenize language can be used with the Split EIP to split the document into one message for each `order` element.

-   Java
    
-   XML
    
-   YAML
    

```java
var ns = new org.apache.camel.support.builder.Namespaces("shop", "urn:shop");

from("direct:start")
  .split()
    .xtokenize("//shop:order", 'i', ns)
      .streaming()
    .to("mock:order");
```

```xml
<route>
    <from uri="direct:start"/>
    <split streaming="true">
        <xtokenize>//shop:order
            <namespace key="shop" value="urn:shop"/>
        </xtokenize>
        <to uri="mock:order"/>
    </split>
</route>
```

```yaml
- route:
    from:
      uri: 'direct:start'
      steps:
        - split:
            streaming: 'true'
            expression:
              xtokenize:
                expression: '//shop:order'
                namespace:
                  - key: shop
                    value: 'urn:shop'
            steps:
              - to:
                  uri: 'mock:order'
```

The Split EIP produces two messages. The body of the first message is:

Output message 1

```xml
<order xmlns="urn:shop">
    <id>1001</id>
    <customer>John</customer>
</order>
```

The body of the second message is:

Output message 2

```xml
<order xmlns="urn:shop">
    <id>1002</id>
    <customer>Jane</customer>
</order>
```

The `shop` namespace is mapped to `urn:shop`, allowing the XPath expression `//shop:order` to identify the namespaced `order` elements.

See the [Split EIP](../eips/split-eip.md) for more examples.