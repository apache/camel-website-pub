# Stop

How can I stop continue routing a message?

![image](_images/eip/MessageExpirationIcon.gif)

Use a special filter to mark the message to be stopped.

## Options

The Stop eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Using Stop

We want to stop routing a message if the message body contains the word Bye. In the [Content Based Router](choice-eip.md) below we use `stop` in such case.

```java
from("direct:start")
    .choice()
        .when(body().contains("Hello")).to("mock:hello")
        .when(body().contains("Bye")).to("mock:bye").stop()
        .otherwise().to("mock:other")
    .end()
.to("mock:result");
```

And in XML:

```xml
<route>
  <from uri="direct:start"/>
  <choice>
    <when>
      <simple>${body} contains 'Hello'</simple>
      <to uri="mock:hello"/>
    </when>
    <when>
      <simple>${body} contains 'Bye'</simple>
      <stop/>
    </when>
    <otherwise>
      <to uri="mock:other"/>
    </otherwise>
  </choice>
</route>
```

### Calling stop from Java

You can also mark an `Exchange` to stop being routed from Java with the following code:

```java
Exchange exchange = ...
exchange.setRouteStop(true);
```