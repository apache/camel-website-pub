# Infinispan

JVM since0.0.1 Native since0.0.1

Read and write from/to Infinispan distributed key/value store and data grid.

## What’s inside

-   [Infinispan component](../../../../components/4.18.x/infinispan-component.md), URI syntax: `infinispan:cacheName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-infinispan)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-infinispan</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Infinispan client configuration

You can configure Camel Infinispan in one of two ways.

1.  Using the relevant Camel Infinispan [component & endpoint options](../../../../components/4.18.x/infinispan-component.html#_component_options)
    
2.  Using the [Quarkus Infinispan extension configuration properties](https://quarkus.io/guides/infinispan-client#configuration-reference).
    

More details about these two configuration methods is described below.

### Camel Infinispan component and endpoint configuration

When using 'pure' Camel Infinispan component and endpoint configuration (I.e. where’s there’s no `quarkus.infinispan-client` configuration set), you **must** disable generation of the default Quarkus Infinispan `RemoteCacheManager` bean by adding the following configuration to `application.properties`.

```properties
quarkus.infinispan-client.devservices.create-default-client=false
```

If you wish to take advantage of [Quarkus Dev Services for Infinispan](https://quarkus.io/guides/infinispan-dev-services), the Camel Infinispan component can be configured as follows in `application.properties`.

```properties
# dev / test mode Quarkus Infinispan Dev services configuration
quarkus.infinispan-client.devservices.port=31222
%dev,test.camel.component.infinispan.username=admin
%dev,test.camel.component.infinispan.password=password
%dev,test.camel.component.infinispan.secure=true
%dev,test.camel.component.infinispan.hosts=localhost:31222

# Example prod mode configuration
%prod.camel.component.infinispan.username=prod-user
%prod.camel.component.infinispan.password=prod-password
%prod.camel.component.infinispan.secure=true
%prod.camel.component.infinispan.hosts=infinispan.prod:11222
```

### Quarkus Infinispan configuration

When using the [Quarkus Infinispan extension configuration properties](https://quarkus.io/guides/infinispan-client#configuration-reference), the Quarkus Infinispan extensions creates and manages a `RemoteCacheManager` bean.

The bean will get automatically autowired into the Camel Infinispan component on application startup.

Note that to materialize the `RemoteCacheManager` beans, you **must** add injection points for them. For example:

```java
public class Routes extends RouteBuilder {
    // Injects the default unnamed RemoteCacheManager
    @Inject
    RemoteCacheManager cacheManager;

    // If configured, injects an optional named RemoteCacheManager
    @Inject
    @InfinispanClientName("myNamedClient")
    RemoteCacheManager namedCacheManager;

    @Override
    public void configure() {
        // Route configuration here...
    }
}
```

## Additional Camel Quarkus configuration

### Camel Infinispan `InfinispanRemoteAggregationRepository` in native mode

If you chose to use the `InfinispanRemoteAggregationRepository` in native mode, then you must [enable native serialization support](core.html#quarkus-camel-native-reflection-serialization-enabled).