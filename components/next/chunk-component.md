# Chunk

**Since Camel 2.15**

**Only producer is supported**

The Chunk component allows for processing a message using a [Chunk](https://github.com/tomj74/chunk-templates) template. This can be ideal when using Templating to generate responses for requests.

## URI format

chunk:templateName\[?options\]

Where **templateName** is the classpath-local URI of the template to invoke.

You can append query options to the URI in the following format: `?option=value&option=value&…​`

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

The Chunk component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Chunk endpoint is configured using URI syntax:

chunk:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the resource. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **encoding** (producer) | Define the encoding of the body. |  | String |
| **extension** (producer) | Define the file extension of the template. |  | String |
| **themeFolder** (producer) | Define the themes folder to scan. |  | String |
| **themeLayer** (producer) | Define the theme layer to elaborate. |  | String |
| **themeSubfolder** (producer) | Define the themes subfolder to scan. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Chunk component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ChunkResourceUri** (producer) Constant: [`CHUNK_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-chunk/latest/org/apache/camel/component/chunk/ChunkConstants.html#CHUNK_RESOURCE_URI) | A URI for the template resource to use instead of the endpoint configured. |  | String |
| **ChunkTemplate** (producer) Constant: [`CHUNK_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-chunk/latest/org/apache/camel/component/chunk/ChunkConstants.html#CHUNK_TEMPLATE) | The template to use instead of the endpoint configured. |  | String |

Chunk component will look for a specific template in the _themes_ folder with extensions _.chtml_ or \_.cxml. \_If you need to specify a different folder or extensions, you will need to use the specific options listed above.

## Usage

### Chunk Context

Camel will provide exchange information in the Chunk context (just a `Map`). The `Exchange` is transferred as:

 
| key | value |
| --- | --- |
| `exchange` | The `Exchange` itself. |
| `exchange.properties` | The `Exchange` properties. |
| `variables` | The variables |
| `headers` | The headers of the In message. |
| `camelContext` | The Camel Context. |
| `request` | The In message. |
| `body` | The In message body. |
| `response` | The Out message (only for InOut message exchange pattern). |

### Dynamic templates

Camel provides two headers by which you can define a different resource location for a template or the template content itself. If any of these headers is set, then Camel uses this over the endpoint configured resource. This allows you to provide a dynamic template at runtime.

## Examples

For example, you could use something like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("chunk:template");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="chunk:template"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: chunk:template
```

To use a Chunk template to formulate a response for a message for InOut message exchanges (where there is a `JMSReplyTo` header).

If you want to use InOnly and consume the message and send it to another destination, you could use:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("chunk:template")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="chunk:template"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: chunk:template
        - to:
            uri: activemq:Another.Queue
```

It’s possible to specify what template the component should use dynamically via a header, so for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("ChunkResourceUri").constant("template")
    .to("chunk:dummy?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="ChunkResourceUri">
    <constant>template</constant>
  </setHeader>
  <to uri="chunk:dummy?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: ChunkResourceUri
            expression:
              constant:
                expression: template
        - to:
            uri: chunk:dummy
            parameters:
              allowTemplateFromHeader: true
```

An example of Chunk component options use:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .to("chunk:file_example?themeFolder=template&themeSubfolder=subfolder&extension=chunk");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="chunk:file_example?themeFolder=template&amp;themeSubfolder=subfolder&amp;extension=chunk"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: chunk:file_example
            parameters:
              themeFolder: template
              themeSubfolder: subfolder
              extension: chunk
```

In this example, the Chunk component will look for the file `file_example.chunk` in the folder `template/subfolder`.

### The Email Example

In this sample, we want to use Chunk templating for an order confirmation email. The email template is laid out in Chunk as:

```text
Dear {$headers.lastName}, {$headers.firstName}

Thanks for the order of {$headers.item}.

Regards Camel Riders Bookstore
{$body}
```