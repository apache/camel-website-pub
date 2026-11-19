# ![aws ses sink](_images/kamelets/aws-ses-sink.svg) AWS SES Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as a plain-text email through Amazon SES (Simple Email Service), to the addresses in the `to` header or the `to` option.

Use it to send notifications, alerts or confirmations by email from an integration, such as an order confirmation or an alert when a job fails.

Input: the body is the text of the email, as plain text. The `to` header (or `ce-to`) gives one or more recipient addresses, separated by commas; it is required unless the `to` option is set. The optional `subject` header (or `ce-subject`) is the subject; without it and without the `subject` option, the subject is a generated ID. The optional `reply-to-addresses` header (or `ce-reply-to-addresses`) is a comma-separated list of addresses that replies go to. Each of these headers takes precedence over the option of the same purpose.

Output: the message is unchanged. The `CamelAwsSesMessageId` header gives the ID that SES gave the email.

Good to know: a message without a `to` header fails, unless the `to` option is set. The `cc`, `bcc`, `returnPath` and `configurationSet` options apply to every email. The `from` address, and `returnPath` when it is set, must be verified in SES, and while the SES account is in the sandbox, the recipients must be verified too. A `configurationSet` that does not exist in SES makes every email fail. To reach a local stand-in of AWS, use `overrideEndpoint` and `uriEndpointOverride`. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. Headers that start with `CamelAwsSes` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `aws-ses-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **from** | From | **Required** The sender address of the emails. It must be an address, or belong to a domain, that is verified in Amazon SES. | string |  | noreply@example.com// |
| **region** | AWS Region | **Required** The AWS region of Amazon SES to send through, where the `from` address is verified, as a region code such as `eu-west-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **bcc** | Bcc | The addresses to send a blind copy of every email to (Bcc), separated by commas. The other recipients do not see them. | string |  | archive@example.com// |
| **cc** | Cc | The addresses to send a copy of every email to (Cc), separated by commas. The recipients see them. | string |  | team@example.com// |
| **configurationSet** | Configuration Set | The name of an SES configuration set to send the emails with, such as `my-configuration-set`, for example to publish their delivery, bounce, open and click events to CloudWatch, SNS or Firehose. It must exist in SES in the region, or every email fails with `ConfigurationSetDoesNotExist`. | string |  | my-configuration-set |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to SES. Use it for a local stand-in of AWS such as LocalStack or Floci, or for a VPC endpoint of SES. | boolean |  |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **replyToAddresses** | Reply-To Addresses | The addresses that replies go to, separated by commas, such as `support@example.com`. A `reply-to-addresses` header on the message takes precedence. When it is not set, the emails have no Reply-To, and replies go to `from`. | string |  | support@example.com// |
| **returnPath** | Return Path | The address that bounces and complaints are sent to, such as `bounces@example.com`. It must be verified in SES, as `from` is. When it is not set, they go to the `from` address. | string |  | bounces@example.com// |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **subject** | Subject | The subject of every email. A `subject` header on the message takes precedence. When it is not set, and there is no `subject` header, the subject is a generated ID. | string |  | Order confirmation |
| **to** | To | The addresses to send every email to, separated by commas, such as `ops@example.com,[oncall@example.com](mailto:oncall@example.com)`. A `to` header on the message takes precedence. When it is not set, the `to` header is required. | string |  | ops@example.com// |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
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

The following header is required, unless the `to` option is set:

-   `to` / `ce-to` to provide a comma-separated list of email addresses.
    

In the headers, you can optionally set the following properties:

-   `subject` / `ce-subject` property to specify the email subject. If you do not set this property in the header, nor the `subject` option, the Kamelet uses a generated unique ID for the email subject.
    
-   `reply-to-addresses` / `ce-reply-to-addresses` to provide a comma-separated list of reply-to email addresses.
    

Each of these headers takes precedence over the option of the same purpose: `to`, `subject` and `replyToAddresses`.

### Example with Fixed Recipients and a Configuration Set

When every email goes to the same people, such as the alerts of a job, set the recipients and the subject as options, and the messages need no headers. **cc** and **bcc** send a copy, and a blind copy, of every email. **returnPath** is the address that bounces and complaints go to; it must be verified in SES, as **from** is. **configurationSet** names an SES configuration set, which can publish the delivery, bounce, open and click events of the emails to CloudWatch, SNS or Firehose; it must exist in SES in the region, or every email fails with `ConfigurationSetDoesNotExist`.

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "job-failures"
        bootstrapServers: "kafka.example.com:9092"
        saslAuthType: "NONE"
      steps:
        - to:
            uri: "kamelet:aws-ses-sink"
            parameters:
              from: "noreply@example.com"
              region: "eu-west-1"
              useDefaultCredentialsProvider: true
              to: "ops@example.com,oncall@example.com"
              cc: "team-lead@example.com"
              bcc: "archive@example.com"
              subject: "Nightly job failed"
              replyToAddresses: "support@example.com"
              returnPath: "bounces@example.com"
              configurationSet: "alerts"
```

The addresses are plain addresses, separated by commas, such as `ops@example.com,[oncall@example.com](mailto:oncall@example.com)`. A `to`, `subject` or `reply-to-addresses` header on a message still takes precedence over the option.

### Example with a Local Stand-in of AWS

To test without AWS, point the Kamelet to a local stand-in that has SES, such as LocalStack or Floci, with **overrideEndpoint** and **uriEndpointOverride**:

```yaml
- to:
    uri: "kamelet:aws-ses-sink"
    parameters:
      from: "noreply@example.com"
      region: "us-east-1"
      accessKey: "test"
      secretKey: "test"
      to: "someone@example.com"
      overrideEndpoint: true
      uriEndpointOverride: "http://localhost:4566"
```

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-ses-sink"
    parameters:
      from: "noreply@example.com"
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ses-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ses-sink.kamelet.yaml)