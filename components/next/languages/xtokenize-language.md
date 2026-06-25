# XML Tokenize

**Since Camel 2.14**

The XML Tokenize language is a built-in language in `camel-stax`, which is a truly XML-aware tokenizer that can be used with the [Split](../eips/split-eip.md) EIP as the conventional [Tokenize](tokenize-language.md) to efficiently and effectively tokenize XML documents.

XML Tokenize is capable of not only recognizing XML namespaces and hierarchical structures of the document but also more efficiently tokenizing XML documents than the conventional [Tokenize](tokenize-language.md) language.

## XML Tokenizer Options

The XML Tokenize language supports 5 options, which are listed below.

   
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

See [Split EIP](../eips/split-eip.md), which has examples using the XML Tokenize language.