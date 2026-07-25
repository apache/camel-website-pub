# Exchange Pattern

There are two _Message Exchange Patterns_ (MEP) you can use in messaging.

From the [Enterprise Integration Patterns](../components/4.18.x/eips/enterprise-integration-patterns.md) they are:

-   [Event Message](../components/4.18.x/eips/event-message.md) (or one-way)
    
-   [Request Reply](../components/4.18.x/eips/requestReply-eip.md)
    

In Camel, we have an `org.apache.camel.ExchangePattern` enumeration which can be configured on the **exchangePattern** property on the Message Exchange indicating if a message exchange is a one way [Event Message](../components/4.18.x/eips/event-message.md) (**InOnly**) or a [Request Reply](../components/4.18.x/eips/requestReply-eip.md) message exchange (**InOut**).

## How Exchange Pattern Works

The exchange pattern is a contract between the route and the **component endpoint**. It tells the component whether the caller expects a reply (`InOut`) or not (`InOnly`).

The exchange pattern does **not** affect how EIPs and processors work within the route. Processors such as `setBody`, `transform`, `process`, and `bean` always operate on the current message body regardless of the exchange pattern. The pattern only matters when the exchange reaches a **producer endpoint** (i.e., a `to` step) that acts on it.

Most components have a fixed exchange pattern — for example, [HTTP](../components/4.18.x/http-component.md) is always `InOut` (request/reply) and [Kafka](../components/4.18.x/kafka-component.md) is always `InOnly` (fire-and-forget). For these components the exchange pattern setting has no effect.

The exchange pattern is historically used by a limited set of components that support **both** `InOnly` and `InOut`, such as [JMS](../components/4.18.x/jms-component.md), [SEDA](../components/4.18.x/seda-component.md), and [AMQP](../components/4.18.x/amqp-component.md). These components use the pattern to decide between fire-and-forget and request/reply messaging. For example, with JMS `InOnly` sends a message to a queue without waiting for a reply, while `InOut` sets up a temporary reply queue (via `JMSReplyTo`) and waits for a response.

For example to override the default pattern on a [JMS](../components/4.18.x/jms-component.md) endpoint you could use the `exchangePattern` parameter in the Endpoint [URI](uris.md) as shown:

```text
jms:myQueue?exchangePattern=InOut
```