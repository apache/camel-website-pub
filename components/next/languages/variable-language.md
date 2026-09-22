# Variable

**Since Camel 4.4**

The Variable Expression Language allows you to extract values of named variables.

## Variable Options

The Variable language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |
| **resolveResource** (advanced) | `false` | `Boolean` | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. |

## Example usage

The `recipientList` EIP can utilize a variable:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a").recipientList(variable("myVar"));
```

```xml
<route>
  <from uri="direct:a" />
  <recipientList>
    <variable>myVar</variable>
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
              variable:
                expression: myVar
```

In this case, the list of recipients are contained in the variable 'myVar'.

## Dependencies

The Header language is part of **camel-core**.