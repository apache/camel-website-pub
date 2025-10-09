# camel-dropbox-sink-kafka-connector sink configuration

Connector Description: Upload Files to Dropbox.

When using camel-dropbox-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-dropbox-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.dropboxsink.CamelDropboxsinkSinkConnector
```

The camel-dropbox-sink sink connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.dropbox-sink.accessToken** | **Required** The access Token to use to access Dropbox. |  | HIGH |
| **camel.kamelet.dropbox-sink.clientIdentifier** | **Required** Dropbox App client Identifier. |  | HIGH |
| **camel.kamelet.dropbox-sink.remotePath** | **Required** Original file or folder to work with. |  | HIGH |
| **camel.kamelet.dropbox-sink.uploadMode** | **Required** The uploading mode in case a file with the same name exists on Dropbox. Choose `add` or `force`. With `add`, the new file is renamed. With `force`, the existing file is overwritten. | "add" | HIGH |

The camel-dropbox-sink sink connector has no converters out of the box.

The camel-dropbox-sink sink connector has no transforms out of the box.

The camel-dropbox-sink sink connector has no aggregation strategies out of the box.