# OCSF

Marshal and unmarshal OCSF (Open Cybersecurity Schema Framework) security events to/from JSON.

## What’s inside

-   [OCSF data format](../../../components/next/dataformats/ocsf-dataformat.md)
    

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
| camel.dataformat.ocsf.allow-unmarshall-type | If enabled then the unmarshal type can be specified via the CamelOcsfUnmarshalType header. This should only be enabled when desired to be used. | false | Boolean |
| camel.dataformat.ocsf.collection-type | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows to use different collection types than java.util.Collection based as default. |  | String |
| camel.dataformat.ocsf.enabled | Whether to enable auto configuration of the ocsf data format. This is enabled by default. |  | Boolean |
| camel.dataformat.ocsf.object-mapper | Lookup and use the existing ObjectMapper with the given id when using Jackson. |  | String |
| camel.dataformat.ocsf.pretty-print | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| camel.dataformat.ocsf.unmarshal-type | Class name of the OCSF event type to use when unmarshalling. Defaults to OcsfEvent. |  | String |
| camel.dataformat.ocsf.use-default-object-mapper | Whether to lookup and use default Jackson ObjectMapper from the registry. | true | Boolean |
| camel.dataformat.ocsf.use-list | To unmarshal to a List of OCSF events. | false | Boolean |