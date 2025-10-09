# camel-dropbox-source-kafka-connector source configuration

Connector Description: Consume Files from Dropbox.

When using camel-dropbox-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-dropbox-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.dropboxsource.CamelDropboxsourceSourceConnector
```

The camel-dropbox-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.dropbox-source.period** | **Required** The interval between fetches to the Dropbox remote path in milliseconds. | 10000 | HIGH |
| **camel.kamelet.dropbox-source.accessToken** | **Required** The access Token to use to access Dropbox. |  | HIGH |
| **camel.kamelet.dropbox-source.clientIdentifier** | **Required** Dropbox App client Identifier. |  | HIGH |
| **camel.kamelet.dropbox-source.remotePath** | **Required** Original file or folder to work with. |  | HIGH |
| **camel.kamelet.dropbox-source.query** | **Required** A space-separated list of sub-strings to search for. A file matches only if it contains all the sub-strings. If this option is not set, all files is matched. |  | HIGH |

The camel-dropbox-source source connector has no converters out of the box.

The camel-dropbox-source source connector has no transforms out of the box.

The camel-dropbox-source source connector has no aggregation strategies out of the box.