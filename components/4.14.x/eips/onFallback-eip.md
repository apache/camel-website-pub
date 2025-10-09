# On Fallback

If you are using **onFallback** then that is intended to be local processing only where you can do a message transformation or call a bean or something as the fallback.

If you need to call an external service over the network, then you should use **onFallbackViaNetwork** that runs in another independent **HystrixCommand** that uses its own thread pool to not exhaust the first command.

## Options

The On Fallback eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** | Sets the description of this node. |  | String |
| **fallbackViaNetwork** | Whether the fallback goes over the network. If the fallback will go over the network it is another possible point of failure. It is important to execute the fallback command on a separate thread-pool, otherwise if the main command were to become latent and fill the thread-pool this would prevent the fallback from running if the two commands share the same pool. | false | Boolean |
| **outputs** | **Required** |  | List |

## Exchange properties

The On Fallback eip has no exchange properties.

## Using fallback

The **onFallback** is used by [Circuit Breaker](circuitBreaker-eip.md) EIPs to execute a fallback route. For example, how to use this see the various Circuit Breaker implementations:

-   [FaultTolerance EIP](fault-tolerance-eip.md) - MicroProfile Fault Tolerance Circuit Breaker
    
-   [Resilience4j EIP](resilience4j-eip.md) - Resilience4j Circuit Breaker