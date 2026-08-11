# Barcode

Transform strings to various 1D/2D barcode bitmap formats and back

## What’s inside

-   [Barcode data format](../../../components/4.22.x/dataformats/barcode-dataformat.md)
    

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
| camel.dataformat.barcode.barcode-format | Barcode format such as QR-Code. | QR\_CODE | String |
| camel.dataformat.barcode.enabled | Whether to enable auto configuration of the barcode data format. This is enabled by default. |  | Boolean |
| camel.dataformat.barcode.height | Height of the barcode. | 100 | Integer |
| camel.dataformat.barcode.image-type | Image type of the barcode such as png. | PNG | String |
| camel.dataformat.barcode.width | Width of the barcode. | 100 | Integer |