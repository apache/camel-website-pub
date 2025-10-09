# Camel data formats supported on Quarkus

There are 47 data formats (0 deprecated, 7 JVM only)

     
| Data format | Artifact | JVM  
since | Native  
since | Support  
level | Description |
| --- | --- | --- | --- | --- | --- |
| [ASN.1 File](extensions/asn1.md) | camel-quarkus-asn1 | 1.1.0 | n/a | Preview | Encode and decode data structures using Abstract Syntax Notation One (ASN.1). |
| [Avro](extensions/avro.md) | camel-quarkus-avro | 1.0.0 | 1.0.0 | Stable | Serialize and deserialize messages using Apache Avro binary data format. |
| [Avro Jackson](extensions/jackson-avro.md) | camel-quarkus-jackson-avro | 2.0.0 | 2.0.0 | Stable | Marshal POJOs to Avro and back using Jackson. |
| [Barcode](extensions/barcode.md) | camel-quarkus-barcode | 1.1.0 | n/a | Preview | Transform strings to various 1D/2D barcode bitmap formats and back. |
| [Base64](extensions/base64.md) | camel-quarkus-base64 | 1.0.0 | 1.0.0 | Stable | Encode and decode data using Base64. |
| [BeanIO](extensions/beanio.md) | camel-quarkus-beanio | 3.8.0 | 3.16.0 | Stable | Marshal and unmarshal Java beans to and from flat files (such as CSV, delimited, or fixed length formats). |
| [Bindy Key Value Pair](extensions/bindy.md) | camel-quarkus-bindy | 1.0.0 | 1.0.0 | Stable | Marshal and unmarshal between POJOs and key-value pair (KVP) format using Camel Bindy |
| [CBOR](extensions/cbor.md) | camel-quarkus-cbor | 1.1.0 | 1.7.0 | Stable | Unmarshal a CBOR payload to POJO and back. |
| [Crypto (Java Cryptographic Extension)](extensions/crypto.md) | camel-quarkus-crypto | 1.1.0 | 1.2.0 | Stable | Encrypt and decrypt messages using Java Cryptography Extension (JCE). |
| [CSV](extensions/csv.md) | camel-quarkus-csv | 0.2.0 | 0.2.0 | Stable | Handle CSV (Comma Separated Values) payloads. |
| [DFDL](extensions/dfdl.md) | camel-quarkus-dfdl | 3.22.0 | n/a | Preview | Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL). |
| [JSON Fastjson](extensions/fastjson.md) | camel-quarkus-fastjson | 1.1.0 | n/a | Preview | Marshal POJOs to JSON and back using Fastjson |
| [FHIR JSon](extensions/fhir.md) | camel-quarkus-fhir | 0.3.0 | 0.3.0 | Stable | Marshall and unmarshall FHIR objects to/from JSON. |
| [FHIR XML](extensions/fhir.md) | camel-quarkus-fhir | 0.3.0 | 0.3.0 | Stable | Marshall and unmarshall FHIR objects to/from XML. |
| [Flatpack](extensions/flatpack.md) | camel-quarkus-flatpack | 1.1.0 | 1.1.0 | Stable | Marshal and unmarshal Java lists and maps to/from flat files (such as CSV, delimited, or fixed length formats) using Flatpack library. |
| [Fory](extensions/fory.md) | camel-quarkus-fory | 3.18.0 | 3.18.0 | Stable | Serialize and deserialize messages using Apache Fory |
| [Grok](extensions/grok.md) | camel-quarkus-grok | 1.0.0 | 1.0.0 | Stable | Unmarshal unstructured data to objects using Logstash based Grok patterns. |
| [JSON Gson](extensions/gson.md) | camel-quarkus-gson | 1.0.0 | 1.0.0 | Stable | Marshal POJOs to JSON and back using Gson |
| [GZip Deflater](extensions/zip-deflater.md) | camel-quarkus-zip-deflater | 1.0.0 | 1.0.0 | Stable | Compress and decompress messages using java.util.zip.GZIPStream. |
| [HL7](extensions/hl7.md) | camel-quarkus-hl7 | 1.1.0 | 1.8.0 | Stable | Marshal and unmarshal HL7 (Health Care) model objects using the HL7 MLLP codec. |
| [iCal](extensions/ical.md) | camel-quarkus-ical | 1.0.0 | 1.0.0 | Stable | Marshal and unmarshal iCal (.ics) documents to/from model objects. |
| [ISO-8583](extensions/iso8583.md) | camel-quarkus-iso8583 | 3.26.0 | 3.26.0 | Stable | Create, edit and read ISO-8583 messages. |
| [JSON Jackson](extensions/jackson.md) | camel-quarkus-jackson | 0.3.0 | 0.3.0 | Stable | Marshal POJOs to JSON and back using Jackson. |
| [Jackson XML](extensions/jacksonxml.md) | camel-quarkus-jacksonxml | 1.0.0 | 1.0.0 | Stable | Unmarshal an XML payloads to POJOs and back using XMLMapper extension of Jackson. |
| [JAXB](extensions/jaxb.md) | camel-quarkus-jaxb | 1.0.0 | 1.0.0 | Stable | Unmarshal XML payloads to POJOs and back using JAXB2 XML marshalling standard. |
| [JSonApi](extensions/jsonapi.md) | camel-quarkus-jsonapi | 1.1.0 | n/a | Preview | Marshal and unmarshal JSON:API resources using JSONAPI-Converter library. |
| [JSON JSON-B](extensions/jsonb.md) | camel-quarkus-jsonb | 1.5.0 | 1.5.0 | Stable | Marshal POJOs to JSON and back using JSON-B. |
| [LZF Deflate Compression](extensions/lzf.md) | camel-quarkus-lzf | 1.0.0 | 1.0.0 | Stable | Compress and decompress streams using LZF deflate algorithm. |
| [MIME Multipart](extensions/mail.md) | camel-quarkus-mail | 0.2.0 | 0.2.0 | Stable | Marshal Camel messages with attachments into MIME-Multipart messages and back. |
| [PGP](extensions/crypto-pgp.md) | camel-quarkus-crypto-pgp | 3.13.0 | 3.13.0 | Stable | Encrypt and decrypt messages using Java Cryptographic Extension (JCE) and PGP. |
| [Protobuf](extensions/protobuf.md) | camel-quarkus-protobuf | 1.0.0 | 1.5.0 | Stable | Serialize and deserialize Java objects using Google’s Protocol buffers. |
| [Protobuf Jackson](extensions/jackson-protobuf.md) | camel-quarkus-jackson-protobuf | 2.0.0 | 2.0.0 | Stable | Marshal POJOs to Protobuf and back using Jackson. |
| [RSS](extensions/rss.md) | camel-quarkus-rss | 1.1.0 | 1.2.0 | Stable | Transform from ROME SyndFeed Java Objects to XML and vice-versa. |
| [Smooks](extensions/smooks.md) | camel-quarkus-smooks | 3.18.0 | n/a | Preview | Transform and bind XML as well as non-XML data, including EDI, CSV, JSON, and YAML using Smooks. |
| [YAML SnakeYAML](extensions/snakeyaml.md) | camel-quarkus-snakeyaml | 0.4.0 | 0.4.0 | Stable | Marshal and unmarshal Java objects to and from YAML using SnakeYAML |
| [SOAP](extensions/soap.md) | camel-quarkus-soap | 1.0.0 | 1.0.0 | Stable | Marshal Java objects to SOAP messages and back. |
| [SWIFT MT](extensions/swift.md) | camel-quarkus-swift | 3.2.0 | 3.2.0 | Stable | Encode and decode SWIFT MT messages. |
| [SWIFT MX](extensions/swift.md) | camel-quarkus-swift | 3.2.0 | 3.2.0 | Stable | Encode and decode SWIFT MX messages. |
| [Syslog](extensions/syslog.md) | camel-quarkus-syslog | 1.1.0 | 1.7.0 | Stable | Marshall SyslogMessages to RFC3164 and RFC5424 messages and back. |
| [Tar File](extensions/tarfile.md) | camel-quarkus-tarfile | 0.3.0 | 0.3.0 | Stable | Archive files into tarballs or extract files from tarballs. |
| [Thrift](extensions/thrift.md) | camel-quarkus-thrift | 1.1.0 | n/a | Preview | Serialize and deserialize messages using Apache Thrift binary data format. |
| [uniVocity CSV](extensions/univocity-parsers.md) | camel-quarkus-univocity-parsers | 1.1.0 | 1.2.0 | Stable | Marshal and unmarshal Java objects from and to CSV (Comma Separated Values) using UniVocity Parsers. |
| [uniVocity Fixed Length](extensions/univocity-parsers.md) | camel-quarkus-univocity-parsers | 1.1.0 | 1.2.0 | Stable | Marshal and unmarshal Java objects from and to fixed length records using UniVocity Parsers. |
| [uniVocity TSV](extensions/univocity-parsers.md) | camel-quarkus-univocity-parsers | 1.1.0 | 1.2.0 | Stable | Marshal and unmarshal Java objects from and to TSV (Tab-Separated Values) records using UniVocity Parsers. |
| [XML Security](extensions/xmlsecurity.md) | camel-quarkus-xmlsecurity | 1.1.0 | 1.7.0 | Stable | Encrypt and decrypt XML payloads using Apache Santuario. |
| [Zip Deflater](extensions/zip-deflater.md) | camel-quarkus-zip-deflater | 1.0.0 | 1.0.0 | Stable | Compress and decompress streams using java.util.zip.Deflater and java.util.zip.Inflater. |
| [Zip File](extensions/zipfile.md) | camel-quarkus-zipfile | 0.2.0 | 0.2.0 | Stable | Compression and decompress streams using java.util.zip.ZipStream. |