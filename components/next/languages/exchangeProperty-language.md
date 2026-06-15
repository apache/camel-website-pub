# ExchangeProperty

**Since Camel 2.0**

The ExchangeProperty Expression Language allows you to extract values of named exchange properties.

## Exchange Property Options

The ExchangeProperty language supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

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