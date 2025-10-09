# Remove Headers

The Remove Headers EIP allows you to remove one or more headers from the [Message](message.md), based on pattern syntax.

## Options

The Remove Headers eip supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **pattern** | **Required** Name or pattern of headers to remove. The pattern is matched in the following order: 1 = exact match 2 = wildcard (pattern ends with a and the name starts with the pattern) 3 = regular expression (all of above is case in-sensitive). |  | String |
| **excludePattern** | Name or patter of headers to not remove. The pattern is matched in the following order: 1 = exact match 2 = wildcard (pattern ends with a and the name starts with the pattern) 3 = regular expression (all of above is case in-sensitive). |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Remove Headers by pattern

The Remove Headers EIP supports pattern matching by the following rules in the given order:

-   match by exact name
    
-   match by wildcard
    
-   match by regular expression
    

## Remove all headers

To remove all headers you can use `*` as the pattern:

```java
from("seda:b")
  .removeHeaders("*")
  .to("mock:result");
```

And in XML:

```xml
<route>
  <from uri="seda:b"/>
  <removeHeaders pattern="*"/>
  <to uri="mock:result"/>
</route>
```

## Remove all Camel headers

To remove all headers that start with `Camel` then use `Camel*` as shown:

```java
from("seda:b")
  .removeHeaders("Camel*")
  .to("mock:result");
```

And in XML:

```xml
<route>
  <from uri="seda:b"/>
  <removeHeaders pattern="Camel*"/>
  <to uri="mock:result"/>
</route>
```

## See Also

Camel provides the following EIPs for removing headers or exchange properties:

-   [Remove Header](removeHeader-eip.md) - To remove a single header
    
-   [Remove Headers](#) - To remove one or more message headers
    
-   [Remove Property](removeProperty-eip.md) - To remove a single exchange property
    
-   [Remove Properties](removeProperties-eip.md) - To remove one or more exchange properties