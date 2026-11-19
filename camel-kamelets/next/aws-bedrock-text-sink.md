# ![aws bedrock text sink](_images/kamelets/aws-bedrock-text-sink.svg) AWS Bedrock Text Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends a prompt to a text model in Amazon Bedrock, such as Amazon Titan or Anthropic Claude, for each message, and gives the answer of the model.

Use it to summarize, classify, translate or write text with a large language model, for example to summarize support tickets or draft replies. To answer questions from your own documents in a Bedrock knowledge base, use `aws-bedrock-agent-runtime-sink`.

Input: the body is the request of the model, as JSON text in the format of the chosen model, not the bare prompt. For Amazon Titan, for example `{"inputText":"Summarize: …​","textGenerationConfig":{"maxTokenCount":500}}`. For Claude 3, the Messages format, for example `{"anthropic_version":"bedrock-2023-05-31","max_tokens":500,"messages":[{"role":"user","content":"Summarize: …​"}]}`.

Output: when it is used inside a route, the body afterwards is the answer, in a form that depends on the model: for Titan the response as JSON text, with the generated text in `results`; for Claude 3 the response as parsed JSON, with the generated text in `content`; for the older Claude models only the generated text, as text.

Good to know: the request and response formats are those of the model provider, described for each model in the Amazon Bedrock documentation; a body in another format fails. Each message is one call of the model. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. Headers that start with `CamelAwsBedrock` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `aws-bedrock-text-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **modelId** | Model ID | **Required** The ID of the Bedrock text model to call. The body must be a request in the format of this model: Amazon Titan (`amazon.titan-text-`**), AI21 Labs Jurassic (`ai21.j2-`**) or Anthropic Claude (`anthropic.claude-*`). Enum values: \* amazon.titan-text-express-v1 \* amazon.titan-text-lite-v1 \* ai21.j2-ultra-v1 \* ai21.j2-mid-v1 \* anthropic.claude-instant-v1 \* anthropic.claude-v2 \* anthropic.claude-v2:1 \* anthropic.claude-3-sonnet-20240229-v1:0 | string |  |  |
| **region** | AWS Region | **Required** The AWS region of Amazon Bedrock to use, such as `us-east-1`. The model must be available in it. Enum values: \* us-east-1 \* us-west-1 \* ap-southeast-1 \* ap-northeast-1 \* eu-central-1 | string |  | us-east-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
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

At runtime, the `aws-bedrock-text-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:aws-bedrock
    
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
            uri: "kamelet:aws-bedrock-text-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Bedrock Text Sink Kamelet Description

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

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-bedrock-text-sink"
    parameters:
      modelId: "anthropic.claude-v2"
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-text-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-text-sink.kamelet.yaml)