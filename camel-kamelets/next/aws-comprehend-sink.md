# ![aws comprehend sink](_images/kamelets/aws-comprehend-sink.svg) AWS Comprehend Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Analyzes the text of each message with Amazon Comprehend, for example to detect its language, its sentiment, or the people, places and personal data it mentions.

Use it to sort customer feedback by sentiment, route support tickets by language, or find personal data in text before it is stored.

Input: the body is the text to analyze.

Output: when it is used inside a route, the body afterwards is what was found, as objects of the AWS SDK for Java (not JSON text): a List for most operations, such as the languages with their scores for `detectDominantLanguage` or the entities for `detectEntities`, and the sentiment with its scores for `detectSentiment`. Headers give the main result: `CamelAwsComprehendDetectedLanguage` with its score, or `CamelAwsComprehendDetectedSentiment` with its scores.

Good to know: every operation except `detectDominantLanguage` needs `languageCode`, and a message fails without it. `classifyDocument` needs `endpointArn`. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid.

## Configuration Options

The following table summarizes the configuration options available for the `aws-comprehend-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region of Amazon Comprehend to use, such as `eu-west-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **endpointArn** | Endpoint ARN | The ARN of the endpoint of a custom document classifier that you trained in Comprehend. Only used, and required, by `classifyDocument`. | string |  | arn:aws:comprehend:eu-west-1:123456789012:document-classifier-endpoint/my-classifier |
| **languageCode** | Language Code | The language of the text, as a two-letter code, such as `en` for English or `es` for Spanish. Required for every operation except `detectDominantLanguage`. | string |  | en |
| **operation** | Operation | What to find in the text: `detectDominantLanguage` (its language), `detectSentiment` (positive, negative, neutral or mixed), `detectEntities` (people, places, organizations, dates, …​), `detectKeyPhrases`, `detectSyntax` (the part of speech of each word), `detectPiiEntities` and `containsPiiEntities` (personal data, such as names and addresses), `detectToxicContent`, or `classifyDocument` (the classes of a custom classifier). Enum values: \* detectDominantLanguage \* detectEntities \* detectKeyPhrases \* detectSentiment \* detectSyntax \* detectPiiEntities \* detectToxicContent \* classifyDocument \* containsPiiEntities | string | detectDominantLanguage |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, the requests go to the address in `uriEndpointOverride` instead of AWS, for example to test against LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile to use from the AWS credentials file. Only used when `useProfileCredentialsProvider` is true. | string |  |  |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **secretKey** | Secret Key | The secret access key that goes with `accessKey`. AWS shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which AWS gives together with their access key and secret key. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to send the requests to instead of the usual AWS address, such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found the way the AWS SDK finds them: from the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the shared credentials file, or the IAM role of the machine, container or pod it runs on. Then `accessKey` and `secretKey` are not needed. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a profile of the AWS credentials file (`~/.aws/credentials`), the one named in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials, such as those of an assumed IAM role: `accessKey`, `secretKey` and `sessionToken` together. | boolean | false |  |

## Dependencies

At runtime, the `aws-comprehend-sink` Kamelet relies upon the presence of the following dependencies:

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

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-comprehend-sink"
    parameters:
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-comprehend-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-comprehend-sink.kamelet.yaml)