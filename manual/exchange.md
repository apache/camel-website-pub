# Message Exchange

A request message and its corresponding reply or exception message is represented in Camel using the `Exchange` interface. This interface provides an abstraction for this pattern of communication between systems. The presence of a reply message is optional and depends on the [exchange pattern](exchange-pattern.md) used in the integration. Thanks to this, Apache Camel can support different integration patterns such as:

-   [Event Messages](../components/4.18.x/eips/event-message.md): messages that have only an inbound message
    
-   [Request and Reply](../components/4.18.x/eips/requestReply-eip.md): messages that have an inbound and an outbound message.
    

## Learn More About Exchanges

-   [Exchange Pooling](exchange-pooling.md)
    
-   [Message Exchange Pattern](exchange-pattern.md)
    
-   [Using Message Exchange Pattern Annotations](using-exchange-pattern-annotations.md)