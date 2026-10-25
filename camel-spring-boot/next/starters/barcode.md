# Barcode

Transform strings to various 1D/2D barcode bitmap formats and back

## What’s inside

-   [Barcode data format](../../../components/next/dataformats/barcode-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-barcode-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.barcode.barcode-format | Barcode format such as QR-Code. MAXICODE, RSS\_14, RSS\_EXPANDED and UPC\_EAN\_EXTENSION cannot be written by marshal, as there is no encoder for them; unmarshal reads the format of the image. | QR\_CODE | String |
| camel.dataformat.barcode.enabled | Whether to enable auto configuration of the barcode data format. This is enabled by default. |  | Boolean |
| camel.dataformat.barcode.height | Height of the barcode. | 100 | Integer |
| camel.dataformat.barcode.image-type | Image type of the barcode such as png. | PNG | String |
| camel.dataformat.barcode.width | Width of the barcode. | 100 | Integer |