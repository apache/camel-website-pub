# Data Formats

A Camel [data format](../../../manual/data-format.md) converts a message body between a serialized form, such as JSON, CSV, HL7 or syslog text, and another representation, usually Java objects. To _marshal_ is to write the body in the serialized form, to _unmarshal_ is to parse the serialized form.

Every connector, Kamelet-based or component-based, can apply a data format to the body of each message it moves, with configuration only.

> **Note**
> A data format is not a Kafka Connect converter. The `key.converter` and `value.converter` of a connector translate between the bytes stored in Kafka and the Kafka Connect record. A data format works on the Camel message body inside the connector: on a sink connector it runs after the converter and the SMTs have produced the record value, on a source connector it runs before the SMTs and the converter.

## Options

 
| Name | Description |
| --- | --- |
| camel.sink.marshal | The data format used to marshal the record value before it is sent to the destination. |
| camel.sink.unmarshal | The data format used to unmarshal the record value before it is sent to the destination. |
| camel.source.marshal | The data format used to marshal the data received from the source before it is written to the topic. |
| camel.source.unmarshal | The data format used to unmarshal the data received from the source before it is written to the topic. |

The value is the name of a data format, for example `jackson` (see [Data format names](#DataFormats-Names)), or the name of a data format bean (see [Configuring the data format](#DataFormats-Configuring)). None of these options is set by default, except in `camel-syslog-kafka-connector`, which sets `camel.source.unmarshal=syslog` and `camel.sink.marshal=syslog`.

## Where the data formats run

Each connector task builds a single Camel route from its configuration. The data formats run at a fixed place in that route, together with the other optional stages; a stage that is not configured is left out.

On a sink connector:

1.  the record value becomes the message body, and by default the record headers starting with `CamelHeader.` or `CamelProperty.` become Camel headers or exchange properties (see [Message Level Headers](basic-configuration.html#BasicConfiguration-MessageLevelHeaders));
    
2.  `camel.remove.headers.pattern` removes the matching headers (see [Remove Headers](remove-headers.md));
    
3.  `camel.sink.marshal`;
    
4.  `camel.sink.unmarshal`;
    
5.  the aggregation, when `camel.beans.aggregate` is set (see [Aggregation](aggregation.md));
    
6.  the idempotent consumer, when `camel.idempotency.enabled=true` (see [Idempotency](idempotency.md));
    
7.  the message is sent to the destination.
    

On a source connector:

1.  the message is received from the source;
    
2.  `camel.source.marshal`;
    
3.  `camel.source.unmarshal`;
    
4.  the aggregation, when `camel.beans.aggregate` is set;
    
5.  the idempotent consumer, when `camel.idempotency.enabled=true`;
    
6.  `camel.remove.headers.pattern` removes the matching headers;
    
7.  the message body becomes the record value, and by default the headers become record headers.
    

As a consequence:

-   when both options of a connector are set, marshal always runs before unmarshal, in both directions;
    
-   the aggregation strategy and the idempotency expression (`camel.idempotency.expression.type=body`) see the body produced by the data formats, not the original one;
    
-   on a sink connector the headers removed by `camel.remove.headers.pattern` never reach the data formats, while on a source connector the data formats still see every header.
    

If a data format cannot process a body, for example `camel.sink.unmarshal=jackson` on a record value that is not JSON, the message fails like any other delivery error.

## Data format names

The value is the name Camel 4 registers the data format under, not the name of its Maven artifact. Some common ones:

  
| Data format | Name | Artifact |
| --- | --- | --- |
| JSON (Jackson) | `jackson` | `camel-jackson` |
| XML (Jackson) | `jacksonXml` | `camel-jacksonxml` |
| Avro (Jackson) | `avroJackson` | `camel-jackson-avro` |
| Protobuf (Jackson) | `protobufJackson` | `camel-jackson-protobuf` |
| JSON (Gson) | `gson` | `camel-gson` |
| Avro | `avro` | `camel-avro` |
| CSV | `csv` | `camel-csv` |
| Base64 | `base64` | `camel-base64` |
| HL7 | `hl7` | `camel-hl7` |
| Syslog | `syslog` | `camel-syslog` |
| YAML (SnakeYAML) | `snakeYaml` | `camel-snakeyaml` |
| Zip file | `zipFile` | `camel-zipfile` |
| GZip deflater | `gzipDeflater` | `camel-zip-deflater` |
| JAXB | `jaxb` | `camel-jaxb` |

The Jackson 3 modules (`camel-jackson3`, `camel-jackson3xml`, `camel-jackson3-avro` and `camel-jackson3-protobuf`) register the same names as their Jackson 2 counterparts.

Older configurations can carry names that no longer exist: the JSON Jackson data format, for example, is `jackson`, while Camel 3.14 and earlier registered it as `json-jackson`. An unknown name makes the connector task fail to start with `Cannot find data format in registry with ref: <name>`.

The [Camel data formats](../../../components/4.22.x/dataformats/index.md) page lists every data format with its options.

## Making the data format available

The core `camel-kafka-connector` jar and its dependencies include no data format. The data format you name must be on the classpath of the connector: its jar, and the jars it depends on, built for the Camel version of the connector, have to be in the connector’s directory under the Kafka Connect `plugin.path`.

Some connectors include a data format already. The component-based connectors, such as `camel-file-kafka-connector`, `camel-https-kafka-connector` or `camel-jdbc-kafka-connector`, and many Kamelet-based connectors, such as `camel-cassandra-sink-kafka-connector`, ship `camel-jackson`; `camel-syslog-kafka-connector` ships `camel-syslog`. Look for the jar of the data format, for example `camel-jackson-<version>.jar`, in the connector’s directory.

To add a data format to a connector, copy its jars into the connector’s directory, or build an extended connector package with the [Extensible Dataformat connector archetype](extending-connector/archetype-dataformat-connector.md), which adds the data format as a dependency of the connector.

## Configuring the data format

Set the data format options with `camel.dataformat.<name>.<option>` properties, where `<name>` is the data format name and `<option>` one of the options listed on its page in the Camel documentation:

```properties
camel.sink.marshal=jackson
camel.dataformat.jackson.prettyPrint=true
```

These properties configure the single instance Camel creates for that name, which every marshal or unmarshal option naming it uses. A `camel.dataformat.<name>.*` property makes the task fail to start when the data format `<name>` is not on the classpath, even when no marshal or unmarshal option uses it.

To configure an instance under a name of your choice, for example to marshal and unmarshal with different settings, declare the data format as a bean and use the bean name as the option value:

```properties
camel.beans.prettyJson=#class:org.apache.camel.component.jackson.JacksonDataFormat
camel.beans.prettyJson.prettyPrint=true
camel.sink.marshal=prettyJson
```

`#class:` creates a new instance of the class, and the `camel.beans.<name>.<property>` entries set its properties; see the Camel [property binding](../../../manual/property-binding.md) documentation for the syntax.

Some data formats can let a message header choose the Java type to unmarshal to, for example Jackson with `allowUnmarshallType=true` (the `CamelJacksonUnmarshalType` header) or `allowJmsType=true` (the `JMSType` header). Both options are disabled by default. On a sink connector a record header `CamelHeader.<name>` becomes the Camel header `<name>`, so keep these options disabled when the topic is written by producers you do not trust, or remove those headers with `camel.remove.headers.pattern` (see the [Security Model](../security-model.md)).

## Marshalling on a source connector

The output of `camel.source.marshal` becomes the record value as a `byte[]`. Use the `ByteArrayConverter` to write it to the topic unchanged:

```properties
camel.source.marshal=jackson
value.converter=org.apache.kafka.connect.converters.ByteArrayConverter
```

The Kafka `StringConverter` writes a `byte[]` value as a Java object reference (`[B@…​`). To get a string value, for example for JSON, convert the value before the converter runs with the `CamelTypeConverterTransform` SMT that every connector includes:

```properties
camel.source.marshal=jackson
transforms=toString
transforms.toString.type=org.apache.camel.kafkaconnector.transforms.CamelTypeConverterTransform$Value
transforms.toString.target.type=java.lang.String
value.converter=org.apache.kafka.connect.storage.StringConverter
```

## Example

This sink connector writes each record of the `orders` topic, which holds JSON objects, to its own file as indented JSON. The `JsonConverter` without schemas turns each record value into a `java.util.Map`, and `camel.sink.marshal` writes it back as JSON. `camel-file-kafka-connector` already ships `camel-jackson`.

```properties
name=orders-to-files
connector.class=org.apache.camel.kafkaconnector.file.CamelFileSinkConnector
tasks.max=1
topics=orders

key.converter=org.apache.kafka.connect.storage.StringConverter
value.converter=org.apache.kafka.connect.json.JsonConverter
value.converter.schemas.enable=false

camel.sink.path.directoryName=/tmp/orders
camel.sink.marshal=jackson
camel.dataformat.jackson.prettyPrint=true
```