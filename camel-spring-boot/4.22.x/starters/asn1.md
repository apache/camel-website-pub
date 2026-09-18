# ASN.1 File

Encode and decode data structures using Abstract Syntax Notation One (ASN.1)

## What’s inside

-   [ASN.1 File data format](../../../components/4.22.x/dataformats/asn1-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-asn1-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.asn1.enabled | Whether to enable auto configuration of the asn1 data format. This is enabled by default. |  | Boolean |
| camel.dataformat.asn1.unmarshal-type | Class to use when unmarshalling. |  | String |
| camel.dataformat.asn1.using-iterator | If the asn1 file has more than one entry, the setting this option to true allows working with the splitter EIP to split each entry individually. | false | Boolean |