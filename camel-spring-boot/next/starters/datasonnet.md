# DataSonnet

To use DataSonnet scripts for message transformations

## What’s inside

-   [DataSonnet language](../../../components/next/languages/datasonnet-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-datasonnet-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.language.datasonnet.body-media-type | The media type of the message body, such as application/json. |  | String |
| camel.language.datasonnet.enabled | Whether to enable auto configuration of the datasonnet language. This is enabled by default. |  | Boolean |
| camel.language.datasonnet.output-media-type | The media type to use for the output result. |  | String |
| camel.language.datasonnet.resolve-resource | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. | false | Boolean |
| camel.language.datasonnet.source | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| camel.language.datasonnet.trim | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. | true | Boolean |