# ![aws sns sink](_images/kamelets/aws-sns-sink.svg) AWS SNS Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Publishes each message to an Amazon SNS topic, which delivers it to every subscriber of the topic, such as SQS queues, Lambda functions, HTTP addresses, email addresses or phone numbers.

Use it to fan out an event to many receivers at once, or to send notifications such as alerts by email or SMS through a topic. For a FIFO topic use `aws-sns-fifo-sink`; to send to a single queue use `aws-sqs-sink`.

Input: the body becomes the text of the notification, as text. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The optional `subject` header (or `ce-subject`) is the subject, which email subscribers see as the subject line; it takes precedence over the `subject` option. The other headers of the message, except the Camel ones, are sent as SNS message attributes.

Output: the message is unchanged. The `CamelAwsSnsMessageId` header gives the ID of the published message.

Good to know: with `messageStructure` set to `json`, the body is a JSON object with a text for each kind of subscriber. `serverSideEncryptionEnabled` and `kmsMasterKeyId` apply only to a topic that `autoCreateTopic` creates. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. Headers that start with `CamelAwsSns` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `aws-sns-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region of the topic, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **topicNameOrArn** | Topic Name | **Required** The name of the topic, such as `order-events`, or its ARN (Amazon Resource Name), such as `arn:aws:sns:eu-west-1:123456789012:order-events`. | string |  | order-events |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **autoCreateTopic** | Autocreate Topic | If true, the topic is created when it does not exist. The credentials need the permission to create topics. | boolean | false |  |
| **kmsMasterKeyId** | KMS Key ID | The key of AWS KMS for a new topic to encrypt its messages with, as its key ID, such as `1234abcd-12ab-34cd-56ef-1234567890ab`, an alias, such as `alias/aws/sns`, or its ARN. Only used when `serverSideEncryptionEnabled` and `autoCreateTopic` are true and the topic does not exist yet. | string |  | alias/aws/sns |
| **messageStructure** | Message Structure | Set it to `json` to send a different text to each kind of subscriber. The body is then a JSON object with a `default` text for all subscribers and, optionally, a text for each protocol, such as `\{"default": "Order 42 received", "email": "Your order 42 was received."}`; SNS rejects a body without `default`. When it is not set, the body is the text for all subscribers. Enum values: \* json | string |  |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **serverSideEncryptionEnabled** | Server-Side Encryption | If true, a topic that `autoCreateTopic` creates is created to encrypt its messages with the key of AWS KMS in `kmsMasterKeyId`, which is then required. It does not change a topic that exists already. | boolean |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **subject** | Subject | The subject of every notification, which email subscribers see as the subject line, and an SQS queue subscribed to the topic gets in the `Subject` field of the notification. A `subject` or `ce-subject` header on the message takes precedence. It is ASCII text without line breaks; a subject longer than 100 characters is cut to 100. When it is not set, only the messages with a header have a subject. | string |  | Order received |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials: `accessKey`, `secretKey` and `sessionToken`, such as the ones AWS STS gives when you assume an IAM role. | boolean | false |  |

## Dependencies

At runtime, the `aws-sns-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:aws2-sns
    
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
            uri: "kamelet:aws-sns-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS SNS Sink Kamelet Description

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

In the Kamelet you can optionally set the following header:

-   `subject` / `ce-subject`: the subject of the message. It takes precedence over the `subject` option.
    

### The Subject

The `subject` option sets the subject of every notification. A `subject` or `ce-subject` header on a message takes precedence over it. Email subscribers see the subject as the subject line, and an SQS queue subscribed to the topic gets it in the `Subject` field of the JSON notification. A subject is ASCII text without line breaks; a longer one than 100 characters is cut to 100.

### A Text for Each Kind of Subscriber

With `messageStructure` set to `json`, the body is a JSON object with a `default` text for all subscribers and, optionally, a text for each protocol, such as `sqs`, `email` or `sms`. SNS rejects a body without `default`. For example, the body

```json
{"default": "Order 42 received", "email": "Your order 42 was received.", "sqs": "{\"orderId\": 42}"}
```

sends `{"orderId": 42}` to the SQS queues subscribed to the topic, and `Your order 42 was received.` to the email addresses.

### Encrypting a New Topic

`serverSideEncryptionEnabled` and `kmsMasterKeyId` apply only to a topic that `autoCreateTopic` creates: the topic is then created to encrypt its messages with that key of AWS KMS. With `serverSideEncryptionEnabled` and no `kmsMasterKeyId`, the integration does not start when the topic must be created. They do not change a topic that exists already.

For example:

```yaml
- to:
    uri: "kamelet:aws-sns-sink"
    parameters:
      topicNameOrArn: "order-events"
      region: "eu-west-1"
      subject: "Order received"
      messageStructure: "json"
```

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-sns-sink"
    parameters:
      topicNameOrArn: "order-events"
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-sns-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-sns-sink.kamelet.yaml)