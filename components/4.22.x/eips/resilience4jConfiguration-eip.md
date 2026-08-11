# Resilience4j Configuration

This page documents all the specific options for the [Resilience4j](resilience4j-eip.md) EIP.

The Resilience4j Configuration eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **circuitBreaker** | Refers to an existing io.github.resilience4j.circuitbreaker.CircuitBreaker instance to lookup and use from the registry. When using this, then any other circuit breaker options are not in use. |  | String |
| **config** | Refers to an existing io.github.resilience4j.circuitbreaker.CircuitBreakerConfig instance to lookup and use from the registry. |  | String |
| **failureRateThreshold** | Configures the failure rate threshold in percentage. If the failure rate is equal or greater than the threshold the CircuitBreaker transitions to open and starts short-circuiting calls. | 50 | Float |
| **permittedNumberOfCallsInHalfOpenState** | Configures the number of permitted calls when the CircuitBreaker is half open. | 10 | Integer |
| **throwExceptionWhenHalfOpenOrOpenState** | Whether to throw io.github.resilience4j.circuitbreaker.CallNotPermittedException when the call is rejected because the circuit breaker is half open or open. | false | Boolean |
| **slidingWindowSize** | Configures the size of the sliding window which is used to record the outcome of calls when the CircuitBreaker is closed. Sliding window can either be count-based or time-based. | 100 | Integer |
| **slidingWindowType** | 
Configures the type of the sliding window which is used to record the outcome of calls when the CircuitBreaker is closed. Sliding window can either be count-based or time-based.

Enum values:

-   TIME\_BASED
    
-   COUNT\_BASED
    





 | COUNT\_BASED | String |
| **slidingWindowSynchronizationStrategy** | 

Configures the synchronization strategy for the sliding window. LOCK\_FREE uses a CAS-based lock-free algorithm for better performance under high concurrency. SYNCHRONIZED uses blocking locks with lower memory allocation.

Enum values:

-   LOCK\_FREE
    
-   SYNCHRONIZED
    





 | SYNCHRONIZED | String |
| **minimumNumberOfCalls** | Configures the minimum number of calls which are required (per sliding window period) before the CircuitBreaker can calculate the error rate. | 100 | Integer |
| **writableStackTraceEnabled** | Enables writable stack traces. When set to false, Exception.getStackTrace returns a zero length array. This may be used to reduce log spam when the circuit breaker is open. | true | Boolean |
| **waitDurationInOpenState** | Configures the wait duration which specifies how long the CircuitBreaker should stay open, before it switches to half open. The default is 60 seconds. | 60000 | String |
| **automaticTransitionFromOpenToHalfOpenEnabled** | Enables automatic transition from OPEN to HALF\_OPEN state once the waitDurationInOpenState has passed. | false | Boolean |
| **maxWaitDurationInHalfOpenState** | Configures the maximum wait duration which controls how long the CircuitBreaker should stay in Half Open state, before it switches to open. Value 0 means circuit breaker will wait in half open state until all permitted calls have been completed. | 0 | String |
| **slowCallRateThreshold** | Configures a threshold in percentage. The CircuitBreaker considers a call as slow when the call duration is greater than slowCallDurationThreshold. When the percentage of slow calls is equal or greater the threshold, the CircuitBreaker transitions to open and starts short-circuiting calls. | 100 | Float |
| **slowCallDurationThreshold** | Configures the duration threshold above which calls are considered as slow and increase the slow calls percentage. The default is 60 seconds. | 60000 | String |
| **bulkheadEnabled** | Whether bulkhead is enabled or not on the circuit breaker. | false | Boolean |
| **bulkheadMaxConcurrentCalls** | Configures the max amount of concurrent calls the bulkhead will support. | 25 | Integer |
| **bulkheadMaxWaitDuration** | Configures a maximum amount of time which the calling thread will wait to enter the bulkhead. The default is 0 (no waiting). | 0 | String |
| **bulkheadFairCallHandlingEnabled** | Configures whether the bulkhead uses a fair calling strategy. When enabled (default), a fair strategy guarantees the order of incoming requests (FIFO). When disabled, no ordering is guaranteed and may improve throughput. | true | Boolean |
| **asynchronous** | Whether to use asynchronous (non-blocking) processing with CompletionStage-based circuit breaker decorators. When enabled, the circuit breaker releases the caller thread immediately and completes processing asynchronously. This is most valuable when the downstream processor supports asynchronous processing (e.g. Netty HTTP, Kafka). When used with timeout, the timeoutExecutorService must be a ScheduledExecutorService. | false | Boolean |
| **timeoutEnabled** | Whether timeout is enabled or not on the circuit breaker. | false | Boolean |
| **timeoutExecutorService** | References to a custom thread pool to use when timeout is enabled (uses ForkJoinPool.commonPool() by default). |  | ExecutorService |
| **timeoutDuration** | Configures the thread execution timeout. Default value is 1 second. | 1000 | String |
| **timeoutCancelRunningFuture** | Configures whether cancel is called on the running future. Defaults to true. | true | Boolean |
| **micrometerEnabled** | Whether to enable collecting statistics using Micrometer for all circuit breaker instances. This is a global setting (configure via camel.resilience4j.micrometerEnabled=true) and requires adding camel-resilience4j-micrometer JAR to the classpath. | false | Boolean |
| **recordException** | Configure a list of exceptions that are recorded as a failure and thus increase the failure rate. Any exception matching or inheriting from one of the list counts as a failure, unless explicitly ignored via ignoreExceptions. |  | List |
| **ignoreException** | Configure a list of exceptions that are ignored and neither count as a failure nor success. Any exception matching or inheriting from one of the list will not count as a failure nor success, even if the exception is part of recordExceptions. |  | List |

## Exchange properties

The Resilience4j Configuration eip has no exchange properties.

## Example

See [Resilience4j](resilience4j-eip.md) EIP for details how to use this EIP.