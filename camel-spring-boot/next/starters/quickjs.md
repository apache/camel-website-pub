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

The starter supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.quickjs.enabled | Whether to enable auto configuration of the quickjs language. This is enabled by default. |  | Boolean |
| camel.language.quickjs.resolve-resource | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. | false | Boolean |
| camel.language.quickjs.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |