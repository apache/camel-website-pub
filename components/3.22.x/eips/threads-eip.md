# Threads

How can I decouple the continued routing of a message from the current thread?

![image](_images/eip/MessagingAdapterIcon.gif)

Submit the message to a thread pool, which then is responsible for the continued routing of the message.

In Camel this is implemented as the Threads EIP.

## Options

The Threads eip supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **executorService** | To use a custom thread pool. |  | ExecutorService |
| **poolSize** | Sets the core pool size. |  | Integer |
| **maxPoolSize** | Sets the maximum pool size. |  | Integer |
| **keepAliveTime** | Sets the keep alive time for idle threads. |  | Long |
| **timeUnit** | 
Sets the keep alive time unit. By default SECONDS is used.

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
| **allowCoreThreadTimeOut** | Whether idle core threads are allowed to timeout and therefore can shrink the pool size below the core pool size Is by default false. | false | Boolean |
| **threadName** | Sets the thread name to use. | Threads | String |
| **rejectedPolicy** | 

Sets the handler for tasks which cannot be executed by the thread pool.

Enum values:

-   Abort
    
-   CallerRuns
    
-   DiscardOldest
    
-   Discard
    





 |  | ThreadPoolRejectedPolicy |
| **callerRunsWhenRejected** | Whether or not to use as caller runs as fallback when a task is rejected being added to the thread pool (when its full). This is only used as fallback if no rejectedPolicy has been configured, or the thread pool has no configured rejection handler. Is by default true. | true | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Using Threads EIP

The example below will add a Thread pool with a pool size of 5 threads before sending to mock:result.

```java
from("seda:a")
  .threads(5)
  .to("mock:result");
```

And in XML DSL

```xml
<route>
    <from uri="seda:a"/>
    <threads poolSize="5"/>
    <to uri="mock:result"/>
</route>
```

And to use a thread pool with a task queue of only 20 elements:

```java
from("seda:a")
  .threads(5).maxQueueSize(20)
  .to("mock:result");
```

And in XML DSL

```xml
<route>
    <from uri="seda:a"/>
    <threads poolSize="5" maxQueueSize="20"/>
    <to uri="mock:result"/>
</route>
```

And you can also use a thread pool with no queue (meaning that a task cannot be pending on a queue):

```java
from("seda:a")
  .threads(5).maxQueueSize(0)
  .to("mock:result");
```

And in XML DSL

```xml
<route>
    <from uri="seda:a"/>
    <threads poolSize="5" maxQueueSize="0"/>
    <to uri="mock:result"/>
</route>
```

### About rejected tasks

The Threads EIP uses a thread pool which has a worker queue for tasks. When the worker queue gets full, the task is rejected.

You can customize how to react upon this using the `rejectedPolicy` and `callerRunsWhenRejected` options. The latter is used to easily switch between the two most common and recommended settings. Either let the current caller thread execute the task (i.e. it will become synchronous), but also give time for the thread pool to process its current tasks, without adding more tasks (self throttling). This is the default behavior.

The `Abort` policy, means the task is rejected, and a `RejectedExecutionException` is thrown.

The other options `Discard` and `DiscardOldest` is **deprecated** and should not be used.

### Default values

The Threads EIP uses the default values from the default [Thread Pool Profile](../../../manual/threading-model.md). If the profile has not been altered, then the default profile are as follows:

  
| Option | Default | Description |
| --- | --- | --- |
| **poolSize** | `10` | Sets the default core pool size (threads to keep minimum in pool) |
| **keepAliveTime** | `60` | Sets the default keep alive time (in seconds) for inactive threads |
| **maxPoolSize** | `20` | Sets the default maximum pool size |
| **maxQueueSize** | `1000` | Sets the default maximum number of tasks in the work queue. Use -1 for an unbounded queue. |
| **allowCoreThreadTimeOut** | `true` | Sets default whether to allow core threads to timeout |
| **rejectedPolicy** | `CallerRuns` | Sets the default handler for tasks which cannot be executed by the thread pool. Has four options: `Abort, CallerRuns, Discard, DiscardOldest` which corresponds to the same four options provided out of the box in the JDK. |

### See Also

See [Threading Model](../../../manual/threading-model.md)