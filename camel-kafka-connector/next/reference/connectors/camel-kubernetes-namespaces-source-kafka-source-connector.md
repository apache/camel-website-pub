# camel-kubernetes-namespaces-source-kafka-connector source configuration

Connector Description: Consume Events from Kubernetes Namespaces

When using camel-kubernetes-namespaces-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kubernetes-namespaces-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kubernetesnamespacessource.CamelKubernetesnamespacessourceSourceConnector
```

The camel-kubernetes-namespaces-source source connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kubernetes-namespaces-source.token** | **Required** The Auth Token to connect to Kubernetes Cluster. |  | HIGH |
| **camel.kamelet.kubernetes-namespaces-source.masterUrl** | **Required** The Kubernetes Cluster Master URL. |  | HIGH |

The camel-kubernetes-namespaces-source source connector has no converters out of the box.

The camel-kubernetes-namespaces-source source connector has no transforms out of the box.

The camel-kubernetes-namespaces-source source connector has no aggregation strategies out of the box.