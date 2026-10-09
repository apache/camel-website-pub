# JavaScript

**Since Camel 3.20**

Camel allows [JavaScript](https://www.graalvm.org/javascript/) to be used as an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) in Camel routes.

For example, you can use JavaScript in a [Predicate](../../../manual/predicate.md) with the [Content-Based Router](../eips/choice-eip.md) EIP.

## JavaScript Options

The JavaScript language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |
| **resolveResource** (advanced) | `false` | `Boolean` | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. |

## Variables

  
| Variable | Type | Description |
| --- | --- | --- |
| **this** | Exchange | the Exchange is the root object |
| exchange | Exchange | the Exchange |
| camelContext | CamelContext | the CamelContext |
| exchangeId | String | the exchange id |
| message | Message | the message |
| request | Message | the message (same as `message`) |
| body | Object | the message body |
| header | Map | the message headers (same as `headers`) |
| headers | Map | the message headers |
| exchangeProperty | Map | the exchange properties (same as `exchangeProperties`) |
| exchangeProperties | Map | the exchange properties |
| variable | Map | the exchange variables (same as `variables`) |
| variables | Map | the exchange variables |
| exception | Exception | the exception if the exchange failed (or the caught exception in an error handler), otherwise `null` |
| context | CamelContext | **Deprecated** use `camelContext` |
| properties | Map | **Deprecated** use `exchangeProperties` |

The variables have the same names as in the [Groovy](groovy-language.md) language, except `in`, which is a reserved word in JavaScript (use `message` or `request`), and the deprecated `out` and `response`. The deprecated `context` and `properties` still work.

The `variable` and `variables` bindings are the exchange-scoped variables (for example set with the [Set Variable](../eips/setVariable-eip.md) EIP). Global and route variables, such as `global:foo`, are not in this map; use `exchange.getVariable('global:foo')` for those.

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