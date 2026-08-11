# OGNL

Evaluates an OGNL expression (Apache Commons OGNL)

## What’s inside

-   [OGNL language](../../../components/4.22.x/languages/ognl-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-ognl-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.ognl.enabled | Whether to enable auto configuration of the ognl language. This is enabled by default. |  | Boolean |
| camel.language.ognl.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |