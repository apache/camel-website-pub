# Grok

Unmarshal unstructured data to objects using Logstash based Grok patterns

## What’s inside

-   [Grok data format](../../../components/next/dataformats/grok-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-grok-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.grok.allow-multiple-matches-per-line | Whether to allow multiple matches per line. If false, every line of input is matched for the pattern only once. Otherwise the line can be scanned multiple times when a non-terminal pattern is used. | true | Boolean |
| camel.dataformat.grok.enabled | Whether to enable auto configuration of the grok data format. This is enabled by default. |  | Boolean |
| camel.dataformat.grok.flattened | Whether to use flattened mode. In flattened mode an exception is thrown when there are multiple pattern matches with the same key. | false | Boolean |
| camel.dataformat.grok.named-only | Whether to capture named expressions only or not (i.e. %\\{IP:ip} but not ${IP}). | false | Boolean |
| camel.dataformat.grok.pattern | The grok pattern to match lines of input. |  | String |