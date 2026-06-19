# Hazelcast

**Since Camel 2.7**

The **hazelcast-** component allows you to work with the [Hazelcast](http://www.hazelcast.com) distributed data grid / cache. Hazelcast is an in-memory data grid, entirely written in Java (single jar). It offers a great palette of different data stores like map, multimap (same key, n values), queue, list and atomic number. The main reason to use Hazelcast is its simple cluster support. If you have enabled multicast on your network, you can run a cluster with a hundred nodes with no extra configuration. Hazelcast can simply configure to add additional features like n copies between nodes (default is 1), cache persistence, network configuration (if needed), near cache, eviction, and so on. For more information, consult the Hazelcast documentation on [http://www.hazelcast.com/docs.jsp](http://www.hazelcast.com/docs.jsp).

## Hazelcast components

See the following for usage of each component:

[Hazelcast Atomic Number](hazelcast-atomicvalue-component.md)

Increment, decrement, set, etc. Hazelcast atomic number (a grid wide number).

[Hazelcast Instance](hazelcast-instance-component.md)

Consume join/leave events of a cache instance in a Hazelcast cluster.

[Hazelcast List](hazelcast-list-component.md)

Perform operations on Hazelcast distributed list.

[Hazelcast Map](hazelcast-map-component.md)

Perform operations on Hazelcast distributed map.

[Hazelcast Multimap](hazelcast-multimap-component.md)

Perform operations on Hazelcast distributed multimap.

[Hazelcast PN Counter](hazelcast-pncounter-component.md)

Increment, decrement, get, etc. operations on a Hazelcast PN Counter (CRDT counter).

[Hazelcast Queue](hazelcast-queue-component.md)

Perform operations on Hazelcast distributed queue.

[Hazelcast Replicated Map](hazelcast-replicatedmap-component.md)

Perform operations on Hazelcast replicated map.

[Hazelcast Ringbuffer](hazelcast-ringbuffer-component.md)

Perform operations on Hazelcast distributed ringbuffer.

[Hazelcast SEDA](hazelcast-seda-component.md)

Asynchronously send/receive Exchanges between Camel routes running on potentially distinct JVMs/hosts backed by Hazelcast BlockingQueue.

[Hazelcast Set](hazelcast-set-component.md)

Perform operations on Hazelcast distributed set.

[Hazelcast Topic](hazelcast-topic-component.md)

Send and receive messages to/from Hazelcast distributed topic.

## Installation

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-hazelcast</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Using hazelcast reference

### By its name

_XML-only: Spring bean configuration with Hazelcast instance by name_

```xml
<bean id="hazelcastLifecycle" class="com.hazelcast.core.LifecycleService"
      factory-bean="hazelcastInstance" factory-method="getLifecycleService"
      destroy-method="shutdown" />

<bean id="config" class="com.hazelcast.config.Config">
    <constructor-arg type="java.lang.String" value="HZ.INSTANCE" />
</bean>

<bean id="hazelcastInstance" class="com.hazelcast.core.Hazelcast" factory-method="newHazelcastInstance">
    <constructor-arg type="com.hazelcast.config.Config" ref="config"/>
</bean>
<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route id="testHazelcastInstanceBeanRefPut">
        <from uri="direct:testHazelcastInstanceBeanRefPut"/>
        <setHeader name="CamelHazelcastOperationType">
            <constant>put</constant>
        </setHeader>
        <to uri="hazelcast-map:testmap?hazelcastInstanceName=HZ.INSTANCE"/>
    </route>

    <route id="testHazelcastInstanceBeanRefGet">
        <from uri="direct:testHazelcastInstanceBeanRefGet" />
        <setHeader name="CamelHazelcastOperationType">
            <constant>get</constant>
        </setHeader>
        <to uri="hazelcast-map:testmap?hazelcastInstanceName=HZ.INSTANCE"/>
        <to uri="seda:out" />
    </route>
</camelContext>
```

### By instance

_XML-only: Spring bean configuration with Hazelcast instance by reference_

```xml
<bean id="hazelcastInstance" class="com.hazelcast.core.Hazelcast"
      factory-method="newHazelcastInstance" />
<bean id="hazelcastLifecycle" class="com.hazelcast.core.LifecycleService"
      factory-bean="hazelcastInstance" factory-method="getLifecycleService"
      destroy-method="shutdown" />

<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route id="testHazelcastInstanceBeanRefPut">
        <from uri="direct:testHazelcastInstanceBeanRefPut"/>
        <setHeader name="CamelHazelcastOperationType">
            <constant>put</constant>
        </setHeader>
        <to uri="hazelcast-map:testmap?hazelcastInstance=#hazelcastInstance"/>
    </route>

    <route id="testHazelcastInstanceBeanRefGet">
        <from uri="direct:testHazelcastInstanceBeanRefGet" />
        <setHeader name="CamelHazelcastOperationType">
            <constant>get</constant>
        </setHeader>
        <to uri="hazelcast-map:testmap?hazelcastInstance=#hazelcastInstance"/>
        <to uri="seda:out" />
    </route>
</camelContext>
```

### Configuring HazelcastInstance on component

You can also configure the hazelcast instance on the component which will then be used by all hazelcast endpoints. In the example above we set up this for the hazelcast map component and setup hazelcast via verbose `<bean>` configurations.

```xml
<bean id="config" class="com.hazelcast.config.Config">
    <constructor-arg type="java.lang.String" value="HZ.INSTANCE" />
    <property name="networkConfig" ref="myNetworkConfig"/>
</bean>

<bean id="myNetworkConfig" class="com.hazelcast.config.NetworkConfig">
  <property name="port">1234</property>
</bean>

<bean id="myHazelcastInstance" class="com.hazelcast.core.Hazelcast" factory-method="newHazelcastInstance">
    <constructor-arg type="com.hazelcast.config.Config" ref="config"/>
</bean>

<bean id="hazelcast" class="org.apache.camel.component.hazelcast.map.HazelcastMapComponent">
  <property name="hazelcastInstance" ref="myHazelcastInstance"/>
</bean>
```