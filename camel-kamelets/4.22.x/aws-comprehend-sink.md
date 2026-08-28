# ![aws comprehend sink](_images/kamelets/aws-comprehend-sink.svg) AWS Comprehend Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Send data to AWS Comprehend for natural language processing.

## Configuration Options

The following table summarizes the configuration options available for the `aws-comprehend-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **endpointArn** | Endpoint ARN | The Amazon Resource Name (ARN) of the endpoint to use for document classification. Required for classifyDocument operation. | string |  |  |
| **languageCode** | Language Code | The language code of the input text. Required for all operations except detectDominantLanguage. Use a 2-letter ISO 639-1 code (e.g., 'en' for English, 'es' for Spanish). | string |  |  |
| **operation** | Operation | The operation to perform on the input text. Enum values: \* detectDominantLanguage \* detectEntities \* detectKeyPhrases \* detectSentiment \* detectSyntax \* detectPiiEntities \* detectToxicContent \* classifyDocument \* containsPiiEntities | string | detectDominantLanguage |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider this parameter sets the profile name. | string |  |  |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume an IAM role. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the Comprehend client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the Comprehend client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the Comprehend client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Comprehend. | boolean | false |  |

## Dependencies

At runtime, the `aws-comprehend-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:aws2-comprehend
    
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
            uri: "kamelet:aws-comprehend-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Comprehend Sink Kamelet Description

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

### Operations

The kamelet supports the following operations:

-   **detectDominantLanguage** (default) - Detects the dominant language of the input text.
    
-   **detectEntities** - Detects named entities (people, places, organizations, etc.) in the input text.
    
-   **detectKeyPhrases** - Detects key noun phrases in the input text.
    
-   **detectSentiment** - Detects the sentiment (positive, negative, neutral, mixed) of the input text.
    
-   **detectSyntax** - Detects the parts of speech (nouns, verbs, adjectives, etc.) in the input text.
    
-   **detectPiiEntities** - Detects personally identifiable information (PII) in the input text.
    
-   **detectToxicContent** - Detects toxic content in the input text.
    
-   **classifyDocument** - Classifies the input text using a custom document classifier endpoint.
    
-   **containsPiiEntities** - Checks whether the input text contains PII entities.
    

### Language Code

The `languageCode` parameter is required for all operations except `detectDominantLanguage`. Use a 2-letter ISO 639-1 code (e.g., `en` for English, `es` for Spanish).

### Document Classification

For the `classifyDocument` operation, you must provide the `endpointArn` parameter pointing to your custom classifier endpoint.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-comprehend-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-comprehend-sink.kamelet.yaml)