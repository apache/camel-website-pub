# DefaultErrorHandler

This is the default [Error Handler](error-handler.md) in Camel.

The default [Error Handler](error-handler.md) has the same power as the [Dead Letter Channel.](../components/4.18.x/eips/dead-letter-channel.md) However, it does **not** support a _dead letter queue_, which is the only difference between the two of them.

The `DefaultErrorHandler` is configured differently from [Dead Letter Channel](../components/4.18.x/eips/dead-letter-channel.md) as it is configured to:

-   not redeliver
    
-   not handled
    
-   no dead letter queue (because it is not possible)
    

By default, any exception thrown during routing will be propagated back to the caller and the [Exchange](exchange.md) ends immediately. However, you can use the [Exception Clause](exception-clause.md) to catch a given exception and lower the exception by marking it as handled. If so, the exception will **not** be sent back to the caller, and the [Exchange](exchange.md) will succeed, but **not continue** being routed. See the _difference_ between `handled` and `continued` in the [Exception Clause](exception-clause.md) documentation.

## Example

In this route below, any exception thrown in, such as the `validateOrder` bean, will be propagated back to the caller via the jetty endpoint, which then returns an HTTP error message back to the client.

-   Java
    
-   XML
    
-   YAML
    

```java
from("jetty:http://localhost/myservice/order")
  .to("bean:validateOrder")
  .to("jms:queue:order");
```

```xml
<route>
    <from uri="jetty:http://localhost/myservice/order"/>
    <to uri="bean:validateOrder"/>
    <to uri="jms:queue:order"/>
</route>
```

```yaml
- route:
    from:
      uri: jetty:http://localhost/myservice/order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: jms:queue:order
```

We can add an `onException` in case we want to catch certain exceptions and route them differently, for instance to catch a `org.apache.camel.ValidationException` and return a fixed response to the caller.

-   Java
    
-   XML
    
-   YAML
    

```java
onException(ValidationException.class)
  .handled(true)
  .transform(constant("INVALID ORDER"));

from("jetty:http://localhost/myservice/order")
  .to("bean:validateOrder")
  .to("jms:queue:order");
```

```xml
<onException>
    <exception>org.apache.camel.ValidationException</exception>
    <handled>
        <constant>true</constant>
    </handled>
    <transform>
        <constant>INVALID ORDER</constant>
    </transform>
</onException>

<route>
    <from uri="jetty:http://localhost/myservice/order"/>
    <to uri="bean:validateOrder"/>
    <to uri="jms:queue:order"/>
</route>
```

```yaml
- onException:
    exception:
      - org.apache.camel.ValidationException
    handled:
      constant:
        expression: "true"
    steps:
      - transform:
          expression:
            constant:
              expression: INVALID ORDER
- route:
    from:
      uri: jetty:http://localhost/myservice/order
      steps:
        - to:
            uri: bean:validateOrder
        - to:
            uri: jms:queue:order
```

When the `ValidationException` is thrown from the `validateOrder` bean, it is intercepted by Camel error handler which lets the `onException(ValidationException.class)` handle the exception. The [Exchange](exchange.md) is routed to this onException route, and since we use `handled(true)`, then the original exception is cleared, and we transform the message into a fixed response that is returned to jetty endpoint that returns it to the original caller.