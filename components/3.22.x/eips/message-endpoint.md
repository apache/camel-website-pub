# Message Endpoint

Camel supports the [Message Endpoint](http://www.enterpriseintegrationpatterns.com/MessageEndpoint.md) from the [EIP patterns](enterprise-integration-patterns.md) using the [Endpoint](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.md) interface.

How does an application connect to a messaging channel to send and receive messages?

![image](_images/eip/MessageEndpointSolution.gif)

Connect an application to a messaging channel using a Message Endpoint, a client of the messaging system that the application can then use to send or receive messages.

When using the [DSL](../../../manual/dsl.md) to create [Routes](../../../manual/routes.md) you typically refer to Message Endpoints by their [URIs](../../../manual/uris.md) rather than directly using the [Endpoint](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.md) interface. It’s then a responsibility of the [CamelContext](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/CamelContext.md) to create and activate the necessary `Endpoint` instances using the available [Components](../index.md).

## Example

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