# Remove Variable

The Remove Variable EIP allows you to remove a single variable.

## Options

The Remove Variable eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **name** | **Required** Name of variable to remove. |  | String |

## Exchange properties

The Remove Variable eip has no exchange properties.

## Example

We want to remove a variable with key "myVar" from the exchange:

-   Java
    
-   XML
    

```java
from("seda:b")
  .removeVariable("myVar")
  .to("mock:result");
```

```xml
<route>
  <from uri="seda:b"/>
  <removeVariable name="myVar"/>
  <to uri="mock:result"/>
</route>
```

> **Tip**
> If you want to remove all variables from the `Exchange` then use `*` as the name.