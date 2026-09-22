# Constant

**Since Camel 1.5**

The Constant Expression Language is really just a way to use a constant value or object.

> **Note**
> This is a fixed constant value (or object) that is only set once during starting up the route, do not use this if you want dynamic values during routing.

## Constant Options

The Constant language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |
| **resolveResource** (advanced) | `false` | `Boolean` | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. |

## Example

The `setHeader` EIP can utilize a constant expression like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .setHeader("theHeader", constant("the value"))
  .to("mock:b");
```

```xml
<route>
  <from uri="seda:a"/>
  <setHeader name="theHeader">
    <constant>the value</constant>
  </setHeader>
  <to uri="mock:b"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - setHeader:
            name: theHeader
            expression:
              constant:
                expression: the value
        - to:
            uri: mock:b
```

In this case, the message coming from the seda:a endpoint will have the header with key `theHeader` set its value as `the value` (string type).

### Specifying type of value

The option `resultType` can be used to specify the type of the value, when the value is given as a `String` value, which happens when using XML or YAML DSL:

For example to set a header with `int` type you can do:

-   XML
    
-   YAML
    

```xml
<route>
  <from uri="seda:a"/>
  <setHeader name="zipCode">
    <constant resultType="int">90210</constant>
  </setHeader>
  <to uri="mock:b"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - setHeader:
            name: zipCode
            expression:
              constant:
                resultType: int
                expression: "90210"
        - to:
            uri: mock:b
```

## Loading constant from external resource

You can externalize the constant and have Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`.  
This is done using the following syntax: `"resource:scheme:location"`, eg to refer to a file on the classpath you can do:

```java
.setHeader("myHeader").constant("resource:classpath:constant.txt")
```

## Dependencies

The Constant language is part of **camel-core**.