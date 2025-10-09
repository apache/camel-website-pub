# AtlasMap

> **Warning**
> **Deprecated:** This atlasmap is deprecated and may be removed in a future release.

**Since Camel 3.7**

**Only producer is supported**

The AtlasMap component allows you to process data mapping using an [AtlasMap](http://www.atlasmap.io/) data mapping definition. The AtlasMap mapping definition is packaged as an ADM archive file when it is exported from the AtlasMap Data Mapper UI. NOTE: Although it is possible to load mapping definition JSON file without being packaged into ADM archive file, some features will not work in that way. It is recommended to always use ADM archive file for other than developer test purpose.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-atlasmap</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

Optionally you can include the DFDL module, which is a POC for [Apache Daffodil](https://daffodil.apache.org/):

```xml
<dependency>
    <groupId>io.atlasmap</groupId>
    <artifactId>atlas-dfdl-module</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as atlasmap-core in camel-atlasmap -->
</dependency>
```

## URI format

```java
atlasmap:mappingName[?options]
```

Where **mappingName** is the classpath-local URI of the AtlasMap mapping definition, either ADM archive file or mapping definition JSON file to process.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The AtlasMap component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **atlasContextFactory** (advanced) | To use the AtlasContextFactory otherwise a new engine is created. |  | AtlasContextFactory |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **propertiesFile** (advanced) | The URI of the properties file which is used for AtlasContextFactory initialization. |  | String |

## Endpoint Options

The AtlasMap endpoint is configured using URI syntax:

atlasmap:resourceUri

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the resource. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | false | boolean |
| **forceReload** (producer) | Whether to enable or disable force reload mode. This is set to false by default and ADM file is loaded from a file only on a first Exchange, and AtlasContext will be reused after that until endpoint is recreated. If this is set to true, ADM file will be loaded from a file on every Exchange. | false | boolean |
| **sourceMapName** (producer) | The Exchange property name for a source message map which hold java.util.Map<String, Message> where the key is AtlasMap Document ID. AtlasMap consumes Message bodies as source documents, as well as message headers as source properties where the scope equals to Document ID. |  | String |
| **targetMapMode** (producer) | 
TargetMapMode enum value to specify how multiple target documents are delivered if exist. 'MAP': Stores them into a java.util.Map, and the java.util.Map is set to an exchange property if 'targetMapName' is specified, otherwise message body. 'MESSAGE\_HEADER': Stores them into message headers. 'EXCHANGE\_PROPERTY': Stores them into exchange properties. ).

Enum values:

-   MAP
    
-   MESSAGE\_HEADER
    
-   EXCHANGE\_PROPERTY
    





 | MAP | TargetMapMode |
| **targetMapName** (producer) | The Exchange property name for a target document map which hold java.util.Map<String, Object> where the key is AtlasMap Document ID. AtlasMap populates multiple target documents into this map. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The AtlasMap component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAtlasResourceUri** (producer) Constant: [`ATLAS_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-atlasmap/latest/org/apache/camel/component/atlasmap/AtlasMapConstants.html#ATLAS_RESOURCE_URI) | The new resource URI to use. |  | String |
| **CamelAtlasMapping** (producer) Constant: [`ATLAS_MAPPING`](https://javadoc.io/doc/org.apache.camel/camel-atlasmap/latest/org/apache/camel/component/atlasmap/AtlasMapConstants.html#ATLAS_MAPPING) | The Atlas mapping to use. |  | String |
| **Content-Type** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-atlasmap/latest/org/apache/camel/component/atlasmap/AtlasMapConstants.html#CONTENT_TYPE) | The content type that is set according to the datasource (json or xml). |  | String |

## Examples

### Producer Example

You could use something like

```java
from("activemq:My.Queue").
  to("atlasmap:atlasmap-mapping.adm");
```

where you can export an ADM archive file from AtlasMap Data Mapper UI.

## Spring Boot Auto-Configuration

When using atlasmap with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-atlasmap-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.atlasmap.atlas-context-factory** | To use the AtlasContextFactory otherwise a new engine is created. The option is a io.atlasmap.api.AtlasContextFactory type. |  | AtlasContextFactory |
| **camel.component.atlasmap.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.atlasmap.enabled** | Whether to enable auto configuration of the atlasmap component. This is enabled by default. |  | Boolean |
| **camel.component.atlasmap.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.atlasmap.properties-file** | The URI of the properties file which is used for AtlasContextFactory initialization. |  | String |