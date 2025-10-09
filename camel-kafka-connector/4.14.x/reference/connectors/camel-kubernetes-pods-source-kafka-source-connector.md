# camel-kubernetes-pods-source-kafka-connector source configuration

Connector Description: Consume Events from Kubernetes Pods

When using camel-kubernetes-pods-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kubernetes-pods-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kubernetespodssource.CamelKubernetespodssourceSourceConnector
```

The camel-kubernetes-pods-source source connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kubernetes-pods-source.token** | **Required** The Auth Token to connect to Kubernetes Cluster. |  | HIGH |
| **camel.kamelet.kubernetes-pods-source.masterUrl** | **Required** The Kubernetes Cluster Master URL. |  | HIGH |
| **camel.kamelet.kubernetes-pods-source.resourceName** | The Resource Name we want to watch. |  | MEDIUM |

The camel-kubernetes-pods-source source connector has no converters out of the box.

The camel-kubernetes-pods-source source connector has no transforms out of the box.

The camel-kubernetes-pods-source source connector has no aggregation strategies out of the box.