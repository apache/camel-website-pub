# camel-fhir-sink-kafka-connector sink configuration

Connector Description: Forward data to a FHIR endpoint.

When using camel-fhir-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-fhir-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.fhirsink.CamelFhirsinkSinkConnector
```

The camel-fhir-sink sink connector supports 15 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.fhir-sink.apiName** | What kind of operation to perform. |  | MEDIUM |
| **camel.kamelet.fhir-sink.methodName** | **Required** What sub operation to use for the selected operation. |  | HIGH |
| **camel.kamelet.fhir-sink.encoding** | Encoding to use for all request. One of: \[JSON\] \[XML\]. | "JSON" | MEDIUM |
| **camel.kamelet.fhir-sink.fhirVersion** | The FHIR Version to use. | "R4" | MEDIUM |
| **camel.kamelet.fhir-sink.log** | Will log every requests and responses. | false | MEDIUM |
| **camel.kamelet.fhir-sink.prettyPrint** | Pretty print all request. | false | MEDIUM |
| **camel.kamelet.fhir-sink.serverUrl** | **Required** The FHIR server base URL. |  | HIGH |
| **camel.kamelet.fhir-sink.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.kamelet.fhir-sink.proxyHost** | The proxy host. |  | MEDIUM |
| **camel.kamelet.fhir-sink.proxyPassword** | The proxy password. |  | MEDIUM |
| **camel.kamelet.fhir-sink.proxyPort** | The proxy port. |  | MEDIUM |
| **camel.kamelet.fhir-sink.proxyUser** | The proxy username. |  | MEDIUM |
| **camel.kamelet.fhir-sink.accessToken** | OAuth access token. |  | MEDIUM |
| **camel.kamelet.fhir-sink.username** | Username to use for basic authentication. |  | MEDIUM |
| **camel.kamelet.fhir-sink.password** | Password to use for basic authentication. |  | MEDIUM |

The camel-fhir-sink sink connector has no converters out of the box.

The camel-fhir-sink sink connector has no transforms out of the box.

The camel-fhir-sink sink connector has no aggregation strategies out of the box.