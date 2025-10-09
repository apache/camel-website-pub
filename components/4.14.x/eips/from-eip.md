# From

Every Camel [route](../../../manual/routes.md) starts from an [Endpoint](../../../manual/endpoint.md) as the input (source) to the route.

The `from` EIP is the input.

> **Note**
> the Java DSL also provides a `fromF` EIP, which can be used to avoid concatenating route parameters and making the code harder to read.

## Options

The From eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** | Sets the description of this node. |  | String |
| **uri** | **Required** Sets the URI of the endpoint to use. |  | String |
| **variableReceive** | To use a variable to store a copy of the received message body (only body, not headers). This is handy for easy access to the received message body via variables. |  | String |

## Exchange properties

The From eip has no exchange properties.

## Example

In the route below, the route starts from a [File](../file-component.md) endpoint.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
  .to("log:inbox");
```

```xml
<route>
  <from uri="file:inbox"/>
  <to uri="log:inbox"/>
</route>
```

```yaml
- from:
    uri: file:inbox
    steps:
      - to:
          uri: log:inbox
```