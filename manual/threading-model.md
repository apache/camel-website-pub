# Threading Model

The threading model in Camel is based on a pluggable reactive routing engine, and thread pools from the JDK concurrency API.

This page focuses on thread pools. Camel leverages thread pools in several places such as:

-   Several [EIP](../components/4.18.x/eips/enterprise-integration-patterns.md) patterns support using thread pools for concurrency
    
-   [SEDA](../components/4.18.x/seda-component.md) component for asynchronous connectivity
    
-   [Threads](../components/4.18.x/eips/threads-eip.md) EIP in Camel routes
    
-   Several components use thread pools out of the box, such as [JMS](../components/4.18.x/jms-component.md), [Kafka](../components/4.18.x/kafka-component.md), [Netty](../components/4.18.x/netty-component.md) or [Jetty](../components/4.18.x/jetty-component.md)
    

## Thread pool profiles

By default, when a thread pool is to be created by Camel, then the pool configuration is based upon a profile, the _default thread pool profile_

The default profile is pre-configured out of the box with the following settings:

  
| Option | Default | Description |
| --- | --- | --- |
| **poolSize** | `10` | Sets the default core pool size (threads to keep minimum in pool) |
| **keepAliveTime** | `60` | Sets the default keep alive time (in seconds) for inactive threads |
| **maxPoolSize** | `20` | Sets the default maximum pool size |
| **maxQueueSize** | `1000` | Sets the default maximum number of tasks in the work queue. Use -1 for an unbounded queue. |
| **allowCoreThreadTimeOut** | `true` | Sets default whether to allow core threads to timeout |
| **rejectedPolicy** | `CallerRuns` | Sets the default handler for tasks which cannot be executed by the thread pool. Has four options: `Abort, CallerRuns, Discard, DiscardOldest` which corresponds to the same four options provided out of the box in the JDK. |

What that means is that for example when you use [Multicast](../components/4.18.x/eips/multicast-eip.md) with `parallelProcessing=true` enabled, then it would create a thread pool based on the profile above.

You can define as many thread pool profiles as you like. But there must be only **one** default profile. A custom thread pool profile will inherit from the default profile. Which means that any option you do not explicit define will fallback and use the option from the default profile.

### Configuring default thread pool profile

In Spring XML you can configure thread pool profile with `threadPoolProfile` as shown:

-   Java
    
-   Spring XML
    
-   Application Properties
    

```java
ThreadPoolProfile profile = camelContext.getExecutorServiceManager().getDefaultThreadPoolProfile();
profile.setPoolSize(5);
profile.setMaxPoolSize(10);
```

```xml
<threadPoolProfile id="defaultThreadPoolProfile"
    defaultProfile="true"
    poolSize="5"
    maxPoolSize="10"/>
```

You can also configure the thread pools in `application.properties`. The default pool can easily be configured as follows:

```properties
## configure default thread pool profile
camel.threadpool.pool-size = 5
camel.threadpool.max-pool-size = 5
```

### Using thread pool profiles

Suppose you want to use a custom thread pool profile for a Multicast EIP pattern in a Camel route you can do it using the `executorServiceRef` attribute as shown in Spring XML:

-   Java
    
-   Spring XML
    
-   YAML
    

In Java DSL you can use `ThreadPoolProfileBuilder` to create a profile and then register the profile:

```java
// setup thread pool profile
ThreadPoolProfileBuilder builder = new ThreadPoolProfileBuilder("fooProfile");
builder.poolSize(20).maxPoolSize(50).maxQueueSize(-1);

// add profile to camel
camelContext.getExecutorServiceManager().registerThreadPoolProfile(builder.build());

// camel routes can now refer to the thread pool via its id
from("direct:start")
  .multicast().aggregationStrategy("myStrategy").executorService("fooProfile").to("xxx");
```

```xml
<camelContext>

    <threadPoolProfile id="fooProfile"
                       poolSize="20" maxPoolSize="50" maxQueueSize="-1"/>

    <route>
       <multicast aggregationStrategy="myStrategy" executorServiceRef="fooProfile">
          ...
       </multicast>
    </route>
</camelContext>
```

To create a new profile, then use `camel.threadpool.config[profileId]` syntax as shown below:

```properties
camel.threadpool.config[fooProfile].id = fooProfile
camel.threadpool.config[fooProfile].pool-size = 20
camel.threadpool.config[fooProfile].max-pool-size = 50
camel.threadpool.config[fooProfile].max-queue-size = -1
```

And then you can refer to the thread pool in the Camel route:

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - multicast:
            aggregationStrategy: myStrategy
            executorService: fooProfile
            steps:
              - to:
                  uri: log:hello
```

What Camel will do at runtime is to lookup in the [Registry](registry.md) for a `ExecutorService` with the id `fooProfile`. If none found it will fallback and see if there is a `ThreadPoolProfile` defined with that id. In this example there is a profile, so the profile is used as base settings for creating a new `ExecutorService` which is handed back to the [Multicast](../components/4.18.x/eips/multicast-eip.md) EIP to use in the Camel route.

## Creating custom thread pools

You can also use the `<threadPool>` tag in Spring XML to create a Java thread pool (`ExecutorService`). Notice that any options you do not explicit define, will have Camel to use the default thread pool profile as fallback. For example if you omit setting the `maxQueueSize` then Camel will fallback and use the value from the default thread pool profiles, which by default is `1000`.

Spring XML

```xml
<camelContext>

    <threadPool id="nyPool" poolSize="20" maxPoolSize="50"/>

    <route>
       <multicast aggregationStrategy="myStrategy" executorServiceRef="myPool">
          ...
       </multicast>
    </route>
