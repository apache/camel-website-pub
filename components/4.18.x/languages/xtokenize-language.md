# XML Tokenize

**Since Camel 2.14**

The XML Tokenize language is a built-in language in `camel-stax`, which is a truly XML-aware tokenizer that can be used with the [Split](../eips/split-eip.md) EIP as the conventional [Tokenize](tokenize-language.md) to efficiently and effectively tokenize XML documents.

XML Tokenize is capable of not only recognizing XML namespaces and hierarchical structures of the document but also more efficiently tokenizing XML documents than the conventional [Tokenize](tokenize-language.md) language.

## XML Tokenizer Options

The XML Tokenize language supports 5 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **mode** (common) | `i` | `Enum` | 
The extraction mode. The available extraction modes are: i - injecting the contextual namespace bindings into the extracted token (default) w - wrapping the extracted token in its ancestor context u - unwrapping the extracted token to its child content t - extracting the text content of the specified element.

Enum values:

-   i
    
-   w
    
-   u
    
-   t
    





 |
| **group** (common) |  | `Integer` | To group N parts together. |
| **source** (common) |  | `String` | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

## Example

See [Split EIP](../eips/split-eip.md), which has examples using the XML Tokenize language.

## Spring Boot Auto-Configuration

When using xtokenize with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-stax-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.stax.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.stax.enabled** | Whether to enable auto configuration of the stax component. This is enabled by default. |  | Boolean |
| **camel.component.stax.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.language.xtokenize.enabled** | Whether to enable auto configuration of the xtokenize language. This is enabled by default. |  | Boolean |
| **camel.language.xtokenize.mode** | The extraction mode. The available extraction modes are: i - injecting the contextual namespace bindings into the extracted token (default) w - wrapping the extracted token in its ancestor context u - unwrapping the extracted token to its child content t - extracting the text content of the specified element. | i | String |
| **camel.language.xtokenize.namespace** | Injects the XML Namespaces of prefix - uri mappings. |  | List |
| **camel.language.xtokenize.source** | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| **camel.language.xtokenize.trim** | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. | true | Boolean |