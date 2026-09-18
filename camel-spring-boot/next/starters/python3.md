# Python 3

Evaluates a Python 3 expression

## What’s inside

-   [Python 3 language](../../../components/next/languages/python3-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-python3-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.python3.enabled | Whether to enable auto configuration of the python3 language. This is enabled by default. |  | Boolean |
| camel.language.python3.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |