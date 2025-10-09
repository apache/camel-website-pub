# Remove Properties

The Remove Properties EIP allows you to remove one or more `Exchange` properties, based on pattern syntax.

## Options

The Remove Properties eip supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **pattern** | **Required** Name or pattern of properties to remove. The pattern is matched in the following order: 1 = exact match 2 = wildcard (pattern ends with a and the name starts with the pattern) 3 = regular expression (all of above is case in-sensitive). |  | String |
| **excludePattern** | Name or pattern of properties to not remove. The pattern is matched in the following order: 1 = exact match 2 = wildcard (pattern ends with a and the name starts with the pattern) 3 = regular expression (all of above is case in-sensitive). |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Remove Properties by pattern

The Remove Properties EIP supports pattern matching by the following rules in the given order:

-   match by exact name
    
-   match by wildcard
    
-   match by regular expression
    

## Remove all properties

```java
from("seda:b")
  .removeProperties("*")
  .to("mock:result");
```

And in XML:

```xml
<route>
  <from uri="seda:b"/>
  <removeProperties pattern="*"/>
  <to uri="mock:result"/>
</route>
```

> **Note**
> Be careful to remove all exchange properties as Camel uses internally exchange properties to keep state on the `Exchange` during routing. So use this with care. You should generally only remove custom exchange properties that are under your own control.

## Remove properties by pattern

To remove all exchange properties that start with `Foo` then use `Foo*` as shown:

```java
from("seda:b")
  .removeProperties("Foo*")
  .to("mock:result");
```

And in XML:

```xml
<route>
  <from uri="seda:b"/>
  <removeProperties pattern="Foo*"/>
  <to uri="mock:result"/>
</route>
```

## See Also

Camel provides the following EIPs for removing headers or exchange properties:

-   [Remove Header](removeHeader-eip.md) - To remove a single header
    
-   [Remove Headers](removeHeaders-eip.md) - To remove one or more message headers
    
-   [Remove Property](removeProperty-eip.md) - To remove a single exchange property
    
-   [Remove Properties](#) - To remove one or more exchange properties