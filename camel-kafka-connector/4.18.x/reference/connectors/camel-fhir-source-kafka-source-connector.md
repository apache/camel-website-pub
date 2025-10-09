# camel-fhir-source-kafka-connector source configuration

Connector Description: Receive data from FHIR server.

When using camel-fhir-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-fhir-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.fhirsource.CamelFhirsourceSourceConnector
```

The camel-fhir-source source connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.fhir-source.serverUrl** | **Required** The FHIR server url. |  | HIGH |
| **camel.kamelet.fhir-source.url** | The FHIR resource type url. | "/Patient" | MEDIUM |
| **camel.kamelet.fhir-source.encoding** | Encoding to use for all request. | "JSON" | MEDIUM |
| **camel.kamelet.fhir-source.fhirVersion** | The FHIR Version to use. | "R4" | MEDIUM |
| **camel.kamelet.fhir-source.username** | **Required** The username to access the FHIR server. |  | HIGH |
| **camel.kamelet.fhir-source.password** | **Required** The password to access the FHIR server. |  | HIGH |
| **camel.kamelet.fhir-source.prettyPrint** | Define if the Json must be pretty print or not. | true | MEDIUM |

The camel-fhir-source source connector has no converters out of the box.

The camel-fhir-source source connector has no transforms out of the box.

The camel-fhir-source source connector has no aggregation strategies out of the box.