# To

Camel supports the [Message Endpoint](http://www.enterpriseintegrationpatterns.com/MessageEndpoint.md) from the [EIP patterns](enterprise-integration-patterns.md) using the [Endpoint](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.md) interface.

How does an application connect to a messaging channel to send and receive messages?

![image](_images/eip/MessageEndpointSolution.gif)

Connect an application to a messaging channel using a Message Endpoint, a client of the messaging system that the application can then use to send or receive messages.

In Camel the To EIP is used for sending [messages](message.md) to static [endpoints](message-endpoint.md).

The To and [ToD](toD-eip.md) EIPs are the most common patterns to use in Camel [routes](../../../manual/routes.md).

## Options

The To eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **variableSend** | To use a variable as the source for the message body to send. This makes it handy to use variables for user data and to easily control what data to use for sending and receiving. Important: When using send variable then the message body is taken from this variable instead of the current message, however the headers from the message will still be used as well. In other words, the variable is used instead of the message body, but everything else is as usual. |  | String |
| **variableReceive** | To use a variable to store the received message body (only body, not headers). This makes it handy to use variables for user data and to easily control what data to use for sending and receiving. Important: When using receive variable then the received body is stored only in this variable and not on the current message. |  | String |
| **uri** | **Required** Sets the uri of the endpoint to send to. |  | String |
| **pattern** | 
Sets the optional ExchangePattern used to invoke this endpoint.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Exchange properties

The To eip supports 1 exchange properties, which are listed below.

The exchange properties are set on the `Exchange` by the EIP, unless otherwise specified in the description. This means those properties are available after this EIP has completed processing the `Exchange`.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelToEndpoint** | Endpoint URI where this Exchange is being sent to. |  | String |

## Different between To and ToD

The `to` is used for sending messages to a static [endpoint](message-endpoint.md). In other words `to` sends messages only to the **same** endpoint.

The `toD` is used for sending messages to a dynamic [endpoint](message-endpoint.md). The dynamic endpoint is evaluated _on-demand_ by an [Expression](../../../manual/expression.md). By default, the [Simple](../../4.18.x/languages/simple-language.md) expression is used to compute the dynamic endpoint URI.

> **Note**
> the Java DSL also provides a `toF` EIP, which can be used to avoid concatenating route parameters and making the code harder to read.

## Using To

The following example route demonstrates the use of a [File](../file-component.md) consumer endpoint and a [JMS](../jms-component.md) producer endpoint, by their [URIs](../../../manual/uris.md):

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:messages/foo")
    .to("jms:queue:foo");
```

```xml
<route>
    <from uri="file:messages/foo"/>
    <to uri="jms:queue:foo"/>
</route>
```

```yaml
- from:
    uri: file:messages/foo
    steps:
      - to:
          uri: jms:queue:foo
```