# ExchangeProperty

**Since Camel 2.0**

The ExchangeProperty Expression Language allows you to extract values of named exchange properties.

## Exchange Property Options

The ExchangeProperty language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |
| **resolveResource** (advanced) | `false` | `Boolean` | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. |

## Message Body

The message body at each side of the ExchangeProperty language: _Expression input_ is the body its expressions can read, and _Expression result_ what they return.

  
| Side | Body | Description |
| --- | --- | --- |
| **Expression result** | `unknown` | The value of the exchange property as it is, null when there is none. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).

## Example

The `recipientList` EIP can utilize a exchangeProperty like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a").recipientList(exchangeProperty("myProperty"));
```

```xml
<route>
  <from uri="direct:a" />
  <recipientList>
    <exchangeProperty>myProperty</exchangeProperty>
  </recipientList>
</route>
```

```yaml
- route:
    from:
      uri: direct:a
      steps:
        - recipientList:
            expression:
              exchangeProperty:
                expression: myProperty
```

In this case, the list of recipients are contained in the property 'myProperty'.

## Dependencies

The ExchangeProperty language is part of **camel-core**.