# ![aws sts assume role action](_images/kamelets/aws-sts-assume-role-action.svg) AWS STS Assume Role Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Assume a role through STS

## Configuration Options

The following table summarizes the configuration options available for the `aws-sts-assume-role-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  |  |
| **accessKey** | Access Key | The access key obtained from AWS. | string |  |  |
| **profileCredentialsName** | Profile Credentials Name | If using a profile credentials provider this parameter sets the profile name. | string |  |  |
| **secretKey** | Secret Key | The secret key obtained from AWS. | string |  |  |
| **sessionToken** | Session Token | Amazon AWS Session Token used when the user needs to assume a IAM role. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | Set whether the STS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | Set whether the STS client should expect to load credentials through a profile credentials provider. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | Set whether the STS client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in STS. | boolean | false |  |

## Dependencies

At runtime, the `aws-sts-assume-role-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
-   camel:aws2-sts
    

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
            uri: "kamelet:aws-sts-assume-role-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS STS Assume Role Action Kamelet Description

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

Only one of access key/secret key or default credentials provider can be used.

For more information, see the [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Required Headers

In this Kamelet you must specify the following headers:

-   `role-arn` / `ce-role-arn` property to specify the role ARN you want to assume.
    
-   `role-session-name` / `ce-role-session-name` property to specify the role Session name you want to use.
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-sts-assume-role-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-sts-assume-role-action.kamelet.yaml)