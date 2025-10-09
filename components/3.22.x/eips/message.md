# Message

Camel supports the [Message](http://www.enterpriseintegrationpatterns.com/Message.md) from the [EIP patterns](enterprise-integration-patterns.md) using the [Message](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Message.md) interface.

![image](_images/eip/MessageSolution.gif)

The `org.apache.camel.Message` is the _data record_ that represents the message part of the [Exchange](../../../manual/exchange.md).

The message contains the following information:

-   _body_ - the message body (i.e. payload)
    
-   _headers_ - headers with additional information
    
-   _messageId_ - Unique id of the message. By default, the message uses the same id as `Exchange.getExchangeId` as messages are associated with the `Exchange` and using different IDs does not offer much value. Another reason is to optimize for performance to avoid generating new IDs. A few Camel components do provide their own message IDs such as the JMS components.
    
-   _timestamp_ - The timestamp the message originates from. Some systems like JMS, Kafka, AWS have a timestamp on the event/message, that Camel received. This method returns the timestamp, if a timestamp exists.