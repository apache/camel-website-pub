# ![aws eventbridge sink](_images/kamelets/aws-eventbridge-sink.svg) AWS Eventbridge Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as an event to an Amazon EventBridge event bus, where rules route it to targets such as Lambda functions, SQS queues or Step Functions.

Use it to publish business events, such as `Order Shipped`, for other applications and AWS services to react to through EventBridge rules.

Input: the body is the detail of the event, as JSON text that holds a JSON object, such as `{"orderId": "A-1"}`. The `detail-type` header (or `ce-detail-type`) is the detail type, such as `Order Shipped`; the `event-source` header (or `ce-event-source`, or `ce-source`) is the source, such as `com.example.shop`; and the `resources-arn` header (or `ce-resources-arn`) is the ARN (Amazon Resource Name) of the resource the event is about, or several separated by commas. Each header falls back on its option: `detailType`, `eventSource` and `resourcesArn`.

Output: when it is used inside a route, the body afterwards is the response of EventBridge, and the `CamelAwsEventbridgeFailedEntryCount` header is 1 when EventBridge rejected the event, 0 otherwise.

Good to know: a message fails when it has no detail type, no source or no resource ARN, from a header or an option. `eventSourcePrefix` is put before every source. An event that EventBridge rejects, such as one whose body is not a JSON object, is not delivered; depending on the Camel version the message then fails, or it only sets `CamelAwsEventbridgeFailedEntryCount` to 1. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. Headers that start with `CamelAwsEventbridge` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `aws-eventbridge-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **eventbusNameOrArn** | Event Bus Name | **Required** The name of the event bus, such as `default` or `orders`, or its ARN (Amazon Resource Name). | string |  | orders |
| **region** | AWS Region | **Required** The AWS region of the event bus, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **detailType** | Event Detail Type | The detail type of the events, a short name of what happened that rules use to match, such as `Order Shipped`. Used when the message has no `detail-type` header. Each event needs one. | string |  | Order Shipped |
| **eventSource** | Event Source | The source of the events, which says what sent them and which rules use to match, such as `com.example.shop`. Used when the message has no `event-source` header. Each event needs one. | string |  | com.example.shop |
| **eventSourcePrefix** | Event Source Prefix | Text put before the source of every event, from the `event-source` header or the `eventSource` option. For example, with `com.example.` a source of `shop` becomes `com.example.shop`. | string |  | com.example. |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **resourcesArn** | Resource ARNs | The ARNs (Amazon Resource Names) of the resources the event is about, separated by commas. Used when the message has no `resources-arn` header. Each event needs at least one. | string |  | arn:aws:s3:::my-bucket |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials: `accessKey`, `secretKey` and `sessionToken`, such as the ones AWS STS gives when you assume an IAM role. | boolean | false |  |

## Dependencies

At runtime, the `aws-eventbridge-sink` Kamelet relies upon the presence of the following dependencies:

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

### Headers

Each event needs a resource ARN, a detail type and a source. Each comes from a header, or, when the message does not have the header, from the option of the Kamelet:

-   the `resources-arn` / `ce-resources-arn` header, or the `resourcesArn` option, to specify the ARN of resources related to the event, separated by commas.
    
-   the `detail-type` / `ce-detail-type` header, or the `detailType` option, to specify the detail type related to the event.
    
-   the `event-source` / `ce-event-source` / `ce-source` header, or the `eventSource` option, to specify the event source related to the event. The `eventSourcePrefix` option is put before it.
    

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-eventbridge-sink"
    parameters:
      eventbusNameOrArn: "orders"
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-eventbridge-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-eventbridge-sink.kamelet.yaml)