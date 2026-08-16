# UBL

Marshal and unmarshal UBL 2.1 (Universal Business Language) documents.

## What’s inside

-   [UBL data format](../../../components/next/dataformats/ubl-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-ubl-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.ubl.enabled | Whether to enable auto configuration of the ubl data format. This is enabled by default. |  | Boolean |
| camel.dataformat.ubl.pretty-print | Whether to enable pretty printing (formatted) output of the XML | false | Boolean |