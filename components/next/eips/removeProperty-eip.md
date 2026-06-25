# Remove Property

The Remove Property EIP allows you to remove a single property from the `Exchange`.

## Options

The Remove Property eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **name** | Name of the exchange property to remove. |  | String |

## Exchange properties

The Remove Property eip has no exchange properties.

## Example

We want to remove an exchange property with key "myProperty" from the exchange:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:b")
  .removeProperty("myProperty")
  .to("mock:result");
```

```xml
<route>
  <from uri="seda:b"/>
  <removeProperty name="myProperty"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:b
      steps:
        - removeProperty:
            name: myProperty
        - to:
            uri: mock:result
```

## See Also

Camel provides the following EIPs for removing headers or exchange properties:

-   [Remove Header](removeHeader-eip.md): To remove a single header
    
-   [Remove Headers](removeHeaders-eip.md): To remove one or more message headers
    
-   [Remove Property](#): To remove a single exchange property
    
-   [Remove Properties](removeProperties-eip.md): To remove one or more exchange properties