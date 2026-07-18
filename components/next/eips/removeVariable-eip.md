# Remove Variable

The Remove Variable EIP allows you to remove a single variable.

## Options

The Remove Variable eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **name** | Name of the variable to remove. |  | String |

## Exchange properties

The Remove Variable eip has no exchange properties.

## Example

We want to remove a variable with key "myVar" from the exchange:

-   Java
    
-   XML
    
-   YAML
    

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

```yaml
- route:
    from:
      uri: seda:b
      steps:
        - removeVariable:
            name: myVar
        - to:
            uri: mock:result
```

> **Tip**
> If you want to remove all variables from the `Exchange` then use `*` as the name.