</camelContext>
```

## What is the difference between thread-pool and thread-pool-profile?

A thread pool profile is a recipe for creating 1 or more actual thread pools (ie `ExecutorService`). A thread pool is a concrete `ExecutorService` object.

The purpose is to use profiles to make it easy to create many thread pools using the same settings.

## Customizing thread names

On the `ExecutorServiceManager` you can configure the thread name pattern using the `setThreadNamePattern` method, which defines the thread names used when a thread pool creates a thread.

The default pattern is:

```text
Camel (#camelId#) thread ##counter# - #name#
```

In the pattern you can use the following placeholders

-   `#camelId#` - The [CamelContext](camelcontext.md) name
    
-   `#counter#` An unique incrementing counter
    
-   `#name#` - The thread name
    
-   `#longName#` - The long thread name which can include endpoint parameters etc.
    

-   Java
    
-   Spring XML
    
-   Application Properties
    

In Javayou set the pattern on the `ExecutorServiceMananger` as shown:

```java
CamelContext camel = ...
camel.getExecutorServiceManager().setThreadNamePattern("Riding the thread #counter#")
```

In Spring XML the pattern can be set with `threadNamePattern` attribute as shown:

```xml
<camelContext threadNamePattern="Riding the thread #counter#">
  <route>
    <from uri="seda:start"/>
    <to uri="log:result"/>
    <to uri="mock:result"/>
  </route>
</camelContext>
```

And with camel-main, Spring Boot or Quarkus you can configure this in the `application.properties|yaml` file:

```properties
camel.main.thread-name-pattern = Riding the thread #counter#
```

## Shutting down thread pools

All thread pools created by Camel will be properly shutdown when `CamelContext` shutdowns which ensures no leaks in the pools in case you run in a server environment with hot deployments and the likes.

The `ExecutorServiceManager` has APIs for shutting down thread pools gracefully and aggressively. It is encouraged to use this API for creating and shutting down thread pools.

The method `shutdownGraceful(executorService)` from `ExecutorServiceManager` will shutdown graceful at first, until a timeout value is hit. After that it shuts down aggressively, again using the timeout value to wait for the operation to complete. This means you can wait at most 2 x timeout for shutting down the thread pool.

The timeout value is by default `10000` millis. You can configure a custom value on the `ExecutorServiceManager` if needed. During shutdown Camel will log every 2 seconds at INFO level progress of shutting down the thread pool. For example in case a shutdown takes a while, then there is activity in the logs.

The APIs on `ExecutorServiceManager` that is related to shutting down a thread pool is as follows:

 
| Method | Description |
| --- | --- |
| shutdown | Marks the thread pool as shutdown(like calling the `ExecutorService.shutdown()` method). |
| shutdownNow | Forces the thread pool to shut down now(like calling the `ExecutorService.shutdownNow()` method). |
| shutdownGraceful | Marks the thread pool as shutdown, and graceful shutdown the pool, by waiting for tasks to complete. A default timeout value of 10 sec is used, before shutdown becomes aggressive using `shutdownNow`, forcing threads to shut down quicker. |
| shutdownGraceful(timeout) | As shutdownGraceful but with custom timeout value |
| awaitTermination | To wait graceful for the termination of a thread pool (e.g. to wait for its tasks to complete). Will wait until all tasks are completed or timed out. |

## JMX Management

All the thread pools that Camel creates are managed, and thus you can see them in JMX under the `threadpools` tree.

> **Note**
> This requires to enabled JMX by including `camel-management` JAR in the classpath.

## Component developers

If you develop your own Camel component and are in need of a thread pool, then it is advised to use the `ExecutorServiceStrategy`/`ExecutorServiceManager` to create the thread pool you need.

### ExecutorServiceStrategy and ExecutorServiceManager

Camel provides a pluggable strategy to hook in your own thread pool provider.See the `org.apache.camel.spi.ExecutorServiceStrategy` interface which you should implement and hook into the WorkManager.

To hook in custom thread pool providers a `ThreadPoolFactory` interface can be implemented. The implementation can be set in the `ExecutorServiceManager`.

## Virtual Threads

Starting from Java 21, the default `ThreadPoolFactory` can build `ExecutorService` and `ScheduledExecutorService` that use [virtual threads](https://openjdk.org/jeps/425) instead of platform threads.

But as it is an experimental feature, it is not enabled by default, you need to set the System property `camel.threads.virtual.enabled` to `true` and run Camel using Java 21 or above to enable it.

Be aware that even if it is enabled, there are some use cases where platform threads are still used, for example, if the thread factory is configured to create non-daemon threads since virtual threads can only be daemons, or when the `ExecutorService` or `ScheduledExecutorService` to build cannot have more than one thread or finally when `corePoolSize` is set to zero and `maxQueueSize` is set to a value less or equal to `0`.