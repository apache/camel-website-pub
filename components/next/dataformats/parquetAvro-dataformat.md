# Parquet File

**Since Camel 4.0**

The ParquetAvro Data Format is a Camel Framework’s data format implementation based on the parquet-avro library for (de)/serialization purposes. Messages can be unmarshalled to Avro’s GenericRecords or plain Java objects (POJOs). With the help of Camel’s routing engine and data transformations, you can then play with them and apply customised formatting and call other Camel Components to convert and send messages to upstream systems.

> **Note**
> This component does not support JDK 22 or later due to a Hadoop incompatibility ([HADOOP-19486](https://issues.apache.org/jira/browse/HADOOP-19486)). Hadoop relies on the deprecated `javax.security.auth.Subject.getSubject()` method, which was removed in JDK 22 (JEP 411). This limitation will be resolved once an updated Hadoop version with a fix is available.

## Parquet Data Format Options

The Parquet File dataformat supports the following options which are listed below.

   
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
| **unmarshalType** (common) |  | `String` | Class to use when (un)marshalling. If omitted, parquet files are converted into Avro GenericRecords for unmarshalling and input objects are assumed as GenericRecords for marshalling. |
| **lazyLoad** (common) | `false` | `Boolean` | Whether the unmarshalling should produce an iterator of records or read all the records at once. |

## Message Body

The message body at each side of the Parquet File data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `list` | A List of Avro GenericRecords, or of objects of the class unmarshalType names. A single record fails, and so does an empty List without unmarshalType. |
| **Marshal output** | `stream`, as binary | The Parquet file in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `bytes`, `stream` or `file`, as binary | A Parquet file, which is read into memory. |
| **Unmarshal output** | `list` | 
A List (ArrayList) of the records: GenericRecords, or objects of the class unmarshalType names. With lazyLoad, an Iterator of them for the split EIP.

-   With `lazyLoad=true`: `iterator`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Unmarshal

There are ways to unmarshal parquet files/structures, usually binary parquet files, where camel DSL allows.

In this first example we unmarshal file payload to a List of the records and send it to mock endpoint: GenericRecords, or POJOs with `unmarshalType`. With `lazyLoad`, the body is an Iterator of them instead.

-   Java
    
-   YAML
    

```java
from("direct:unmarshal").unmarshal(parquet).to("mock:unmarshal");
```

```yaml
- route:
    from:
      uri: direct:unmarshal
      steps:
        - unmarshal:
            parquetAvro:
              unmarshalType: com.example.Order
        - to:
            uri: mock:unmarshal
```

With `unmarshalType`, the records are objects of that class. Without it, they are `GenericRecord` objects.

## Marshal

Marshalling is the reverse process of unmarshalling, so when you have a List of `GenericRecord` objects or POJOs and marshal it, you will get the parquet-formatted output stream on your producer endpoint. A single record that is not in a List fails.

-   Java
    
-   YAML
    

```java
from("direct:marshal").marshal(parquet).to("mock:marshal");
```

```yaml
- route:
    from:
      uri: direct:marshal
      steps:
        - marshal:
            parquetAvro:
              unmarshalType: com.example.Order
        - to:
            uri: mock:marshal
```

To marshal POJOs, set `unmarshalType` on marshal as well: the data format makes the parquet schema from that class. A `GenericRecord` has its own schema.

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