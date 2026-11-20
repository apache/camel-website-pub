# ![aws translate action](_images/kamelets/aws-translate-action.svg) AWS Translate Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Translates the text of each message from one language into another with Amazon Translate.

Use it to translate customer messages, support tickets or product descriptions, for example from Italian into English before they are analyzed or stored, also when the messages come in several languages.

Input: the body is the text to translate.

Output: the body is the translated text, and the `Content-Type` header is `text/plain`.

Good to know: the target language is fixed by `targetLanguage`. The source language is fixed by `sourceLanguage`, or, with `autodetectSourceLanguage`, Amazon Translate detects it in each message. Only the listed language codes can be chosen, although Amazon Translate knows more languages. With `terminologyNames`, your own translations of terms, such as product and brand names, are applied. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. Headers that start with `CamelAwsTranslate` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `aws-translate-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region of Amazon Translate to use, such as `eu-west-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **targetLanguage** | Target Language | **Required** The language to translate the text into, as a language code, such as `en` for English or `de` for German. Enum values: \* ar \* zh \* zh-TW \* cs \* da \* nl \* en \* fi \* fr \* de \* he \* hi \* id \* it \* ja \* ko \* ms \* no \* fa \* pl \* pt \* ru \* es \* sv \* tr | string |  | en |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **autodetectSourceLanguage** | Detect Source Language | If true, Amazon Translate detects the language of each message, so messages in different languages can be translated into `targetLanguage`; `sourceLanguage` is then not used. When it is not set, the language is `sourceLanguage`. | boolean |  | true |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile to use from the AWS credentials file. Only used when `useProfileCredentialsProvider` is true. | string |  |  |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **secretKey** | Secret Key | The secret access key that goes with `accessKey`. AWS shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which AWS gives together with their access key and secret key. Only used when `useSessionCredentials` is true. | string |  |  |
| **sourceLanguage** | Source Language | The language of the text, as a language code, such as `it` for Italian or `en` for English. Required, unless `autodetectSourceLanguage` is true; without either, a message fails. Enum values: \* ar \* zh \* zh-TW \* cs \* da \* nl \* en \* fi \* fr \* de \* he \* hi \* id \* it \* ja \* ko \* ms \* no \* fa \* pl \* pt \* ru \* es \* sv \* tr | string |  | it |
| **terminologyNames** | Terminology Names | The name of a custom terminology to apply, such as `product-names`. A custom terminology is a list of terms with their translations, such as brand names that must not be translated, which you create in Amazon Translate beforehand. Several names are separated by commas. When it is not set, no custom terminology is used. | string |  | product-names |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found the way the AWS SDK finds them: from the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the shared credentials file, or the IAM role of the machine, container or pod it runs on. Then `accessKey` and `secretKey` are not needed. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a profile of the AWS credentials file (`~/.aws/credentials`), the one named in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials, such as those of an assumed IAM role: `accessKey`, `secretKey` and `sessionToken` together. | boolean | false |  |

## Dependencies

At runtime, the `aws-translate-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:aws2-translate
    

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
            uri: "kamelet:aws-translate-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Translate Action Kamelet Description

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

### Detecting the Language and Custom Terminologies

When the messages come in different languages, set `autodetectSourceLanguage` to `true` instead of `sourceLanguage`: Amazon Translate then detects the language of each message. When both are set, the language is detected, and `sourceLanguage` is not used.

A custom terminology is a list of terms with their translations, such as product or brand names that must not be translated. Create it in Amazon Translate beforehand, and name it in `terminologyNames`; several names are separated by commas.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-translate-action"
    parameters:
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      autodetectSourceLanguage: true
      targetLanguage: "en"
      terminologyNames: "product-names"
```

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-translate-action"
    parameters:
      region: "eu-west-1"
      sourceLanguage: "it"
      targetLanguage: "en"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-translate-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-translate-action.kamelet.yaml)