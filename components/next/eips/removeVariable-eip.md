# Remove Variable

The Remove Variable EIP allows you to remove a single variable.

## Options

The Remove Variable eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **name** | **Required** Name of the variable to remove. |  | String |

## Message Body

The message body at each side of the Remove Variable EIP: _EIP input_ is the body it needs, _EIP output_ the body after it, and _Steps_ the body its own steps start with.

  
| Side | Body | Description |
| --- | --- | --- |
| **EIP output** | `unchanged` | Removes a variable: the body stays as it was. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

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