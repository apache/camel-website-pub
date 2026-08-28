# QuickJS

Evaluates a JavaScript expression using QuickJS4J

## What’s inside

-   [QuickJS language](../../../components/next/languages/quickjs-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-quickjs-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.quickjs.enabled | Whether to enable auto configuration of the quickjs language. This is enabled by default. |  | Boolean |
| camel.language.quickjs.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |