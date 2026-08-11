# OCSF

Marshal and unmarshal OCSF (Open Cybersecurity Schema Framework) security events to/from JSON

## What’s inside

-   [OCSF data format](../../../components/4.22.x/dataformats/ocsf-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-ocsf-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.ocsf.allow-unmarshall-type | Whether to allow the unmarshal type to be specified via the CamelOcsfUnmarshalType header. | false | Boolean |
| camel.dataformat.ocsf.collection-type | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows using different collection types than java.util.Collection based as default. |  | String |
| camel.dataformat.ocsf.enabled | Whether to enable auto configuration of the ocsf data format. This is enabled by default. |  | Boolean |
| camel.dataformat.ocsf.object-mapper | Lookup and use the existing ObjectMapper with the given id when using Jackson. |  | String |
| camel.dataformat.ocsf.pretty-print | Whether to enable pretty printing output nicely formatted. | false | Boolean |
| camel.dataformat.ocsf.unmarshal-type | Class name of the OCSF event type to use when unmarshalling. Defaults to OcsfEvent. |  | String |
| camel.dataformat.ocsf.use-default-object-mapper | Whether to lookup and use default Jackson ObjectMapper from the registry. | true | Boolean |
| camel.dataformat.ocsf.use-list | Whether to unmarshal to a List of OCSF events. | false | Boolean |