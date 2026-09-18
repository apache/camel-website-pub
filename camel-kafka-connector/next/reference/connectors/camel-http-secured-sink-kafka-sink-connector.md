# camel-http-secured-sink-kafka-connector sink configuration

Connector Description: Forwards an event to a secured HTTP endpoint. Supports Oauth and Basic authentication.

When using camel-http-secured-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-http-secured-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.httpsecuredsink.CamelHttpsecuredsinkSinkConnector
```

The camel-http-secured-sink sink connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.http-secured-sink.url** | **Required** The URL to send data to Example: [https://my-service/path](https://my-service/path). |  | HIGH |
| **camel.kamelet.http-secured-sink.method** | The HTTP method to use. | "POST" | MEDIUM |
| **camel.kamelet.http-secured-sink.authMethod** | Authentication methods allowed to use as a comma separated list of values Basic, Digest or NTLM. |  | MEDIUM |
| **camel.kamelet.http-secured-sink.authenticationPreemptive** | If this option is true, camel-http sends preemptive basic authentication to the server. | false | MEDIUM |
| **camel.kamelet.http-secured-sink.authUsername** | Authentication username. |  | MEDIUM |
| **camel.kamelet.http-secured-sink.authPassword** | Authentication password. |  | MEDIUM |
| **camel.kamelet.http-secured-sink.oauth2ClientId** | Oauth2 Client Id. |  | MEDIUM |
| **camel.kamelet.http-secured-sink.oauth2ClientSecret** | Oauth2 Client Secret. |  | MEDIUM |
| **camel.kamelet.http-secured-sink.oauth2TokenEndpoint** | Oauth2 Token Endpoint. |  | MEDIUM |
| **camel.kamelet.http-secured-sink.oauth2Scope** | Oauth2 Scope. |  | MEDIUM |

The camel-http-secured-sink sink connector has no converters out of the box.

The camel-http-secured-sink sink connector has no transforms out of the box.

The camel-http-secured-sink sink connector has no aggregation strategies out of the box.