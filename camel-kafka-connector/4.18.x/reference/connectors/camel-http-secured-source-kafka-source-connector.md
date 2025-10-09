# camel-http-secured-source-kafka-connector source configuration

Connector Description: Periodically fetches a secured HTTP resource and provides the content as output. Supports Oauth and Basic authentication.

When using camel-http-secured-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-http-secured-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.httpsecuredsource.CamelHttpsecuredsourceSourceConnector
```

The camel-http-secured-source source connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.http-secured-source.period** | The interval between fetches in milliseconds. | 10000 | MEDIUM |
| **camel.kamelet.http-secured-source.contentType** | The content type accepted for the resource. | "application/json" | MEDIUM |
| **camel.kamelet.http-secured-source.url** | **Required** The URL to fetch for data Example: [https://gist.githubusercontent.com/nicolaferraro/e3c72ace3c751f9f88273896611ce5fe/raw/3b6f54060bacb56b6719b7386a4645cb59ad6cc1/quote.json](https://gist.githubusercontent.com/nicolaferraro/e3c72ace3c751f9f88273896611ce5fe/raw/3b6f54060bacb56b6719b7386a4645cb59ad6cc1/quote.json). |  | HIGH |
| **camel.kamelet.http-secured-source.authMethod** | Authentication methods allowed to use as a comma separated list of values Basic, Digest or NTLM. |  | MEDIUM |
| **camel.kamelet.http-secured-source.authenticationPreemptive** | If this option is true, camel-http sends preemptive basic authentication to the server. | false | MEDIUM |
| **camel.kamelet.http-secured-source.authUsername** | Authentication username. |  | MEDIUM |
| **camel.kamelet.http-secured-source.authPassword** | Authentication password. |  | MEDIUM |
| **camel.kamelet.http-secured-source.oauth2ClientId** | Oauth2 Client Id. |  | MEDIUM |
| **camel.kamelet.http-secured-source.oauth2ClientSecret** | Oauth2 Client Secret. |  | MEDIUM |
| **camel.kamelet.http-secured-source.oauth2TokenEndpoint** | Oauth2 Token Endpoint. |  | MEDIUM |
| **camel.kamelet.http-secured-source.oauth2Scope** | Oauth2 Scope. |  | MEDIUM |

The camel-http-secured-source source connector has no converters out of the box.

The camel-http-secured-source source connector has no transforms out of the box.

The camel-http-secured-source source connector has no aggregation strategies out of the box.