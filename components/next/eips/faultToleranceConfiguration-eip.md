# Fault Tolerance Configuration

This page documents all the specific options for the [Fault Tolerance](fault-tolerance-eip.md) EIP.

The Fault Tolerance Configuration eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **typedGuard** | Refers to an existing io.smallrye.faulttolerance.api.TypedGuard instance to lookup and use from the registry. When using this, then any other TypedGuard circuit breaker options are not in use. |  | String |
| **delay** | Control how long the circuit breaker stays open. The default is 5 seconds. | 5000 | String |
| **successThreshold** | Controls the number of trial calls which are allowed when the circuit breaker is half-open. | 1 | Integer |
| **requestVolumeThreshold** | Controls the size of the rolling window used when the circuit breaker is closed. | 20 | Integer |
| **failureRatio** | Configures the failure rate threshold in percentage. If the failure rate is equal or greater than the threshold the CircuitBreaker transitions to open and starts short-circuiting calls. | 50 | Integer |
| **timeoutEnabled** | Whether timeout is enabled or not on the circuit breaker. | false | Boolean |
| **timeoutDuration** | Configures the thread execution timeout. Default value is 1 second. | 1000 | String |
| **timeoutPoolSize** | Configures the pool size of the thread pool when timeout is enabled. | 10 | Integer |
| **bulkheadEnabled** | Whether bulkhead is enabled or not on the circuit breaker. | false | Boolean |
| **bulkheadMaxConcurrentCalls** | Configures the max amount of concurrent calls the bulkhead will support. | 10 | Integer |
| **bulkheadWaitingTaskQueue** | Configures the task queue size for holding waiting tasks to be processed by the bulkhead. | 10 | Integer |
| **threadOffloadExecutorService** | References a custom thread pool to use when offloading a guarded action to another thread. |  | ExecutorService |

## Exchange properties

The Fault Tolerance Configuration eip has no exchange properties.

## Example

See [Fault Tolerance](fault-tolerance-eip.md) EIP for details how to use this EIP.