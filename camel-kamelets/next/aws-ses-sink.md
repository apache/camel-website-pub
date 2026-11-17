# ![aws ses sink](_images/kamelets/aws-ses-sink.svg) AWS SES Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as a plain-text email through Amazon SES (Simple Email Service), to the addresses in the `to` header.

Use it to send notifications, alerts or confirmations by email from an integration, such as an order confirmation or an alert when a job fails.

Input: the body is the text of the email, as plain text. The `to` header (or `ce-to`) is required: one or more recipient addresses, separated by commas. The optional `subject` header (or `ce-subject`) is the subject; without it, the subject is a generated ID. The optional `reply-to-addresses` header (or `ce-reply-to-addresses`) is a comma-separated list of addresses that replies go to.

Output: the message is unchanged. The `CamelAwsSesMessageId` header gives the ID that SES gave the email.

Good to know: a message without a `to` header fails. The `from` address must be verified in SES, and while the SES account is in the sandbox, the recipients must be verified too.

## Configuration Options

The following table summarizes the configuration options available for the `aws-ses-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **from** | From | **Required** The sender address of the emails. It must be an address, or belong to a domain, that is verified in Amazon SES. | string |  | noreply@example.com// |
| **region** | AWS Region | **Required** The AWS region of Amazon SES to send through, where the `from` address is verified, as a region code such as `eu-west-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials: `accessKey`, `secretKey` and `sessionToken`, such as the ones AWS STS gives when you assume an IAM role. | boolean | false |  |

## Dependencies

At runtime, the `aws-ses-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:aws2-ses
    
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
            uri: "kamelet:aws-ses-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS SES Sink Kamelet Description

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

### Headers

The following header is required:

-   `to` / `ce-to` to provide a comma-separated list of email addresses.
    

In the headers, you can optionally set the following properties:

-   `subject` / `ce-subject` property to specify the email subject. If you do not set this property in the header, the Kamelet uses a generated unique ID for the email subject.
    
-   `reply-to-addresses` / `ce-reply-to-addresses` to provide a comma-separated list of reply-to email addresses.
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ses-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ses-sink.kamelet.yaml)