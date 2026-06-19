# DataSonnet

To use DataSonnet scripts for message transformations.

## What’s inside

-   [DataSonnet language](../../../components/next/languages/datasonnet-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-datasonnet-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.datasonnet.body-media-type | The String representation of the message’s body MediaType |  | String |
| camel.language.datasonnet.enabled | Whether to enable auto configuration of the datasonnet language. This is enabled by default. |  | Boolean |
| camel.language.datasonnet.output-media-type | The String representation of the MediaType to output |  | String |
| camel.language.datasonnet.source | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| camel.language.datasonnet.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. | true | Boolean |