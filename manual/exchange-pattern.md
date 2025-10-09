# Exchange Pattern

There are two _Message Exchange Patterns_ you can use in messaging.

From there [Enterprise Integration Patterns](../components/4.18.x/eips/enterprise-integration-patterns.md) they are:

-   [Event Message](../components/4.18.x/eips/event-message.md) (or one-way)
    
-   [Request Reply](../components/4.18.x/eips/requestReply-eip.md)
    

In Camel, we have an `org.apache.camel.ExchangePattern` enumeration which can be configured on the **exchangePattern** property on the Message Exchange indicating if a message exchange is a one way [Event Message](../components/4.18.x/eips/event-message.md) (**InOnly**) or a [Request Reply](../components/4.18.x/eips/requestReply-eip.md) message exchange (**InOut**).

For example to override the default pattern on a [JMS](../components/4.18.x/jms-component.md) endpoint you could use the `exchangePattern` parameter in the Endpoint [URI](uris.md) as shown:

```text
jms:myQueue?exchangePattern=InOut
```