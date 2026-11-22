# ![aws eventbridge source](_images/kamelets/aws-eventbridge-source.svg) AWS Eventbridge Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the events that an Amazon EventBridge rule matches on an event bus, one message per event, through an SQS queue that it adds to the rule as a target.

Use it to react to the events of your applications or of AWS services, such as `Order Shipped` from a shop or a change of state of an EC2 instance, without setting up a queue yourself. To publish events, use `aws-eventbridge-sink`. For the events of an S3 bucket, `aws-s3-event-based-source` reads a queue that you made the target of a rule yourself, gives each event an ID that is the same in its copies, and can fetch the files.

Output: the body is the whole EventBridge event, as JSON text: `id` (the ID that EventBridge gave the event), `detail-type`, `source`, `account`, `time`, `region`, `resources` and `detail`, which holds what the sender of the event put in it, such as `{"orderId": "A-1"}`. The `CamelAwsEventbridgeMessageId` header is the ID of the SQS message that carried the event, and `CamelAwsEventbridgeReceiptHandle` its receipt handle.

Good to know: the rule must exist on the event bus before the Kamelet starts, or it fails to start, and no queue is created; its event pattern decides which events arrive. Create it in the EventBridge console or with `aws events put-rule`. Without `queueURL`, it creates a queue whose policy lets only this rule send events to it, and adds it to the rule. By default the queue is named `camel-eventbridge-` followed by the rule name and a random part, and when the Kamelet stops, it removes the queue from the rule and deletes it, so the events of the time it does not run are lost, and each replica gets its own queue and every event. With `deleteQueueOnShutdown` false, the queue is named `camel-eventbridge-` followed by the rule name and a part made from the event bus and the rule name, and it stays a target of the rule when the Kamelet stops: it collects the events while the Kamelet does not run, the next start reuses it, and the replicas share it and its events. Delete that queue yourself once it is no longer used. With `queueURL`, it adds your queue to the rule and leaves it there, so the queue collects the events while the Kamelet does not run, and the replicas share the events. Each event is deleted from the queue once it has been processed; an event that fails stays in the queue and is received again each time `visibilityTimeout` ends, until it is processed. Stopping the Kamelet can take up to `waitTimeSeconds`, as it waits for the last request to SQS to end. It logs in to EventBridge and SQS with the same credentials, which need `events:PutTargets` and `events:RemoveTargets` on the rule, and `sqs:ReceiveMessage`, `sqs:DeleteMessage` and `sqs:GetQueueAttributes` on the queue, plus `events:DescribeRule` on the rule and `sqs:CreateQueue`, `sqs:SetQueueAttributes` and `sqs:DeleteQueue` without `queueURL`. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid.

## Configuration Options

The following table summarizes the configuration options available for the `aws-eventbridge-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **eventbusNameOrArn** | Event Bus Name | **Required** The name of the event bus of the rule, such as `default` or `orders`, or its ARN (Amazon Resource Name). | string |  | orders |
| **region** | AWS Region | **Required** The AWS region of the event bus and the queue, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **ruleName** | Rule Name | **Required** The name of the EventBridge rule whose events to receive, such as `orders-shipped`. The rule must exist on the event bus; its event pattern decides which events arrive. | string |  | orders-shipped |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **delay** | Delay | How long to wait between two polls of the queue, in milliseconds. | integer | 500 |  |
| **deleteQueueOnShutdown** | Delete Queue On Stop | Only used without `queueURL`. If true, the queue that the Kamelet creates is removed from the rule and deleted when the Kamelet stops, so the events of the time it does not run are lost. If false, the queue has a name made from the event bus and the rule name and stays a target of the rule, so it collects the events while the Kamelet does not run, and the next start reuses it. | boolean | true |  |
| **greedy** | Greedy Scheduler | If true, it polls again right away when the last poll received events, instead of waiting for `delay`. | boolean | false |  |
| **maxMessagesPerPoll** | Max Events Per Poll | The most events to receive in one request to SQS, from 1 to 10. SQS may return fewer. | integer | 10 |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **queueURL** | Queue URL | The full address of an SQS queue of your own to receive the events through, as the SQS console shows it. Its access policy must let EventBridge (`events.amazonaws.com`) send messages to it. It stays a target of the rule when the Kamelet stops. When it is not set, a queue is created when the Kamelet starts, and deleted when it stops unless `deleteQueueOnShutdown` is false. | string |  | https://sqs.eu-west-1.amazonaws.com/123456789012/orders-events |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, for EventBridge and SQS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials: `accessKey`, `secretKey` and `sessionToken`, such as the ones AWS STS gives when you assume an IAM role. | boolean | false |  |
| **visibilityTimeout** | Visibility Timeout | How long a received event stays hidden from other readers of the queue, in seconds. If it has not been processed by then, it is received again. Set it longer than processing one event takes. | integer | 30 |  |
| **waitTimeSeconds** | Wait Time | How long one request waits for an event to arrive when the queue is empty, in seconds, from 0 to 20 (long polling). It saves requests, and so cost, when events are rare. | integer | 20 |  |

## Dependencies

At runtime, the `aws-eventbridge-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:aws-eventbridge-source"
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-eventbridge-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-eventbridge-source.kamelet.yaml)