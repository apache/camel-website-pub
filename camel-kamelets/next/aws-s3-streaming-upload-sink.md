# ![aws s3 streaming upload sink](_images/kamelets/aws-s3-streaming-upload-sink.svg) AWS S3 Streaming upload Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Writes many messages into a few large files in an Amazon S3 bucket, adding each message to the current file and starting a new file after a number of messages or bytes.

Use it to store a stream of small records, such as log lines, events or sensor readings, as a few large files instead of one file per message. To upload one file per message, use `aws-s3-sink`.

Input: the body is added to the end of the current file as it is, as text, bytes or a stream. Nothing is put between two messages: end each message with a line break if the file must have one record per line. Headers are not used: the names of the files come from `keyName`.

Output: the message is unchanged. The message that completes a file gets the `CamelAwsS3ETag` header of that file.

Good to know: a file is uploaded when it has `batchMessageNumber` messages or `batchSize` bytes, or when `streamingUploadTimeout` has passed; until then it is not in the bucket. With the default `namingStrategy` of `progressive`, the first file is named `keyName`, such as `logs/app.log`, and the next ones `logs/app-1.log`, `logs/app-2.log` and so on. With `restartingPolicy` set to `override`, a new run starts again from `keyName` and replaces the files of the earlier run.

## Configuration Options

The following table summarizes the configuration options available for the `aws-s3-streaming-upload-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name | **Required** The name of the bucket, such as `my-bucket`, or its ARN (Amazon Resource Name), such as `arn:aws:s3:::my-bucket`. | string |  | my-bucket |
| **keyName** | Key Name | **Required** The key (the path in the bucket) of the first file, such as `logs/app.log`. The next files get a number or an ID added before the extension, as `namingStrategy` says. | string |  | logs/app.log |
| **region** | AWS Region | **Required** The AWS region of the bucket, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist. The credentials need the permission to create buckets. | boolean | false |  |
| **batchMessageNumber** | Batch Message Number | How many messages make one file. The file is uploaded when it has this many messages, or `batchSize` bytes, whichever comes first. | integer | 10 |  |
| **batchSize** | Batch Size | How big a file may grow, in bytes, before it is uploaded and a new file is started. 1000000 is about 1 MB. | integer | 1000000 |  |
| **forcePathStyle** | Force Path Style | If true, the bucket name is put in the path of the address (`[https://host/my-bucket/key](https://host/my-bucket/key)`) instead of in the host name (`[https://my-bucket.host/key](https://my-bucket.host/key)`). S3-compatible storage such as MinIO often needs it. | boolean | false |  |
| **namingStrategy** | Naming Strategy | How the files after the first one are named, from `keyName` such as `logs/app.log`. `progressive` adds a number that counts up (`logs/app-1.log`, `logs/app-2.log`), `random` adds a random ID, and `timestamp` adds the time in milliseconds. | string | progressive |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack, or for S3-compatible storage such as MinIO. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **restartingPolicy** | Restarting Policy | What to do when the integration starts again and files from an earlier run exist. `lastPart` goes on numbering after the newest file, such as `logs/app-3.log`; `override` starts again from `keyName` and replaces the files of the earlier run. Only `progressive` naming uses it. | string | lastPart |  |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **streamingUploadTimeout** | Streaming Upload Timeout | How long to wait, in milliseconds, before the current file is uploaded even when it is not full. When it is not set, a file is uploaded only when it is full. | integer |  | 60000 |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials: `accessKey`, `secretKey` and `sessionToken`, such as the ones AWS STS gives when you assume an IAM role. | boolean | false |  |

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

## AWS S3 Streaming Upload Sink Kamelet Description

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

### File names

This Kamelet uses no headers: the name of the files comes from the `keyName` option.

With the default `namingStrategy` of `progressive` and a `keyName` of `logs/app.log`, the first file is `logs/app.log` and the next ones are `logs/app-1.log`, `logs/app-2.log` and so on. With `random` or `timestamp`, a random ID or the time in milliseconds is added to the name instead of a number.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-streaming-upload-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-streaming-upload-sink.kamelet.yaml)