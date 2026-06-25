# Exception Clause - Redelivery

[Back to Exception Clause](exception-clause.md)

## Configuring RedeliveryPolicy (redeliver options)

[RedeliveryPolicy](https://www.javadoc.io/doc/org.apache.camel/camel-base/current/org/apache/camel/processor/errorhandler/RedeliveryPolicy.md) requires to use the [Dead Letter Channel](../components/4.18.x/eips/dead-letter-channel.md) as the [Error Handler](error-handler.md). Dead Letter Channel supports attempting to redeliver the message exchange a number of times before sending it to a dead letter endpoint. See [Dead Letter Channel](../components/4.18.x/eips/dead-letter-channel.md) for further information about redeliver and which redeliver options exists.

### No redelivery is default for onException

By default, any [Exception Clause](exception-clause.md) will **not** redeliver! (as it sets the `maximumRedeliveries` option to 0).

Sometimes you want to configure the redelivery policy on a per exception type basis. By default in the top examples, if an **`org.apache.camel.ValidationException`** occurs then the message will not be redelivered; however if some other exception occurs, e.g., **`IOException`** or whatever, the route will be retried according to the settings from the [Dead Letter Channel](../components/4.18.x/eips/dead-letter-channel.md).

However if you want to customize any methods on the [RedeliveryPolicy](https://www.javadoc.io/doc/org.apache.camel/camel-base/current/org/apache/camel/processor/errorhandler/RedeliveryPolicy.md) object, you can do this via the fluent API. So lets retry in case of **`org.apache.camel.ValidationException`** up till two times.

-   Java
    
-   XML
    
-   YAML
    

```java
onException(ValidationException.class)
    .maximumRedeliveries(2);
```

```xml
<onException>
    <exception>com.mycompany.ValidationException</exception>
    <redeliveryPolicy maximumRedeliveries="2"/>
</onException>
```

```yaml
- onException:
    exception:
      - org.apache.camel.ValidationException
    redeliveryPolicy:
      maximumRedeliveries: 2
```

You can customize any of the `RedeliveryPolicy` options, for instance set a different delay of **`5000`** millis:

-   Java
    
-   XML
    
-   YAML
    

```java
onException(ValidationException.class)
    .maximumRedeliveries(2).redeliveryDelay(5000);
```

```xml
<onException>
    <exception>com.mycompany.ValidationException</exception>
    <redeliveryPolicy maximumRedeliveries="2" redeliveryDelay="5000"/>
</onException>
```

```yaml
- onException:
    exception:
      - org.apache.camel.ValidationException
    redeliveryPolicy:
      maximumRedeliveries: 2
      redeliveryDelay: 5000
```

## Point of Entry for Redelivery Attempts

All redelivery attempts start at the point of the failure. So the route:

_Java-only: redelivery starts at the point of failure_

```java
onException(ConnectException.class)
    .from("direct:start")
    .process("processor1")
    .process("processor2") // <--- throws a ConnectException
    .to("mock:theEnd")
```

Will retry from **`processor2`** - not the complete route.

## Asynchronous Delayed Redelivery

Camel has a feature to _not block_ while waiting for a delayed redelivery to occur. However, if you use transacted routes then Camel will block as it’s mandated by the transaction manager to execute all the work in the same thread context. You can enable the non-blocking asynchronous behavior by the **`asyncDelayedRedelivery`** option. This option can be set on the **`errorHandler`**, **`onException`** or the redelivery policies.

By default, the error handler will create and use a scheduled thread pool to trigger redelivery in the future. You can also configure the **`executorServiceRef`** on the [Error Handler](error-handler.md) to indicate a reference to either a shared thread pool you can enlist in the registry, or a thread pool profile in case you want to be able to control pool settings.

## Catching Multiple Exceptions

Multiple exception can be caught as shown:

-   Java
    
-   XML
    
-   YAML
    

In Java DSL you can add multiple exceptions separated by comma.

```java
onException(MyBusinessException.class, MyOtherBusinessException.class)
    .maximumRedeliveries(2)
    .to("activemq:businessFailed");
```

And in XML DSL you just add another exception element:

```xml
<onException>
    <exception>com.mycompany.MyBusinessException</exception>
    <exception>com.mycompany.MyOtherBusinessException</exception>
    <redeliveryPolicy maximumRedeliveries="2"/>
    <to uri="activemq:businessFailed"/>
</onException>
```

And in YAML DSL you just add another exception in the array:

```yaml
- onException:
    exception:
      - com.mycompany.MyBusinessException
      - com.mycompany.MyOtherBusinessException
    redeliveryPolicy:
      maximumRedeliveries: 2
    steps:
      - to:
          uri: activemq:businessFailed
```