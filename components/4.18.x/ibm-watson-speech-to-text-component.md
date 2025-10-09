# IBM Watson Speech to Text

**Since Camel 4.17**

**Only producer is supported**

The IBM Watson Speech to Text component allows you to convert speech audio into written text using [IBM Watson Speech to Text service](https://cloud.ibm.com/catalog/services/speech-to-text).

Prerequisites

You must have a valid IBM Cloud account and an instance of the Watson Speech to Text service. More information is available at [IBM Watson Speech to Text](https://cloud.ibm.com/catalog/services/speech-to-text).

## URI Format

ibm-watson-speech-to-text:label\[?options\]

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

The IBM Watson Speech to Text component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | WatsonSpeechToTextConfiguration |
| **serviceUrl** (common) | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **contentType** (producer) | The audio format (MIME type). Default is audio/wav. Supported formats: audio/wav, audio/mp3, audio/flac, audio/ogg, audio/webm. | audio/wav | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **model** (producer) | The language model to use for recognition. Default is en-US\_BroadbandModel. Examples: en-US\_NarrowbandModel, en-GB\_BroadbandModel, es-ES\_BroadbandModel, fr-FR\_BroadbandModel. | en-US\_BroadbandModel | String |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   recognize
    
-   listModels
    
-   getModel
    
-   listCustomModels
    
-   getCustomModel
    





 |  | WatsonSpeechToTextOperations |
| **speakerLabels** (producer) | Whether to identify different speakers in the audio. Default is false. | false | boolean |
| **timestamps** (producer) | Whether to include timestamps for each word in the transcription. Default is false. | false | boolean |
| **wordConfidence** (producer) | Whether to include confidence scores for each word. Default is false. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **apiKey** (security) | **Required** The IBM Cloud API key for authentication. |  | String |

## Endpoint Options

The IBM Watson Speech to Text endpoint is configured using URI syntax:

ibm-watson-speech-to-text:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceUrl** (common) | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **contentType** (producer) | The audio format (MIME type). Default is audio/wav. Supported formats: audio/wav, audio/mp3, audio/flac, audio/ogg, audio/webm. | audio/wav | String |
| **model** (producer) | The language model to use for recognition. Default is en-US\_BroadbandModel. Examples: en-US\_NarrowbandModel, en-GB\_BroadbandModel, es-ES\_BroadbandModel, fr-FR\_BroadbandModel. | en-US\_BroadbandModel | String |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   recognize
    
-   listModels
    
-   getModel
    
-   listCustomModels
    
-   getCustomModel
    





 |  | WatsonSpeechToTextOperations |
| **speakerLabels** (producer) | Whether to identify different speakers in the audio. Default is false. | false | boolean |
| **timestamps** (producer) | Whether to include timestamps for each word in the transcription. Default is false. | false | boolean |
| **wordConfidence** (producer) | Whether to include confidence scores for each word. Default is false. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiKey** (security) | **Required** The IBM Cloud API key for authentication. |  | String |

## Message Headers

The IBM Watson Speech to Text component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIBMWatsonSTTOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelIBMWatsonSTTAudioFile** (producer) Constant: [`AUDIO_FILE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#AUDIO_FILE) | The audio file to transcribe. |  | File |
| **CamelIBMWatsonSTTModel** (producer) Constant: [`MODEL`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#MODEL) | The language model to use for recognition. |  | String |
| **CamelIBMWatsonSTTContentType** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#CONTENT_TYPE) | The audio format (e.g., audio/wav, audio/mp3, audio/flac). |  | String |
| **CamelIBMWatsonSTTTimestamps** (producer) Constant: [`TIMESTAMPS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#TIMESTAMPS) | Whether to include timestamps in the transcription. |  | Boolean |
| **CamelIBMWatsonSTTWordConfidence** (producer) Constant: [`WORD_CONFIDENCE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#WORD_CONFIDENCE) | Whether to include word confidence scores. |  | Boolean |
| **CamelIBMWatsonSTTSpeakerLabels** (producer) Constant: [`SPEAKER_LABELS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#SPEAKER_LABELS) | Whether to identify different speakers. |  | Boolean |
| **CamelIBMWatsonSTTModelName** (producer) Constant: [`MODEL_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#MODEL_NAME) | The name of the model to retrieve. |  | String |
| **CamelIBMWatsonSTTLanguage** (producer) Constant: [`LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#LANGUAGE) | The language for filtering models. |  | String |
| **CamelIBMWatsonSTTTranscript** (producer) Constant: [`TRANSCRIPT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-speech-to-text/latest/org/apache/camel/component/ibm/watson/stt/WatsonSpeechToTextConstants.html#TRANSCRIPT) | The transcription result text. |  | String |

Required Watson Speech to Text component options

You must provide the `apiKey` to access IBM Watson Speech to Text. Optionally, you can specify a custom `serviceUrl` if you’re using a dedicated or private instance.

## Usage

### Watson Speech to Text Producer operations

The IBM Watson Speech to Text component provides the following operations:

-   recognize - Transcribe audio to text
    
-   listModels - Get available language models
    
-   getModel - Get information about a specific model
    
-   listCustomModels - List custom language models
    
-   getCustomModel - Get information about a custom language model
    

If you don’t specify an operation explicitly, you must set it via the `operation` parameter.

## Examples

### Recognize Audio to Text

Transcribe a WAV audio file to text:

```java
from("file:/var/audio?noop=true")
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=recognize&contentType=audio/wav")
  .process(exchange -> {
      String transcript = exchange.getMessage().getHeader(WatsonSpeechToTextConstants.TRANSCRIPT, String.class);
      System.out.println("Transcription: " + transcript);
  });
```

This will transcribe the audio file and extract the text.

### Recognize with Timestamps

Transcribe audio and get word-level timestamps:

```java
from("direct:start")
  .setHeader(WatsonSpeechToTextConstants.AUDIO_FILE, constant(new File("/path/to/audio.wav")))
  .setHeader(WatsonSpeechToTextConstants.TIMESTAMPS, constant(true))
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=recognize")
  .process(exchange -> {
      SpeechRecognitionResults results = exchange.getMessage().getBody(SpeechRecognitionResults.class);
      results.getResults().forEach(result -> {
          result.getAlternatives().forEach(alt -> {
              alt.getTimestamps().forEach(timestamp -> {
                  System.out.println("Word: " + timestamp.getWord() +
                                   " - Start: " + timestamp.getStartTime() +
                                   " - End: " + timestamp.getEndTime());
              });
          });
      });
  });
```

### Recognize with Word Confidence

Get confidence scores for each transcribed word:

```java
from("direct:start")
  .setBody(constant(audioInputStream))
  .setHeader(WatsonSpeechToTextConstants.WORD_CONFIDENCE, constant(true))
  .setHeader(WatsonSpeechToTextConstants.CONTENT_TYPE, constant("audio/mp3"))
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=recognize")
  .process(exchange -> {
      SpeechRecognitionResults results = exchange.getMessage().getBody(SpeechRecognitionResults.class);
      results.getResults().forEach(result -> {
          result.getAlternatives().forEach(alt -> {
              alt.getWordConfidence().forEach(wc -> {
                  System.out.println("Word: " + wc.getWord() +
                                   " - Confidence: " + wc.getConfidence());
              });
          });
      });
  });
```

### Available Language Models

Some commonly used models include:

**English Models:** - en-US\_BroadbandModel - US English for high-quality audio (16 kHz) - en-US\_NarrowbandModel - US English for telephony audio (8 kHz) - en-GB\_BroadbandModel - UK English broadband - en-GB\_NarrowbandModel - UK English narrowband

**Spanish Models:** - es-ES\_BroadbandModel - Castilian Spanish - es-ES\_NarrowbandModel - Castilian Spanish narrowband - es-MX\_BroadbandModel - Mexican Spanish - es-LA\_BroadbandModel - Latin American Spanish

**French Models:** - fr-FR\_BroadbandModel - French broadband - fr-FR\_NarrowbandModel - French narrowband - fr-CA\_BroadbandModel - Canadian French

**German Models:** - de-DE\_BroadbandModel - German broadband - de-DE\_NarrowbandModel - German narrowband

**Other Languages:** - ja-JP\_BroadbandModel - Japanese - ko-KR\_BroadbandModel - Korean - pt-BR\_BroadbandModel - Brazilian Portuguese - zh-CN\_BroadbandModel - Mandarin Chinese - it-IT\_BroadbandModel - Italian - ar-MS\_BroadbandModel - Modern Standard Arabic

### List Available Models

Get a list of all available language models:

```java
from("direct:listModels")
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=listModels")
  .process(exchange -> {
      List<SpeechModel> models = exchange.getMessage().getBody(List.class);
      models.forEach(model -> {
          System.out.println("Model: " + model.getName() +
                           " - Language: " + model.getLanguage() +
                           " - Description: " + model.getDescription());
      });
  });
```

### Get Model Information

Get detailed information about a specific model:

```java
from("direct:getModel")
  .setHeader(WatsonSpeechToTextConstants.MODEL_NAME, constant("en-US_BroadbandModel"))
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=getModel")
  .process(exchange -> {
      SpeechModel model = exchange.getMessage().getBody(SpeechModel.class);
      System.out.println("Model details: " + model);
  });
```

### Audio Format Options

The component supports various audio formats via the `contentType` parameter:

-   audio/wav - WAV format (default), PCM 16-bit
    
-   audio/mp3 - MP3 format
    
-   audio/flac - FLAC format, lossless compression
    
-   audio/ogg - Ogg Vorbis format with Opus codec
    
-   audio/webm - WebM format
    

Example with MP3 input:

```java
from("file:/var/audio?include=.*\\.mp3")
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=recognize&contentType=audio/mp3")
  .log("Transcript: ${header.CamelIBMWatsonSTTTranscript}");
```

### Recognize Different Languages

Transcribe audio in different languages by specifying the appropriate model:

```java
// Transcribe Spanish audio
from("direct:spanish")
  .setBody(constant(spanishAudioFile))
  .setHeader(WatsonSpeechToTextConstants.MODEL, constant("es-ES_BroadbandModel"))
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=recognize")
  .log("Spanish transcript: ${header.CamelIBMWatsonSTTTranscript}");

// Transcribe French audio
from("direct:french")
  .setBody(constant(frenchAudioFile))
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=recognize&model=fr-FR_BroadbandModel")
  .log("French transcript: ${header.CamelIBMWatsonSTTTranscript}");
```

### Speaker Identification

Identify different speakers in multi-speaker audio:

```java
from("direct:speakers")
  .setHeader(WatsonSpeechToTextConstants.SPEAKER_LABELS, constant(true))
  .setHeader(WatsonSpeechToTextConstants.TIMESTAMPS, constant(true))
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=recognize")
  .process(exchange -> {
      SpeechRecognitionResults results = exchange.getMessage().getBody(SpeechRecognitionResults.class);
      results.getSpeakerLabels().forEach(label -> {
          System.out.println("Speaker " + label.getSpeaker() +
                           " from " + label.getFrom() +
                           " to " + label.getTo() +
                           ": " + label.getFinal());
      });
  });
```

### Using Custom Language Models

If you have created a custom language model, you can use it for recognition:

```java
from("direct:customModel")
  .setHeader(WatsonSpeechToTextConstants.MODEL, constant("your-custom-model-guid"))
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=recognize")
  .log("Custom model transcript: ${header.CamelIBMWatsonSTTTranscript}");
```

### List Custom Models

List all your custom language models:

```java
from("direct:listCustomModels")
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=listCustomModels")
  .process(exchange -> {
      List<LanguageModel> models = exchange.getMessage().getBody(List.class);
      models.forEach(model -> {
          System.out.println("Custom Model: " + model.getCustomizationId() +
                           " - Name: " + model.getName() +
                           " - Language: " + model.getLanguage() +
                           " - Status: " + model.getStatus());
      });
  });
```

### Get Custom Model Details

Get detailed information about a custom model:

```java
from("direct:getCustomModel")
  .setHeader(WatsonSpeechToTextConstants.MODEL_NAME, constant("your-custom-model-guid"))
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&operation=getCustomModel")
  .process(exchange -> {
      LanguageModel model = exchange.getMessage().getBody(LanguageModel.class);
      System.out.println("Custom model: " + model.getName() +
                       " - Status: " + model.getStatus() +
                       " - Progress: " + model.getProgress() + "%");
  });
```

### Watson Speech to Text Authentication

IBM Watson Speech to Text uses IBM Cloud IAM (Identity and Access Management) for authentication. You need to provide your IBM Cloud API key.

You can create API keys in the IBM Cloud console: 1. Go to [https://cloud.ibm.com/iam/apikeys](https://cloud.ibm.com/iam/apikeys) 2. Click "Create an IBM Cloud API key" 3. Copy the API key and use it in your Camel routes

For more information about authentication, see the [IBM Watson STT documentation](https://cloud.ibm.com/docs/speech-to-text?topic=speech-to-text-getting-started).

### Watson Speech to Text Endpoints

If you have a dedicated or regional instance, you can specify a custom service URL:

```java
from("direct:start")
  .setBody(constant(audioFile))
  .to("ibm-watson-speech-to-text:mySTT?apiKey=RAW(yourApiKey)&serviceUrl=https://api.eu-gb.speech-to-text.watson.cloud.ibm.com&operation=recognize")
  .log("Transcript: ${header.CamelIBMWatsonSTTTranscript}");
```

Common regional endpoints: - Dallas: [https://api.us-south.speech-to-text.watson.cloud.ibm.com](https://api.us-south.speech-to-text.watson.cloud.ibm.com) - Washington DC: [https://api.us-east.speech-to-text.watson.cloud.ibm.com](https://api.us-east.speech-to-text.watson.cloud.ibm.com) - Frankfurt: [https://api.eu-de.speech-to-text.watson.cloud.ibm.com](https://api.eu-de.speech-to-text.watson.cloud.ibm.com) - London: [https://api.eu-gb.speech-to-text.watson.cloud.ibm.com](https://api.eu-gb.speech-to-text.watson.cloud.ibm.com) - Tokyo: [https://api.jp-tok.speech-to-text.watson.cloud.ibm.com](https://api.jp-tok.speech-to-text.watson.cloud.ibm.com) - Sydney: [https://api.au-syd.speech-to-text.watson.cloud.ibm.com](https://api.au-syd.speech-to-text.watson.cloud.ibm.com)

## Integration Tests

This component includes comprehensive integration tests that validate the functionality against the actual IBM Watson Speech to Text service. These tests are disabled by default to prevent accidental API calls during regular builds.

### Prerequisites for Running Integration Tests

1.  **IBM Cloud Account**: You need a valid IBM Cloud account
    
2.  **Watson Speech to Text Service**: Create a Watson Speech to Text service instance in IBM Cloud
    
3.  **API Credentials**: Obtain your API key and service URL from the IBM Cloud console
    

To get your credentials:

1.  Log in to [IBM Cloud Console](https://cloud.ibm.com/)
    
2.  Navigate to your Speech to Text service instance
    
3.  Go to "Manage" → "Credentials"
    
4.  Copy your **API Key** and **Service URL**
    

### Running Integration Tests

Integration tests are executed with the `verify` goal and require system properties:

```bash
mvn verify \
  -Dcamel.ibm.watson.stt.apiKey=YOUR_API_KEY \
  -Dcamel.ibm.watson.stt.serviceUrl=YOUR_SERVICE_URL
```

Alternatively, using environment variables:

```bash
export CAMEL_IBM_WATSON_STT_API_KEY=YOUR_API_KEY
export CAMEL_IBM_WATSON_STT_SERVICE_URL=YOUR_SERVICE_URL

mvn verify \
  -Dcamel.ibm.watson.stt.apiKey=${CAMEL_IBM_WATSON_STT_API_KEY} \
  -Dcamel.ibm.watson.stt.serviceUrl=${CAMEL_IBM_WATSON_STT_SERVICE_URL}
```

### Integration Test Coverage

The integration tests cover all major operations:

**Recognition Operations:**

-   Basic audio-to-text transcription with default model
    
-   Transcription with word timestamps
    
-   Transcription with word confidence scores
    
-   Different audio formats (WAV, MP3, FLAC)
    
-   Multiple languages (English, Spanish, French, German)
    

**Model Operations:**

-   Listing all available language models
    
-   Getting detailed information about specific models
    

**Audio File Operations:**

-   Reading audio files from disk
    
-   Processing different audio formats
    
-   Validating transcription accuracy
    

**Custom Model Operations:**

-   Listing custom language models (if available)
    
-   Getting custom model details (if available)
    

**File Output Operations:**

-   Saving transcription results to text files
    
-   Saving detailed results with timestamps to text files
    
-   Saving results with word confidence scores to text files
    
-   Processing multiple audio files and saving transcripts
    

### Generated Audio Test Files

Integration tests automatically generate sample audio files in `target/audio-input/`:

-   `test-audio.wav` - Sample WAV file for testing
    
-   `test-audio-timestamps.wav` - Sample WAV for timestamp testing
    
-   `test-audio-confidence.wav` - Sample WAV for confidence score testing
    

These files are simple synthesized audio with known text for validation purposes.

### Generated Transcription Output Files

When integration tests run successfully, transcription files are created in `target/transcription-output/`:

-   `transcript-basic.txt` - Basic transcription output
    
-   `transcript-with-timestamps.txt` - Transcription with word-level timestamps
    
-   `transcript-detailed.txt` - Detailed results with timestamps and word confidence scores
    
-   `transcript-file1.txt`, `transcript-file2.txt`, `transcript-file3.txt` - Multiple file processing results
    

These files can be reviewed to verify transcription accuracy and examine the detailed recognition results including timestamps and confidence scores.

### Important Notes

-   Integration tests make **real API calls** to IBM Watson and may incur charges
    
-   Tests are automatically skipped during regular `mvn test` execution
    
-   Audio files in `target/` are cleaned with `mvn clean`
    
-   Tests verify transcription accuracy by comparing against known text
    
-   All tests include proper resource cleanup
    

### Example Output

```none
[INFO] Running org.apache.camel.component.ibm.watson.stt.integration.WatsonSpeechToTextIT
Created input directory: target/audio-input
Created output directory: target/transcription-output
Generated test audio file: target/audio-input/test-audio.wav
Successfully transcribed audio. Transcript: "Hello this is a test of IBM Watson Speech to Text"
Confidence: 0.98
Found 25 language models
  Model: en-US_BroadbandModel - Language: en-US - Rate: 16000
  Model: en-GB_BroadbandModel - Language: en-GB - Rate: 16000
Retrieved model details: en-US_BroadbandModel - Description: US English broadband model
Successfully transcribed with timestamps (5 words with timing information)
Successfully transcribed with word confidence (5 words with confidence scores)
Successfully saved transcript to file: target/transcription-output/transcript-basic.txt (size: 156 bytes)
Successfully saved transcript with timestamps to: target/transcription-output/transcript-with-timestamps.txt (size: 452 bytes)
Successfully saved detailed transcript to: target/transcription-output/transcript-detailed.txt (size: 678 bytes)
Created transcript file: transcript-file1.txt (size: 156 bytes)
Created transcript file: transcript-file2.txt (size: 156 bytes)
Created transcript file: transcript-file3.txt (size: 156 bytes)
Successfully transcribed and saved 3 audio files
[INFO] Tests run: 12, Failures: 0, Errors: 0, Skipped: 0
```

## Dependencies

Maven users will need to add the following dependency to their `pom.xml`.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ibm-watson-speech-to-text</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

where `x.x.x` is the version number of Camel.

## Spring Boot Auto-Configuration

When using ibm-watson-speech-to-text with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ibm-watson-speech-to-text-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.ibm-watson-speech-to-text.api-key** | The IBM Cloud API key for authentication. |  | String |
| **camel.component.ibm-watson-speech-to-text.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ibm-watson-speech-to-text.configuration** | Component configuration. The option is a org.apache.camel.component.ibm.watson.stt.WatsonSpeechToTextConfiguration type. |  | WatsonSpeechToTextConfiguration |
| **camel.component.ibm-watson-speech-to-text.content-type** | The audio format (MIME type). Default is audio/wav. Supported formats: audio/wav, audio/mp3, audio/flac, audio/ogg, audio/webm. | audio/wav | String |
| **camel.component.ibm-watson-speech-to-text.enabled** | Whether to enable auto configuration of the ibm-watson-speech-to-text component. This is enabled by default. |  | Boolean |
| **camel.component.ibm-watson-speech-to-text.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.ibm-watson-speech-to-text.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.ibm-watson-speech-to-text.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ibm-watson-speech-to-text.model** | The language model to use for recognition. Default is en-US\_BroadbandModel. Examples: en-US\_NarrowbandModel, en-GB\_BroadbandModel, es-ES\_BroadbandModel, fr-FR\_BroadbandModel. | en-US\_BroadbandModel | String |
| **camel.component.ibm-watson-speech-to-text.operation** | The operation to perform. |  | WatsonSpeechToTextOperations |
| **camel.component.ibm-watson-speech-to-text.service-url** | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **camel.component.ibm-watson-speech-to-text.speaker-labels** | Whether to identify different speakers in the audio. Default is false. | false | Boolean |
| **camel.component.ibm-watson-speech-to-text.timestamps** | Whether to include timestamps for each word in the transcription. Default is false. | false | Boolean |
| **camel.component.ibm-watson-speech-to-text.word-confidence** | Whether to include confidence scores for each word. Default is false. | false | Boolean |