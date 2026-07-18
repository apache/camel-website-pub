# Spring AI Image

**Since Camel 4.19**

**Only producer is supported**

The Spring AI Image component generates images from text prompts using any image model supported by [Spring AI](https://docs.spring.io/spring-ai/reference/), including OpenAI DALL-E, Stability AI, and local models via Ollama.

Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-ai-image</artifactId>
    <version>x.x.x</version>
</dependency>
```

## URI format

spring-ai-image:imageId\[?options\]

Where **imageId** can be any string to uniquely identify the endpoint.

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

The Spring AI Image component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration. |  | SpringAiImageConfiguration |
| **height** (producer) | Image height in pixels. |  | Integer |
| **imageModel** (producer) | **Autowired** **Required** The ImageModel to use for generating images. |  | ImageModel |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **model** (producer) | The model to use for image generation. |  | String |
| **n** (producer) | Number of images to generate. |  | Integer |
| **responseFormat** (producer) | Response format: url or b64\_json. |  | String |
| **style** (producer) | Image style (e.g., vivid, natural). |  | String |
| **width** (producer) | Image width in pixels. |  | Integer |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Spring AI Image endpoint is configured using URI syntax:

spring-ai-image:imageId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **imageId** (producer) | **Required** The id. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **height** (producer) | Image height in pixels. |  | Integer |
| **imageModel** (producer) | **Autowired** **Required** The ImageModel to use for generating images. |  | ImageModel |
| **model** (producer) | The model to use for image generation. |  | String |
| **n** (producer) | Number of images to generate. |  | Integer |
| **responseFormat** (producer) | Response format: url or b64\_json. |  | String |
| **style** (producer) | Image style (e.g., vivid, natural). |  | String |
| **width** (producer) | Image width in pixels. |  | Integer |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Spring AI Image component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSpringAiImageN** (producer) Constant: [`N`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-image/latest/org/apache/camel/component/springai/image/SpringAiImageHeaders.html#N) | Number of images to generate. |  | Integer |
| **CamelSpringAiImageWidth** (producer) Constant: [`WIDTH`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-image/latest/org/apache/camel/component/springai/image/SpringAiImageHeaders.html#WIDTH) | Image width in pixels. |  | Integer |
| **CamelSpringAiImageHeight** (producer) Constant: [`HEIGHT`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-image/latest/org/apache/camel/component/springai/image/SpringAiImageHeaders.html#HEIGHT) | Image height in pixels. |  | Integer |
| **CamelSpringAiImageModel** (producer) Constant: [`MODEL`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-image/latest/org/apache/camel/component/springai/image/SpringAiImageHeaders.html#MODEL) | The model to use for image generation. |  | String |
| **CamelSpringAiImageResponseFormat** (producer) Constant: [`RESPONSE_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-image/latest/org/apache/camel/component/springai/image/SpringAiImageHeaders.html#RESPONSE_FORMAT) | Response format: url or b64\_json. |  | String |
| **CamelSpringAiImageStyle** (producer) Constant: [`STYLE`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-image/latest/org/apache/camel/component/springai/image/SpringAiImageHeaders.html#STYLE) | Image style (e.g., vivid, natural). |  | String |
| **CamelSpringAiImageResponseMetadata** (producer) Constant: [`RESPONSE_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-image/latest/org/apache/camel/component/springai/image/SpringAiImageHeaders.html#RESPONSE_METADATA) | The image response metadata. |  | ImageResponseMetadata |
| **CamelSpringAiImageGeneration** (producer) Constant: [`IMAGE_GENERATION`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-image/latest/org/apache/camel/component/springai/image/SpringAiImageHeaders.html#IMAGE_GENERATION) | The ImageGeneration object for single image results. |  | ImageGeneration |
| **CamelSpringAiImageGenerations** (producer) Constant: [`IMAGE_GENERATIONS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-image/latest/org/apache/camel/component/springai/image/SpringAiImageHeaders.html#IMAGE_GENERATIONS) | List of ImageGeneration objects for multiple image results. |  | List |

## Usage

### Configuring the ImageModel

The component requires a Spring AI `ImageModel` bean. When using Spring Boot with a Spring AI starter (e.g., `spring-ai-starter-model-openai`), the `ImageModel` bean is auto-configured.

### Basic Image Generation

Send a text prompt as the message body to generate an image:

_Java-only: Java lambda Processor with Spring AI Image API_

```java
from("direct:generate")
    .setBody(constant("A camel walking through the desert at sunset"))
    .to("spring-ai-image:gen?imageModel=#imageModel")
    .log("Generated image: ${body.getClass().getSimpleName()}")
    .process(exchange -> {
        Image image = exchange.getIn().getBody(Image.class);
        String base64Data = image.getB64Json();  // Base64-encoded image bytes
        String imageUrl = image.getUrl();         // URL (provider-dependent)
        log.info("Image base64 length: {}, URL: {}",
            base64Data != null ? base64Data.length() : "N/A", imageUrl);
    });
```

The response body is a `org.springframework.ai.image.Image` object containing either base64-encoded image data (`b64Json`) or a URL (`url`), depending on the provider and `responseFormat` setting.

The component includes built-in type converters that automatically convert `Image` objects to `byte[]` (by decoding the base64 data), `InputStream`, or `String`. This means downstream components like `file:` can consume the image directly without any intermediate processing.

### Image Options

Control image generation parameters via endpoint configuration or headers. Headers override endpoint configuration at runtime.

#### Via Endpoint Configuration

_Java-only: Java string concatenation in URI_

```java
from("direct:generate")
    .to("spring-ai-image:gen?imageModel=#imageModel"
        + "&model=dall-e-3"
        + "&width=512&height=512"
        + "&responseFormat=b64_json"
        + "&style=vivid");
```

#### Via Headers

_Java-only: Java test API (ProducerTemplate with lambda)_

```java
Exchange exchange = template.request("direct:generate", e -> {
    e.getIn().setBody("A red apple on a white table");
    e.getIn().setHeader(SpringAiImageHeaders.WIDTH, 256);
    e.getIn().setHeader(SpringAiImageHeaders.HEIGHT, 256);
    e.getIn().setHeader(SpringAiImageHeaders.MODEL, "dall-e-3");
    e.getIn().setHeader(SpringAiImageHeaders.RESPONSE_FORMAT, "b64_json");
});
```

### Saving Images to Files

The component includes a built-in `TypeConverter` that automatically converts `Image` objects to `byte[]`. This means you can pipe generated images directly to the `file:` component without any intermediate processing:

-   Java
    
-   XML
    
-   YAML
    

```java
// Generate and save — no processor needed
from("direct:generate")
    .to("spring-ai-image:gen?imageModel=#imageModel&width=512&height=512")
    .to("file:output?fileName=generated.png");
```

```xml
<route>
    <from uri="direct:generate"/>
    <to uri="spring-ai-image:gen?imageModel=#imageModel&amp;width=512&amp;height=512"/>
    <to uri="file:output?fileName=generated.png"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:generate
    steps:
      - to:
          uri: spring-ai-image:gen
          parameters:
            imageModel: "#imageModel"
            width: 512
            height: 512
      - to:
          uri: file:output?fileName=generated.png
```

The `Image` → `byte[]` conversion decodes the base64 data automatically.

### Using with Ollama (Local Image Generation)

Ollama supports image generation models via its OpenAI-compatible API. Configure the Spring AI OpenAI `ImageModel` to point at Ollama:

_Java-only: Java Spring AI SDK configuration_

```java
// Ollama returns application/x-ndjson — register a converter that handles it
MappingJackson2HttpMessageConverter ndjsonConverter = new MappingJackson2HttpMessageConverter();
ndjsonConverter.setSupportedMediaTypes(
    List.of(MediaType.APPLICATION_JSON, MediaType.valueOf("application/x-ndjson")));

RestClient.Builder restClientBuilder = RestClient.builder()
    .messageConverters(converters -> converters.addFirst(ndjsonConverter));

OpenAiImageApi imageApi = OpenAiImageApi.builder()
    .baseUrl("http://localhost:11434")
    .apiKey("unused")
    .restClientBuilder(restClientBuilder)
    .build();

OpenAiImageOptions defaultOptions = OpenAiImageOptions.builder()
    .model("x/flux2-klein:4b")
    .build();

ImageModel imageModel = new OpenAiImageModel(imageApi, defaultOptions,
    RetryUtils.DEFAULT_RETRY_TEMPLATE);
```

Then use the Camel endpoint to control resolution:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:generate")
    .to("spring-ai-image:gen?imageModel=#imageModel&width=512&height=512")
    .to("file:output?fileName=camel-image.png");
```

```xml
<route>
    <from uri="direct:generate"/>
    <to uri="spring-ai-image:gen?imageModel=#imageModel&amp;width=512&amp;height=512"/>
    <to uri="file:output?fileName=camel-image.png"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:generate
    steps:
      - to:
          uri: spring-ai-image:gen
          parameters:
            imageModel: "#imageModel"
            width: 512
            height: 512
      - to:
          uri: file:output?fileName=camel-image.png
```

### Multiple Image Generation

Set the `n` parameter to generate multiple images. When `n > 1`, the body contains a `List<Image>` instead of a single `Image`:

_Java-only: Java test API (ProducerTemplate)_

```java
from("direct:batch")
    .to("spring-ai-image:gen?imageModel=#imageModel&n=3");

// Usage:
List<Image> images = template.requestBody("direct:batch",
    "A camel in different art styles", List.class);
```

### Type Converters

The component registers automatic type converters for `Image` objects:

  
| From | To | Behavior |
| --- | --- | --- |
| `Image` | `byte[]` | Decodes base64 data |
| `Image` | `InputStream` | Wraps decoded bytes in ByteArrayInputStream |
| `Image` | `String` | Returns base64 string or URL |

## See Also

-   [Spring AI Image API](https://docs.spring.io/spring-ai/reference/api/image.md)
    
-   [Spring AI Chat Component](spring-ai-chat-component.md)