# XML Tokenize

**Since Camel 2.14**

The XML Tokenize language is a built-in language in `camel-stax`, which is a truly XML-aware tokenizer that can be used with the [Split](../eips/split-eip.md) EIP as the conventional [Tokenize](tokenize-language.md) to efficiently and effectively tokenize XML documents.

XML Tokenize is capable of not only recognizing XML namespaces and hierarchical structures of the document but also more efficiently tokenizing XML documents than the conventional [Tokenize](tokenize-language.md) language.

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
| **namespacesRef** (advanced) |  | `String` | Reference to a org.apache.camel.support.builder.Namespaces bean in the registry to use for the XML Namespaces of prefix to uri mappings. |
| **source** (common) |  | `String` | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Namespaces

The XML Tokenize language is namespace aware, so a tokenized element can be selected by its prefix. The prefix to URI mappings can be declared inline, or shared across several expressions by registering a `org.apache.camel.support.builder.Namespaces` bean and referring to it with the `namespacesRef` option:

-   XML
    
-   YAML
    

```xml
<camel xmlns="http://camel.apache.org/schema/xml-io">

  <bean name="myNamespaces" type="org.apache.camel.support.builder.Namespaces">
    <properties>
      <property key="namespaces[c]" value="http://acme.com/cheese"/>
    </properties>
  </bean>

  <route>
    <from uri="file:inbox"/>
    <split>
      <xtokenize namespacesRef="myNamespaces">//c:order</xtokenize>
      <to uri="mock:result"/>
    </split>
  </route>

</camel>
```

```yaml
- beans:
    - name: myNamespaces
      type: org.apache.camel.support.builder.Namespaces
      properties:
        namespaces[c]: "http://acme.com/cheese"
- route:
    from:
      uri: "file:inbox"
      steps:
        - split:
            expression:
              xtokenize:
                expression: "//c:order"
                namespacesRef: "myNamespaces"
            steps:
              - to: "mock:result"
```

Each prefix is configured as a `namespaces[prefix]` property on the bean, with the namespace URI as the value.

If the expression declares namespaces inline as well, then the inline namespaces win and `namespacesRef` is ignored.

## Example

See [Split EIP](../eips/split-eip.md), which has examples using the XML Tokenize language.