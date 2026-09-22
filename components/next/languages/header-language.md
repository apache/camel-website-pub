# Header

**Since Camel 1.5**

The Header Expression Language allows you to extract values of named headers.

## Header Options

The Header language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |
| **resolveResource** (advanced) | `false` | `Boolean` | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. |

## Example usage

The `recipientList` EIP can utilize a header:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a").recipientList(header("myHeader"));
```

```xml
<route>
  <from uri="direct:a" />
  <recipientList>
    <header>myHeader</header>
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
              header:
                expression: myHeader
```

In this case, the list of recipients are contained in the header 'myHeader'.

## Dependencies

The Header language is part of **camel-core**.