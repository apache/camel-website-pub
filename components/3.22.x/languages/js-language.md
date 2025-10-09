# JavaScript

**Since Camel 3.20**

Camel allows [JavaScript](https://www.graalvm.org/javascript/) to be used as an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) in Camel routes.

For example, you can use JavaScript in a [Predicate](../../../manual/predicate.md) with the [Content Based Router](../eips/choice-eip.md) EIP.

## JavaScript Options

The JavaScript language supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** |  | `String` | Sets the class of the result type (type from output). |
| **trim** | `true` | `Boolean` | Whether to trim the value to remove leading and trailing whitespaces and line breaks. |

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

To use JavaScript in your camel routes you need to add the dependency on **camel-javascript** which implements the JavaScript language (JavaScript with GraalVM).

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-javascript</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using js with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-javascript-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.language.js.enabled** | Whether to enable auto configuration of the js language. This is enabled by default. |  | Boolean |
| **camel.language.js.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |