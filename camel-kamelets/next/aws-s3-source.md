# ![aws s3 source](_images/kamelets/aws-s3-source.svg) AWS S3 Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files (objects) in an Amazon S3 bucket, one message per file, and by default deletes each file once it has been read.

Use it to process files that another system drops into a bucket, such as uploaded documents, exported reports or log files. To react to new files through S3 event notifications instead of reading the bucket over and over, use `aws-s3-event-based-source`.

Output: the body is the content of the file, as bytes, and the `Content-Type` header is `application/octet-stream`. The headers give the bucket name, the key (the path of the file in the bucket), the content type and the ETag of the file.

Good to know: files are deleted from the bucket after they are read, unless `deleteAfterRead` is set to false; then the same files are read again on every poll. `moveAfterRead` moves them to another bucket instead. It also works with S3-compatible storage, such as MinIO, through `overrideEndpoint` and `uriEndpointOverride`. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid.

## Configuration Options

The following table summarizes the configuration options available for the `aws-s3-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name | **Required** The S3 Bucket name or Amazon Resource Name (ARN). | string |  |  |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | Specifies to automatically create the S3 bucket. | boolean | false |  |
| **delay** | Delay | The number of milliseconds before the next poll of the selected bucket. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Objects | If true, each file is deleted from the bucket after it has been read. Set it to false to keep the files; they are then read again on every poll. | boolean | true |  |
| **destinationBucket** | Destination Bucket | Define the destination bucket where an object must be moved when moveAfterRead is set to true. | string |  |  |
| **destinationBucketPrefix** | Destination Bucket Prefix | Define the destination bucket prefix to use when an object must be moved, and moveAfterRead is set to true. | string |  |  |
| **destinationBucketSuffix** | Destination Bucket Suffix | Define the destination bucket suffix to use when an object must be moved, and moveAfterRead is set to true. | string |  |  |
| **forcePathStyle** | Force Path Style | Forces path style when accessing AWS S3 buckets. | boolean | false |  |
| **ignoreBody** | Ignore Body | If true, the S3 Object body is ignored. Setting this to true overrides any behavior defined by the `includeBody` option. If false, the S3 object is put in the body. | boolean | false |  |
| **maxMessagesPerPoll** | Max Messages Per Poll | The most files to read at each poll. Use 0 or a negative number for no limit. | integer | 10 |  |
| **moveAfterRead** | Move Objects After Delete | Move objects from S3 bucket to a different bucket after they have been retrieved. | boolean | false |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **prefix** | Prefix | The AWS S3 bucket prefix to consider while searching. | string |  | folder/ |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider this parameter sets the profile name. | string |  |  |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume a IAM role. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the S3 client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the S3 client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the S3 client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in S3. | boolean | false |  |

## Dependencies

At runtime, the `aws-s3-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:aws-s3-source"
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

## AWS S3 Source Kamelet Description

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

### Usage examples

You could consume the bucket content and directly delete the object once consumed

```yaml
- route:
    from:
      uri: "kamelet:aws-s3-source"
      parameters:
        useDefaultCredentialsProvider: true
        region: "eu-west-1"
        bucketNameOrArn: "kamelets"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This kind of approach ensures that the object is consumed just one time and after the consumption it is deleted from the S3 bucket.

The `deleteAfterRead` property is true by default.

If you set the property to false you’ll consume the same set of objects multiple times and you’ll have to deal with managing the situation.

The `ignoreBody` option is set to false by default, but you can enable it. With that option set you’re going to ignore the file payload and just consume the object metadata.

You could also define a `prefix` parameter. With that set you’re going to consume only files starting with that prefix. As an example you could have:

```yaml
- route:
    from:
      uri: "kamelet:aws-s3-source"
      parameters:
        useDefaultCredentialsProvider: true
        region: "eu-west-1"
        bucketNameOrArn: "kamelets"
        prefix: "foo/"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

By using the prefix `foo/` the files consumed will only come from the folder named `foo`.

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

```yaml
- route:
    from:
      uri: "kamelet:aws-s3-source"
      parameters:
        bucketNameOrArn: "kamelets"
        region: "eu-west-1"
        useDefaultCredentialsProvider: true
        proxyHost: "proxy.example.com"
        proxyPort: 3128
        proxyProtocol: "HTTP"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-source.kamelet.yaml)