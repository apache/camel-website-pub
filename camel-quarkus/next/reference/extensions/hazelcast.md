# Hazelcast Atomic Number

JVM since1.1.0 Native since1.6.0 ⚠️Deprecated

Increment, decrement, set, etc. Hazelcast atomic number (a grid wide number).

## What’s inside

-   [Hazelcast Atomic Number component](../../../../components/4.22.x/hazelcast-atomicvalue-component.md), URI syntax: `hazelcast-atomicvalue:cacheName`
    
-   [Hazelcast Instance component](../../../../components/4.22.x/hazelcast-instance-component.md), URI syntax: `hazelcast-instance:cacheName`
    
-   [Hazelcast List component](../../../../components/4.22.x/hazelcast-list-component.md), URI syntax: `hazelcast-list:cacheName`
    
-   [Hazelcast Map component](../../../../components/4.22.x/hazelcast-map-component.md), URI syntax: `hazelcast-map:cacheName`
    
-   [Hazelcast Multimap component](../../../../components/4.22.x/hazelcast-multimap-component.md), URI syntax: `hazelcast-multimap:cacheName`
    
-   [Hazelcast PN Counter component](../../../../components/4.22.x/hazelcast-pncounter-component.md), URI syntax: `hazelcast-pncounter:cacheName`
    
-   [Hazelcast Queue component](../../../../components/4.22.x/hazelcast-queue-component.md), URI syntax: `hazelcast-queue:cacheName`
    
-   [Hazelcast Replicated Map component](../../../../components/4.22.x/hazelcast-replicatedmap-component.md), URI syntax: `hazelcast-replicatedmap:cacheName`
    
-   [Hazelcast Ringbuffer component](../../../../components/4.22.x/hazelcast-ringbuffer-component.md), URI syntax: `hazelcast-ringbuffer:cacheName`
    
-   [Hazelcast SEDA component](../../../../components/4.22.x/hazelcast-seda-component.md), URI syntax: `hazelcast-seda:cacheName`
    
-   [Hazelcast Set component](../../../../components/4.22.x/hazelcast-set-component.md), URI syntax: `hazelcast-set:cacheName`
    
-   [Hazelcast Topic component](../../../../components/4.22.x/hazelcast-topic-component.md), URI syntax: `hazelcast-topic:cacheName`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-hazelcast)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-hazelcast</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).

## Additional Camel Quarkus configuration

This extension leverages [Hazelcast Client for Quarkus](https://github.com/hazelcast/quarkus-hazelcast-client). The configuration of the HazelcastInstance is managed by the extension. To configure Hazelcast Instance, check the [Hazelcast Client for Quarkus](https://github.com/hazelcast/quarkus-hazelcast-client) guide.

> **Important**
> `camel-quarkus-hazelcast` works only in client mode.

To use the `HazelcastInstance` bean in the Hazelcast component, you should configure the component as follows.

```java
    (1)
    @Inject
    HazelcastInstance hazelcastInstance;

    @Produces
    @ApplicationScoped
    @Unremovable
    @Named("hazelcast-map")
    HazelcastDefaultComponent hazelcastMap() {
        final HazelcastMapComponent hazelcastComponent = new HazelcastMapComponent();
        hazelcastComponent.setHazelcastInstance(hazelcastInstance);
        (2)
        hazelcastComponent.setHazelcastMode(HazelcastConstants.HAZELCAST_CLIENT_MODE);
        return getHazelcastComponent(hazelcastComponent);
    }
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>The <code>HazelcastInstance</code> bean instance created by the <code>quarkus-hazelcast</code> extension</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>The Hazelcast mode must be set to client mode</td></tr></tbody></table>

Some more examples can be found in the Camel Quarkus Hazelcast [integration tests](https://github.com/apache/camel-quarkus/tree/main/integration-tests/hazelcast).