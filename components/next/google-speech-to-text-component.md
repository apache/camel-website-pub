# Google Cloud Speech To Text

**Since Camel 4.19**

**Only producer is supported**

The Google Cloud Speech To Text component provides access to [Google Cloud Speech-to-Text API](https://cloud.google.com/speech-to-text) via the [Google Cloud Speech Client for Java](https://github.com/googleapis/java-speech).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-speech-to-text</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

## Authentication Configuration

Google Cloud Speech To Text component authentication is targeted for use with the GCP Service Accounts. For more information, please refer to [Google Cloud Authentication](https://github.com/googleapis/google-cloud-java#authentication).

When you have the **service account key**, you can provide authentication credentials to your application code. Google security credentials can be set through the component endpoint:

_Java-only: constructing the endpoint URI programmatically_

```java
String endpoint = "google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json";
```

Or by setting the environment variable `GOOGLE_APPLICATION_CREDENTIALS` :

export GOOGLE\_APPLICATION\_CREDENTIALS="/home/user/Downloads/my-key.json"

## URI Format

google-speech-to-text://operation\[?options\]

You can append query options to the URI in the following format, `?options=value&option2=value&…​`

For example, in order to perform speech recognition on audio data, use the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: google-speech-to-text://recognize
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
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

The Google Cloud Speech To Text component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Google Cloud Speech To Text endpoint is configured using URI syntax:

google-speech-to-text:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (common) | **Required** The operation name. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceAccountKey** (common) | Service account key to authenticate an application as a service account. |  | String |
| **encoding** (producer) | The encoding of the audio data. Supported values: LINEAR16, FLAC, MULAW, AMR, AMR\_WB, OGG\_OPUS, SPEEX\_WITH\_HEADER\_BYTE, WEBM\_OPUS, MP3. | LINEAR16 | String |
| **languageCode** (producer) | The language of the audio data as a BCP-47 language tag (e.g., en-US, fr-FR). | en-US | String |
| **pojoRequest** (producer) | Specifies if the request is a pojo request. | false | boolean |
| **sampleRateHertz** (producer) | The sample rate in Hertz of the audio data. Valid values range from 8000 to 48000. |  | Integer |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (advanced) | **Autowired** The client to use during service invocation. |  | SpeechClient |

## Message Headers

The Google Cloud Speech To Text component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleCloudSpeechToTextOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-speech-to-text/latest/org/apache/camel/component/google/speechtotext/GoogleCloudSpeechToTextConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   recognize
    





 |  | GoogleCloudSpeechToTextOperations |
| **CamelGoogleCloudSpeechToTextResponseObject** (producer) Constant: [`RESPONSE_OBJECT`](https://javadoc.io/doc/org.apache.camel/camel-google-speech-to-text/latest/org/apache/camel/component/google/speechtotext/GoogleCloudSpeechToTextConstants.html#RESPONSE_OBJECT) | The response object resulting from the Google Cloud Speech-to-Text API invocation. |  | RecognizeResponse |

## Usage

### Message body

The message body should contain the audio data as a `byte[]`.

When `pojoRequest=true`, the body should be a `com.google.cloud.speech.v1.RecognizeRequest` instance instead.

### Google Cloud Speech To Text Producer operations

Google Cloud Speech To Text component provides the following operation on the producer side:

-   recognize
    

The operation is specified as part of the endpoint URI (e.g., `google-speech-to-text://recognize`). You can override the operation at runtime by setting the `GoogleCloudSpeechToTextOperation` message header.

### Advanced component configuration

If you need to have more control over the `SpeechClient` instance configuration, you can create your own instance and refer to it in your Camel google-speech-to-text component configuration:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("google-speech-to-text://recognize?client=#mySpeechClient");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="google-speech-to-text://recognize?client=#mySpeechClient"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: google-speech-to-text://recognize
            parameters:
              client: "#mySpeechClient"
```

### Google Cloud Speech To Text Producer Operation examples

-   `recognize`: this operation transcribes audio data to text. The message body should contain the audio data as a `byte[]`.
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json&encoding=LINEAR16&sampleRateHertz=16000&languageCode=en-US")
    .log("body:${body}")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json&amp;encoding=LINEAR16&amp;sampleRateHertz=16000&amp;languageCode=en-US"/>
  <log message="body:${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: google-speech-to-text://recognize
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
              encoding: LINEAR16
              sampleRateHertz: 16000
              languageCode: en-US
        - log:
            message: "body:${body}"
        - to:
            uri: mock:result
```

This operation will return the transcribed text as a `String`. The full `RecognizeResponse` is available via the `GoogleCloudSpeechToTextResponseObject` message header.

-   Using different audio encodings:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json&encoding=FLAC&languageCode=fr-FR")
    .log("body:${body}")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json&amp;encoding=FLAC&amp;languageCode=fr-FR"/>
  <log message="body:${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: google-speech-to-text://recognize
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
              encoding: FLAC
              languageCode: fr-FR
        - log:
            message: "body:${body}"
        - to:
            uri: mock:result
```

-   Using POJO request for full control:
    

_Java-only: Google Cloud SDK RecognizeRequest builder_

```java
from("direct:start")
    .process(exchange -> {
        RecognitionConfig config = RecognitionConfig.newBuilder()
            .setEncoding(RecognitionConfig.AudioEncoding.LINEAR16)
            .setSampleRateHertz(16000)
            .setLanguageCode("en-US")
            .build();
        RecognitionAudio audio = RecognitionAudio.newBuilder()
            .setContent(ByteString.copyFrom(audioData))
            .build();
        RecognizeRequest request = RecognizeRequest.newBuilder()
            .setConfig(config)
            .setAudio(audio)
            .build();
        exchange.getIn().setBody(request);
    })
    .to("google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json&pojoRequest=true")
    .log("body:${body}")
    .to("mock:result");
```

When using `pojoRequest=true`, the body should be a `RecognizeRequest` and the transcribed text is returned as the body.

-   Overriding the operation at runtime via header:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelGoogleCloudSpeechToTextOperation", constant("recognize"))
    .to("google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json")
    .log("body:${body}")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelGoogleCloudSpeechToTextOperation">
    <constant>recognize</constant>
  </setHeader>
  <to uri="google-speech-to-text://recognize?serviceAccountKey=/home/user/Downloads/my-key.json"/>
  <log message="body:${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelGoogleCloudSpeechToTextOperation
            constant: recognize
        - to:
            uri: google-speech-to-text://recognize
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
        - log:
            message: "body:${body}"
        - to:
            uri: mock:result
```