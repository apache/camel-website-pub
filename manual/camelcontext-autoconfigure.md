# CamelContext Auto Configuration

The [CamelContext](camelcontext.md) is autoconfigured when running Camel with either [Camel Main](../components/4.22.x/others/main.md), Camel Spring Boot, Camel Quarkus.

## Camel Autoconfiguration

Under these runtimes then the autoconfiguration is performed by shared code from the `camel-main` JAR to ensure the configuration is similar on these runtimes.

The autoconfiguration is executed in several steps:

1.  Configure `CamelContext` (and more such as components) from [properties](../components/4.22.x/properties-component.md) from external sources like `application.properties|yaml`
    
2.  Configure optional services that have been registered in the [Registry](registry.md)
    

### Autoconfiguration of Properties

This is used for configuring the standard set of more than 100 options which are listed in the _Camel Main Options_ table at [Camel Main](../components/4.22.x/others/main.md).

> **Note**
> When using Camel on Spring Boot, then these options are prefixed with `camel.springboot`, and not `camel.main`.

### Autoconfiguration of Optional Services

After configuring the standard options, then Camel will look in the [Registry](registry.md) for custom services to be used. For example, to plug in a custom `UnitOfWorkFactory`.

The services can be anything that can be plugged into Camel (typically services that implement an SPI interface `org.apache.camel.spi`).

The following SPI services can only a single instance (singleton) be in the [Registry](registry.md).

 
| SPI | Description |
| --- | --- |
| `AsyncProcessorAwaitManager` | To use a custom async processor await manager |
| `BacklogTracer` | To use a custom backlog tracer |
| `ClassResolver` | To use a custom class resolver. This is only necessary if you run Camel on a special application server to deal with classloading. |
| `Debugger` | To use a custom [debugger](debugger.md) |
| `EventFactory` | To use a custom event notifier factory |
| `ExchangeFactory` | To use a custom [exchange factory](exchange-pooling.md) |
| `ExecutorServiceManager` | To use a custom [thread pool manager](threading-model.md) |
| `FactoryFinderResolver` | To use a custom factory finder resolver. This is only necessary if you run Camel on a special application server to deal with classloading. |
| `HealthCheckRegistry` | To use a custom [health check registry](health-check.md) |
| `InflightRepository` | To use a custom in flight repository |
| `ManagementObjectNameStrategy` | To use a custom JMX MBean object naming |
| `ManagementStrategy` | To use a custom JMX management strategy |
| `MessageHistoryFactory` | To use a custom factory for [message history](../components/4.22.x/eips/message-history.md) |
| `ModelJAXBContextFactory` | To use a custom `JAXBContext` factory (only needed if you run Camel on a special application server to deal with JAXB classloading) |
| `NodeIdFactory` | To use a custom factory for creating auto generated node ids |
| `ProcessorFactory` | To use a custom factory for creating [EIP](../components/4.22.x/eips/enterprise-integration-patterns.md) processors |
| `PropertiesComponent` | To use a custom properties component |
| `ReactiveExecutor` | To use a custom reactive engine in the Camel routing engine |
| `RouteController` | To use a custom [route controller](route-controller.md) |
| `RuntimeEndpointRegistry` | To use a custom runtime [endpoint](endpoint.md) registry |
| `ShutdownStrategy` | To use a custom [shutdown strategy](graceful-shutdown.md) |
| `StartupStepRecorder` | To use a custom startup recorder |
| `ThreadPoolFactory` | To use a custom [thread pool factory](threading-model.md) |
| `UnitOfWorkFactory` | To use a custom unit of work factory |
| `UuidGenerator` | To use a custom [uuid generator](uuidgenerator.md) |

For the following SPI services, there can be multiple (one or more) implementations in the [Registry](registry.md).

 
| SPIs | Description |
| --- | --- |
| `CamelClusterService` | Adds all the custom [camel-cluster services](clustering.md) |
| `EndpointStrategy` | Adds all the custom [endpoint strategies](endpoint.md) |
| `EventNotifier` | Adds all the custom event notifiers |
| `GlobalSSLContextParametersSupplier` | To use a custom supplier for [JSSE (Java Security)](camel-configuration-utilities.md) |
| `InterceptStrategy` | Adds all the custom intercept strategies |
| `LifecycleStrategy` | Adds all the custom lifecycle strategies |
| `LogListener` | Adds all the log listeners |
| `ModelLifecycleStrategy` | Adds all the custom model lifecycle strategies |
| `RoutePolicyFactory` | Adds all the custom [route policy factories](route-policy.md) |
| `ServiceRegistry` | Adds all the custom camel-cloud service registries |
| `ThreadPoolProfile` | Adds all the [thread pool profiles](threading-model.md) |
| `TypeConverters` | Adds all the custom [type converters](type-converter.md) |