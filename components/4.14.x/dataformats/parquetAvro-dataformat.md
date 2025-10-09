# Parquet File

**Since Camel 4.0**

The ParquetAvro Data Format is a Camel Framework’s data format implementation based on the parquet-avro library for (de)/serialization purposes. Messages can be unmarshalled to Avro’s GenericRecords or plain Java objects (POJOs). With the help of Camel’s routing engine and data transformations, you can then play with them and apply customised formatting and call other Camel Components to convert and send messages to upstream systems.

## Parquet Data Format Options

The Parquet File dataformat supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **compressionCodecName** (common) | `GZIP` | `Enum` | 
Compression codec to use when marshalling.

Enum values:

-   UNCOMPRESSED
    
-   SNAPPY
    
-   GZIP
    
-   LZO
    
-   BROTLI
    
-   LZ4
    
-   ZSTD
    
-   LZ4\_RAW
    





 |
| **unmarshalType** (common) |  | `String` | Class to use when (un)marshalling. If omitted, parquet files are converted into Avro’s GenericRecords for unmarshalling and input objects are assumed as GenericRecords for marshalling. |
| **lazyLoad** (common) | `false` | `Boolean` | Whether the unmarshalling should produce an iterator of records or read all the records at once. |

## Unmarshal

There are ways to unmarshal parquet files/structures, usually binary parquet files, where camel DSL allows.

In this first example we unmarshal file payload to OutputStream and send it to mock endpoint, then we will be able to get GenericRecord or POJO (it could be a list if that is coming through)

```java
from("direct:unmarshal").unmarshal(parquet).to("mock:unmarshal");
```

## Marshal

Marshalling is the reverse process of unmarshalling, so when you have your `GenericRecord` or POJO and marshal it, you will get the parquet-formatted output stream on your producer endpoint.

```java
from("direct:marshal").marshal(parquet).to("mock:marshal");
```

## Dependencies

To use parquet-avro data format in your camel routes you need to add a dependency on **camel-parquet-avro** which implements this data format.

If you use Maven you can add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-parquet-avro</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using parquetAvro with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-parquet-avro-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.parquet-avro.compression-codec-name** | Compression codec to use when marshalling. | GZIP | String |
| **camel.dataformat.parquet-avro.enabled** | Whether to enable auto configuration of the parquetAvro data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.parquet-avro.lazy-load** | Whether the unmarshalling should produce an iterator of records or read all the records at once. | false | Boolean |
| **camel.dataformat.parquet-avro.unmarshal-type** | Class to use when (un)marshalling. If omitted, parquet files are converted into Avro’s GenericRecords for unmarshalling and input objects are assumed as GenericRecords for marshalling. |  | String |