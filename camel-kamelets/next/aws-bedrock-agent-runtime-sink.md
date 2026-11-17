# ![aws bedrock agent runtime sink](_images/kamelets/aws-bedrock-agent-runtime-sink.svg) AWS Bedrock Agent Runtime Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Answers the question in each message from the documents of an Amazon Bedrock knowledge base, with a model that writes the answer from the passages it finds.

Use it to build a question-and-answer service or a chatbot over your own documents, such as manuals, policies or FAQs, loaded into a Bedrock knowledge base. To load new documents into the knowledge base, use `aws-bedrock-agent-sink`; to call a model without a knowledge base, use `aws-bedrock-text-sink`.

Input: the body is the question, as text. The optional `CamelAwsBedrockAgentRuntimeSessionId` header continues an earlier conversation: set it to the session ID of an earlier answer.

Output: when it is used inside a route, the body afterwards is the answer, as text. The `CamelAwsBedrockAgentRuntimeSessionId` header holds the ID of the session, and the `CamelAwsBedrockAgentRuntimeCitations` header the passages of the documents the answer is based on, as objects of the AWS SDK for Java.

## Configuration Options

The following table summarizes the configuration options available for the `aws-bedrock-agent-runtime-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **knowledgeBaseId** | Knowledge Base ID | **Required** The ID of the knowledge base to search, a code of 10 letters and digits shown in the Bedrock console. | string |  | AB12CD34EF |
| **modelId** | Model ID | **Required** The ID of the Bedrock model that writes the answers from the parts of the documents that were found. It must be available in the region of the knowledge base. Enum values: \* anthropic.claude-instant-v1 \* anthropic.claude-v2 \* anthropic.claude-v2:1 \* anthropic.claude-3-sonnet-20240229-v1:0 | string |  |  |
| **region** | AWS Region | **Required** The AWS region of the knowledge base, such as `us-east-1`. Enum values: \* us-east-1 \* us-west-1 | string |  | us-east-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, the requests go to the address in `uriEndpointOverride` instead of AWS, for example to test against LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile to use from the AWS credentials file. Only used when `useProfileCredentialsProvider` is true. | string |  |  |
| **secretKey** | Secret Key | The secret access key that goes with `accessKey`. AWS shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which AWS gives together with their access key and secret key. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to send the requests to instead of the usual AWS address, such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found the way the AWS SDK finds them: from the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the shared credentials file, or the IAM role of the machine, container or pod it runs on. Then `accessKey` and `secretKey` are not needed. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a profile of the AWS credentials file (`~/.aws/credentials`), the one named in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials, such as those of an assumed IAM role: `accessKey`, `secretKey` and `sessionToken` together. | boolean | false |  |

## Dependencies

At runtime, the `aws-bedrock-agent-runtime-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:aws-bedrock-agent-runtime-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Bedrock Agent Runtime Sink Kamelet Description

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-agent-runtime-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-agent-runtime-sink.kamelet.yaml)