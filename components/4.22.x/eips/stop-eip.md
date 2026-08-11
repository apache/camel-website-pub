# Stop

How can I stop routing a message?

![image](_images/eip/MessageExpirationIcon.gif)

Use a special filter to mark the message to be stopped.

## Options

The Stop eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |

## Exchange properties

The Stop eip has no exchange properties.

## Using Stop

We want to stop routing a message if the message body contains the word Bye. In the [Content-Based Router](choice-eip.md) below we use `stop` in such a case.

Java

```java
from("direct:start")
    .choice()
        .when(body().contains("Hello")).to("mock:hello")
        .when(body().contains("Bye")).to("mock:bye").stop()
        .otherwise().to("mock:other")
    .end()
.to("mock:result");
```

XML

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

YAML

In YAML you use an empty `stop: {}` node as shown:

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - choice:
            when:
              - steps:
                  - to:
                      uri: mock:hello
              - steps:
                  - to:
                      uri: mock:bye
                  - stop: {}
            otherwise:
              steps:
                - to:
                    uri: mock:other
        - to:
            uri: mock:result
```

### Stopping Exchange from Java code

You can also mark an `Exchange` to stop being routed using the `setRouteStop(true)` method using Java code:

```java
Exchange exchange = ...
exchange.setRouteStop(true);
```

## See Also

See also the related [Throw Exception](throwException-eip.md) EIP.