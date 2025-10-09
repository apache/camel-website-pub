# camel-http-source-kafka-connector source configuration

Connector Description: Periodically fetches an HTTP resource and provides the content as output.

When using camel-http-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-http-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.httpsource.CamelHttpsourceSourceConnector
```

The camel-http-source source connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.http-source.period** | The interval between fetches in milliseconds. | 10000 | MEDIUM |
| **camel.kamelet.http-source.contentType** | The content type accepted for the resource. | "application/json" | MEDIUM |
| **camel.kamelet.http-source.url** | **Required** The URL to fetch for data. Example: [https://gist.githubusercontent.com/nicolaferraro/e3c72ace3c751f9f88273896611ce5fe/raw/3b6f54060bacb56b6719b7386a4645cb59ad6cc1/quote.json](https://gist.githubusercontent.com/nicolaferraro/e3c72ace3c751f9f88273896611ce5fe/raw/3b6f54060bacb56b6719b7386a4645cb59ad6cc1/quote.json). |  | HIGH |

The camel-http-source source connector has no converters out of the box.

The camel-http-source source connector has no transforms out of the box.

The camel-http-source source connector has no aggregation strategies out of the box.