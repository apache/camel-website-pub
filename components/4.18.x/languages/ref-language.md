# Ref

**Since Camel 2.8**

The Ref Expression Language is really just a way to lookup a custom `Expression` or `Predicate` from the [Registry](../../../manual/registry.md).

This is particular useable in XML DSLs.

## Ref Language options

The Ref language supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

## Example usage

The Splitter EIP in XML DSL can utilize a custom expression using `<ref>` like:

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

in this case, the message coming from the seda:a endpoint will be split using a custom `Expression` which has the id `myExpression` in the [Registry](../../../manual/registry.md).

And the same example using Java DSL:

```java
from("seda:a").split().ref("myExpression").to("seda:b");
```

## Dependencies

The Ref language is part of **camel-core**.