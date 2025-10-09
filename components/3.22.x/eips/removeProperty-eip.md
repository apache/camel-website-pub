# Remove Property

The Remove Property EIP allows you to remove a single property from the `Exchange`.

## Options

The Remove Property eip supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** | **Required** Name of property to remove. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Example

We want to remove an exchange property with key "myProperty" from the exchange:

```java
from("seda:b")
  .removeProperty("myProperty")
  .to("mock:result");
```

And in XML:

```xml
<route>
  <from uri="seda:b"/>
  <removeProperty name="myProperty"/>
  <to uri="mock:result"/>
</route>
```

## See Also

Camel provides the following EIPs for removing headers or exchange properties:

-   [Remove Header](removeHeader-eip.md) - To remove a single header
    
-   [Remove Headers](removeHeaders-eip.md) - To remove one or more message headers
    
-   [Remove Property](#) - To remove a single exchange property
    
-   [Remove Properties](removeProperties-eip.md) - To remove one or more exchange properties