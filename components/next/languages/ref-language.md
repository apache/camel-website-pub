# Ref

**Since Camel 2.8**

The Ref Expression Language is really just a way to lookup a custom `Expression` or `Predicate` from the [Registry](../../../manual/registry.md).

This is particular useable in XML DSLs.

## Ref Language options

The Ref language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |
| **resolveResource** (advanced) | `false` | `Boolean` | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. |

## Message Body

The message body at each side of the Ref language: _Expression input_ is the body its expressions can read, and _Expression result_ what they return.

  
| Side | Body | Description |
| --- | --- | --- |
| **Expression input** | `any` | As the expression or the predicate in the registry reads it. |
| **Expression result** | `unknown` | What the expression in the registry returns; a Boolean for a predicate.
With `resultType` set: an object of the class it names, or null.

 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Example usage

The Splitter EIP can utilize a custom expression using `ref` like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a").split().ref("myExpression").to("seda:b");
```

```xml
<bean id="myExpression" class="com.mycompany.MyCustomExpression"/>

<route>
  <from uri="seda:a"/>
  <split>
    <ref>myExpression</ref>
    <to uri="mock:b"/>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - split:
            expression:
              ref:
                expression: myExpression
            steps:
              - to:
                  uri: mock:b
```

In this case, the message coming from the seda:a endpoint will be split using a custom `Expression` which has the id `myExpression` in the [Registry](../../../manual/registry.md).

## Dependencies

The Ref language is part of **camel-core**.