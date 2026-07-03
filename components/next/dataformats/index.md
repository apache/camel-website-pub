# Data Formats Index

Index of Camel data formats.

# Data Formats

Below is the list of data formats that are provided by Apache Camel.

Number of Data Formats: 56 in 50 JAR artifacts (0 deprecated)

    
| Data Format | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [ASN.1 File](asn1-dataformat.md) | camel-asn1 | Stable | 2.20 | Encode and decode data structures using Abstract Syntax Notation One (ASN.1) |
| [Avro](avro-dataformat.md) | camel-avro | Stable | 2.14 | Serialize and deserialize messages using Apache Avro binary data format |
| [Avro Jackson 2](avroJackson2-dataformat.md) | camel-jackson-avro | Stable | 3.10 | Marshal POJOs to Avro and back using Jackson. |
| [Avro Jackson 3](avroJackson3-dataformat.md) | camel-jackson3-avro | Stable | 4.19 | Marshal POJOs to Avro and back using Jackson. |
| [Barcode](barcode-dataformat.md) | camel-barcode | Stable | 2.14 | Transform strings to various 1D/2D barcode bitmap formats and back |
| [Base64](base64-dataformat.md) | camel-base64 | Stable | 2.11 | Encode and decode data using Base64 |
| [BeanIO](beanio-dataformat.md) | camel-beanio | Stable | 2.10 | Marshal and unmarshal Java beans to and from flat files (such as CSV, delimited, or fixed length formats) |
| [Bindy](bindy-dataformat.md) | camel-bindy | Stable | 2.0 | Marshal and unmarshal between POJOs and key-value pair (KVP) format using Camel Bindy |
| [CBOR](cbor-dataformat.md) | camel-cbor | Stable | 3.0 | Unmarshal a CBOR payload to POJO and back |
| [Crypto (Java Cryptographic Extension)](crypto-dataformat.md) | camel-crypto | Stable | 2.3 | Encrypt and decrypt messages using Java Cryptography Extension (JCE) |
| [CSV](csv-dataformat.md) | camel-csv | Stable | 1.3 | Handle CSV (Comma Separated Values) payloads |
| [DFDL](dfdl-dataformat.md) | camel-dfdl | Stable | 4.11 | Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL) |
| [FHIR JSon](fhirJson-dataformat.md) | camel-fhir | Stable | 2.21 | Marshall and unmarshall FHIR objects to/from JSON |
| [FHIR XML](fhirXml-dataformat.md) | camel-fhir | Stable | 2.21 | Marshall and unmarshall FHIR objects to/from XML |
| [Flatpack](flatpack-dataformat.md) | camel-flatpack | Stable | 2.1 | Marshal and unmarshal Java lists and maps to/from flat files (such as CSV, delimited, or fixed length formats) using Flatpack library |
| [Fory](fory-dataformat.md) | camel-fory | Stable | 4.9 | Serialize and deserialize messages using Apache Fory |
| [Grok](grok-dataformat.md) | camel-grok | Stable | 3.0 | Unmarshal unstructured data to objects using Logstash based Grok patterns |
| [Groovy JSon](groovyJson-dataformat.md) | camel-groovy | Stable | 4.19 | Transform between JSon and java.util.Map or java.util.List objects |
| [Groovy XML](groovyXml-dataformat.md) | camel-groovy | Stable | 4.15 | Transform between XML and Groovy Node (Map structure) objects |
| [GZip Deflater](gzipDeflater-dataformat.md) | camel-zip-deflater | Stable | 2.0 | Compress and decompress messages using java.util.zip.GZIP\*Stream |
| [HL7](hl7-dataformat.md) | camel-hl7 | Stable | 2.0 | Marshal and unmarshal HL7 (Health Care) model objects using the HL7 MLLP codec |
| [iCal](ical-dataformat.md) | camel-ical | Stable | 2.12 | Marshal and unmarshal iCal (\*.ics) documents to/from model objects |
| [ISO-8583](iso8583-dataformat.md) | camel-iso8583 | Stable | 4.14 | Create, edit and read ISO-8583 messages |
| [Jackson XML 2](jacksonXml2-dataformat.md) | camel-jacksonxml | Stable | 2.16 | Unmarshal an XML payloads to POJOs and back using XMLMapper extension of Jackson |
| [Jackson XML 3](jacksonXml3-dataformat.md) | camel-jackson3xml | Stable | 4.19 | Unmarshal an XML payloads to POJOs and back using XMLMapper extension of Jackson |
| [JAXB](jaxb-dataformat.md) | camel-jaxb | Stable | 1.0 | Unmarshal XML payloads to POJOs and back using JAXB2 XML marshalling standard |
| [JSON Fastjson](fastjson-dataformat.md) | camel-fastjson | Stable | 2.20 | Marshal POJOs to JSON and back using Fastjson |
| [JSON Gson](gson-dataformat.md) | camel-gson | Stable | 2.10 | Marshal POJOs to JSON and back using Gson |
| [JSON Jackson 2](jackson2-dataformat.md) | camel-jackson | Stable | 2.0 | Marshal POJOs to JSON and back using Jackson. |
| [JSON Jackson 3](jackson3-dataformat.md) | camel-jackson3 | Stable | 4.19 | Marshal POJOs to JSON and back using Jackson. |
| [JSON JSON-B](jsonb-dataformat.md) | camel-jsonb | Stable | 3.7 | Marshal POJOs to JSON and back using JSON-B. |
| [JSonApi](jsonApi-dataformat.md) | camel-jsonapi | Stable | 3.0 | Marshal and unmarshal JSON:API resources using JSONAPI-Converter library |
| [LZF Deflate Compression](lzf-dataformat.md) | camel-lzf | Stable | 2.17 | Compress and decompress streams using LZF deflate algorithm |
| [MIME Multipart](mimeMultipart-dataformat.md) | camel-mail | Stable | 2.17 | Marshal Camel messages with attachments into MIME-Multipart messages and back |
| [OCSF](ocsf-dataformat.md) | camel-ocsf | Stable | 4.18 | Marshal and unmarshal OCSF (Open Cybersecurity Schema Framework) security events to/from JSON |
| [Parquet File](parquetAvro-dataformat.md) | camel-parquet-avro | Stable | 4.0 | Parquet Avro serialization and de-serialization |
| [PGP (Pretty Good Privacy Cryptographic)](pgp-dataformat.md) | camel-crypto-pgp | Stable | 2.9 | Encrypt and decrypt messages using Java Cryptographic Extension (JCE) and PGP |
| [PQC (Post-Quantum Cryptography)](pqc-dataformat.md) | camel-pqc | Stable | 4.16 | Encrypt and decrypt messages using Post-Quantum Cryptography Key Encapsulation Mechanisms (KEM) |
| [Protobuf](protobuf-dataformat.md) | camel-protobuf | Stable | 2.2 | Serialize and deserialize Java objects using Google’s Protocol buffers |
| [Protobuf Jackson 2](protobufJackson2-dataformat.md) | camel-jackson-protobuf | Stable | 3.10 | Marshal POJOs to Protobuf and back using Jackson. |
| [Protobuf Jackson 3](protobufJackson3-dataformat.md) | camel-jackson3-protobuf | Stable | 4.19 | Marshal POJOs to Protobuf and back using Jackson. |
| [RSS](rss-dataformat.md) | camel-rss | Stable | 2.1 | Transform from ROME SyndFeed Java Objects to XML and vice-versa |
| [Smooks](smooks-dataformat.md) | camel-smooks | Stable | 4.9 | Transform and bind XML as well as non-XML data, including EDI, CSV, JSON, and YAML using Smooks |
| [SOAP](soap-dataformat.md) | camel-soap | Stable | 2.3 | Marshal Java objects to SOAP messages and back |
| [SWIFT MT](swiftMt-dataformat.md) | camel-swift | Stable | 3.20 | Encode and decode SWIFT MT messages |
| [SWIFT MX](swiftMx-dataformat.md) | camel-swift | Stable | 3.20 | Encode and decode SWIFT MX messages |
| [Syslog](syslog-dataformat.md) | camel-syslog | Stable | 2.6 | Marshall SyslogMessages to RFC3164 and RFC5424 messages and back |
| [Tar File](tarFile-dataformat.md) | camel-tarfile | Stable | 2.16 | Archive files into tarballs or extract files from tarballs |
| [Thrift](thrift-dataformat.md) | camel-thrift | Stable | 2.20 | Serialize and deserialize messages using Apache Thrift binary data format |
| [uniVocity CSV](univocityCsv-dataformat.md) | camel-univocity-parsers | Stable | 2.15 | Marshal and unmarshal Java objects from and to CSV (Comma Separated Values) using UniVocity Parsers |
| [uniVocity Fixed Length](univocityFixed-dataformat.md) | camel-univocity-parsers | Stable | 2.15 | Marshal and unmarshal Java objects from and to fixed length records using UniVocity Parsers |
| [uniVocity TSV](univocityTsv-dataformat.md) | camel-univocity-parsers | Stable | 2.15 | Marshal and unmarshal Java objects from and to TSV (Tab-Separated Values) records using UniVocity Parsers |
| [XML Security](xmlSecurity-dataformat.md) | camel-xmlsecurity | Stable | 2.0 | Encrypt and decrypt XML payloads using Apache Santuario |
| [YAML SnakeYAML](snakeYaml-dataformat.md) | camel-snakeyaml | Stable | 2.17 | Marshal and unmarshal Java objects to and from YAML using SnakeYAML |
| [Zip Deflater](zipDeflater-dataformat.md) | camel-zip-deflater | Stable | 2.12 | Compress and decompress streams using java.util.zip.Deflater and java.util.zip.Inflater |
| [Zip File](zipFile-dataformat.md) | camel-zipfile | Stable | 2.11 | Compression and decompress streams using java.util.zip.Zip\*Stream |