# Base64

Encode and decode data using Base64.

## What’s inside

-   [Base64 data format](../../../components/next/dataformats/base64-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-base64-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.base64.enabled | Whether to enable auto configuration of the base64 data format. This is enabled by default. |  | Boolean |
| camel.dataformat.base64.line-length | To specific a maximum line length for the encoded data. By default 76 is used. | 76 | Integer |
| camel.dataformat.base64.line-separator | The line separators to use. Uses new line characters (CRLF) by default. |  | String |
| camel.dataformat.base64.url-safe | Instead of emitting '' and '/' we emit '-' and '\_' respectively. urlSafe is only applied to encode operations. Decoding seamlessly handles both modes. Is by default false. | false | Boolean |