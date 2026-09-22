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

The starter supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.python3.enabled | Whether to enable auto configuration of the python3 language. This is enabled by default. |  | Boolean |
| camel.language.python3.resolve-resource | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. | false | Boolean |
| camel.language.python3.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |