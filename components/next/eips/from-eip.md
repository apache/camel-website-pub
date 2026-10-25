# From

Every Camel [route](../../../manual/routes.md) starts from an [Endpoint](../../../manual/endpoint.md) as the input (source) to the route.

The `from` EIP is the input.

> **Note**
> the Java DSL also provides a `fromF` EIP, which can be used to avoid concatenating route parameters and making the code harder to read.

## Options

The From eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **uri** | **Required** The endpoint URI to consume from. |  | String |
| **variableReceive** | To use a variable to store the received message body (only body, not headers). This makes it handy to use variables for user data and to easily control what data to use for sending and receiving. |  | String |

## Message Body

The message body at each side of the From EIP: _EIP input_ is the body it needs, _EIP output_ the body after it, and _Steps_ the body its own steps start with.

  
| Side | Body | Description |
| --- | --- | --- |
| **EIP output** | what the consumer of its endpoint receives | 
The message the consumer of the endpoint receives. With variableReceive it goes into the variable, and the route starts with no body.

-   With `variableReceive` set: `null`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).

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
- route:
    from:
      uri: file:inbox
      steps:
        - to:
            uri: log:inbox
```