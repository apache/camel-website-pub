# FOP

**Since Camel 2.10**

**Only producer is supported**

The FOP component allows you to render a message into different output formats using [Apache FOP](http://xmlgraphics.apache.org/fop/index.md).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-fop</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

fop://outputFormat?\[options\]

## Usage

### Output Formats

The primary output format is PDF, but other output [formats](http://xmlgraphics.apache.org/fop/0.95/output.md) are also supported:

  
| name | outputFormat | description |
| --- | --- | --- |
| PDF | application/pdf | Portable Document Format |
| PS | application/postscript | Adobe Postscript |
| PCL | application/x-pcl | Printer Control Language |
| PNG | image/png | PNG images |
| JPEG | image/jpeg | JPEG images |
| SVG | image/svg+xml | Scalable Vector Graphics |
| XML | application/X-fop-areatree | Area tree representation |
| MIF | application/mif | FrameMaker’s MIF |
| RTF | application/rtf | Rich Text Format |
| TXT | text/plain | Text |

The complete list of valid output formats can be found in the `MimeConstants.java` source file.

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

The FOP component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The FOP endpoint is configured using URI syntax:

fop:outputType

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **outputType** (producer) | 
**Required** The primary output format is PDF but other output formats are also supported.

Enum values:

-   pdf
    
-   ps
    
-   pcl
    
-   png
    
-   jpeg
    
-   svg
    
-   xml
    
-   mif
    
-   rtf
    
-   txt
    





 |  | FopOutputType |

### Query Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **fopFactory** (producer) | Allows to use a custom configured or implementation of org.apache.fop.apps.FopFactory. |  | FopFactory |
| **userConfigURL** (producer) | The location of a configuration file which can be loaded from classpath or file system. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The FOP component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelFop.Output.Format** (producer) Constant: [`CAMEL_FOP_OUTPUT_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-fop/latest/org/apache/camel/component/fop/FopConstants.html#CAMEL_FOP_OUTPUT_FORMAT) | The output format. |  | String |

### Configuration file

The location of a configuration file with the following [structure](http://xmlgraphics.apache.org/fop/1.0/configuration.md). The file is loaded from the classpath by default. You can use `file:`, or `classpath:` as prefix to load the resource from file or classpath. In previous releases, the file is always loaded from the file system.

### Message Operations

  
| name | default value | description |
| --- | --- | --- |
| `CamelFop.Output.Format` |  | Overrides the output format for that message |
| `CamelFop.Encrypt.userPassword` |  | PDF user password |
| `CamelFop.Encrypt.ownerPassword` |  | PDF owner password |
| `CamelFop.Encrypt.allowPrint` | `true` | Allows printing the PDF |
| `CamelFop.Encrypt.allowCopyContent` | `true` | Allows copying content of the PDF |
| `CamelFop.Encrypt.allowEditContent` | `true` | Allows editing content of the PDF |
| `CamelFop.Encrypt.allowEditAnnotations` | `true` | Allows editing annotation of the PDF |
| `CamelFop.Render.producer` | Apache FOP | Metadata element for the system/software that produces the document |
| `CamelFop.Render.creator` |  | Metadata element for the user that created the document |
| `CamelFop.Render.creationDate` |  | Creation Date |
| `CamelFop.Render.author` |  | Author of the content of the document |
| `CamelFop.Render.title` |  | Title of the document |
| `CamelFop.Render.subject` |  | Subject of the document |
| `CamelFop.Render.keywords` |  | Set of keywords applicable to this document |

### Example

Below is an example route that renders PDFs from XML data and XSLT template and saves the PDF files in the target folder:

```java
from("file:source/data/xml")
    .to("xslt:xslt/template.xsl")
    .to("fop:application/pdf")
    .to("file:target/data");
```

## Spring Boot Auto-Configuration

When using fop with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-fop-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.fop.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.fop.enabled** | Whether to enable auto configuration of the fop component. This is enabled by default. |  | Boolean |
| **camel.component.fop.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |