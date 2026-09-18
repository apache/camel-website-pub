# Event Driven Consumer

Camel supports the [Event Driven Consumer](http://www.enterpriseintegrationpatterns.com/EventDrivenConsumer.md) from the [EIP patterns](enterprise-integration-patterns.md).

The default consumer model is event-based (i.e., asynchronous) as this means that the Camel container can then manage pooling, threading and concurrency for you in a declarative manner.

> **Tip**
> The alternative consumer mode is [Polling Consumer](polling-consumer.md).

![image](_images/eip/EventDrivenConsumerSolution.gif)

The Event Driven Consumer is implemented by consumers implementing the [Processor](http://javadoc.io/doc/org.apache.camel/camel-api/latest/org/apache/camel/Processor.md) interface which is invoked by the [Message Endpoint](message-endpoint.md) when a [Message](message.md) is available for processing.

## Example

The following demonstrates a [Bean](bean-eip.md) being invoked when an event occurs from a [JMS](../jms-component.md) queue.

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms:queue:foo")
    .bean(MyBean.class);
```

```xml
<route>
    <from uri="jms:queue:foo"/>
    <bean beanType="com.foo.MyBean"/>
</route>
```

```yaml
- from:
    uri: jms:queue:foo
    steps:
      - bean:
          beanType: com.foo.MyBean
```