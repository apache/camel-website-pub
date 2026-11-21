# ![aws s3 sink](_images/kamelets/aws-s3-sink.svg) AWS S3 Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file (object) to an Amazon S3 bucket, under a key (file name) taken from a header, the `keyName` option, or a generated ID.

Use it to store data in S3 for other systems or for archiving, such as exported records, received documents or events. To collect many small messages into a few large files, use `aws-s3-streaming-upload-sink`.

Input: the body is the content of the file, as text, bytes, a stream or a file. Text is turned into bytes before the upload, and the `Content-Type` header is set to `application/octet-stream`. A file is passed on as it is, and so is a stream, unless stream caching is turned off. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The optional `file` header (or `ce-file`) is the key, the path of the file in the bucket, such as `orders/order-1.json`. Without it, and without `keyName`, the key is a generated unique ID. The optional `CamelAwsS3ContentType` header sets the content type of the file; the `Content-Type` header is not used, and without it the file is stored as `application/octet-stream`.

Output: the body is the content of the file, as bytes when it was text, and the `Content-Type` header is `application/octet-stream`. The `CamelAwsS3Key` and `CamelAwsS3ETag` headers give the key and the ETag of the uploaded file.

Good to know: a file with the same key is replaced without warning, unless `conditionalWritesEnabled` is true: then the upload of a key that exists already fails. When `keyName` is set, the `file` header is ignored and every message replaces the same file. To copy files from `aws-s3-source` under their own names, set the `file` header from its `CamelAwsS3Key` header first. It also works with S3-compatible storage, such as MinIO, through `overrideEndpoint`, `uriEndpointOverride` and `forcePathStyle`. To encrypt the files with a key of AWS KMS, as a bucket policy may require, set `useAwsKMS` and `awsKMSKeyId`; `storageClass` sets their storage class. One upload takes at most 5 GB; for larger files, set `multiPartUpload` to true, and each file of `partSize` or more is uploaded in parts. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. Headers that start with `CamelAwsS3`, except `CamelAwsS3ContentType` and `CamelAwsS3StorageClass`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `aws-s3-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name | **Required** The name of the bucket, such as `my-bucket`, or its ARN (Amazon Resource Name), such as `arn:aws:s3:::my-bucket`. | string |  | my-bucket |
| **region** | AWS Region | **Required** The AWS region of the bucket, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist. The credentials need the permission to create buckets. | boolean | false |  |
| **awsKMSKeyId** | AWS KMS Key ID | The KMS key to encrypt the files with, as its key ID, such as `1234abcd-12ab-34cd-56ef-1234567890ab`, or its ARN, such as `arn:aws:kms:eu-west-1:111122223333:key/1234abcd-12ab-34cd-56ef-1234567890ab`. Use the ARN for a key of another AWS account. Only used when `useAwsKMS` is true. | string |  | arn:aws:kms:eu-west-1:111122223333:key/1234abcd-12ab-34cd-56ef-1234567890ab |
| **conditionalWritesEnabled** | Conditional Writes | If true, a file is uploaded only when its key does not exist yet in the bucket (`If-None-Match`), so an existing file is never replaced. The upload of a key that exists fails with `PreconditionFailed` (status 412), and the message fails. Together with `keyName`, only the first message is stored. When it is not set, an existing file is replaced. | boolean |  |  |
| **forcePathStyle** | Force Path Style | If true, the bucket name is put in the path of the address (`[https://host/my-bucket/key](https://host/my-bucket/key)`) instead of in the host name (`[https://my-bucket.host/key](https://my-bucket.host/key)`). S3-compatible storage such as MinIO often needs it. | boolean | false |  |
| **keyName** | Key Name | The key (the path of the file in the bucket) to write every message to, such as `reports/latest.csv`. When it is set, the `file` header is not used and each message replaces the file of the previous one. When it is not set, the key comes from the `file` header, or is a generated unique ID. | string |  | reports/latest.csv |
| **multiPartUpload** | Multipart Upload | If true, a file of `partSize` bytes or more is uploaded in parts (an S3 multipart upload), one request per part, and S3 joins the parts into one file. Smaller files are uploaded in one request, as without it. Use it for files over 5 GB, which S3 does not take in one request. If the upload fails, it is aborted, so that S3 discards the parts sent so far, and the message fails. When it is not set, every file is uploaded in one request. | boolean |  |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack, or for S3-compatible storage such as MinIO. | boolean | false |  |
| **partSize** | Part Size | The size of each part of a multipart upload, in bytes, such as `104857600` for 100 MB; the last part takes the rest. It is also the size from which a file is uploaded in parts. S3 takes parts of at least 5 MB (`5242880`), except the last one: with smaller parts, all the parts are sent and the upload then fails with `EntityTooSmall`. S3 takes at most 10,000 parts per file. Only used when `multiPartUpload` is true. When it is not set, it is 25 MB (`26214400`). | integer |  | 104857600 |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **storageClass** | Storage Class | The storage class of the files: `STANDARD`, `STANDARD_IA`, `ONEZONE_IA`, `INTELLIGENT_TIERING`, `GLACIER_IR`, `GLACIER`, `DEEP_ARCHIVE` or `REDUCED_REDUNDANCY`. A file in `GLACIER` or `DEEP_ARCHIVE` must be restored before it can be read. When it is not set, the files are stored as `STANDARD`. A `CamelAwsS3StorageClass` header on the message takes precedence. | string |  | STANDARD\_IA |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useAwsKMS** | Use AWS KMS | If true, each file is encrypted in S3 with a key of AWS KMS (SSE-KMS): the key in `awsKMSKeyId`. Use it when the bucket policy requires SSE-KMS, or a key of your own. The credentials need the permission to use the key (`kms:GenerateDataKey`), and readers of the files the permission to decrypt with it (`kms:Decrypt`). Without `awsKMSKeyId`, it has no effect. | boolean |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean | false |  |
| **useSSES3** | Use SSE-S3 | If true, the upload asks S3 to encrypt each file with keys that S3 manages (SSE-S3, `AES256`), in the `x-amz-server-side-encryption` header that some bucket policies require. S3 encrypts new files this way anyway, unless the bucket is set to another encryption. Do not combine it with `useAwsKMS`. | boolean |  |  |
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

### Example with Encryption by a KMS Key and a Storage Class

A bucket policy can require every file to be encrypted with a given key of AWS KMS (SSE-KMS); an upload without it is refused with `AccessDenied`. Set **useAwsKMS** and **awsKMSKeyId** to encrypt the files with that key, and **storageClass** to store them in another class than `STANDARD`:

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "invoices"
        bootstrapServers: "kafka.example.com:9092"
        saslAuthType: "NONE"
      steps:
        - to:
            uri: "kamelet:aws-s3-sink"
            parameters:
              bucketNameOrArn: "my-bucket"
              region: "eu-west-1"
              useDefaultCredentialsProvider: true
              useAwsKMS: true
              awsKMSKeyId: "arn:aws:kms:eu-west-1:111122223333:key/1234abcd-12ab-34cd-56ef-1234567890ab"
              storageClass: "STANDARD_IA"
```

The credentials need the permission to use the key (`kms:GenerateDataKey`), and whoever reads the files the permission to decrypt with it (`kms:Decrypt`). Without **awsKMSKeyId**, **useAwsKMS** has no effect. To ask for the encryption with keys that S3 manages (SSE-S3) instead, as some bucket policies require, set **useSSES3** to `true`. The storage class can be any class of S3, such as `STANDARD_IA`, `INTELLIGENT_TIERING` or `GLACIER_IR`; a file in `GLACIER` or `DEEP_ARCHIVE` must be restored before it can be read. A `CamelAwsS3StorageClass` header on the message takes precedence over **storageClass**.

### Example with Multipart Uploads and Conditional Writes

S3 takes at most 5 GB in one upload. With **multiPartUpload** set to `true`, a file of **partSize** bytes or more is uploaded in parts, one request per part, and S3 joins them into one file; smaller files are still uploaded in one request. **partSize** is 25 MB (`26214400`) when it is not set. S3 takes parts of at least 5 MB (`5242880`), except the last one, and at most 10,000 parts per file, so for a file of 500 GB the parts must be at least 50 MB. An upload that fails is aborted, so that S3 discards the parts sent so far.

With **conditionalWritesEnabled** set to `true`, a file is stored only when its key does not exist yet in the bucket. The upload of an existing key fails with `PreconditionFailed` (status 412), and the message fails; the file in the bucket is not changed. Use it when a file must never be replaced, such as received documents kept as they came.

```yaml
- route:
    from:
      uri: "file:/data/outbox"
      steps:
        - setHeader:
            name: file
            simple: "archive/$\{header.CamelFileName}"
        - to:
            uri: "kamelet:aws-s3-sink"
            parameters:
              bucketNameOrArn: "my-bucket"
              region: "eu-west-1"
              useDefaultCredentialsProvider: true
              multiPartUpload: true
              partSize: 104857600
              conditionalWritesEnabled: true
```

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-s3-sink"
    parameters:
      bucketNameOrArn: "my-bucket"
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-sink.kamelet.yaml)