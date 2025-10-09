# Content Filter

Camel supports the [Content Filter](http://www.enterpriseintegrationpatterns.com/ContentFilter.md) from the [EIP patterns](enterprise-integration-patterns.md) using one of the following mechanisms in the routing logic to transform content from the inbound message.

![image](_images/eip/ContentFilter.gif)

-   Using a [Message Translator](message-translator.md)
    
-   Invoking a [Bean](bean-eip.md) with the filtering programmed in Java
    
-   Using a [Processor](../../../manual/processor.md) with the filtering programmed in Java
    
-   Using an [Expression](../../../manual/expression.md)
    

## Message Content filtering using a Processor

In this example, we add our own [Processor](../../../manual/processor.md) using explicit Java to filter the message:

```java
from("direct:start")
    .process(new Processor() {
        public void process(Exchange exchange) {
            String body = exchange.getMessage().getBody(String.class);
            // do something with the body
            // and replace it back
            exchange.getMessage().setBody(body);
        }
    })
    .to("mock:result");
```

## Message Content filtering using a Bean EIP

We can use [Bean EIP](bean-eip.md) to use any Java method on any bean to act as a content filter:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .bean("myBeanName", "doFilter")
    .to("activemq:Another.Queue");
```

```xml
<route>
    <from uri="activemq:Input"/>
    <bean ref="myBeanName" method="doFilter"/>
    <to uri="activemq:Output"/>
</route>
```

```yaml
- from:
    uri: activemq:Input
    steps:
      - bean:
          ref: myBeanName
          method: doFilter
      - to:
          uri: activemq:Output
```

## Message Content filtering using expression

Some languages like [XPath](../languages/xpath-language.md), and [XQuery](../languages/xquery-language.md) can be used to transform and filter content from messages.

In the example we use xpath to filter a XML message to select all the `<foo><bar>` elements:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:Input")
  .setBody().xpath("//foo:bar")
  .to("activemq:Output");
```

```xml
<route>
  <from uri="activemq:Input"/>
  <setBody>
    <xpath>//foo:bar</xpath>
  </setBody>
  <to uri="activemq:Output"/>
</route>
```

```yaml
- from:
    uri: activemq:Input
    steps:
      - setBody:
          expression:
            xpath: //foo:bar
      - to:
          uri: activemq:Output
```