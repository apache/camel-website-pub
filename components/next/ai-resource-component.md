# AI Resource

**Since Camel 4.23**

**Only consumer is supported**

The AI Resource component exposes Camel routes as read-only resources that an AI client can fetch by uri. Where [AI Tool](ai-tool-component.md) models an action the model decides to invoke, a resource models content the client reads: a configuration file, a report on S3, a document on an FTP server.

Today the only adapter reading this registry is [camel-mcp-server](others/mcp-server.md), which publishes the selected resources over MCP `resources/list` and `resources/read`.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ai-resource</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

ai-resource:resourceName?resourceUri=uri\[&options\]

Where **resourceName** is the human-readable label shown in resource listings, and **resourceUri** is the address clients use to read the resource. The uri must be unique within the CamelContext. For a family of resources, use `uriTemplate` instead of `resourceUri`; the two options are mutually exclusive.

A `uriTemplate` follows RFC 6570 level 1: each variable must occupy an entire path segment, for example `crm://customers/{id}`. Variables do not match across `/` separators. A concrete variable must use RFC 3986 `pchar` characters (including well-formed percent-encoded octets); raw query/fragment characters, controls, malformed percent escapes, and `.` or `..` dot segments do not match. Fixed resources take precedence over a matching template when the same concrete URI is read. Tagged templates in one CamelContext must not overlap, even when they belong to different tags; a conflicting route fails startup rather than depending on registration order. A fixed `resourceUri` must not contain raw `{` or `}`; use `uriTemplate` for variable paths.

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

The AI Resource component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configuration** (consumer) | The component configuration. |  | AiResourceConfiguration |
| **description** (consumer) | Human-readable description of what this resource contains. Passed verbatim to the client. When omitted, defaults to the resource name. |  | String |
| **mimeType** (consumer) | MIME type of the content the route produces. Types denoting text, such as any text subtype, application/json, and any subtype ending in json, xml or yaml, are read as a string. Every other type is read as raw bytes and delivered to clients as a binary blob. | text/plain | String |
| **resourceUri** (consumer) | The fixed resource uri clients use to read this resource. Configure this or uriTemplate, but not both. The uri must be unique within the CamelContext. |  | String |
| **tags** (consumer) | Comma-separated list of tags used to group resources. Adapters filter the registry by these tags to select which resources to expose. When omitted, the resource goes into a default pool which camel-mcp-server never exposes. |  | String |
| **title** (consumer) | Optional display title for resource listings. Advisory hint for clients only. |  | String |
| **uriTemplate** (consumer) | RFC 6570 level 1 URI template. Each variable must occupy a whole path segment, for example crm://customers/{id}. Configure this or resourceUri, but not both. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The AI Resource endpoint is configured using URI syntax:

ai-resource:resourceName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceName** (consumer) | **Required** The resource name. This is the human-readable label clients see in resource listings. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** (consumer) | Human-readable description of what this resource contains. Passed verbatim to the client. When omitted, defaults to the resource name. |  | String |
| **mimeType** (consumer) | MIME type of the content the route produces. Types denoting text, such as any text subtype, application/json, and any subtype ending in json, xml or yaml, are read as a string. Every other type is read as raw bytes and delivered to clients as a binary blob. | text/plain | String |
| **resourceUri** (consumer) | The fixed resource uri clients use to read this resource. Configure this or uriTemplate, but not both. The uri must be unique within the CamelContext. |  | String |
| **tags** (consumer) | Comma-separated list of tags used to group resources. Adapters filter the registry by these tags to select which resources to expose. When omitted, the resource goes into a default pool which camel-mcp-server never exposes. |  | String |
| **title** (consumer) | Optional display title for resource listings. Advisory hint for clients only. |  | String |
| **uriTemplate** (consumer) | RFC 6570 level 1 URI template. Each variable must occupy a whole path segment, for example crm://customers/{id}. Configure this or resourceUri, but not both. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Message Headers

