# Jactl

Evaluates a Jactl script

## What’s inside

-   [Jactl language](../../../components/next/languages/jactl-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-jactl-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.jactl.enabled | Whether to enable auto configuration of the jactl language. This is enabled by default. |  | Boolean |
| camel.language.jactl.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |