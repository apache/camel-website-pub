# Header

**Since Camel 1.5**

The Header Expression Language allows you to extract values of named headers.

## Header Options

The Header language supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

## Example usage

The `recipientList` EIP can utilize a header:

```xml
<route>
  <from uri="direct:a" />
  <recipientList>
    <header>myHeader</header>
  </recipientList>
</route>
```

In this case, the list of recipients are contained in the header 'myHeader'.

And the same example in Java DSL:

```java
from("direct:a").recipientList(header("myHeader"));
```

## Dependencies

The Header language is part of **camel-core**.