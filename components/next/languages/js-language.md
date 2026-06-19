# JavaScript

**Since Camel 3.20**

Camel allows [JavaScript](https://www.graalvm.org/javascript/) to be used as an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) in Camel routes.

For example, you can use JavaScript in a [Predicate](../../../manual/predicate.md) with the [Content-Based Router](../eips/choice-eip.md) EIP.

## JavaScript Options

The JavaScript language supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

## Variables

  
| Variable | Type | Description |
| --- | --- | --- |
| **this** | Exchange | the Exchange is the root object |
| context | CamelContext | the CamelContext |
| exchange | Exchange | the Exchange |
| exchangeId | String | the exchange id |
| message | Message | the message |
| body | Message | the message body |
| headers | Map | the message headers |
| properties | Map | the exchange properties |

## Dependencies

To use JavaScript in your Camel routes, you need to add the dependency on **camel-javascript**, which implements the JavaScript language (JavaScript with GraalVM).

If you use Maven, you could add the following to your pom.xml, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-javascript</artifactId>
  <version>x.x.x</version>
</dependency>
```