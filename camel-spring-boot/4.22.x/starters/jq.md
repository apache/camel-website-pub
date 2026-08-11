# JQ

Evaluates a JQ expression against a JSON message body

## What’s inside

-   [JQ language](../../../components/4.22.x/languages/jq-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-jq-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.jq.enabled | Whether to enable auto configuration of the jq language. This is enabled by default. |  | Boolean |
| camel.language.jq.source | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| camel.language.jq.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |