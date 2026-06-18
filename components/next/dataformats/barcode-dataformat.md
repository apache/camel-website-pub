# Barcode

**Since Camel 2.14**

The Barcode data format is based on the [zxing library](https://github.com/zxing/zxing). The goal of this component is to create a barcode image from a String (marshal) and a String from a barcode image (unmarshal). You’re free to use all features that zxing offers.

## Dependencies

To use the barcode data format in your camel routes, you need to add a dependency on **camel-barcode** which implements this data format.

If you use maven, you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-barcode</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Barcode Options

The Barcode dataformat supports 4 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **barcodeFormat** (common) | `QR_CODE` | `Enum` | 
Barcode format such as QR-Code.

Enum values:

-   AZTEC
    
-   CODABAR
    
-   CODE\_39
    
-   CODE\_93
    
-   CODE\_128
    
-   DATA\_MATRIX
    
-   EAN\_8
    
-   EAN\_13
    
-   ITF
    
-   MAXICODE
    
-   PDF\_417
    
-   QR\_CODE
    
-   RSS\_14
    
-   RSS\_EXPANDED
    
-   UPC\_A
    
-   UPC\_E
    
-   UPC\_EAN\_EXTENSION
    





 |
| **imageType** (common) | `PNG` | `Enum` | 

Image type of the barcode such as png.

Enum values:

-   JPG
    
-   GIF
    
-   PNG
    





 |
| **width** (common) | `100` | `Integer` | Width of the barcode. |
| **height** (common) | `100` | `Integer` | Height of the barcode. |

## Using the Java DSL

First, you have to initialize the barcode data format class. You can use the default constructor, or one of parameterized (see JavaDoc). The default values are:

 
| Parameter | Default Value |
| --- | --- |
| image type (BarcodeImageType) | PNG |
| width | 100 px |
| height | 100 px |
| encoding | UTF-8 |
| barcode format (BarcodeFormat) | QR-Code |

_Java-only: Java programmatic data format instantiation_

```java
// QR-Code default
DataFormat code = new BarcodeDataFormat();
```

If you want to use zxing hints, you can use the 'addToHintMap' method of your BarcodeDataFormat instance:

_Java-only: Java data format configuration API_

```java
code.addToHintMap(DecodeHintType.TRY_HARDER, Boolean.true);
```

For possible hints, please consult the xzing documentation.

### Marshalling

_Java-only: route using Java data format variable_

```java
from("direct://code")
  .marshal(code)
  .to("file://barcode_out");
```

You can call the route from a test class with:

_Java-only: Java test API (ProducerTemplate)_

```java
template.sendBody("direct://code", "This is a testmessage!");
```

You should find inside the 'barcode\_out' folder this image:

![image](../_images/qr-code.png)

### Unmarshalling

The unmarshaller is generic. For unmarshalling, you can use any BarcodeDataFormat instance. If you’ve two instances, one for (generating) QR-Code and one for PDF417, it doesn’t matter which one will be used.

_Java-only: route using Java data format variable_

```java
from("file://barcode_in?noop=true")
  .unmarshal(code) // for unmarshalling, the instance doesn't matter
  .to("mock:out");
```

If you’ll paste the QR-Code image above into the 'barcode\_in' folder, you should find _\`This is a testmessage!\`_ inside the mock. You can find the barcode data format as header variable:

  
| Name | Type | Description |
| --- | --- | --- |
| BarcodeFormat | String | Value of com.google.zxing.BarcodeFormat. |

If you’ll paste the code 39 barcode that is rotated some degrees into the 'barcode\_in' folder, You can find the ORIENTATION as header variable:

  
| Name | Type | Description |
| --- | --- | --- |
| ORIENTATION | Integer | rotate value in degrees . |

## Spring Boot Auto-Configuration

When using barcode with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-barcode-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.barcode.barcode-format** | Barcode format such as QR-Code. | QR\_CODE | String |
| **camel.dataformat.barcode.enabled** | Whether to enable auto configuration of the barcode data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.barcode.height** | Height of the barcode. | 100 | Integer |
| **camel.dataformat.barcode.image-type** | Image type of the barcode such as png. | PNG | String |
| **camel.dataformat.barcode.width** | Width of the barcode. | 100 | Integer |