# PDF

**Since Camel 2.16**

**Only producer is supported**

The PDF component provides the ability to create, modify or extract content from PDF documents. This component uses [Apache PDFBox](https://pdfbox.apache.org/) as the underlying library to work with PDF documents.

To use the PDF component, Maven users will need to add the following dependency to their `pom.xml`:

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

The PDF component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The PDF endpoint is configured using URI syntax:

pdf:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** Operation type.

Enum values:

-   create
    
-   append
    
-   extractText
    
-   merge
    





 |  | PdfOperation |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **font** (producer) | 
Font.

Enum values:

-   COURIER
    
-   COURIER\_BOLD
    
-   COURIER\_OBLIQUE
    
-   COURIER\_BOLD\_OBLIQUE
    
-   HELVETICA
    
-   HELVETICA\_BOLD
    
-   HELVETICA\_OBLIQUE
    
-   HELVETICA\_BOLD\_OBLIQUE
    
-   TIMES\_ROMAN
    
-   TIMES\_BOLD
    
-   TIMES\_ITALIC
    
-   TIMES\_BOLD\_ITALIC
    
-   SYMBOL
    
-   ZAPF\_DINGBATS
    





 | HELVETICA | String |
| **fontSize** (producer) | Font size in pixels. | 14 | float |
| **marginBottom** (producer) | Margin bottom in pixels. | 20 | int |
| **marginLeft** (producer) | Margin left in pixels. | 20 | int |
| **marginRight** (producer) | Margin right in pixels. | 40 | int |
| **marginTop** (producer) | Margin top in pixels. | 20 | int |
| **pageSize** (producer) | 

Page size: LETTER, LEGAL or A0 to A6. The older names PAGE\_SIZE\_A0 to PAGE\_SIZE\_A6 and PAGE\_SIZE\_LETTER are also accepted.

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

The PDF component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelPdfProtectionPolicy** (producer) Constant: [`PROTECTION_POLICY_HEADER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pdf/latest/org/apache/camel/component/pdf/PdfHeaderConstants.html#PROTECTION_POLICY_HEADER_NAME) | Expected type is [https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/encryption/ProtectionPolicy.htmlProtectionPolicy](https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/encryption/ProtectionPolicy.htmlProtectionPolicy). If specified then PDF document will be encrypted with it. |  | ProtectionPolicy |
| **CamelPdfDocument** (producer) Constant: [`PDF_DOCUMENT_HEADER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pdf/latest/org/apache/camel/component/pdf/PdfHeaderConstants.html#PDF_DOCUMENT_HEADER_NAME) | Mandatory header for append operation and ignored in all other operations. Expected type is [https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/PDDocument.htmlPDDocument](https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/PDDocument.htmlPDDocument). Stores PDF document which will be used for append operation. |  | PDDocument |
| **CamelPdfDecryptionMaterial** (producer) Constant: [`DECRYPTION_MATERIAL_HEADER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pdf/latest/org/apache/camel/component/pdf/PdfHeaderConstants.html#DECRYPTION_MATERIAL_HEADER_NAME) | Expected type is [https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/encryption/DecryptionMaterial.htmlDecryptionMaterial](https://pdfbox.apache.org/docs/2.0.13/javadocs/org/apache/pdfbox/pdmodel/encryption/DecryptionMaterial.htmlDecryptionMaterial). Mandatory header if PDF document is encrypted. |  | DecryptionMaterial |
| **CamelPdfFilesToMerge** (producer) Constant: [`FILES_TO_MERGE_HEADER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pdf/latest/org/apache/camel/component/pdf/PdfHeaderConstants.html#FILES_TO_MERGE_HEADER_NAME) | Mandatory header for merge operation and ignored in all other operations. The list of pdf files that will be merged, each given as a java.io.File or a java.nio.file.Path. |  | List |

## Message Body

The message body at each side of the PDF component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `text`, `bytes`, `stream` or `file` | 
The text to write for create and append, which takes the document from the CamelPdfDocument header; a Map or a POJO is written as its toString: marshal it first. extractText reads a PDF from bytes, such as the ByteArrayOutputStream of create, a stream, a file or a PDDocument, not from text; another body, or none, fails. merge takes the files from the CamelPdfFilesToMerge header.

-   With `operation=extractText`: `bytes`, `stream`, `file` or `pojo`
    
-   With `operation=merge`: `any`
    





 |
| **Producer output** | `bytes` (`java.io.ByteArrayOutputStream`) | 

The PDF of create, append and merge as bytes, in a ByteArrayOutputStream, which extractText reads as it is. The text of the document for extractText.

-   With `operation=extractText`: `text` (`java.lang.String`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Type converter

Since Camel 4.8, the component is capable of doing simple document conversions. For instance, suppose you are receiving a PDF byte as a byte array:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("pdf:extractText")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="pdf:extractText"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: pdf:extractText
        - to:
            uri: mock:result
```

It is now possible to get the body as a PD Document by using `PDDocument doc = exchange.getIn().getBody(PDDocument.class);`, which saves the trouble of converting the byte-array to a document.

The type converter reads a PDF from a `byte[]`, a `ByteArrayOutputStream`, an `InputStream`, a `java.io.File` or a `java.nio.file.Path`. The `create`, `append` and `merge` operations leave the PDF in a `ByteArrayOutputStream`, so `pdf:create` can be followed by `pdf:extractText` directly. The `extractText` operation fails with an `InvalidPayloadException` naming the type of the body when the body is missing or is not one of these types.

> **Note**
> this only works for unprotected PDF files. For password-protected, the files still need to be converted manually.

### Creating a PDF from text

The `create` operation needs a body with the text to write; without a body it fails with an `InvalidPayloadException`.

With the default `textProcessingFactory=lineTermination`, the text is written line by line: a line ends at `\r\n`, `\r` or `\n`. A tab is written as four spaces, and other control characters, which the fonts cannot show, are left out.

The `pageSize` option takes `LETTER`, `LEGAL` or `A0` to `A6` (default `A4`). The older names `PAGE_SIZE_A0` to `PAGE_SIZE_A6` and `PAGE_SIZE_LETTER` are still accepted. An unknown value fails when the endpoint is created.

### Merging PDF files

The `merge` operation reads the files to merge from the `CamelPdfFilesToMerge` header: a list of at least two elements, each a `java.io.File` or a `java.nio.file.Path`.