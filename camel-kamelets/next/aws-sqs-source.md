# ![aws sqs source](_images/kamelets/aws-sqs-source.svg) AWS SQS Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the messages of an Amazon SQS queue, one message each, and by default deletes each message from the queue once it has been processed.

Use it to process work that other systems put in a queue, such as orders, jobs or notifications, or the events that SNS, S3 or EventBridge send to a queue. For the events of an S3 bucket, `aws-s3-event-based-source` can also fetch the files.

Output: the body is the body of the SQS message, as text. The headers give the message ID (`CamelAwsSqsMessageId`), the receipt handle and the MD5 checksum of the body. The message attributes, which the sender sets on a message, are read only when `messageAttributeNames` names them, and the system attributes of SQS, such as `SentTimestamp`, only when `attributeNames` names them. Each attribute that is read becomes a header of the same name, except a message attribute whose name starts with `Camel`.

Good to know: a message is deleted only after it has been processed without error; a message that fails stays in the queue and is received again when its visibility timeout ends. With `deleteAfterRead` set to false, the messages stay in the queue and are received again and again. A message that takes longer to process than the visibility timeout is received a second time, by this or another reader: set `extendMessageVisibility` to keep it hidden for as long as it is processed. By default one message is processed at a time; `concurrentConsumers` processes several in parallel. Without `queueURL`, `queueOwnerAWSAccountId` or an ARN in `queueNameOrArn`, the queue is looked up by listing the queues, which needs the `sqs:ListQueues` permission. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid.

## Configuration Options