The AI Resource component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAiResourceUri** (consumer) Constant: [`RESOURCE_URI_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-ai-resource/latest/org/apache/camel/component/ai/resource/AiResource.html#RESOURCE_URI_HEADER) | Header containing the concrete URI requested for a resource-template read. |  | String |
| **CamelAiResourceTemplateVariable.** (consumer) Constant: [`TEMPLATE_VARIABLE_HEADER_PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-ai-resource/latest/org/apache/camel/component/ai/resource/AiResource.html#TEMPLATE_VARIABLE_HEADER_PREFIX) | Prefix for headers carrying raw, client-supplied template variables. |  | String |

## Message Body

The message body at each side of the AI Resource component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `null` | No request body is supplied. A template read carries the concrete requested URI and raw path-segment variables in the CamelAiResourceUri and CamelAiResourceTemplateVariable.\* headers. These values are untrusted client input and must be validated before use. |
| **Consumer reply** | `text`, `bytes`, `stream` or `file` | The content the route ends with: converted to a String when the mimeType is textual (the default text/plain, json, xml, yaml), else to a byte\[\] sent as a blob. A Map, a List or another object is sent as its toString as text and fails as a blob: marshal it first. No body is an error. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

A resource read carries no arguments: the route is invoked with an empty exchange and its message body is the content returned to the client. Retrieval therefore uses whatever Camel already offers for reading on demand: a producer with a read operation (`aws2-s3` with `operation=getObject`), or `pollEnrich` for the polling components (`file`, `ftp`, `sftp`), whose producers write rather than read.

Always give `pollEnrich` an explicit `timeout` - it is a parameter of the EIP, not an endpoint option. It defaults to `-1`, which waits until a message is available and parks the route thread for good when the file is not there. The client is still answered - the read returns a timeout error after `camel.server.mcp-resource-timeout` - but the route stays blocked. Note also that `noop=true` implies `idempotent=true`, so `idempotent=false` is what keeps the same file readable on every request.

### Textual resource

-   Java
    
-   XML
    
-   YAML
    

```java
from("ai-resource:app_config"
    + "?resourceUri=camel:///config/app.json"
    + "&tags=crm"
    + "&description=Current application configuration"
    + "&mimeType=application/json")
    .pollEnrich("file:config?fileName=app.json&noop=true&idempotent=false", 5000);
```

```xml
<route>
  <from uri="ai-resource:app_config?resourceUri=camel:///config/app.json&amp;tags=crm&amp;description=Current application configuration&amp;mimeType=application/json"/>
  <pollEnrich timeout="5000">
    <constant>file:config?fileName=app.json&amp;noop=true&amp;idempotent=false</constant>
  </pollEnrich>
</route>
```

```yaml
- route:
    from:
      uri: ai-resource:app_config
      parameters:
        resourceUri: "camel:///config/app.json"
        tags: crm
        description: "Current application configuration"
        mimeType: application/json
      steps:
        - pollEnrich:
            timeout: 5000
            expression:
              constant:
                expression: "file:config?fileName=app.json&noop=true&idempotent=false"
```

### Templated resource

Use `uriTemplate` when one route serves a family of client-addressable resources. The example below exposes `crm://customers/{id}` and makes the concrete URI and captured variable available to the route:

```java
from("ai-resource:customer?uriTemplate=crm://customers/{id}&tags=crm")
    .process(exchange -> {
        String customerId = exchange.getMessage().getHeader(
            "CamelAiResourceTemplateVariable.id", String.class);
        String requestedUri = exchange.getMessage().getHeader("CamelAiResourceUri", String.class);
        // Validate customerId against the application's identifier rules before using it.
        exchange.getMessage().setBody("Customer " + customerId + " requested as " + requestedUri);
    });
```

For each template read, Camel sets `CamelAiResourceUri` to the concrete URI sent by the client and sets one header per variable using the prefix `CamelAiResourceTemplateVariable.` followed by the variable name. Variable values are passed as raw strings; percent-encoding is retained. These values are untrusted client input. Validate them against an allowlist or strict format before using them to build file paths, database queries or downstream URIs. Do not treat them as Camel property placeholders or evaluate them as expressions.

### Binary resource

The `mimeType` decides how the route body is read. Types denoting text, such as any `text` subtype, `application/json`, and any subtype ending in `json`, `xml` or `yaml`, are converted to a string. Every other type is read as `byte[]` and delivered to the client as a binary blob.

```java
from("ai-resource:latest_report"
    + "?resourceUri=s3://reports/latest.pdf"
    + "&tags=crm"
    + "&description=Latest sales report"
    + "&mimeType=application/pdf")
    .to("aws2-s3://reports?keyName=latest.pdf&operation=getObject");
```

## Tags and exposure

Tags group resources so that an adapter can select which ones to expose. A resource without tags goes into a default pool that `camel-mcp-server` never exposes: crossing the boundary to a remote client is an explicit per-route opt-in. See the [MCP server](others/mcp-server.md) documentation for how the tag patterns are configured.

## Lifecycle

A resource is registered when its route starts or resumes and deregistered when the route stops or suspends. Adapters that support it turn those events into `notifications/resources/list_changed`, so clients see the resource list follow the routes.