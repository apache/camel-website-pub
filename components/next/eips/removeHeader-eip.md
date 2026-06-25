# Remove Header

The Remove Header EIP allows you to remove a single header from the [Message](message.md).

## Options

The Remove Header eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **name** | **Required** Name of header to remove. |  | String |

## Exchange properties

The Remove Header eip has no exchange properties.

## Example

We want to remove a header with key "myHeader" from the message:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:b")
  .removeHeader("myHeader")
  .to("mock:result");
```

```xml
<route>
  <from uri="seda:b"/>
  <removeHeader name="myHeader"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:b
      steps:
        - removeHeader:
            name: myHeader
        - to:
            uri: mock:result
```

## See Also

Camel provides the following EIPs for removing headers or exchange properties:

-   [Remove Header](#): To remove a single header
    
-   [Remove Headers](removeHeaders-eip.md): To remove one or more message headers
    
-   [Remove Property](removeProperty-eip.md): To remove a single exchange property
    
-   [Remove Properties](removeProperties-eip.md): To remove one or more exchange properties