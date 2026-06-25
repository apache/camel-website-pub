# Circuit Breaker

The Circuit Breaker pattern is inspired by the real-world electrical circuit breaker, which is used to detect excessive current draw and fail fast to protect electrical equipment. The software-based circuit breaker works on the same notion, by encapsulating the operation and monitoring it for failures. The Circuit Breaker pattern operates in three states, as illustrated in the following figure:

![image](_images/eip/CircuitBreaker.png)

The states are as follows:

-   **Closed**: When operating successfully.
    
-   **Open**: When failure is detected, and the breaker opens to short-circuit and fails fast. In this state, the circuit breaker avoids invoking the protected operation and avoids putting the additional load on the struggling service.
    
-   **Half-Open**: After a short period in the open state, an operation is attempted to see whether it can complete successfully, and depending on the outcome, it will transfer to either open or closed state.
    

The Circuit Breaker eip supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **configuration** | Refers to a circuit breaker configuration to use for configuring the circuit breaker EIP. |  | String |
| **inheritErrorHandler** | Whether to inherit Camel error handling during circuit breaker. By default, Camel error handler is turned off. | false | Boolean |
| **resilience4jConfiguration** | Configures the circuit breaker to use Resilience4j with the given configuration. |  | Resilience4jConfigurationDefinition |
| **faultToleranceConfiguration** | Configures the circuit breaker to use MicroProfile Fault Tolerance with the given configuration. |  | FaultToleranceConfigurationDefinition |
| **onFallback** | The fallback route path to execute when the circuit breaker triggers. |  | OnFallbackDefinition |
| **outputs** | **Required** |  | List |

## Exchange properties

The Circuit Breaker eip supports 7 exchange properties, which are listed below.

The exchange properties are set on the `Exchange` by the EIP, unless otherwise specified in the description. This means those properties are available after this EIP has completed processing the `Exchange`.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelResponseSuccessfulExecution** | Whether the exchange was processed successfully by the circuit breaker. |  | boolean |
| **CamelResponseFromFallback** | Whether the exchange was processed by the onFallback by the circuit breaker. |  | boolean |
| **CamelResponseShortCircuited** | Whether the exchange was short circuited by the breaker. |  | boolean |
| **CamelResponseTimedOut** | Whether the exchange timed out during processing by the circuit breaker. |  | boolean |
| **CamelResponseRejected** | Whether the circuit breaker rejected processing the exchange. |  | boolean |
| **CamelResponseIgnored** | Whether the circuit breaker ignored an exception during processing. |  | boolean |
| **CamelResponseState** | The state of the circuit breaker. |  | String |

## Example

Below is an example route showing a circuit breaker endpoint that protects against slow operation by falling back to the in-lined fallback route.

By default, the timeout request is just \*1000ms, so the HTTP endpoint has to be fairly quick to succeed.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .circuitBreaker()
        .to("http://fooservice.com/slow")
    .onFallback()
        .transform().constant("Fallback message")
    .end()
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <circuitBreaker>
    <to uri="http://fooservice.com/slow"/>
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
              - to:
                  uri: http://fooservice.com/slow
              - onFallback:
                  steps:
                    - transform:
                        expression:
                          constant:
                            expression: Fallback message
        - to:
            uri: mock:result
```

## Circuit Breaker components

Camel provides two implementations of this pattern:

-   [Resilience4j](resilience4j-eip.md): Using the Resilience4j implementation
    
-   [Fault Tolerance](fault-tolerance-eip.md): Using the MicroProfile Fault Tolerance implementation