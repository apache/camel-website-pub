# Python

Evaluates a Python expression

## What’s inside

-   [Python language](../../../components/next/languages/python-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-python-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.python.enabled | Whether to enable auto configuration of the python language. This is enabled by default. |  | Boolean |
| camel.language.python.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |