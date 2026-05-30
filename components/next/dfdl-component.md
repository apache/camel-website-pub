# DFDL

**Since Camel 4.11**

**Only producer is supported**

The DFDL component allows you to transform the fixed format data such as EDI message from/to XML using [Data Format Description Language](https://ogf.org/ogf/doku.php/standards/dfdl/dfdl.md), also known as DFDL. DFDL schema is an XML schema annotated with DFDL elements and attributes.

While DFDL schema defines the XML representation of the data structure, it also defines how the conversion between the fixed format and XML is processed using DFDL annotations.

This component uses [Apache Daffodil](https://daffodil.apache.org/) as an underlying DFDL implementation.

## URI format

dfdl:schemaUri\[?options\]

The URI format contains **schemaUri**, which can be the classpath-local URI of the DFDL schema file.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The DFDL component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The DFDL endpoint is configured using URI syntax:

dfdl:schemaUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **schemaUri** (producer) | **Required** The path to the DFDL schema file. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **parseDirection** (producer) | 
Transform direction. Either PARSE or UNPARSE.

Enum values:

-   PARSE
    
-   UNPARSE
    





 | PARSE | ParseDirection |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **rootElement** (advanced) | The root element name of the schema to use. If not specified, the first root element in the schema will be used. |  | String |
| **rootNamespace** (advanced) | The root namespace of the schema to use. |  | String |

/ component headers: START

## DFDL Schemas

Many DFDL schemas are freely available at [DFDLSchemas on GitHub](https://github.com/DFDLSchemas) including:

-   [UN/EDIFACT](https://github.com/DFDLSchemas/EDIFACT) — models UN/EDIFACT interchanges (ISO 9735) including Supply Chain messages (ORDERS, INVOIC, DESADV, etc.)
    
-   [NACHA](https://github.com/DFDLSchemas/NACHA) — ACH payment transactions
    
-   [HL7](https://github.com/DFDLSchemas/HL7-v2.7) — healthcare messaging
    
-   [PCAP](https://github.com/DFDLSchemas/PCAP) — network packet capture
    

## Using DFDL endpoints

The following format is an example of using DFDL to convert an EDI message to an XML using `X12-837P-dfdl.xsd` DFDL schema file.

```java
from("direct:parse").
  to("dfdl:X12-837P.dfdl.xsd");
```

The following format is an example of using DFDL to convert an XML to an EDI message using `X12-837P-dfdl.xsd` DFDL schema file. Note that `UNPARSE` is specified for the `parseDirection` parameter.

```java
from("direct:unparse").
  to("dfdl:X12-837P.dfdl.xsd?parseDirection=UNPARSE");
```

## Spring Boot Auto-Configuration

When using dfdl with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-dfdl-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.dfdl.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.dfdl.enabled** | Whether to enable auto configuration of the dfdl component. This is enabled by default. |  | Boolean |
| **camel.component.dfdl.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.dataformat.dfdl.enabled** | Whether to enable auto configuration of the dfdl data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.dfdl.root-element** | The root element name of the schema to use. If not specified, the first root element in the schema will be used. |  | String |
| **camel.dataformat.dfdl.root-namespace** | The root namespace of the schema to use. |  | String |
| **camel.dataformat.dfdl.schema-uri** | The path to the DFDL schema file. |  | String |