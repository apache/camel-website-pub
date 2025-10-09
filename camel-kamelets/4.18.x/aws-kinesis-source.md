# ![aws kinesis source](_images/kamelets/aws-kinesis-source.svg) AWS Kinesis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from AWS Kinesis.

## Configuration Options

The following table summarizes the configuration options available for the `aws-kinesis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  |  |
| **stream** | Stream Name | **Required** The Kinesis stream that you want to access. The Kinesis stream that you specify must already exist. | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **asyncClient** | Async Client | If we want a KinesisAsyncClient instance set it to true. | boolean | false |  |
| **delay** | Delay | The number of milliseconds before the next poll of the selected stream. | integer | 500 |  |
| **kclDisableCloudwatchMetricsExport** | KCL Disable Cloudwatch Metrics Export | Define if we want to use a KCL Consumer and disable the CloudWatch Metrics Export. | boolean | false |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider this parameter sets the profile name. | string |  |  |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume a IAM role. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the Kinesis client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | boolean | false |  |
| **useKclConsumers** | KCL Consumer | If we want to a KCL Consumer set it to true. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the Kinesis client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the Kinesis client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis. | boolean | false |  |

## Dependencies

At runtime, the `aws-kinesis-source` Kamelet relies upon the presence of the following dependencies:

-   camel:aws2-kinesis
    
-   camel:kamelet
    
-   camel:core
    

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
      uri: "kamelet:aws-kinesis-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Kinesis Source Kamelet Description

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

### Usage example with plain consumer

You could consume the stream content directly

```yaml
- route:
    from:
      uri: "kamelet:aws-kinesis-source"
      parameters:
        useDefaultCredentialsProvider: true
        region: "eu-west-1"
        stream: "kamelets"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Usage example with KCL Consumer

You could consume the stream content with the KCL support

```yaml
- route:
    from:
      uri: "kamelet:aws-kinesis-source"
      parameters:
        stream: "kamelets"
        useDefaultCredentialsProvider: true
        region: "eu-west-1"
        asyncClient: true
        useKclConsumers: true
      steps:
      - to:
          uri: "kamelet:log-sink"
          parameters:
            showHeaders: true
```

With the `useKclConsumers` enabled, you won’t have to deal with shard iteration directly. Everything is managed by the AWS Kinesis client library and the KCL layer.

As a side note you need to remember that the KCL consumer will need access to DynamoDB and Cloudwatch services from AWS, so it will create clients to these services under the hood and it will use them.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-kinesis-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-kinesis-source.kamelet.yaml)