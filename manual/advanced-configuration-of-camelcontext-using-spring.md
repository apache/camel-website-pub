# Camel Spring XML Auto Configuration

This is only applicable when using Spring XML files with the `camel-spring-xml` JAR.

A spring XML file is the XML files that uses `<beans>` as root tag and have an embedded `<camelContext>`. This is the classic way of using XML DSL with Apache Camel. That was implemented before Spring Boot.

If you use Camel on Spring Boot, then look at [Camel Context Auto Configuration](camelcontext-autoconfigure.md) instead.

## Autoconfiguration of Optional Services

Camel will configure these functions by doing a lookup in the Spring bean registry to find beans of the given type.

The following list all requires at most one bean defined. If there is more than one bean of this type, then Camel will **not** use it.

  
| Type | Number of beans | Description |
| --- | --- | --- |
| `AsyncProcessorAwaitManager` | 0..1 | To use a third-party async process await manager. |
| `BacklogTracer` | 0..1 | To use a third-party [BacklogTracer](backlog-tracer.md). |
| `ClassResolver` | 0..1 | To use a third-party class resolver. More details at [Pluggable Class Resolvers](pluggable-class-resolvers.md). |
| `Debugger` | 0..1 | To use a [Debugger](debugger.md) usually for tooling. |
| `Delayer` | 0..1 | To use a third-party [Delayer](../components/4.22.x/eips/delay-eip.md). |
| `EventFactory` | 0..1 | To use a third-party event factory. |
| `ExecutorServiceManager` | 0..1 | To use a third-party executor service manager. More details at [Threading Model](threading-model.md). |
| `ExecutorServiceStrategy` | 0..1 | To use a third-party executor service strategy. More details at [Threading Model](threading-model.md). |
| `FactoryFinderResolver` | 0..1 | To use a third-party factory finder. |
| `HeadersMapFactory` | 0..1 | To use a third-party HeadersMapFactory implementation. |
| `HealthCheckRegistry` | 0..1 | To use a third-party [HealthCheckRegistry](health-check.md) implementation. |
| `InflightRepository` | 0..1 | To use a third-party in flight repository. |
| `Logger` | 0..1 | To use provided org.slf4j.Logger for [Log](../components/4.22.x/log-component.md) component and [log() EIP](../components/4.22.x/eips/log-eip.md). |
| `ManagementObjectNameStrategy` | 0..1 | To use a third-party strategy for naming `MBeans` for [management](jmx.md). |
| `ManagementStrategy` | 0..1 | To use a third-party strategy for [management](jmx.md), for example, JMX management. |
| `MessageHistoryFactory` | 0..1 | To use a third-party MessageHistoryFactory implementation. |
| `ModelJAXBContextFactory` | 0..1 | To use a third-party model JAXB ContextFactory |
| `NodeIdFactory` | 0..1 | To use a third-party node id factory. |
| `PackageScanClassResolver` | 0..1 | To use a third-party package scan resolver. More details at [Pluggable Class Resolvers](pluggable-class-resolvers.md). |
| `ProcessorFactory` | 0..1 | To use a third-party processor factory. |
| `Registry` | 0..1 | To use a third-party bean registry. By default, Camel will use Spring ApplicationContext (when using Spring) as registry. |
| `RuntimeEndpointRegistry` | 0..1 | To use a third-party `RuntimeEndpointRegistry` implementation. |
| `RuntimeEndpointRegistry` | 0..1 | To use a third-party `RuntimeEndpointRegistry` implementation. |
| `ShutdownStrategy` | 0..1 | To use a third-party shutdown strategy. |
| `StreamCachingStrategy` | 0..1 | To use a third-party [Stream caching](stream-caching.md) strategy. |
| `ThreadPoolFactory` | 0..1 | To use a third-party thread pool factory. More details at [Threading Model](threading-model.md). |
| `TraceFormatter` | 0..1 | To use a bean that has the tracing options configured. |
| `` Tracer` `` | 0..1 | To use a third-party [Tracer](tracer.md). |
| `` UnitOfWorkFactory` `` | 0..1 | To use third-party `UnitOfWork` implementations created by the factory. |
| `` UuidGenerator` `` | 0..1 | To use a third-party [UuidGenerator](uuidgenerator.md). |

And the following options have support for any number of beans defined.

  
| Type | Number of beans | Description |
| --- | --- | --- |
| `CamelClusterService` | 0..n | To detect [Clustering](clustering.md) services. |
| `EndpointStrategy` | 0..n | To use third-party endpoint strategies. |
| `EventNotifier` | 0..n | To use third-party event notifiers. |
| `HealthCheckRepository` | 0..n | To use Camel [Health Check](health-check.md) repositories. |
| `InterceptStrategy` | 0..n | To use your own [Intercept](../components/4.22.x/eips/intercept.md)that intercepts every processing step in all routes in the [CamelContext](camelcontext.md). For instance, you can use this to do an AOP like performance timer interceptor. |
| `LifecycleStrategy` | 0..n | To use third-party lifecycle strategies. |
| `LogListener` | 0..n | To use custom `LogListener` implementations. |
| `MainListener` | 0..n | To use custom `MainListener` implementations. |
| `ModelLifecycleStrategy` | 0..n | To use third-party model lifecycle strategies. |
| `RoutePolicyFactory` | 0..n | To use a third-party route policy factory to create a route policy for every route. |