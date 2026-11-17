# ![aws s3 sink](_images/kamelets/aws-s3-sink.svg) AWS S3 Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file (object) to an Amazon S3 bucket, under a key (file name) taken from a header, the `keyName` option, or a generated ID.

Use it to store data in S3 for other systems or for archiving, such as exported records, received documents or events. To collect many small messages into a few large files, use `aws-s3-streaming-upload-sink`.

Input: the body is the content of the file, as text, bytes, a stream or a file. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The optional `file` header (or `ce-file`) is the key, the path of the file in the bucket, such as `orders/order-1.json`. Without it, and without `keyName`, the key is a generated unique ID. The optional `CamelAwsS3ContentType` header sets the content type of the file; the `Content-Type` header is not used, and without it the file is stored as `application/octet-stream`.

Output: the message is unchanged. The `CamelAwsS3Key` and `CamelAwsS3ETag` headers give the key and the ETag of the uploaded file.

Good to know: a file with the same key is replaced without warning. When `keyName` is set, the `file` header is ignored and every message replaces the same file. To copy files from `aws-s3-source` under their own names, set the `file` header from its `CamelAwsS3Key` header first. It also works with S3-compatible storage, such as MinIO, through `overrideEndpoint`, `uriEndpointOverride` and `forcePathStyle`.

## Configuration Options

The following table summarizes the configuration options available for the `aws-s3-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name | **Required** The name of the bucket, such as `my-bucket`, or its ARN (Amazon Resource Name), such as `arn:aws:s3:::my-bucket`. | string |  | my-bucket |
| **region** | AWS Region | **Required** The AWS region of the bucket, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist. The credentials need the permission to create buckets. | boolean | false |  |
| **forcePathStyle** | Force Path Style | If true, the bucket name is put in the path of the address (`[https://host/my-bucket/key](https://host/my-bucket/key)`) instead of in the host name (`[https://my-bucket.host/key](https://my-bucket.host/key)`). S3-compatible storage such as MinIO often needs it. | boolean | false |  |
| **keyName** | Key Name | The key (the path of the file in the bucket) to write every message to, such as `reports/latest.csv`. When it is set, the `file` header is not used and each message replaces the file of the previous one. When it is not set, the key comes from the `file` header, or is a generated unique ID. | string |  | reports/latest.csv |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack, or for S3-compatible storage such as MinIO. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials: `accessKey`, `secretKey` and `sessionToken`, such as the ones AWS STS gives when you assume an IAM role. | boolean | false |  |

## Dependencies

At runtime, the `aws-s3-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:aws-s3-sink"
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

If you do not set the property in the header, the Kamelet uses a generated unique ID for the file name.

When the `keyName` option is set, the `file` / `ce-file` header is not used, and every message is written to that key, replacing the previous file.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-sink.kamelet.yaml)