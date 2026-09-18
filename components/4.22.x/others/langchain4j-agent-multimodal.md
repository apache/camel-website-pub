# LangChain4j Agent - Multimodal Content Support

[Back to LangChain4j Agent Component](../langchain4j-agent-component.md)

## Multimodal Content Support

The LangChain4j Agent component supports multimodal content, allowing you to send images, PDFs, audio, video, and text files to AI models that support vision and document understanding capabilities.

### Sending Multimodal Content via AiAgentBody

You can explicitly create an `AiAgentBody` with multimodal content:

_Java-only: `AiAgentBody` with `ImageContent`, `Files.readAllBytes()`, and ProducerTemplate test API_

```java
// Load an image and create ImageContent
byte[] imageBytes = Files.readAllBytes(Path.of("image.png"));
String base64Image = Base64.getEncoder().encodeToString(imageBytes);
Image image = Image.builder()
    .base64Data(base64Image)
    .mimeType("image/png")
    .build();
ImageContent imageContent = ImageContent.from(image);

// Create request body with image content
AiAgentBody<ImageContent> body = new AiAgentBody<ImageContent>()
    .withUserMessage("What do you see in this image?")
    .withContent(imageContent);

String response = template.requestBody("direct:chat", body, String.class);
```

### Automatic File Conversion from Camel Components

The agent component automatically converts files from various Camel components to multimodal content. This enables seamless integration with file-based sources.

#### Supported Input Types

  
| Input Type | Source Components | MIME Type Detection |
| --- | --- | --- |
| `WrappedFile` | `file:`, `ftp:`, `sftp:`, `smb:` | From file extension or headers |
| `byte[]` | `aws2-s3:`, `azure-storage-blob:`, `google-storage:` | From content type headers (required) |
| `InputStream` | Various streaming components | From content type headers (required) |

#### Example: Processing Images from File Component

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox/images?noop=true&include=.*\\.png")
    .setHeader("CamelLangChain4jAgentUserMessage", constant("Describe this image"))
    .to("langchain4j-agent:vision?agent=#visionAgent")
    .to("log:response");
```

```xml
<route>
  <from uri="file:inbox/images?noop=true&amp;include=.*\.png"/>
  <setHeader name="CamelLangChain4jAgentUserMessage">
    <constant>Describe this image</constant>
  </setHeader>
  <to uri="langchain4j-agent:vision?agent=#visionAgent"/>
  <to uri="log:response"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox/images
      parameters:
        noop: true
        include: ".*\\.png"
      steps:
        - setHeader:
            name: CamelLangChain4jAgentUserMessage
            constant: Describe this image
        - to:
            uri: langchain4j-agent:vision
            parameters:
              agent: "#visionAgent"
        - to:
            uri: log:response
```

#### Example: Processing Files from AWS S3

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws2-s3://my-bucket?prefix=images/&includeBody=true")
    .setHeader("CamelLangChain4jAgentUserMessage", constant("What do you see in this image?"))
    .to("langchain4j-agent:vision?agent=#visionAgent")
    .to("log:response");
```

```xml
<route>
  <from uri="aws2-s3://my-bucket?prefix=images/&amp;includeBody=true"/>
  <setHeader name="CamelLangChain4jAgentUserMessage">
    <constant>What do you see in this image?</constant>
  </setHeader>
  <to uri="langchain4j-agent:vision?agent=#visionAgent"/>
  <to uri="log:response"/>
</route>
```

```yaml
- route:
    from:
      uri: aws2-s3://my-bucket
      parameters:
        prefix: images/
        includeBody: true
      steps:
        - setHeader:
            name: CamelLangChain4jAgentUserMessage
            constant: "What do you see in this image?"
        - to:
            uri: langchain4j-agent:vision
            parameters:
              agent: "#visionAgent"
        - to:
            uri: log:response
```

> **Note**
> When using `byte[]` or `InputStream` inputs, a MIME type header is required since the type cannot be auto-detected from the content. The component checks for MIME type in this priority order:
>
> 1.  `CamelLangChain4jAgentMediaType` header (highest priority - explicit override)
>     
> 2.  `CamelAwsS3ContentType` header (from AWS S3)
>     
> 3.  `Content-Type` header
>     
> 4.  `CamelFileContentType` header (from file components)

#### Example: Overriding MIME Type

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:process-file")
    .setHeader("CamelLangChain4jAgentUserMessage", constant("Analyze this document"))
    .setHeader("CamelLangChain4jAgentMediaType", constant("application/pdf"))
    .to("langchain4j-agent:analyzer?agent=#analyzerAgent");
```

```xml
<route>
  <from uri="direct:process-file"/>
  <setHeader name="CamelLangChain4jAgentUserMessage">
    <constant>Analyze this document</constant>
  </setHeader>
  <setHeader name="CamelLangChain4jAgentMediaType">
    <constant>application/pdf</constant>
  </setHeader>
  <to uri="langchain4j-agent:analyzer?agent=#analyzerAgent"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:process-file
      steps:
        - setHeader:
            name: CamelLangChain4jAgentUserMessage
            constant: Analyze this document
        - setHeader:
            name: CamelLangChain4jAgentMediaType
            constant: application/pdf
        - to:
            uri: langchain4j-agent:analyzer
            parameters:
              agent: "#analyzerAgent"
```

### Complete Multimodal Route Example

Here’s a complete example showing how to process images from a file system and send them to an AI agent for analysis:

_Java-only: `ChatModel` and `AgentConfiguration` bean registration_

```java
// Create a vision-capable chat model
ChatModel chatModel = OpenAiChatModel.builder()
    .apiKey(apiKey)
    .modelName("gpt-4o")  // Vision-capable model
    .build();

// Create agent configuration
AgentConfiguration configuration = new AgentConfiguration()
    .withChatModel(chatModel);

Agent visionAgent = new AgentWithoutMemory(configuration);
context.getRegistry().bind("visionAgent", visionAgent);
```

Route to process images:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox/images?noop=true&include=.*\\.(png|jpg|jpeg)")
    .setHeader("CamelLangChain4jAgentUserMessage",
        constant("Describe what you see in this image. Be detailed but concise."))
    .to("langchain4j-agent:vision?agent=#visionAgent")
    .log("AI Response: ${body}")
    .to("file:outbox/descriptions");
```

```xml
<route>
  <from uri="file:inbox/images?noop=true&amp;include=.*\.(png|jpg|jpeg)"/>
  <setHeader name="CamelLangChain4jAgentUserMessage">
    <constant>Describe what you see in this image. Be detailed but concise.</constant>
  </setHeader>
  <to uri="langchain4j-agent:vision?agent=#visionAgent"/>
  <log message="AI Response: ${body}"/>
  <to uri="file:outbox/descriptions"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox/images
      parameters:
        noop: true
        include: ".*\\.(png|jpg|jpeg)"
      steps:
        - setHeader:
            name: CamelLangChain4jAgentUserMessage
            constant: "Describe what you see in this image. Be detailed but concise."
        - to:
            uri: langchain4j-agent:vision
            parameters:
              agent: "#visionAgent"
        - log:
            message: "AI Response: ${body}"
        - to:
            uri: file:outbox/descriptions
```