# ![aws bedrock agent sink](_images/kamelets/aws-bedrock-agent-sink.svg) AWS Bedrock Agent Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Manage the data source ingestion jobs of an AWS Bedrock knowledge base.

Use startIngestionJob to kick off an ingestion of the configured data source, listIngestionJobs to list the jobs of a knowledge base, or getIngestionJob to look one up. For getIngestionJob the job id is taken from the CamelAwsBedrockAgentIngestionJobId header.

## Configuration Options

The following table summarizes the configuration options available for the `aws-bedrock-agent-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **knowledgeBaseId** | Knowledge Base Id | **Required** The Knowledge Base the ingestion job belongs to. | string |  |  |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* us-east-1 \* us-east-2 \* us-west-2 \* us-gov-west-1 \* ap-northeast-1 \* ap-northeast-2 \* ap-south-1 \* ap-southeast-1 \* ap-southeast-2 \* ca-central-1 \* eu-central-1 \* eu-central-2 \* eu-west-1 \* eu-west-2 \* eu-west-3 \* sa-east-1 | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **dataSourceId** | Data Source Id | The data source to ingest. Required by the startIngestionJob operation. | string |  |  |
| **operation** | Operation | The ingestion job operation to perform. Enum values: \* startIngestionJob \* listIngestionJobs \* getIngestionJob | string | startIngestionJob |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider, this parameter states the profile name. | string |  |  |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume an IAM role. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the SDK looks for credentials through the default provider chain rather than the accessKey and secretKey properties. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the Bedrock client should expect to use session credentials. This is useful in a session token scenario. | boolean | false |  |

## Dependencies

At runtime, the `aws-bedrock-agent-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:aws-bedrock-agent-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-agent-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-agent-sink.kamelet.yaml)