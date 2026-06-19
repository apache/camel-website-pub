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

The Tika component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Tika endpoint is configured using URI syntax:

tika:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** Operation type.

Enum values:

-   parse
    
-   detect
    





 |  | TikaOperation |

### Query Parameters (5 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **tikaParseOutputEncoding** (producer) | Tika Parse Output Encoding. |  | String |
| **tikaParseOutputFormat** (producer) | 
Tika Output Format. Supported output formats. xml: Returns Parsed Content as XML. html: Returns Parsed Content as HTML. text: Returns Parsed Content as Text. textMain: Uses the boilerpipe library to automatically extract the main content from a web page.

Enum values:

-   xml
    
-   html
    
-   text
    





 | xml | TikaParseOutputFormat |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **tikaConfig** (advanced) | Tika Config. |  | TikaConfig |
| **tikaConfigUri** (advanced) | Tika Config Url. |  | String |

## Usage

### To Detect a file’s MIME Type

The file should be placed in the Body.

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

The file should be placed in the Body.

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