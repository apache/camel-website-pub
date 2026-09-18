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