# ![aws polly sink](_images/kamelets/aws-polly-sink.svg) AWS Polly Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Turns the text of each message into speech with Amazon Polly, and gives the audio, such as an MP3 file.

Use it to create voice messages, audio versions of articles or spoken announcements from text. Write the audio to a file or a bucket as the next step, for example with `aws-s3-sink`.

Input: the body is the text to speak, as plain text, or as SSML when `textType` is `SSML`. The voice comes from `voiceId`, or when that is not set from the `CamelAwsPollyVoiceId` header; one of them is required.

Output: when it is used inside a route, the body afterwards is the audio, as a stream in the format of `outputFormat`, and the `CamelAwsPollyContentType` header holds its content type, such as `audio/mpeg`.

Good to know: the stream can be read only once, so write it to a file or a bucket right away. A voice that is not available with the chosen `engine` fails the message.

## Configuration Options

The following table summarizes the configuration options available for the `aws-polly-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region of Amazon Polly to use, such as `eu-west-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **engine** | Engine | The kind of voice: `standard`, `neural` (more natural), `long-form` (for long texts such as articles) or `generative`. Not every voice is available with every engine. When it is not set, Polly uses its default engine. Enum values: \* standard \* neural \* long-form \* generative | string |  |  |
| **languageCode** | Language Code | The language to speak in, such as `en-IN` or `hi-IN`. Only needed for a bilingual voice, such as `Aditi`, to choose one of its two languages. | string |  | en-IN |
| **outputFormat** | Output Format | The format of the audio: `MP3`, `OggVorbis`, `Pcm` (raw audio), or `Json` for speech marks, which give the timing of the words instead of audio. Enum values: \* MP3 \* OggVorbis \* Pcm \* Json | string | MP3 |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, the requests go to the address in `uriEndpointOverride` instead of AWS, for example to test against LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile to use from the AWS credentials file. Only used when `useProfileCredentialsProvider` is true. | string |  |  |
| **sampleRate** | Sample Rate | The sample rate of the audio, in hertz, such as `22050` for MP3 or `16000` for PCM. When it is not set, Polly uses the default of the format. | string |  | 22050 |
| **secretKey** | Secret Key | The secret access key that goes with `accessKey`. AWS shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which AWS gives together with their access key and secret key. Only used when `useSessionCredentials` is true. | string |  |  |
| **textType** | Text Type | Whether the body is plain text (`TEXT`) or SSML (`SSML`), the markup language that controls pronunciation, pauses, volume and speed. Enum values: \* TEXT \* SSML | string | TEXT |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to send the requests to instead of the usual AWS address, such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found the way the AWS SDK finds them: from the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the shared credentials file, or the IAM role of the machine, container or pod it runs on. Then `accessKey` and `secretKey` are not needed. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a profile of the AWS credentials file (`~/.aws/credentials`), the one named in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials, such as those of an assumed IAM role: `accessKey`, `secretKey` and `sessionToken` together. | boolean | false |  |
| **voiceId** | Voice ID | The name of the voice to speak with, such as `Joanna` (US English) or `Hans` (German); the voice also sets the language. The Polly console lists the voices. When it is not set, the `CamelAwsPollyVoiceId` header gives the voice. | string |  | Joanna |

## Dependencies

At runtime, the `aws-polly-sink` Kamelet relies upon the presence of the following dependencies:

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