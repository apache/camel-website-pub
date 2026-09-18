# Variable

**Since Camel 4.4**

The Variable Expression Language allows you to extract values of named variables.

## Variable Options

The Variable language supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

## Example usage

The `recipientList` EIP can utilize a variable:

```xml
<route>
  <from uri="direct:a" />
  <recipientList>
    <variable>myVar</variable>
  </recipientList>
</route>
```

In this case, the list of recipients are contained in the variable 'myVar'.

And the same example in Java DSL:

```java
from("direct:a").recipientList(variable("myVar"));
```

## Dependencies

The Header language is part of **camel-core**.