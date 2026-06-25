# Tokenize

**Since Camel 2.0**

The tokenizer language is a built-in language in `camel-core`, which is most often used with the [Split](../eips/split-eip.md) EIP to split a message using a token-based strategy.

The tokenizer language is intended to tokenize text documents using a specified delimiter pattern. It can also be used to tokenize XML documents with some limited capability. For a truly XML-aware tokenization, the use of the [XML Tokenize](xtokenize-language.md) language is recommended as it offers a faster, more efficient tokenization specifically for XML documents.

## Tokenize Options

The Tokenize language supports 12 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **token** (common) |  | `String` | The (start) token to use as tokenizer, for example you can use the new line token. You can use simple language as the token to support dynamic tokens. |
| **endToken** (common) |  | `String` | The end token to use as tokenizer if using start/end token pairs. You can use simple language as the token to support dynamic tokens. |
| **inheritNamespaceTagName** (advanced) |  | `String` | To inherit namespaces from a root/parent tag name when using XML. You can use simple language as the tag name to support dynamic names. |
| **regex** (advanced) | `false` | `Boolean` | If the token is a regular expression pattern. |
| **xml** (common) | `false` | `Boolean` | Whether the input is XML messages. This option must be set to true if working with XML payloads. |
| **includeTokens** (common) | `false` | `Boolean` | Whether to include the tokens in the parts when using pairs. When including tokens then the endToken property must also be configured (to use pair mode). |
| **group** (advanced) |  | `String` | To group N parts together, for example to split big files into chunks of 1000 lines. You can use simple language as the group to support dynamic group sizes. |
| **groupDelimiter** (advanced) |  | `String` | Sets the delimiter to use when grouping. If this has not been set then token will be used as the delimiter. |
| **skipFirst** (advanced) | `false` | `Boolean` | To skip the very first element. |
| **source** (common) |  | `String` | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Example

The following example shows how to take a request from the direct:a endpoint then split it into pieces using an [Expression](../../../manual/expression.md), then forward each piece to direct:b:

> **Important**
> When using new-line (`\n`) as tokenizer, then XML and YAML DSL must use the `token` option\\ as done in the following example.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .split(body().tokenize("\n"))
        .to("direct:b");
```

```xml
<route>
  <from uri="direct:a"/>
  <split>
    <tokenize token="\n"/>
    <to uri="direct:b"/>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: direct:a
      steps:
        - split:
            expression:
              tokenize:
                token: "\n"
            steps:
              - to:
                  uri: direct:b
```

## See Also

For more examples see [Split](../eips/split-eip.md) EIP.

## Dependencies

The Tokenize language is part of **camel-core**.