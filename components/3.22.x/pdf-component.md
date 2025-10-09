# PDF

**Since Camel 2.16**

**Only producer is supported**

The PDF components provides the ability to create, modify or extract content from PDF documents. This component uses [Apache PDFBox](https://pdfbox.apache.org/) as underlying library to work with PDF documents.

In order to use the PDF component, Maven users will need to add the following dependency to their `pom.xml`:

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-pdf</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

The PDF component only supports producer endpoints.

pdf:operation\[?options\]

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

The PDF component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The PDF endpoint is configured using URI syntax:

pdf:operation

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** Operation type.

Enum values:

-   create
    
-   append
    
-   extractText
    





 |  | PdfOperation |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **font** (producer) | 
Font.

Enum values:

-   Courier
    
-   Courier-Bold
    
-   Courier-Oblique
    
-   Courier-BoldOblique
    
-   Helvetica
    
-   Helvetica-Bold
    
-   Helvetica-Oblique
    
-   Helvetica-BoldOblique
    
-   Times-Roman
    
-   Times-Bold
    
-   Times-Italic
    
-   Times-BoldItalic
    
-   Symbol
    
-   ZapfDingbats
    





 | Helvetica | String |
| **fontSize** (producer) | Font size in pixels. | 14 | float |
| **marginBottom** (producer) | Margin bottom in pixels. | 20 | int |
| **marginLeft** (producer) | Margin left in pixels. | 20 | int |
| **marginRight** (producer) | Margin right in pixels. | 40 | int |
| **marginTop** (producer) | Margin top in pixels. | 20 | int |
| **pageSize** (producer) | 

Page size.

Enum values:

-   LETTER
    
-   LEGAL
    
-   A0
    
-   A1
    
-   A2
    
-   A3
    
-   A4
    
-   A5
    
-   A6
    





 | A4 | String |
| **textProcessingFactory** (producer) | 

Text processing to use. autoFormatting: Text is getting sliced by words, then max amount of words that fits in the line will be written into pdf document. With this strategy all words that doesn’t fit in the line will be moved to the new line. lineTermination: Builds set of classes for line-termination writing strategy. Text getting sliced by line termination symbol and then it will be written regardless it fits in the line or not.

Enum values:

-   autoFormatting
    
-   lineTermination
    





 | lineTermination | TextProcessingFactory |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The PDF component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **protection-policy** (producer) Constant: [`PROTECTION_POLICY_HEADER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pdf/latest/org/apache/camel/component/pdf/PdfHeaderConstants.html#PROTECTION_POLICY_HEADER_NAME) | Expected type is [https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/encryption/ProtectionPolicy.htmlProtectionPolicy](https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/encryption/ProtectionPolicy.htmlProtectionPolicy). If specified then PDF document will be encrypted with it. |  | ProtectionPolicy |
| **pdf-document** (producer) Constant: [`PDF_DOCUMENT_HEADER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pdf/latest/org/apache/camel/component/pdf/PdfHeaderConstants.html#PDF_DOCUMENT_HEADER_NAME) | Mandatory header for append operation and ignored in all other operations. Expected type is [https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/PDDocument.htmlPDDocument](https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/PDDocument.htmlPDDocument). Stores PDF document which will be used for append operation. |  | PDDocument |
| **decryption-material** (producer) Constant: [`DECRYPTION_MATERIAL_HEADER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pdf/latest/org/apache/camel/component/pdf/PdfHeaderConstants.html#DECRYPTION_MATERIAL_HEADER_NAME) | Expected type is [https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/encryption/DecryptionMaterial.htmlDecryptionMaterial](https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/encryption/DecryptionMaterial.htmlDecryptionMaterial). Mandatory header if PDF document is encrypted. |  | DecryptionMaterial |

## Spring Boot Auto-Configuration

When using pdf with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-pdf-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.pdf.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.pdf.enabled** | Whether to enable auto configuration of the pdf component. This is enabled by default. |  | Boolean |
| **camel.component.pdf.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |