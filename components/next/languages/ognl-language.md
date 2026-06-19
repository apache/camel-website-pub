# OGNL

> **Warning**
> **Deprecated:** This ognl is deprecated and may be removed in a future release.

**Since Camel 1.1**

Camel allows [OGNL](https://en.wikipedia.org/wiki/OGNL), supported by [(Apache Commons OGNL)](http://commons.apache.org/proper/commons-ognl/), to be used as an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) in Camel routes.

For example, you can use MVEL in a [Predicate](../../../manual/predicate.md) with the [Content-Based Router](../eips/choice-eip.md) EIP.

You can use OGNL dot notation to invoke operations. If you for instance have a body that contains a POJO that has a `getFamilyName` method then you can construct the syntax as follows:

```text
request.body.familyName
```

Or use similar syntax as in Java:

_Java-only: OGNL expression using Java method call syntax_

```java
getRequest().getBody().getFamilyName()
```

## OGNL Options

The OGNL language supports 2 options, which are listed below.

   
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
| exception | Throwable | the Exchange exception (if any) |
| request | Message | the message |
| message | Message | the message |
| headers | Map | the message headers |
| header(name) | Object | the message header by the given name |
| header(name, type) | Type | the message header by the given name as the given type |
| properties | Map | the exchange properties |
| property(name) | Object | the exchange property by the given name |
| property(name, type) | Type | the exchange property by the given name as the given type |

## Example

For example, you could use OGNL inside a [Message Filter](../eips/filter-eip.md)

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo")
  .filter().ognl("request.headers.foo == 'bar'")
    .to("seda:bar");
```

```xml
<route>
  <from uri="seda:foo"/>
  <filter>
    <ognl>request.headers.foo == 'bar'</ognl>
    <to uri="seda:bar"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: seda:foo
      steps:
        - filter:
            expression:
              ognl:
                expression: request.headers.foo == 'bar'
            steps:
              - to:
                  uri: seda:bar
```

## Loading script from external resource

You can externalize the script and have Apache Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g., to refer to a file on the classpath you can do:

_Java-only: loading an OGNL script from the classpath_

```java
.setHeader("myHeader").ognl("resource:classpath:myognl.txt")
```

## Dependencies

To use OGNL in your camel routes, you need to add the dependency on **camel-ognl**, which implements the OGNL language.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-ognl</artifactId>
  <version>x.x.x</version>
</dependency>
```