# Threads

How can I decouple the continued routing of a message from the current thread?

![image](_images/eip/MessagingAdapterIcon.gif)

Submit the message to a thread pool, which then is responsible for the continued routing of the message.

In Camel, this is implemented as the Threads EIP.

## Options

The Threads eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **executorService** | To refer to a custom thread pool or use a thread pool profile (as overlay). |  | ExecutorService |
| **poolSize** | Sets the core pool size (number of threads to keep in the pool, even if idle). |  | Integer |
| **maxPoolSize** | Sets the maximum pool size (the upper bound of threads in the pool). |  | Integer |
| **keepAliveTime** | Sets the keep alive time for idle threads before they are terminated. Only applies to threads above the core pool size. |  | Long |
| **timeUnit** | 
Sets the time unit for the keep alive time. By default SECONDS is used.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 |  | TimeUnit |
| **maxQueueSize** | Sets the maximum number of tasks in the work queue. Use -1 or Integer.MAX\_VALUE for an unbounded queue. |  | Integer |
| **allowCoreThreadTimeOut** | Whether idle core threads are allowed to timeout and therefore can shrink the pool size below the core pool size. | false | Boolean |
| **threadName** | Sets the thread name pattern to use for naming threads created by this thread pool. | Threads | String |
| **rejectedPolicy** | 

Sets the handler for tasks which cannot be executed by the thread pool.

Enum values:

-   Abort
    
-   CallerRuns
    
-   Block
    





 |  | ThreadPoolRejectedPolicy |
| **callerRunsWhenRejected** | Whether to use the caller thread as fallback when a task is rejected being added to the thread pool (when its full). This is only used as fallback if no rejectedPolicy has been configured, or the thread pool has no configured rejection handler. | true | Boolean |

## Exchange properties

The Threads eip has no exchange properties.

## Using Threads EIP

The example below will add a Thread pool with a pool size of five threads before sending to `mock:result`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .threads(5)
  .to("mock:result");
```

```xml
<route>
    <from uri="seda:a"/>
    <threads poolSize="5"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - threads:
            poolSize: 5
        - to:
            uri: mock:result
```

And to use a thread pool with a task queue of only 20 elements:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .threads(5).maxQueueSize(20)
  .to("mock:result");
```

```xml
<route>
    <from uri="seda:a"/>
    <threads poolSize="5" maxQueueSize="20"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - threads:
            poolSize: 5
            maxQueueSize: 20
        - to:
            uri: mock:result
```

And you can also use a thread pool with no queue (meaning that a task cannot be pending on a queue):

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .threads(5).maxQueueSize(0)
  .to("mock:result");
```

```xml
<route>
    <from uri="seda:a"/>
    <threads poolSize="5" maxQueueSize="0"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - threads:
            poolSize: 5
            maxQueueSize: 0
        - to:
            uri: mock:result
```

### About rejected tasks

The Threads EIP uses a thread pool which has a worker queue for tasks. When the worker queue gets full, the task is rejected.

You can customize how to react upon this using the `rejectedPolicy` and `callerRunsWhenRejected` options. The latter is used to easily switch between the two most common and recommended settings. Either let the current caller thread execute the task (i.e. it will become synchronous), but also give time for the thread pool to process its current tasks, without adding more tasks (self throttling). This is the default behavior.

The `Abort` policy, means the task is rejected, and a `RejectedExecutionException` is thrown.

> **Important**
> The reject policy options `Discard` and `DiscardOldest` is deprecated in Camel 3.x and removed in Camel 4 onwards.

### Default values

The Threads EIP uses the default values from the default [Thread Pool Profile](../../../manual/threading-model.md). If the profile has not been altered, then the default profile is as follows:

  
| Option | Default | Description |
| --- | --- | --- |
| **poolSize** | `10` | Sets the default core pool size (minimum number of threads to keep in pool) |
| **keepAliveTime** | `60` | Sets the default keep-alive time (in seconds) for inactive threads |
| **maxPoolSize** | `20` | Sets the default maximum pool size |
| **maxQueueSize** | `1000` | Sets the default maximum number of tasks in the work queue. Use -1 for an unbounded queue. |
| **allowCoreThreadTimeOut** | `true` | Sets default whether to allow core threads to timeout |
| **rejectedPolicy** | `CallerRuns` | Sets the default handler for tasks which cannot be executed by the thread pool. Has four options: `Abort, CallerRuns, Discard, DiscardOldest` which corresponds to the same four options provided out of the box in the JDK. |

### See Also

See [Threading Model](../../../manual/threading-model.md)