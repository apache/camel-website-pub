# Python

**Since Camel 3.19**

Camel allows [Python](https://www.jython.org/) to be used as an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) in Camel routes.

For example, you can use Python in a [Predicate](../../../manual/predicate.md) with the [Content-Based Router](../eips/choice-eip.md) EIP.

## Python Options

The Python language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |
| **resolveResource** (advanced) | `false` | `Boolean` | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. |

## Message Body

The message body at each side of the Python language: _Expression input_ is the body its expressions can read, and _Expression result_ what they return.

  
| Side | Body | Description |
| --- | --- | --- |
| **Expression input** | `any` | The body as it is, in the variable body: a String is a Python unicode string, and other Java objects keep their methods. |
| **Expression result** | `unknown` | The Java value of what the script returns: a dict as a Map, a list or a tuple as a List, a set as a Set, and None as null.
With `resultType` set: an object of the class it names, or null.

 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).

## Variables

  
| Variable | Type | Description |
| --- | --- | --- |
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
| exception | Exception | the exception if the exchange failed (or the caught exception in an error handler), otherwise `None` |
| context | CamelContext | **Deprecated** use `camelContext` |
| properties | Map | **Deprecated** use `exchangeProperties` |

The variables have the same names as in the [Groovy](groovy-language.md) language, except `in`, which is a reserved word in Python (use `message` or `request`), and the deprecated `out` and `response`. The deprecated `context` and `properties` still work.

The `variable` and `variables` bindings are the exchange-scoped variables (for example set with the [Set Variable](../eips/setVariable-eip.md) EIP). Global and route variables, such as `global:foo`, are not in this map; use `exchange.getVariable('global:foo')` for those.

The result of a script is its Java value: `None` is `null`, a string, a number or a boolean is the Java `String`, number or `Boolean`, a dict, list, tuple or set is a `Map`, `List` or `Set` of Java values, and a Java object, such as the body, is returned as it is. Set `resultType` to convert the result to another type.

## Examples

A Python predicate in a [Content-Based Router](../eips/choice-eip.md):

```yaml
- route:
    from:
      uri: direct:orders
      steps:
        - choice:
            when:
              - expression:
                  python:
                    expression: "headers.get('priority') == 'high'"
                steps:
                  - to:
                      uri: direct:fast
            otherwise:
              steps:
                - to:
                    uri: direct:normal
```

A Python expression that sets the message body from the body and a header:

```yaml
- route:
    from:
      uri: direct:greet
      steps:
        - setBody:
            expression:
              python:
                expression: "'Hello ' + str(body) + ', your priority is ' + str(headers.get('priority'))"
        - to:
            uri: log:greeting
```

## Dependencies

To use Python in your Camel routes, you need to add the dependency on **camel-python** which implements the Python language.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-python</artifactId>
  <version>x.x.x</version>
</dependency>
```