# JavaScript

Evaluates a JavaScript expression

## What’s inside

-   [JavaScript language](../../../components/4.22.x/languages/js-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-javascript-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.js.enabled | Whether to enable auto configuration of the js language. This is enabled by default. |  | Boolean |
| camel.language.js.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |