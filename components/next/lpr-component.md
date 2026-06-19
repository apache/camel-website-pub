# Printer

**Since Camel 2.1**

**Only producer is supported**

The Printer component provides a way to direct payloads on a route to a printer. The payload has to be a formatted piece of payload in order for the component to appropriately print it. The goal is to be able to direct specific payloads as jobs to a line printer in a camel flow.

The functionality allows for the payload to be printed on a default printer, named local, remote or wireless linked printer using the javax printing API under the covers.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-printer</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

Since the URI scheme for a printer has not been standardized (the nearest thing to a standard being the IETF print standard), and therefore not uniformly applied by vendors, we have chosen **"lpr"** as the scheme.

lpr://localhost/default\[?options\]
lpr://remotehost:port/path/to/printer\[?options\]

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

The Printer component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Printer endpoint is configured using URI syntax:

lpr:hostname:port/printername

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **hostname** (producer) | **Required** Hostname of the printer. |  | String |
| **port** (producer) | Port number of the printer. |  | int |
| **printername** (producer) | Name of the printer. |  | String |

### Query Parameters (11 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **copies** (producer) | Number of copies to print. | 1 | int |
| **docFlavor** (producer) | Sets DocFlavor to use. |  | DocFlavor |
| **flavor** (producer) | Sets DocFlavor to use. |  | String |
| **mediaSize** (producer) | Sets the stationary as defined by enumeration names in the javax.print.attribute.standard.MediaSizeName API. The default setting is to use North American Letter sized stationary. The value’s case is ignored, e.g. values of iso\_a4 and ISO\_A4 may be used. | na-letter | String |
| **mediaTray** (producer) | Sets MediaTray supported by the javax.print.DocFlavor API, for example upper,middle etc. |  | String |
| **mimeType** (producer) | Sets mimeTypes supported by the javax.print.DocFlavor API. |  | String |
| **orientation** (producer) | 
Sets the page orientation.

Enum values:

-   portrait
    
-   landscape
    
-   reverse-portrait
    
-   reverse-landscape
    





 | portrait | String |
| **printerPrefix** (producer) | Sets the prefix name of the printer, it is useful when the printer name does not start with //hostname/printer. |  | String |
| **sendToPrinter** (producer) | etting this option to false prevents sending of the print data to the printer. | true | boolean |
| **sides** (producer) | 

Sets one sided or two sided printing based on the javax.print.attribute.standard.Sides API.

Enum values:

-   one-sided
    
-   duplex
    
-   tumble
    
-   two-sided-short-edge
    
-   two-sided-long-edge
    





 | one-sided | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Printer component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **PrinterJobName** (producer) Constant: [`JOB_NAME`](https://javadoc.io/doc/org.apache.camel/camel-printer/latest/org/apache/camel/component/printer/PrinterEndpoint.html#JOB_NAME) | The name of the job. |  | String |

## Usage

### Sending Messages to a Printer

#### Printer Producer

Sending data to the printer is very straightforward and involves creating a producer endpoint that can be sent message exchanges on in route.

## Examples

Usage samples.

### Printing text-based payloads

Printing text-based payloads on a Default printer using letter stationary and one-sided mode

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://inputdir/?delete=true")
    .to("lpr://localhost/default?copies=2&flavor=DocFlavor.INPUT_STREAM&mimeType=AUTOSENSE&mediaSize=NA_LETTER&sides=one-sided");
```

```xml
<route>
  <from uri="file://inputdir/?delete=true"/>
  <to uri="lpr://localhost/default?copies=2&amp;flavor=DocFlavor.INPUT_STREAM&amp;mimeType=AUTOSENSE&amp;mediaSize=NA_LETTER&amp;sides=one-sided"/>
</route>
```

```yaml
- route:
    from:
      uri: file://inputdir/
      parameters:
        delete: true
      steps:
        - to:
            uri: lpr://localhost/default
            parameters:
              copies: 2
              flavor: DocFlavor.INPUT_STREAM
              mimeType: AUTOSENSE
              mediaSize: NA_LETTER
              sides: one-sided
```

### Printing GIF-based payloads

Printing GIF-based payloads on a remote printer using A4 stationary and one-sided mode

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://inputdir/?delete=true")
    .to("lpr://remotehost/sales/salesprinter?copies=2&sides=one-sided&mimeType=GIF&mediaSize=ISO_A4&flavor=DocFlavor.INPUT_STREAM");
```

```xml
<route>
  <from uri="file://inputdir/?delete=true"/>
  <to uri="lpr://remotehost/sales/salesprinter?copies=2&amp;sides=one-sided&amp;mimeType=GIF&amp;mediaSize=ISO_A4&amp;flavor=DocFlavor.INPUT_STREAM"/>
</route>
```

```yaml
- route:
    from:
      uri: file://inputdir/
      parameters:
        delete: true
      steps:
        - to:
            uri: lpr://remotehost/sales/salesprinter
            parameters:
              copies: 2
              sides: one-sided
              mimeType: GIF
              mediaSize: ISO_A4
              flavor: DocFlavor.INPUT_STREAM
```

### Printing JPEG-based payloads

Printing JPEG-based payloads on a remote printer using Japanese Postcard stationary and one-sided mode

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://inputdir/?delete=true")
    .to("lpr://remotehost/sales/salesprinter?copies=2&sides=one-sided&mimeType=JPEG&mediaSize=JAPANESE_POSTCARD&flavor=DocFlavor.INPUT_STREAM");
```

```xml
<route>
  <from uri="file://inputdir/?delete=true"/>
  <to uri="lpr://remotehost/sales/salesprinter?copies=2&amp;sides=one-sided&amp;mimeType=JPEG&amp;mediaSize=JAPANESE_POSTCARD&amp;flavor=DocFlavor.INPUT_STREAM"/>
</route>
```

```yaml
- route:
    from:
      uri: file://inputdir/
      parameters:
        delete: true
      steps:
        - to:
            uri: lpr://remotehost/sales/salesprinter
            parameters:
              copies: 2
              sides: one-sided
              mimeType: JPEG
              mediaSize: JAPANESE_POSTCARD
              flavor: DocFlavor.INPUT_STREAM
```