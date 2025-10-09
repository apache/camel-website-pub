# From

Every Camel [route](../../../manual/routes.md) starts from an [Endpoint](../../../manual/endpoint.md) as the input (source) to the route.

The From EIP is the input.

## Options

The From eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **uri** | **Required** Sets the URI of the endpoint to use. |  | String |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Example

In the route below the route starts from a [File](../file-component.md) endpoint.

```java
from("file:inbox")
  .to("log:inbox");
```

And the same example in XML DSL:

```xml
<route>
  <from uri="file:inbox"/>
  <to uri="log:inbox"/>
</route>
```