The following table summarizes the configuration options available for the `aws-sqs-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **queueNameOrArn** | Queue Name | **Required** The name of the queue, such as `orders`, or its ARN (Amazon Resource Name), such as `arn:aws:sqs:eu-west-1:123456789012:orders`. | string |  | orders |
| **region** | AWS Region | **Required** The AWS region of the queue, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **amazonAWSHost** | AWS Host | The host name of AWS. Leave it as `amazonaws.com` for AWS. Any other value is the address to connect to instead, as `host:port`, together with `protocol`; `uriEndpointOverride` does the same. | string | amazonaws.com |  |
| **attributeNames** | System Attribute Names | Which of the system attributes that SQS keeps for each message to read: `All`, or a comma-separated list of names from `SenderId`, `SentTimestamp`, `ApproximateReceiveCount`, `ApproximateFirstReceiveTimestamp`, `SequenceNumber`, `MessageDeduplicationId`, `MessageGroupId`, `AWSTraceHeader` and `DeadLetterQueueSourceArn`. A name that is not one of these is ignored, with a warning in the log. Each attribute that is read becomes a header of the same name, as text; the timestamps are in milliseconds since 1970. When it is not set, no system attribute is read. | string |  | SentTimestamp,ApproximateReceiveCount |
| **autoCreateQueue** | Autocreate Queue | If true, the queue is created when it does not exist. A name that ends in `.fifo` creates a FIFO queue. The credentials need the permission to create queues. | boolean | false |  |
| **concurrentConsumers** | Concurrent Consumers | How many threads poll the queue and process its messages at the same time. When it is not set, one thread does, and the messages are processed one after the other. With more, they are processed in parallel, in no particular order. | integer |  | 5 |
| **delay** | Delay | How long to wait between two polls of the queue, in milliseconds. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Messages | If true, each message is deleted from the queue once it has been processed. Set it to false to keep the messages; they are then received again each time the visibility timeout ends. | boolean | true |  |
| **extendMessageVisibility** | Extend Message Visibility | If true, a message is kept hidden from other readers for as long as it is processed, so a message that takes longer than the visibility timeout is not received a second time. It needs `visibilityTimeout`, without which the integration does not start. Every half of `visibilityTimeout`, the visibility timeout of the messages being processed is extended by `visibilityTimeout` seconds; the credentials need the `sqs:ChangeMessageVisibility` permission. | boolean |  |  |
| **greedy** | Greedy Scheduler | If true, it polls again right away when the last poll received messages, instead of waiting for `delay`. | boolean | false |  |
| **maxMessagesPerPoll** | Max Messages Per Poll | The most messages to receive in one request to SQS, from 1 to 10. SQS may return fewer. | integer | 1 |  |
| **messageAttributeNames** | Message Attribute Names | The message attributes to read: `All`, or a comma-separated list of names, such as `customer,priority`. A name that ends in `.`**, such as `trace.`**, reads the attributes whose names start with `trace.`. Each attribute that is read becomes a header of the same name: a String attribute as text, a Number attribute as text, or as a number when its type has a label such as `Number.int`, and a Binary attribute as bytes (an AWS SDK `SdkBytes`). A message attribute whose name starts with `Camel` is not made a header. When it is not set, no message attribute is read. | string |  | All |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **protocol** | Protocol | `https` or `http`. Only used when `amazonAWSHost` is not `amazonaws.com`. | string | https | http |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **queueOwnerAWSAccountId** | Queue Owner AWS Account ID | The 12-digit ID of the AWS account that owns the queue, such as `123456789012`. When it is set, the address of the queue is built from the account, `region` and the queue name, and the queue is not looked up by listing the queues. Use it for a queue of another AWS account, or when the credentials may not list the queues. An ARN in `queueNameOrArn` gives the account too. | string |  | 123456789012 |
| **queueURL** | Queue URL | The full address of the queue, as the SQS console shows it. When it is set, it is used as it is, and the queue is not looked up by name, which needs the permission to list the queues. | string |  | https://sqs.eu-west-1.amazonaws.com/123456789012/orders |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials: `accessKey`, `secretKey` and `sessionToken`, such as the ones AWS STS gives when you assume an IAM role. | boolean | false |  |
| **visibilityTimeout** | Visibility Timeout | How long a received message stays hidden from other readers, in seconds. If it is not deleted by then, it is received again. When it is not set, the visibility timeout of the queue is used (30 seconds for a new queue). | integer |  | 30 |
| **waitTimeSeconds** | Wait Time | How long one request waits for a message to arrive when the queue is empty, in seconds, from 0 to 20 (long polling). When it is not set, the wait time of the queue is used. | integer |  | 20 |

## Dependencies

At runtime, the `aws-sqs-source` Kamelet relies upon the presence of the following dependencies:

-   camel:aws2-sqs
    
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
      uri: "kamelet:aws-sqs-source"
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

## AWS SQS Source Kamelet Description

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

### Reading the attributes of a message

By default the Kamelet reads only the body of each message. Two options ask SQS for the attributes too:

-   **Message Attribute Names** (`messageAttributeNames`): the message attributes, which the sender sets on a message. Use `All`, a comma-separated list of names, or a name that ends in `.` **for all the names with that start, such as `trace.`**.
    
-   **System Attribute Names** (`attributeNames`): the attributes that SQS keeps for each message, such as `SentTimestamp` (in milliseconds since 1970) and `ApproximateReceiveCount`. Use `All` or a comma-separated list of names.
    

Each attribute that is read becomes a header of the same name, so the next steps can use it as `customer` or `SentTimestamp`. The values are:

 
| Attribute | Header value |
| --- | --- |
| String | Text. |
| Number | Text, such as `5`. With a type label such as `Number.int`, a number. |
| Binary | Bytes, as an AWS SDK `SdkBytes`. |
| System attribute | Text. |

A message attribute whose name starts with `Camel` does not become a header. It is still in the `CamelAwsSqsMessageAttributes` header, a Map from each name to an AWS SDK `MessageAttributeValue`.

For example, to read all the message attributes and the time each message was sent:

```yaml
queueNameOrArn: orders
region: eu-west-1
messageAttributeNames: All
attributeNames: SentTimestamp
```

### Slow Messages and Parallel Processing

A received message stays hidden from other readers for its visibility timeout, 30 seconds for a new queue. A message that takes longer to process is received again, by this or another reader, and processed twice. Set `extendMessageVisibility` to true, together with `visibilityTimeout`, to keep each message hidden for as long as it is processed: every half of `visibilityTimeout`, its visibility timeout is extended by `visibilityTimeout` seconds.

By default one thread polls the queue, and the messages are processed one after the other. `concurrentConsumers` sets how many threads poll and process at the same time.

For example, to process up to five slow messages at a time, without receiving any of them twice:

```yaml
queueNameOrArn: orders
region: eu-west-1
concurrentConsumers: 5
visibilityTimeout: 60
extendMessageVisibility: true
```

### Without Permission to List the Queues

By default the Kamelet finds the address of the queue by listing the queues, which needs the `sqs:ListQueues` permission. It does not list the queues when it is given the address:

-   **Queue URL** (`queueURL`): the full address of the queue, as the SQS console shows it.
    
-   **Queue Owner AWS Account ID** (`queueOwnerAWSAccountId`): the 12-digit ID of the account that owns the queue. The address is then built from the account, the region and the queue name. Use it for a queue of another AWS account too.
    
-   An ARN in **Queue Name** (`queueNameOrArn`), which holds the account.
    

For example, for the queue `orders` of the account `123456789012`:

```yaml
queueNameOrArn: orders
region: eu-west-1
queueOwnerAWSAccountId: "123456789012"
```

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

```yaml
- route:
    from:
      uri: "kamelet:aws-sqs-source"
      parameters:
        queueNameOrArn: "orders"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-sqs-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-sqs-source.kamelet.yaml)