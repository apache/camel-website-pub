# ![aws polly sink](_images/kamelets/aws-polly-sink.svg) AWS Polly Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Synthesize speech from text using AWS Polly.

## Configuration Options

The following table summarizes the configuration options available for the `aws-polly-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **engine** | Engine | Specifies the engine (standard, neural, long-form, generative) for Amazon Polly to use when processing input text for speech synthesis. Enum values: \* standard \* neural \* long-form \* generative | string |  |  |
| **languageCode** | Language Code | Optional language code for voice synthesis. This is only necessary if using a bilingual voice. | string |  |  |
| **outputFormat** | Output Format | The audio format in which the resulting stream will be encoded. Enum values: \* MP3 \* OggVorbis \* Pcm \* Json | string | MP3 |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider this parameter sets the profile name. | string |  |  |
| **sampleRate** | Sample Rate | The audio frequency in Hz. | string |  |  |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume an IAM role. | string |  |  |
| **textType** | Text Type | Specifies whether the input text is plain text or SSML. Enum values: \* TEXT \* SSML | string | TEXT |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the Polly client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the Polly client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the Polly client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Polly. | boolean | false |  |
| **voiceId** | Voice Id | The voice ID to use for speech synthesis (e.g., Joanna, Matthew, Amy, Brian). | string |  |  |

## Dependencies

At runtime, the `aws-polly-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:aws2-polly
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:aws-polly-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Polly Sink Kamelet Description

### Authentication methods

In this Kamelet you can avoid using explicit static credentials by specifying the `useDefaultCredentialsProvider` option and set it to `true`.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You can also use the Profile Credentials Provider, by setting the `useProfileCredentialsProvider` option to `true` and `profileCredentialsName` to the profile name.

Only one of access key/secret key or default credentials provider could be used

For more information, see the [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Speech Synthesis

The kamelet sends text to AWS Polly for speech synthesis and returns the audio stream in the configured output format. The message body should contain the text to synthesize.

### Voice Selection

Use the `voiceId` parameter to select a specific voice (e.g., `Joanna`, `Matthew`, `Amy`, `Brian`). If not set, the voice ID can be provided via the `CamelAwsPollyVoiceId` message header.

### Engine Selection

Amazon Polly supports multiple engines:

-   **standard** - Standard synthesis engine.
    
-   **neural** - Neural synthesis engine for more natural sounding speech.
    
-   **long-form** - Optimized for long-form content like articles and books.
    
-   **generative** - Generative synthesis engine for the most expressive and natural speech.
    

### Output Formats

The following output formats are supported:

-   **MP3** (default) - MP3 audio format.
    
-   **OggVorbis** - Ogg Vorbis audio format.
    
-   **Pcm** - Raw PCM audio format.
    
-   **Json** - Speech marks in JSON format.
    

### SSML Support

Set the `textType` parameter to `SSML` to use Speech Synthesis Markup Language for fine-grained control over pronunciation, volume, pitch, and speech rate.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-polly-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-polly-sink.kamelet.yaml)