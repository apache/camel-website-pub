# ![aws kinesis sink](_images/kamelets/aws-kinesis-sink.svg) AWS Kinesis Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to AWS Kinesis.

## Configuration Options

The following table summarizes the configuration options available for the `aws-kinesis-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  |  |
| **stream** | Stream Name | **Required** The Kinesis stream that you want to access. The Kinesis stream that you specify must already exist. | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider this parameter sets the profile name. | string |  |  |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume a IAM role. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the Kinesis client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the Kinesis client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the Kinesis client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis. | boolean | false |  |

## Dependencies

At runtime, the `aws-kinesis-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:aws2-kinesis
    
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
            uri: "kamelet:aws-kinesis-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Kinesis Sink Kamelet Description

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

In the header, you can optionally set the `file` / `ce-partition` property to set the Kinesis partition key.

If you do not set the property in the header, the Kamelet uses the exchange ID for the partition key.

You can also set the `sequence-number` / `ce-sequencenumber` property in the header to specify the Sequence number.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-kinesis-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-kinesis-sink.kamelet.yaml)