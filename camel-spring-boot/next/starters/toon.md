# TOON

Marshal JSON-compatible Java values to TOON (Token-Oriented Object Notation) and unmarshal TOON back to Java objects.

## What’s inside

-   [TOON data format](../../../components/next/dataformats/toon-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-toon-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.toon.content-type-header | Whether the data format should set the Content-Type header to text/toon when marshalling. | true | Boolean |
| camel.dataformat.toon.delimiter | Delimiter used for tabular array rows and inline primitive arrays. | COMMA | String |
| camel.dataformat.toon.enabled | Whether to enable auto configuration of the toon data format. This is enabled by default. |  | Boolean |
| camel.dataformat.toon.indent | Number of spaces per indentation level. | 2 | Integer |
| camel.dataformat.toon.length-marker | Whether to prefix array lengths with a hash marker so arrays render as hash-prefixed lengths instead of plain lengths. | false | Boolean |
| camel.dataformat.toon.strict | Whether to enable strict validation when unmarshalling TOON. When false, JToon uses best-effort parsing. | true | Boolean |