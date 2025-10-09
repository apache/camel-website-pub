# Fault Tolerance EIP

This component supports the [Circuit Breaker](circuitBreaker-eip.md) EIP with the [MicroProfile Fault Tolerance](../others/microprofile-fault-tolerance.md) library.

## Options

The Fault Tolerance EIP supports two options which are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **faultToleranceConfiguration** | Configure the Fault Tolerance EIP. When the configuration is complete, use `end()` to return to the Fault Tolerance EIP. |  | `FaultToleranceConfigurationDefinition` |
| **faultToleranceConfigurationRef** | Refers to a Fault Tolerance configuration to use for configuring the Fault Tolerance EIP. |  | String |

See [Fault Tolerance Configuration](faultToleranceConfiguration-eip.md) for all the configuration options on the Fault Tolerance [Circuit Breaker](circuitBreaker-eip.md).

## Using Fault Tolerance EIP

Below is an example route showing a Fault Tolerance EIP circuit breaker that protects against a downstream HTTP operation with fallback.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .circuitBreaker()
        .to("http://fooservice.com/faulty")
    .onFallback()
        .transform().constant("Fallback message")
    .end()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:start"/>
    <circuitBreaker>
        <to uri="http://fooservice.com/faulty"/>
        <onFallback>
            <transform>
                <constant>Fallback message</constant>
            </transform>
        </onFallback>
    </circuitBreaker>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - circuitBreaker:
            steps:
              - onFallback:
                  steps:
                    - transform:
                        expression:
                          constant:
                            expression: Fallback message
              - to:
                  uri: http://fooservice.com/faulty
        - to:
            uri: mock:result
```

In case the calling the downstream HTTP service is failing, and an exception is thrown, then the circuit breaker will react and execute the fallback route instead.

If there was no fallback, then the circuit breaker will throw an exception.

> **Tip**
> For more information about fallback, see [onFallback](onFallback-eip.md).

### Configuring Fault Tolerance

You can fine-tune the Fault Tolerance EIP by the many [Fault Tolerance Configuration](faultToleranceConfiguration-eip.md) options.

For example, to use a 2-second execution timeout, you can do as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .circuitBreaker()
        // use a 2-second timeout
        .faultToleranceConfiguration().timeoutEnabled(true).timeoutDuration(2000).end()
        .log("Fault Tolerance processing start: ${threadName}")
        .to("http://fooservice.com/faulty")
        .log("Fault Tolerance processing end: ${threadName}")
    .end()
    .log("After Fault Tolerance ${body}");
```

```xml
<route>
  <from uri="direct:start"/>
  <circuitBreaker>
    <faultToleranceConfiguration timeoutEnabled="true" timeoutDuration="2000"/>
    <log message="Fault Tolerance processing start: ${threadName}"/>
    <to uri="http://fooservice.com/faulty"/>
    <log message="Fault Tolerance processing end: ${threadName}"/>
  </circuitBreaker>
  <log message="After Fault Tolerance: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - circuitBreaker:
            steps:
              - faultToleranceConfiguration:
                  timeoutDuration: 2000
                  timeoutEnabled: "true"
              - log:
                  message: "Fault Tolerance processing start: ${threadName}"
              - to:
                  uri: http://fooservice.com/faulty
              - log:
                  message: "Fault Tolerance processing end: ${threadName}"
        - log:
            message: "After Fault Tolerance: ${body}"
```

In this example, if calling the downstream service does not return a response within 2 seconds, a timeout is triggered, and the exchange will fail with a TimeoutException.

## Camel’s Error Handler and Circuit Breaker EIP

By default, the [Circuit Breaker](circuitBreaker-eip.md) EIP handles errors by itself. This means if the circuit breaker is open, and the message fails, then Camel’s error handler is not reacting also.

However, you can enable Camels error handler with circuit breaker by enabling the `inheritErrorHandler` option, as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
// Camel's error handler that will attempt to redeliver the message 3 times
errorHandler(deadLetterChannel("mock:dead").maximumRedeliveries(3).redeliveryDelay(0));

from("direct:start")
    .to("log:start")
    // turn on Camel's error handler on circuit breaker so Camel can do redeliveries
    .circuitBreaker().inheritErrorHandler(true)
        .to("mock:a")
        .throwException(new IllegalArgumentException("Forced"))
    .end()
    .to("log:result")
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="log:start"/>
    <circuitBreaker inheritErrorHandler="true">
        <to uri="mock:a"/>
        <throwException exceptionType="java.lang.IllegalArgumentException" message="Forced"/>
    </circuitBreaker>
    <to uri="log:result"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: log:start
        - circuitBreaker:
            inheritErrorHandler: "true"
            steps:
              - to:
                  uri: mock:a
              - throwException:
                  exceptionType: "java.lang.IllegalArgumentException"
                  message: "Forced"
        - to:
            uri: log:result
        - to:
            uri: mock:result
```

This example is from a test, where you can see the Circuit Breaker EIP block has been hardcoded to always fail by throwing an exception. Because the `inheritErrorHandler` has been enabled, then Camel’s error handler will attempt to call the Circuit Breaker EIP block again.

That means the `mock:a` endpoint will receive the message again, and a total of `1 + 3 = 4` message (first time + 3 redeliveries).

If we turn off the `inheritErrorHandler` option (default) then the Circuit Breaker EIP will only be executed once because it handled the error itself.

## Dependencies

> **Note**
> Camel provides the [Circuit Breaker](circuitBreaker-eip.md) EIP in the route model, which allows to plug in different implementations. MicroProfile Fault Tolerance is one such implementation.

Maven users will need to add the following dependency to their pom.xml to use this EIP:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-microprofile-fault-tolerance</artifactId>
    <version>x.x.x</version><!-- use the same version as your Camel core version -->
</dependency>
```

### Using Fault Tolerance with Spring Boot

This component is **not supported** Spring Boot. Instead, it is supported in Standalone and with Camel Quarkus.