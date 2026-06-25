# On Fallback

If you are using **onFallback** then that is intended to be local processing only where you can do a message transformation or call a bean or something as the fallback.

If you need to call an external service over the network, then you should use **onFallbackViaNetwork** that runs in another independent **HystrixCommand** that uses its own thread pool to not exhaust the first command.

## Options

The On Fallback eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **fallbackViaNetwork** | Whether the fallback goes over the network. If so, the fallback is executed on a separate thread-pool to avoid exhausting the main thread-pool. | false | Boolean |
| **outputs** | **Required** |  | List |

## Exchange properties

The On Fallback eip has no exchange properties.

## Using fallback

The **onFallback** is used by [Circuit Breaker](circuitBreaker-eip.md) EIPs to execute a fallback route. For example, how to use this see the various Circuit Breaker implementations:

-   [FaultTolerance EIP](fault-tolerance-eip.md) - MicroProfile Fault Tolerance Circuit Breaker
    
-   [Resilience4j EIP](resilience4j-eip.md) - Resilience4j Circuit Breaker