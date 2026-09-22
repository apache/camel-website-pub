# JQ

Evaluates a JQ expression against a JSON message body

## What’s inside

-   [JQ language](../../../components/next/languages/jq-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-jq-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.jq.enabled | Whether to enable auto configuration of the jq language. This is enabled by default. |  | Boolean |
| camel.language.jq.resolve-resource | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. | false | Boolean |
| camel.language.jq.source | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| camel.language.jq.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |