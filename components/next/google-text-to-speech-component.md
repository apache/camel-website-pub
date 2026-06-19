# Google Cloud Text To Speech

**Since Camel 4.19**

**Only producer is supported**

The Google Cloud Text-to-Speech component provides access to [Google Cloud Text-to-Speech API](https://cloud.google.com/text-to-speech) via the [Google Cloud Text-to-Speech Client for Java](https://github.com/googleapis/java-texttospeech).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-text-to-speech</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

## Authentication Configuration

Google Cloud Text-to-Speech component authentication is targeted for use with the GCP Service Accounts. For more information, please refer to [Google Cloud Authentication](https://github.com/googleapis/google-cloud-java#authentication).

When you have the **service account key**, you can provide authentication credentials to your application code. Google security credentials can be set through the component endpoint:

_Java-only: constructing the endpoint URI programmatically_

```java
String endpoint = "google-text-to-speech://synthesize?serviceAccountKey=/home/user/Downloads/my-key.json";
```

Or by setting the environment variable `GOOGLE_APPLICATION_CREDENTIALS` :

export GOOGLE\_APPLICATION\_CREDENTIALS="/home/user/Downloads/my-key.json"

## URI Format

google-text-to-speech://operation\[?options\]

You can append query options to the URI in the following format, `?options=value&option2=value&…​`

For example, in order to synthesize speech from text, use the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("google-text-to-speech://synthesize?serviceAccountKey=/home/user/Downloads/my-key.json");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="google-text-to-speech://synthesize?serviceAccountKey=/home/user/Downloads/my-key.json"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: google-text-to-speech://synthesize
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

The Google Cloud Text To Speech component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Google Cloud Text To Speech endpoint is configured using URI syntax:

google-text-to-speech:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (common) | **Required** The operation name. |  | String |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceAccountKey** (common) | Service account key to authenticate an application as a service account. |  | String |
| **audioEncoding** (producer) | The audio encoding of the output. Supported values: MP3, LINEAR16, OGG\_OPUS, MULAW, ALAW. | MP3 | String |
| **languageCode** (producer) | The language code for the voice (e.g., en-US, fr-FR). | en-US | String |
| **pitch** (producer) | The pitch, from -20.0 to 20.0 semitones. Default is 0.0. |  | Double |
| **pojoRequest** (producer) | Specifies if the request is a pojo request. | false | boolean |
| **speakingRate** (producer) | The speaking rate, from 0.25 to 4.0. Default is 1.0. |  | Double |
| **voiceName** (producer) | The name of the voice. If not set, the service selects a default voice for the specified language. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (advanced) | **Autowired** The client to use during service invocation. |  | TextToSpeechClient |

## Message Headers

The Google Cloud Text To Speech component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleCloudTextToSpeechOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-text-to-speech/latest/org/apache/camel/component/google/texttospeech/GoogleCloudTextToSpeechConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   synthesize
    
-   listVoices
    





 |  | GoogleCloudTextToSpeechOperations |
| **CamelGoogleCloudTextToSpeechResponseObject** (producer) Constant: [`RESPONSE_OBJECT`](https://javadoc.io/doc/org.apache.camel/camel-google-text-to-speech/latest/org/apache/camel/component/google/texttospeech/GoogleCloudTextToSpeechConstants.html#RESPONSE_OBJECT) | The response object resulting from the Google Cloud Text-to-Speech API invocation. |  | SynthesizeSpeechResponse |

## Usage

### Message body

For the `synthesize` operation, the message body should contain the text to synthesize as a `String`.

For the `listVoices` operation, the message body is ignored.

When `pojoRequest=true`, the body should be a `com.google.cloud.texttospeech.v1.SynthesizeSpeechRequest` instance instead.

### Google Cloud Text-to-Speech Producer operations

Google Cloud Text-to-Speech component provides the following operations on the producer side:

-   synthesize
    
-   listVoices
    

The operation is specified as part of the endpoint URI (e.g., `google-text-to-speech://synthesize`). You can override the operation at runtime by setting the `GoogleCloudTextToSpeechOperation` message header.

### Advanced component configuration

If you need to have more control over the `TextToSpeechClient` instance configuration, you can create your own instance and refer to it in your Camel google-text-to-speech component configuration:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("google-text-to-speech://synthesize?client=#myTextToSpeechClient");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="google-text-to-speech://synthesize?client=#myTextToSpeechClient"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: google-text-to-speech://synthesize
            parameters:
              client: "#myTextToSpeechClient"
```

### Google Cloud Text-to-Speech Producer Operation examples

-   `synthesize`: this operation converts text to speech audio. The message body should contain the text to synthesize as a `String`.
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("Hello, how are you today?"))
    .to("google-text-to-speech://synthesize?serviceAccountKey=/home/user/Downloads/my-key.json&languageCode=en-US&audioEncoding=MP3")
    .log("body:${body}")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <constant>Hello, how are you today?</constant>
  </setBody>
  <to uri="google-text-to-speech://synthesize?serviceAccountKey=/home/user/Downloads/my-key.json&amp;languageCode=en-US&amp;audioEncoding=MP3"/>
  <log message="body:${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            constant: "Hello, how are you today?"
        - to:
            uri: google-text-to-speech://synthesize
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
              languageCode: en-US
              audioEncoding: MP3
        - log:
            message: "body:${body}"
        - to:
            uri: mock:result
```

This operation will return a `byte[]` containing the synthesized audio content.

-   `synthesize` with voice customization:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("Bonjour, comment allez-vous?"))
    .to("google-text-to-speech://synthesize?serviceAccountKey=/home/user/Downloads/my-key.json&languageCode=fr-FR&voiceName=fr-FR-Wavenet-A&audioEncoding=OGG_OPUS&speakingRate=1.2&pitch=-2.0")
    .log("body:${body}")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <constant>Bonjour, comment allez-vous?</constant>
  </setBody>
  <to uri="google-text-to-speech://synthesize?serviceAccountKey=/home/user/Downloads/my-key.json&amp;languageCode=fr-FR&amp;voiceName=fr-FR-Wavenet-A&amp;audioEncoding=OGG_OPUS&amp;speakingRate=1.2&amp;pitch=-2.0"/>
  <log message="body:${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            constant: "Bonjour, comment allez-vous?"
        - to:
            uri: google-text-to-speech://synthesize
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
              languageCode: fr-FR
              voiceName: fr-FR-Wavenet-A
              audioEncoding: OGG_OPUS
              speakingRate: 1.2
              pitch: -2.0
        - log:
            message: "body:${body}"
        - to:
            uri: mock:result
```

This operation will return a `byte[]` with the audio in OGG\_OPUS format using a specific French voice.

-   `listVoices`: this operation lists available voices
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("google-text-to-speech://listVoices?serviceAccountKey=/home/user/Downloads/my-key.json&languageCode=en-US")
    .log("body:${body}")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="google-text-to-speech://listVoices?serviceAccountKey=/home/user/Downloads/my-key.json&amp;languageCode=en-US"/>
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
            uri: google-text-to-speech://listVoices
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
              languageCode: en-US
        - log:
            message: "body:${body}"
        - to:
            uri: mock:result
```

This operation will return a `List<Voice>` with the available voices for the specified language.

-   Using POJO request for full control:
    

_Java-only: Google Cloud SDK SynthesizeSpeechRequest builder_

```java
from("direct:start")
    .process(exchange -> {
        SynthesisInput input = SynthesisInput.newBuilder()
            .setText("Hello world")
            .build();
        VoiceSelectionParams voice = VoiceSelectionParams.newBuilder()
            .setLanguageCode("en-US")
            .setName("en-US-Wavenet-D")
            .build();
        AudioConfig audioConfig = AudioConfig.newBuilder()
            .setAudioEncoding(AudioEncoding.MP3)
            .build();
        SynthesizeSpeechRequest request = SynthesizeSpeechRequest.newBuilder()
            .setInput(input)
            .setVoice(voice)
            .setAudioConfig(audioConfig)
            .build();
        exchange.getIn().setBody(request);
    })
    .to("google-text-to-speech://synthesize?serviceAccountKey=/home/user/Downloads/my-key.json&pojoRequest=true")
    .log("body:${body}")
    .to("mock:result");
```

When using `pojoRequest=true`, the body should be a `SynthesizeSpeechRequest` and the audio bytes are returned as body.

-   Overriding the operation at runtime via header:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("Hello world"))
    .setHeader("CamelGoogleCloudTextToSpeechOperation", constant("synthesize"))
    .to("google-text-to-speech://listVoices?serviceAccountKey=/home/user/Downloads/my-key.json")
    .log("body:${body}")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <constant>Hello world</constant>
  </setBody>
  <setHeader name="CamelGoogleCloudTextToSpeechOperation">
    <constant>synthesize</constant>
  </setHeader>
  <to uri="google-text-to-speech://listVoices?serviceAccountKey=/home/user/Downloads/my-key.json"/>
  <log message="body:${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            constant: Hello world
        - setHeader:
            name: CamelGoogleCloudTextToSpeechOperation
            constant: synthesize
        - to:
            uri: google-text-to-speech://listVoices
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
        - log:
            message: "body:${body}"
        - to:
            uri: mock:result
```