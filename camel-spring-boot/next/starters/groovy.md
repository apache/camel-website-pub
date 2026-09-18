# Groovy

Evaluates a Groovy script

## What’s inside

-   [Groovy language](../../../components/next/languages/groovy-language.md)
    
-   [Groovy JSon data format](../../../components/next/dataformats/groovyJson-dataformat.md)
    
-   [Groovy XML data format](../../../components/next/dataformats/groovyXml-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-groovy-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.groovy-json.enabled | Whether to enable auto configuration of the groovyJson data format. This is enabled by default. |  | Boolean |
| camel.dataformat.groovy-json.pretty-print | Whether to pretty print output nicely formatted. | true | Boolean |
| camel.dataformat.groovy-xml.attribute-mapping | Whether to enable attribute mapping. When enabled, keys that start with \_ or character will be mapped to an XML attribute, and vice versa. | true | Boolean |
| camel.dataformat.groovy-xml.enabled | Whether to enable auto configuration of the groovyXml data format. This is enabled by default. |  | Boolean |
| camel.language.groovy.enabled | Whether to enable auto configuration of the groovy language. This is enabled by default. |  | Boolean |
| camel.language.groovy.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |