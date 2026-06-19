# SWIFT MT

Encode and decode SWIFT MT messages.

## What’s inside

-   [SWIFT MT data format](../../../components/next/dataformats/swiftMt-dataformat.md)
    
-   [SWIFT MX data format](../../../components/next/dataformats/swiftMx-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-swift-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.swift-mt.enabled | Whether to enable auto configuration of the swiftMt data format. This is enabled by default. |  | Boolean |
| camel.dataformat.swift-mt.write-in-json | The flag indicating that messages must be marshalled in a JSON format. | false | Boolean |
| camel.dataformat.swift-mx.enabled | Whether to enable auto configuration of the swiftMx data format. This is enabled by default. |  | Boolean |
| camel.dataformat.swift-mx.read-config | Refers to a specific configuration to use when unmarshalling an input stream to lookup from the registry. The option is a com.prowidesoftware.swift.model.mx.MxReadConfiguration type. |  | String |
| camel.dataformat.swift-mx.read-message-id | The type of MX message to produce when unmarshalling an input stream. If not set, it will be automatically detected from the namespace used. The option is a com.prowidesoftware.swift.model.MxId type. |  | String |
| camel.dataformat.swift-mx.write-config | Refers to a specific configuration to use when marshalling a message to lookup from the registry. The option is a com.prowidesoftware.swift.model.mx.MxWriteConfiguration type. |  | String |
| camel.dataformat.swift-mx.write-in-json | The flag indicating that messages must be marshalled in a JSON format. | false | Boolean |