# To

Camel supports the [Message Endpoint](http://www.enterpriseintegrationpatterns.com/MessageEndpoint.md) from the [EIP patterns](enterprise-integration-patterns.md) using the [Endpoint](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.md) interface.

How does an application connect to a messaging channel to send and receive messages?

![image](_images/eip/MessageEndpointSolution.gif)

Connect an application to a messaging channel using a Message Endpoint, a client of the messaging system that the application can then use to send or receive messages.

In Camel the To EIP is used for sending [messages](message.md) to static [endpoints](message-endpoint.md).

The To and [ToD](toD-eip.md) EIPs are the most common patterns to use in Camel [routes](../../../manual/routes.md).

## Options

The To eip supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **uri** | **Required** Sets the uri of the endpoint to send to. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **pattern** | 
Sets the optional ExchangePattern used to invoke this endpoint.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

### Different between To and ToD

The `to` is used for sending messages to a static [endpoint](message-endpoint.md). In other words `to` sends message only to the **same** endpoint.

The `toD` is used for sending message to a dynamic [endpoint](message-endpoint.md). The dynamic endpoint is evaluated _on-demand_ by an [Expression](../../../manual/expression.md). By default, the [Simple](../../4.18.x/languages/simple-language.md) expression is used to compute the dynamic endpoint URI.

## Using To

The following example route demonstrates the use of a [File](../file-component.md) consumer endpoint and a [JMS](../jms-component.md) producer endpoint, by their [URIs](../../../manual/uris.md):

```java
from("file:messages/foo")
    .to("jms:queue:foo");
```

And in XML:

```xml
<route>
    <from uri="file:messages/foo"/>
    <to uri="jms:queue:foo"/>
</route>
```