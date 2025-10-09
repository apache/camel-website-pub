# IBM Watson Text to Speech

**Since Camel 4.17**

**Only producer is supported**

The IBM Watson Text to Speech component allows you to convert written text into natural-sounding speech using [IBM Watson Text to Speech service](https://cloud.ibm.com/catalog/services/text-to-speech).

Prerequisites

You must have a valid IBM Cloud account and an instance of the Watson Text to Speech service. More information is available at [IBM Watson Text to Speech](https://cloud.ibm.com/catalog/services/text-to-speech).

## URI Format

ibm-watson-text-to-speech:label\[?options\]

You can append query options to the URI in the following format:

`?option=value&option2=value&…​`

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

The IBM Watson Text to Speech component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceUrl** (common) | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **accept** (producer) | The audio format for synthesized speech. Default is audio/wav. Supported formats: audio/wav, audio/mp3, audio/ogg, audio/flac, audio/webm. | audio/wav | String |
| **configuration** (producer) | Component configuration. |  | WatsonTextToSpeechConfiguration |
| **customizationId** (producer) | The customization ID (GUID) of a custom voice model to use for synthesis. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   synthesize
    
-   listVoices
    
-   getVoice
    
-   listCustomModels
    
-   getCustomModel
    
-   getPronunciation
    





 |  | WatsonTextToSpeechOperations |
| **voice** (producer) | The voice to use for synthesis. Default is en-US\_MichaelV3Voice. Examples: en-US\_AllisonV3Voice, en-GB\_KateV3Voice, es-ES\_EnriqueV3Voice, fr-FR\_NicolasV3Voice. | en-US\_MichaelV3Voice | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **apiKey** (security) | **Required** The IBM Cloud API key for authentication. |  | String |

## Endpoint Options

The IBM Watson Text to Speech endpoint is configured using URI syntax:

ibm-watson-text-to-speech:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceUrl** (common) | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **accept** (producer) | The audio format for synthesized speech. Default is audio/wav. Supported formats: audio/wav, audio/mp3, audio/ogg, audio/flac, audio/webm. | audio/wav | String |
| **customizationId** (producer) | The customization ID (GUID) of a custom voice model to use for synthesis. |  | String |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   synthesize
    
-   listVoices
    
-   getVoice
    
-   listCustomModels
    
-   getCustomModel
    
-   getPronunciation
    





 |  | WatsonTextToSpeechOperations |
| **voice** (producer) | The voice to use for synthesis. Default is en-US\_MichaelV3Voice. Examples: en-US\_AllisonV3Voice, en-GB\_KateV3Voice, es-ES\_EnriqueV3Voice, fr-FR\_NicolasV3Voice. | en-US\_MichaelV3Voice | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiKey** (security) | **Required** The IBM Cloud API key for authentication. |  | String |

## Message Headers

The IBM Watson Text to Speech component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIBMWatsonTTSOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelIBMWatsonTTSText** (producer) Constant: [`TEXT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#TEXT) | The text to synthesize into speech. |  | String |
| **CamelIBMWatsonTTSVoice** (producer) Constant: [`VOICE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#VOICE) | The voice to use for synthesis. |  | String |
| **CamelIBMWatsonTTSAccept** (producer) Constant: [`ACCEPT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#ACCEPT) | The audio format (e.g., audio/wav, audio/mp3, audio/ogg). |  | String |
| **CamelIBMWatsonTTSCustomizationId** (producer) Constant: [`CUSTOMIZATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#CUSTOMIZATION_ID) | The customization ID for a custom voice model. |  | String |
| **CamelIBMWatsonTTSWord** (producer) Constant: [`WORD`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#WORD) | The word for which to get pronunciation. |  | String |
| **CamelIBMWatsonTTSFormat** (producer) Constant: [`FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#FORMAT) | The pronunciation format (ipa or ibm). |  | String |
| **CamelIBMWatsonTTSLanguage** (producer) Constant: [`LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#LANGUAGE) | The language for filtering custom models. |  | String |
| **CamelIBMWatsonTTSModelId** (producer) Constant: [`MODEL_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#MODEL_ID) | The custom model ID. |  | String |
| **CamelIBMWatsonTTSVoiceName** (producer) Constant: [`VOICE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-text-to-speech/latest/org/apache/camel/component/ibm/watson/tts/WatsonTextToSpeechConstants.html#VOICE_NAME) | The name of the voice. |  | String |

Required Watson Text to Speech component options

You must provide the `apiKey` to access IBM Watson Text to Speech. Optionally, you can specify a custom `serviceUrl` if you’re using a dedicated or private instance.

## Usage

### Watson Text to Speech Producer operations

The IBM Watson Text to Speech component provides the following operations:

-   synthesize - Convert text to speech audio
    
-   listVoices - Get available voices for synthesis
    
-   getVoice - Get information about a specific voice
    
-   listCustomModels - List custom voice models
    
-   getCustomModel - Get information about a custom voice model
    
-   getPronunciation - Get pronunciation for a specific word
    

If you don’t specify an operation explicitly, you must set it via the `operation` parameter.

## Examples

### Synthesize Text to Speech

Convert text to speech using the default voice:

```java
from("direct:start")
  .setHeader(WatsonTextToSpeechConstants.TEXT, constant("Hello, welcome to IBM Watson Text to Speech!"))
  .to("ibm-watson-text-to-speech:myTTS?apiKey=RAW(yourApiKey)&operation=synthesize")
  .to("file:/var/audio?fileName=output.wav");
```

This will synthesize the text and produce an audio WAV file.

### Synthesize with Custom Voice

Convert text to speech using a specific voice:

```java
from("direct:start")
  .setBody(constant("Bonjour, bienvenue sur IBM Watson!"))
  .to("ibm-watson-text-to-speech:myTTS?apiKey=RAW(yourApiKey)&operation=synthesize&voice=fr-FR_NicolasV3Voice&accept=audio/mp3")
  .to("file:/var/audio?fileName=output.mp3");
```

This will synthesize French text using the Nicolas voice and produce an MP3 file.

### Available Voices

Some commonly used voices include:

-   English (US): en-US\_AllisonV3Voice, en-US\_MichaelV3Voice, en-US\_LisaV3Voice
    
-   English (UK): en-GB\_KateV3Voice, en-GB\_CharlotteV3Voice
    
-   Spanish (ES): es-ES\_EnriqueV3Voice, es-ES\_LauraV3Voice
    
-   French (FR): fr-FR\_NicolasV3Voice, fr-FR\_ReneeV3Voice
    
-   German (DE): de-DE\_BirgitV3Voice, de-DE\_DieterV3Voice
    
-   Italian (IT): it-IT\_FrancescaV3Voice
    
-   Japanese (JP): ja-JP\_EmiV3Voice
    
-   Portuguese (BR): pt-BR\_IsabelaV3Voice
    

### List Available Voices

Get a list of all available voices:

```java
from("direct:listVoices")
  .to("ibm-watson-text-to-speech:myTTS?apiKey=RAW(yourApiKey)&operation=listVoices")
  .process(exchange -> {
      List<Voice> voices = exchange.getMessage().getBody(List.class);
      voices.forEach(voice -> {
          System.out.println("Voice: " + voice.getName() +
                           " - Language: " + voice.getLanguage() +
                           " - Description: " + voice.getDescription());
      });
  });
```

### Get Voice Information

Get detailed information about a specific voice:

```java
from("direct:getVoice")
  .setHeader(WatsonTextToSpeechConstants.VOICE_NAME, constant("en-US_AllisonV3Voice"))
  .to("ibm-watson-text-to-speech:myTTS?apiKey=RAW(yourApiKey)&operation=getVoice")
  .process(exchange -> {
      Voice voice = exchange.getMessage().getBody(Voice.class);
      System.out.println("Voice details: " + voice);
  });
```

### Audio Format Options

The component supports various audio formats via the `accept` parameter:

-   audio/wav (default) - WAV format, uncompressed
    
-   audio/mp3 - MP3 format, compressed
    
-   audio/ogg - Ogg Vorbis format
    
-   audio/flac - FLAC format, lossless compression
    
-   audio/webm - WebM format
    

Example with MP3 output:

```java
from("direct:mp3")
  .setBody(constant("This will be an MP3 file"))
  .to("ibm-watson-text-to-speech:myTTS?apiKey=RAW(yourApiKey)&operation=synthesize&accept=audio/mp3")
  .to("file:/var/audio?fileName=speech.mp3");
```

### Using Custom Voice Models

If you have created a custom voice model, you can use it for synthesis:

```java
from("direct:customVoice")
  .setBody(constant("Text to synthesize with custom voice"))
  .setHeader(WatsonTextToSpeechConstants.CUSTOMIZATION_ID, constant("your-customization-guid"))
  .to("ibm-watson-text-to-speech:myTTS?apiKey=RAW(yourApiKey)&operation=synthesize")
  .to("file:/var/audio");
```

### List Custom Models

List all your custom voice models:

```java
from("direct:listCustomModels")
  .to("ibm-watson-text-to-speech:myTTS?apiKey=RAW(yourApiKey)&operation=listCustomModels")
  .process(exchange -> {
      List<CustomModel> models = exchange.getMessage().getBody(List.class);
      models.forEach(model -> {
          System.out.println("Model: " + model.getCustomizationId() +
                           " - Name: " + model.getName() +
                           " - Language: " + model.getLanguage());
      });
  });
```

### Get Pronunciation

Get the pronunciation for a specific word:

```java
from("direct:pronunciation")
  .setHeader(WatsonTextToSpeechConstants.WORD, constant("synthesize"))
  .setHeader(WatsonTextToSpeechConstants.FORMAT, constant("ipa"))
  .to("ibm-watson-text-to-speech:myTTS?apiKey=RAW(yourApiKey)&operation=getPronunciation")
  .process(exchange -> {
      Pronunciation pronunciation = exchange.getMessage().getBody(Pronunciation.class);
      System.out.println("IPA Pronunciation: " + pronunciation.getPronunciation());
  });
```

### Watson Text to Speech Authentication

IBM Watson Text to Speech uses IBM Cloud IAM (Identity and Access Management) for authentication. You need to provide your IBM Cloud API key.

You can create API keys in the IBM Cloud console: 1. Go to [https://cloud.ibm.com/iam/apikeys](https://cloud.ibm.com/iam/apikeys) 2. Click "Create an IBM Cloud API key" 3. Copy the API key and use it in your Camel routes

For more information about authentication, see the [IBM Watson TTS documentation](https://cloud.ibm.com/docs/text-to-speech?topic=text-to-speech-getting-started).

### Watson Text to Speech Endpoints

If you have a dedicated or regional instance, you can specify a custom service URL:

```java
from("direct:start")
  .setBody(constant("Hello World"))
  .to("ibm-watson-text-to-speech:myTTS?apiKey=RAW(yourApiKey)&serviceUrl=https://api.eu-gb.text-to-speech.watson.cloud.ibm.com&operation=synthesize")
  .to("file:/var/audio");
```

Common regional endpoints: - Dallas: [https://api.us-south.text-to-speech.watson.cloud.ibm.com](https://api.us-south.text-to-speech.watson.cloud.ibm.com) - Washington DC: [https://api.us-east.text-to-speech.watson.cloud.ibm.com](https://api.us-east.text-to-speech.watson.cloud.ibm.com) - Frankfurt: [https://api.eu-de.text-to-speech.watson.cloud.ibm.com](https://api.eu-de.text-to-speech.watson.cloud.ibm.com) - London: [https://api.eu-gb.text-to-speech.watson.cloud.ibm.com](https://api.eu-gb.text-to-speech.watson.cloud.ibm.com) - Tokyo: [https://api.jp-tok.text-to-speech.watson.cloud.ibm.com](https://api.jp-tok.text-to-speech.watson.cloud.ibm.com) - Sydney: [https://api.au-syd.text-to-speech.watson.cloud.ibm.com](https://api.au-syd.text-to-speech.watson.cloud.ibm.com)

## Integration Tests

This component includes comprehensive integration tests that validate the functionality against the actual IBM Watson Text to Speech service. These tests are disabled by default to prevent accidental API calls during regular builds.

### Prerequisites for Running Integration Tests

1.  **IBM Cloud Account**: You need a valid IBM Cloud account
    
2.  **Watson Text to Speech Service**: Create a Watson Text to Speech service instance in IBM Cloud
    
3.  **API Credentials**: Obtain your API key and service URL from the IBM Cloud console
    

To get your credentials:

1.  Log in to [IBM Cloud Console](https://cloud.ibm.com/)
    
2.  Navigate to your Text to Speech service instance
    
3.  Go to "Manage" → "Credentials"
    
4.  Copy your **API Key** and **Service URL**
    

### Running Integration Tests

Integration tests are executed with the `verify` goal and require system properties:

```bash
mvn verify \
  -Dcamel.ibm.watson.tts.apiKey=YOUR_API_KEY \
  -Dcamel.ibm.watson.tts.serviceUrl=YOUR_SERVICE_URL
```

Alternatively, using environment variables:

```bash
export CAMEL_IBM_WATSON_TTS_API_KEY=YOUR_API_KEY
export CAMEL_IBM_WATSON_TTS_SERVICE_URL=YOUR_SERVICE_URL

mvn verify \
  -Dcamel.ibm.watson.tts.apiKey=${CAMEL_IBM_WATSON_TTS_API_KEY} \
  -Dcamel.ibm.watson.tts.serviceUrl=${CAMEL_IBM_WATSON_TTS_SERVICE_URL}
```

### Integration Test Coverage

The integration tests cover all major operations:

**Synthesis Operations:**

-   Basic text-to-speech with default voice
    
-   Text-to-speech with custom voices (Allison, Michael, Kate)
    
-   Multiple audio formats (WAV, MP3)
    
-   Multiple languages (English, Spanish, French, German)
    
-   Longer text passages
    

**Voice Operations:**

-   Listing all available voices
    
-   Getting detailed information about specific voices
    

**Pronunciation Operations:**

-   Getting IPA pronunciation for words
    

**File Output Operations:**

-   Saving synthesized speech to MP3 files
    
-   Saving synthesized speech to WAV files
    
-   Creating audio files with different voices
    
-   Creating multilingual audio files
    

### Generated Audio Files

When integration tests run successfully, audio files are created in `target/audio-output/`:

-   `test-output.mp3` - Sample MP3 file
    
-   `test-output.wav` - Sample WAV file
    
-   `michael.mp3`, `allison.mp3`, `kate.mp3` - Different voice samples
    
-   `english.mp3`, `spanish.mp3`, `french.mp3`, `german.mp3` - Multilingual samples
    

These files can be played with any media player to verify audio quality and compare different voices and languages.

### Important Notes

-   Integration tests make **real API calls** to IBM Watson and may incur charges
    
-   Tests are automatically skipped during regular `mvn test` execution
    
-   Audio files in `target/` are cleaned with `mvn clean`
    
-   File format validation checks MP3 ID3 tags and WAV RIFF headers
    
-   All tests include proper resource cleanup
    

### Example Output

```none
[INFO] Running org.apache.camel.component.ibm.watson.tts.integration.WatsonTextToSpeechIT
Created output directory: target/audio-output
Successfully synthesized text with default voice. Bytes read: 44032
Found 28 voices
  Voice: en-US_MichaelV3Voice - Language: en-US - Gender: male
  Voice: en-US_AllisonV3Voice - Language: en-US - Gender: female
Successfully saved MP3 file: target/audio-output/test-output.mp3 (size: 51234 bytes)
Successfully created audio files in 4 different languages
[INFO] Tests run: 12, Failures: 0, Errors: 0, Skipped: 0
```

## Dependencies

Maven users will need to add the following dependency to their `pom.xml`.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ibm-watson-text-to-speech</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

where `x.x.x` is the version number of Camel.

## Spring Boot Auto-Configuration

When using ibm-watson-text-to-speech with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ibm-watson-text-to-speech-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 12 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.ibm-watson-text-to-speech.accept** | The audio format for synthesized speech. Default is audio/wav. Supported formats: audio/wav, audio/mp3, audio/ogg, audio/flac, audio/webm. | audio/wav | String |
| **camel.component.ibm-watson-text-to-speech.api-key** | The IBM Cloud API key for authentication. |  | String |
| **camel.component.ibm-watson-text-to-speech.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ibm-watson-text-to-speech.configuration** | Component configuration. The option is a org.apache.camel.component.ibm.watson.tts.WatsonTextToSpeechConfiguration type. |  | WatsonTextToSpeechConfiguration |
| **camel.component.ibm-watson-text-to-speech.customization-id** | The customization ID (GUID) of a custom voice model to use for synthesis. |  | String |
| **camel.component.ibm-watson-text-to-speech.enabled** | Whether to enable auto configuration of the ibm-watson-text-to-speech component. This is enabled by default. |  | Boolean |
| **camel.component.ibm-watson-text-to-speech.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.ibm-watson-text-to-speech.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.ibm-watson-text-to-speech.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ibm-watson-text-to-speech.operation** | The operation to perform. |  | WatsonTextToSpeechOperations |
| **camel.component.ibm-watson-text-to-speech.service-url** | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **camel.component.ibm-watson-text-to-speech.voice** | The voice to use for synthesis. Default is en-US\_MichaelV3Voice. Examples: en-US\_AllisonV3Voice, en-GB\_KateV3Voice, es-ES\_EnriqueV3Voice, fr-FR\_NicolasV3Voice. | en-US\_MichaelV3Voice | String |