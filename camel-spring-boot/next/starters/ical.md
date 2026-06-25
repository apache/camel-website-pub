# iCal

Marshal and unmarshal iCal (\*.ics) documents to/from model objects

## What’s inside

-   [iCal data format](../../../components/next/dataformats/ical-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-ical-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.ical.enabled | Whether to enable auto configuration of the ical data format. This is enabled by default. |  | Boolean |
| camel.dataformat.ical.validating | Whether to validate the iCal document. | false | Boolean |