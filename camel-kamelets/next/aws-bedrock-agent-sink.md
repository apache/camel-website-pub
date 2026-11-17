# ![aws bedrock agent sink](_images/kamelets/aws-bedrock-agent-sink.svg) AWS Bedrock Agent Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Starts, lists or looks up the ingestion jobs of an Amazon Bedrock knowledge base, which load the documents of a data source, such as an S3 bucket, into the knowledge base.

Use it to refresh a knowledge base after its documents changed, for example to start an ingestion job when new files arrive in the bucket of the data source, or every night from `timer-source`, and to check how the job went. To ask questions of the knowledge base, use `aws-bedrock-agent-runtime-sink`.

Input: the body is not used. For `getIngestionJob`, the `CamelAwsBedrockAgentIngestionJobId` header is the ID of the job to look up, and is required.

Output: when it is used inside a route, the body afterwards depends on the operation: for `startIngestionJob` the ID of the new job, as text; for `listIngestionJobs` a List of job summaries; for `getIngestionJob` the job, an object of the AWS SDK for Java, with its status, such as `IN_PROGRESS`, `COMPLETE` or `FAILED`, also in the `CamelAwsBedrockAgentIngestionJobStatus` header.

Good to know: an ingestion job runs in the background, and `startIngestionJob` returns at once; to follow it, copy the ID from the body into the `CamelAwsBedrockAgentIngestionJobId` header and use `getIngestionJob`. The operation, the knowledge base and the data source come only from the options; headers cannot change them.

## Configuration Options

The following table summarizes the configuration options available for the `aws-bedrock-agent-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **dataSourceId** | Data Source ID | **Required** The ID of the data source of the knowledge base whose documents are loaded, a code of 10 letters and digits shown in the Bedrock console. Needed by all three operations. | string |  | GH56IJ78KL |
| **knowledgeBaseId** | Knowledge Base ID | **Required** The ID of the knowledge base, a code of 10 letters and digits shown in the Bedrock console. | string |  | AB12CD34EF |
| **region** | AWS Region | **Required** The AWS region of the knowledge base, such as `eu-west-1`. Enum values: \* us-east-1 \* us-east-2 \* us-west-2 \* us-gov-west-1 \* ap-northeast-1 \* ap-northeast-2 \* ap-south-1 \* ap-southeast-1 \* ap-southeast-2 \* ca-central-1 \* eu-central-1 \* eu-central-2 \* eu-west-1 \* eu-west-2 \* eu-west-3 \* sa-east-1 | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **operation** | Operation | What to do: `startIngestionJob` starts loading the documents of the data source into the knowledge base; `listIngestionJobs` lists the ingestion jobs of the data source; `getIngestionJob` looks up the job whose ID is in the `CamelAwsBedrockAgentIngestionJobId` header. Enum values: \* startIngestionJob \* listIngestionJobs \* getIngestionJob | string | startIngestionJob |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, the requests go to the address in `uriEndpointOverride` instead of AWS, for example to test against LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile to use from the AWS credentials file. Only used when `useProfileCredentialsProvider` is true. | string |  |  |
| **secretKey** | Secret Key | The secret access key that goes with `accessKey`. AWS shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which AWS gives together with their access key and secret key. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to send the requests to instead of the usual AWS address, such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found the way the AWS SDK finds them: from the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the shared credentials file, or the IAM role of the machine, container or pod it runs on. Then `accessKey` and `secretKey` are not needed. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a profile of the AWS credentials file (`~/.aws/credentials`), the one named in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials, such as those of an assumed IAM role: `accessKey`, `secretKey` and `sessionToken` together. | boolean | false |  |

## Dependencies

At runtime, the `aws-bedrock-agent-sink` Kamelet relies upon the presence of the following dependencies:

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

## AWS Bedrock Agent Sink Kamelet Description

### Operations

This Kamelet manages the data source ingestion jobs of a knowledge base. The operation property selects which one runs:

-   `startIngestionJob` - kick off an ingestion of the configured data source
    
-   `listIngestionJobs` - list the ingestion jobs of the knowledge base
    
-   `getIngestionJob` - look up a single job
    

### Job Id

For the `getIngestionJob` operation the job id is taken from the `CamelAwsBedrockAgentIngestionJobId` header, which is the one input this Kamelet deliberately reads from the message. Every other `CamelAwsBedrockAgent*` header is removed before the call, so an inbound message cannot change the operation, the knowledge base or the data source.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-agent-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-bedrock-agent-sink.kamelet.yaml)