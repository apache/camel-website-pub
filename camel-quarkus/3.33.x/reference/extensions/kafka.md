# Kafka

JVM since1.0.0 Native since1.0.0

Send and receive messages to/from an Apache Kafka broker.

## What’s inside

-   [Kafka component](../../../../components/4.18.x/kafka-component.md), URI syntax: `kafka:topic`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-kafka)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-kafka</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Quarkus Kafka Dev Services

Camel Quarkus Kafka can take advantage of [Quarkus Kafka Dev services](https://quarkus.io/guides/kafka-dev-services) to simplify development and testing with a local containerized Kafka broker.

Kafka Dev Services is enabled by default in dev & test mode. The Camel Kafka component is automatically configured so that the `brokers` component option is set to point at the local containerized Kafka broker. Meaning that there’s no need to configure this option yourself.

This functionality can be disabled with the configuration property `quarkus.kafka.devservices.enabled=false`.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.kafka.kubernetes-service-binding.merge-configuration](#quarkus-camel-kafka-kubernetes-service-binding-merge-configuration)`
If `true` then any Kafka configuration properties discovered by the Quarkus Kubernetes Service Binding extension (if configured) will be merged with those set via Camel Kafka component or endpoint options. If `false` then any Kafka configuration properties discovered by the Quarkus Kubernetes Service Binding extension are ignored, and all of the Kafka component configuration is driven by Camel.

 | `boolean` | `true` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.