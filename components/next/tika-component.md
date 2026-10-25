# Tika

**Since Camel 2.19**

**Only producer is supported**

The Tika component provides the ability to detect and parse documents with Apache Tika. This component uses [Apache Tika](https://tika.apache.org/) as the underlying library to work with documents.

To use the Tika component, Maven users will need to add the following dependency to their `pom.xml`:

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-tika</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The Tika component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Tika endpoint is configured using URI syntax:

tika:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** Operation type.

Enum values:

-   parse
    
-   detect
    





 |  | TikaOperation |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **tikaParseOutputEncoding** (producer) | The character encoding of the parsed output. Defaults to the default charset of the JVM. The parse operation sets this encoding as the charset of the exchange, so converting the output to text decodes it with this encoding. |  | String |
| **tikaParseOutputFormat** (producer) | 
Tika Output Format. Supported output formats. xml: Returns Parsed Content as XML. html: Returns Parsed Content as HTML. text: Returns Parsed Content as Text.

Enum values:

-   xml
    
-   html
    
-   text
    





 | xml | TikaParseOutputFormat |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **tikaConfigFile** (advanced) | Path to a Tika JSON configuration file. |  | String |
| **tikaLoader** (advanced) | Tika loader used to configure parsers and detectors. |  | TikaLoader |

## Message Body

The message body at each side of the Tika component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `text`, `bytes`, `stream` or `file` | The document: text, bytes, a stream or a file. A Map, a List, a POJO or no body fails, and parse fails on an empty document. |
| **Producer output** | `bytes` (`java.io.ByteArrayOutputStream`) | 
parse gives the content as bytes, in a ByteArrayOutputStream: XHTML, or HTML or plain text with tikaParseOutputFormat, in tikaParseOutputEncoding, and the metadata of the document in headers; camel-tika parses HTML and text, other types need their Tika parser module. detect gives the media type as text, such as text/html.

-   With `operation=detect`: `text` (`java.lang.String`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### To Detect a file’s MIME Type

The body is the document: text, bytes, a stream or a file. After `detect`, the body is the MIME type as text, such as `text/html`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
        .to("tika:detect");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="tika:detect"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: tika:detect
```

### To Parse a File

The body is the document: text, bytes, a stream or a file. After `parse`, the body is a `ByteArrayOutputStream` with the content as XHTML, or as HTML or plain text with `tikaParseOutputFormat`, which converts to a `String`, and the metadata of the document are headers, such as `dc:title`. The component has the Tika parsers of HTML and text: other types need their Tika parser module, such as `org.apache.tika:tika-parser-pdf-module` for PDF, or the content is empty.

The body of `detect` and `parse` must convert to an `InputStream`, such as a `java.io.File`, a `byte[]`, a `String` or a stream. A missing body or a body that does not convert, such as a `Map`, fails with an `InvalidPayloadException`.

The `parse` operation writes its output in the `tikaParseOutputEncoding` and sets that encoding as the charset of the exchange (the `CamelCharsetName` exchange property), so converting the output to a `String` decodes it right.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
        .to("tika:parse");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="tika:parse"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: tika:parse
```