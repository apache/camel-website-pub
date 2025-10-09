# ![aws eventbridge sink](_images/kamelets/aws-eventbridge-sink.svg) AWS Eventbridge Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send events to an Amazon Eventbridge Eventbus. In the headers, you can set the `resources-arn` / `ce-resources-arn` property to specify the ARN of resources related to the event. In the headers, you can set the `detail-type` / `ce-detail-type` property to specify the detail type related to the event. In the headers, you can set the `event-source` / `ce-event-source` property to specify the event source related to the event. If you do not set the property in the header, the Kamelet uses the given Kamelet properties as a default.

## Configuration Options

The following table summarizes the configuration options available for the `aws-eventbridge-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **eventbusNameOrArn** | Eventbus Name | **Required** The Eventbridge Eventbus name or Amazon Resource Name (ARN). | string |  |  |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **detailType** | Event Detail Type | The event detail type related to the AWS event. | string |  |  |
| **eventSource** | Event Source | The event source related to the AWS event (e.g. `aws.s3`). | string |  |  |
| **eventSourcePrefix** | Event Source Prefix | The event source prefix set for all events sent to the eventbus. | string |  |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider this parameter sets the profile name. | string |  |  |
| **resourcesArn** | Event Resource ARN | The ARN of resources related to the AWS event (e.g. `arn:aws:s3:eu-east-1:000000000001:test`). | string |  |  |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume a IAM role. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the Eventbridge client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the Eventbridge client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the Eventbridge client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Eventbridge. | boolean | false |  |

## Dependencies

At runtime, the `aws-eventbridge-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:aws2-eventbridge
    
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
            uri: "kamelet:aws-eventbridge-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS Eventbridge Sink Kamelet Description

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

### Required Headers

You need to set the `resources-arn` / `ce-resources-arn` property to specify the ARN of resources related to the event.

You need to set the `detail-type` / `ce-detail-type` property to specify the detail type related to the event.

You need to set the `event-source` / `ce-event-source` property to specify the event source related to the event.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-eventbridge-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-eventbridge-sink.kamelet.yaml)