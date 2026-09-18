# ![aws s3 streaming upload sink](_images/kamelets/aws-s3-streaming-upload-sink.svg) AWS S3 Streaming upload Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Upload data to AWS S3 in streaming upload mode.

## Configuration Options

The following table summarizes the configuration options available for the `aws-s3-streaming-upload-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name | **Required** The S3 Bucket name or Amazon Resource Name (ARN). | string |  |  |
| **keyName** | Key Name | **Required** Setting the key name for an element in the bucket through endpoint parameter. In Streaming Upload, with the default configuration, this is the base for the progressive creation of files. | string |  |  |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | Setting the autocreation of the S3 bucket bucketName. | boolean | false |  |
| **batchMessageNumber** | Batch Message Number | The number of messages composing a batch in streaming upload mode. | integer | 10 |  |
| **batchSize** | Batch Size | The batch size (in bytes) in streaming upload mode. | integer | 1000000 |  |
| **forcePathStyle** | Force Path Style | Forces path style when accessing AWS S3 buckets. | boolean | false |  |
| **namingStrategy** | Naming Strategy | The naming strategy to use in streaming upload mode. There are 2 enums and the value can be one of progressive, random. | string | progressive |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider this parameter sets the profile name. | string |  |  |
| **restartingPolicy** | Restarting Policy | The restarting policy to use in streaming upload mode. There are 2 enums and the value can be one of `override`, `lastPart`. | string | lastPart |  |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume a IAM role. | string |  |  |
| **streamingUploadTimeout** | Streaming Upload Timeout | While streaming upload mode is true, this option set the timeout to complete upload. | integer |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the S3 client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the S3 client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in S3. | boolean | false |  |

## Dependencies

At runtime, the `aws-s3-streaming-upload-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:aws2-s3
    
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
            uri: "kamelet:aws-s3-streaming-upload-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS S3 Sink Kamelet Description

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

### Optional Headers

In the header, you can optionally set the `file` / `ce-file` property to specify the name of the file to upload.

If you do not set the property in the header, the Kamelet uses the exchange ID for the file name.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-streaming-upload-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-streaming-upload-sink.kamelet.yaml)