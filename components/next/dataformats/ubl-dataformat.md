# UBL

**Since Camel 4.23**

The UBL data format is used for marshalling and unmarshalling [UBL 2.1 (Universal Business Language)](https://docs.oasis-open.org/ubl/UBL-2.1.md) documents.

UBL 2.1 is an OASIS standard that defines XML business document types such as invoices, credit notes, orders, despatch advice, and more. It is the document format used by the [Peppol e-invoicing network](https://peppol.org/) and is increasingly mandated across the EU (ViDA directive), and other countries.

The data format uses the [ph-ubl](https://github.com/phax/ph-ubl) library by Philip Helger as the underlying JAXB binding layer. It supports all 65 UBL 2.1 document types and auto-detects the document type from the Java class name (when marshalling) or from the XML root element (when unmarshalling).

## UBL Options

The UBL dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **prettyPrint** (common) | `false` | `Boolean` | Whether to enable pretty printing (formatted) output of the XML. |

## Message Body

The message body at each side of the UBL data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `pojo` | A UBL 2.1 document of ph-ubl, such as an InvoiceType or a CreditNoteType: its class name gives the document type. Text fails. |
| **Marshal output** | `stream`, as xml | The UBL XML in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as xml | A UBL 2.1 document, whose root element gives the document type. |
| **Unmarshal output** | `pojo` | The ph-ubl object of the document type, such as an InvoiceType for an Invoice. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).

## Supported Document Types

The data format supports all 65 UBL 2.1 document types, including:

-   Invoice, CreditNote, DebitNote
    
-   Order, OrderResponse, OrderCancellation, OrderChange
    
-   DespatchAdvice, ReceiptAdvice
    
-   Quotation, RequestForQuotation
    
-   Catalogue, CatalogueRequest
    
-   ApplicationResponse
    
-   Waybill, BillOfLading, FreightInvoice
    
-   Statement, RemittanceAdvice, Reminder
    
-   and many more
    

## Usage

### Marshalling (Java object to XML)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:marshal")
    .marshal().ubl()
    .to("file:output");
```

```xml
<route>
  <from uri="direct:marshal"/>
  <marshal>
    <ubl/>
  </marshal>
  <to uri="file:output"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:marshal
      steps:
        - marshal:
            ubl: {}
        - to:
            uri: file:output
```

### Unmarshalling (XML to Java object)

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:invoices")
    .unmarshal().ubl()
    .process(exchange -> {
        InvoiceType invoice = exchange.getIn().getBody(InvoiceType.class);
        String id = invoice.getIDValue();
    });
```

```xml
<route>
  <from uri="file:invoices"/>
  <unmarshal>
    <ubl/>
  </unmarshal>
  <to uri="direct:process"/>
</route>
```

```yaml
- route:
    from:
      uri: file:invoices
      steps:
        - unmarshal:
            ubl: {}
        - to:
            uri: direct:process
```

### With pretty printing

-   Java
    
-   XML
    
-   YAML
    

```java
UblDataFormat ubl = new UblDataFormat();
ubl.setPrettyPrint(true);

from("direct:marshal")
    .marshal(ubl)
    .to("file:output");
```

```xml
<route>
  <from uri="direct:marshal"/>
  <marshal>
    <ubl prettyPrint="true"/>
  </marshal>
  <to uri="file:output"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:marshal
      steps:
        - marshal:
            ubl:
              prettyPrint: true
        - to:
            uri: file:output
```

## Dependencies

To use UBL in your Camel routes, you need to add the dependency on **camel-ubl** which implements this data format.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest and greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-ubl</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```