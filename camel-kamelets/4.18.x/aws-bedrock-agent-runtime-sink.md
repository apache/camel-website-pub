# ![aws bedrock agent runtime sink](_images/kamelets/aws-bedrock-agent-runtime-sink.svg) AWS Bedrock Agent Runtime Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data for invoking a knowledge base from AWS Bedrock.

## Configuration Options

The following table summarizes the configuration options available for the `aws-bedrock-agent-runtime-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **knowledgeBaseId** | Knowledge Base Id | **Required** The Knowledge Base Id to be used to retrieve and generate responses. | string |  |  |
| **modelId** | Model Id | **Required** The model Id to be used to generate responses. Enum values: \* anthropic.claude-instant-v1 \* anthropic.claude-v2 \* anthropic.claude-v2:1 \* anthropic.claude-3-sonnet-20240229-v1:0 | string |  |  |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* us-east-1 \* us-west-1 | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider this parameter sets the profile name. | string |  |  |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume a IAM role. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the Bedrock client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the Bedrock client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Bedrock. | boolean | false |  |

## Dependencies

At runtime, the `aws-bedrock-agent-runtime-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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