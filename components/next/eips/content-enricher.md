# Content Enricher

Camel supports the [Content Enricher](http://www.enterpriseintegrationpatterns.com/DataEnricher.md) from the [EIP patterns](enterprise-integration-patterns.md).

![image](_images/eip/DataEnricher.gif)

In Camel the Content Enricher can be done in several ways:

-   Using [Enrich](enrich-eip.md) EIP
    
-   Using a [Message Translator](message-translator.md)
    
-   Using a [Processor](../../../manual/processor.md) with the enrichment programmed in Java
    
-   Using a [Bean](bean-eip.md) EIP with the enrichment programmed in Java
    

The most natural Camel approach is using [Enrich](enrich-eip.md) EIP.

## Content enrichment using a Message Translator

You can consume a message from one destination, transform it with something like [Velocity](../velocity-component.md) or [XQuery](../xquery-component.md), and then send it on to another destination.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("velocity:com/acme/MyResponse.vm")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="velocity:com/acme/MyResponse.vm"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- from:
    uri: activemq:My.Queue
    steps:
      - to:
          uri: velocity:com/acme/MyResponse.vm
      - to:
          uri: activemq:Another.Queue
```

You can also enrich the message in Java DSL directly (using fluent builder) as an [Expression](../../../manual/expression.md). In the example below, the message is enriched by appending \` World!\` to the message body:

```java
from("direct:start")
    .setBody(body().append(" World!"))
    .to("mock:result");
```

The fluent builder is not available in XML or YAML DSL, instead you can use [Simple](../languages/simple-language.md) language:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(simple("${body} World!"))
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <simple>${body} World!</simple>
  </setBody>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct
      parameters:
        name: start
      steps:
        - setBody:
            expression:
              simple:
                expression: "${body} World!"
        - to:
            uri: mock
            parameters:
              name: result
```

## Content enrichment using a Processor

In this example, we add our own [Processor](../../../manual/processor.md) using explicit Java to enrich the message:

```java
from("direct:start")
    .process(new Processor() {
        public void process(Exchange exchange) {
            Message msg = exchange.getMessage();
            msg.setBody(msg.getBody(String.class) + " World!");
        }
    })
    .to("mock:result");
```

In the Java code above we used an inlined `Processor` which is harder to do with XML or YAML DSL. A good practice is to use a class for your custom `Processor` which can then be referenced in the DSL:

```java
@BindToRegistry("myProcessor")
public class MyProcessor implements Processor {

    @Override
    public void process(Exchange exchange) {
        Message msg = exchange.getMessage();
        msg.setBody(msg.getBody(String.class) + " World!");
    }
}
```

Then you can refer to this processor by its id.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .process("myProcessor")
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:start"/>
    <process ref="myProcessor"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct
      parameters:
        name: start
      steps:
        - process:
            ref: myProcessor
        - to:
            uri: mock
            parameters:
              name: result
```

## Content enrichment using a Bean EIP

We can use [Bean EIP](bean-eip.md) to use any Java method on any bean to act as content enricher:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .bean("myBeanName", "doTransform")
    .to("activemq:Another.Queue");
```

```xml
<route>
    <from uri="activemq:Input"/>
    <bean ref="myBeanName" method="doTransform"/>
    <to uri="activemq:Output"/>
</route>
```

```yaml
- from:
    uri: activemq:Input
    steps:
      - bean:
          ref: myBeanName
          method: doTransform
      - to:
          uri: activemq:Output
```

## Content enrichment using Enrich EIP

Camel comes with two kinds of Content Enricher EIPs:

-   [Enrich](enrich-eip.md) EIP: This is the most common content enricher that uses a `Producer` to obtain the data. It is usually used for [Request Reply](requestReply-eip.md) messaging, for instance, to invoke an external web service.
    
-   [Poll Enrich](pollEnrich-eip.md) EIP: Uses a [Polling Consumer](polling-consumer.md) to obtain the additional data. It is usually used for [Event Message](event-message.md) messaging, for instance, to read a file or download one using [FTP](../ftp-component.md).
    

For more details, see [Enrich](enrich-eip.md) EIP and [Poll Enrich](pollEnrich-eip.md) EIP.