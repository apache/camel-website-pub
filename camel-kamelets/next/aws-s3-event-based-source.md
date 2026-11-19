# ![aws s3 event based source](_images/kamelets/aws-s3-event-based-source.svg) AWS S3 Event Based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives the events of an Amazon S3 bucket, such as a new or a deleted file, from the Amazon SQS queue that Amazon EventBridge sends them to, one message per event.

Use it to react to new files in a bucket as soon as they arrive, without listing the bucket again and again, for example to process uploaded documents or imported data files. To read the files of a bucket by polling it, use `aws-s3-source`.

Output: the body is the EventBridge event, as JSON text: `detail-type` says what happened (such as `Object Created` or `Object Deleted`), `detail.bucket.name` is the bucket and `detail.object.key` the key of the file. With `getObject` set to true, the event of a file uploaded with a simple upload (PutObject) carries the content of the file instead, as a stream, with the `CamelAwsS3ProducedBucketName` and `CamelAwsS3ProducedKey` headers; the other events then come as parsed JSON (a Jackson `JsonNode`).

Good to know: it needs a setup in AWS. In the properties of the bucket, turn on sending events to Amazon EventBridge; then create an EventBridge rule for the events of source `aws.s3` and that bucket, with the queue as its target. Each event is deleted from the queue once it has been processed, unless `deleteAfterRead` is false; an event that fails stays in the queue and is received again when its visibility timeout (`visibilityTimeout`) ends. The files stay in the bucket. `getObject` skips files created by a multipart upload or a copy, and never connects through `uriEndpointOverride`. It logs in to the queue and, with `getObject`, to the bucket with `accessKey` and `secretKey`, or without keys, through the IAM role or the AWS profile of the environment, with `useDefaultCredentialsProvider` or `useProfileCredentialsProvider`. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid.

## Configuration Options

The following table summarizes the configuration options available for the `aws-s3-event-based-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **queueNameOrArn** | Queue Name | **Required** The name of the SQS queue that the EventBridge rule sends the S3 events to, such as `s3-events`, or its ARN (Amazon Resource Name). | string |  | s3-events |
| **region** | AWS Region | **Required** The AWS region of the queue and the bucket, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **amazonAWSHost** | AWS Host | The host name of AWS. Leave it as `amazonaws.com` for AWS. Any other value is the address to connect to instead, as `host:port`, together with `protocol`; `uriEndpointOverride` does the same. | string | amazonaws.com |  |
| **autoCreateQueue** | Autocreate Queue | If true, the queue is created when it does not exist. A name that ends in `.fifo` creates a FIFO queue. The credentials need the permission to create queues. | boolean | false |  |
| **delay** | Delay | How long to wait between two polls of the queue, in milliseconds. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Messages | If true, each event is deleted from the queue once it has been processed. Set it to false to keep the events; they are then received again each time the visibility timeout of the queue ends. | boolean | true |  |
| **getObject** | Get Object | If true, for an event of a file uploaded with a simple upload (PutObject), it fetches the file and sends its content instead of the event. It connects to S3 with the same credentials as the queue and with `region`, not with `uriEndpointOverride`. | boolean | false |  |
| **greedy** | Greedy Scheduler | If true, it polls again right away when the last poll received messages, instead of waiting for `delay`. | boolean | false |  |
| **maxMessagesPerPoll** | Max Messages Per Poll | The most events to receive in one request to SQS, from 1 to 10. SQS may return fewer. When it is not set, it is 10. | integer |  | 5 |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to SQS. Use it for a local stand-in of AWS such as LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **protocol** | Protocol | `https` or `http`. Only used when `amazonAWSHost` is not `amazonaws.com`. | string | https | http |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **queueURL** | Queue URL | The full address of the queue, as the SQS console shows it. When it is set, it is used as it is, and the queue is not looked up by name. | string |  | https://sqs.eu-west-1.amazonaws.com/123456789012/s3-events |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean |  |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean |  |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials: `accessKey`, `secretKey` and `sessionToken`, such as the ones AWS STS gives when you assume an IAM role. | boolean |  |  |
| **visibilityTimeout** | Visibility Timeout | How long a received event stays hidden from other readers, in seconds. If it is not deleted by then, it is received again. Set it longer than processing one event takes, such as fetching a large file with `getObject`. When it is not set, the visibility timeout of the queue is used (30 seconds for a new queue). | integer |  | 120 |
| **waitTimeSeconds** | Wait Time | How long one request waits for an event to arrive when the queue is empty, in seconds, from 0 to 20 (long polling). It saves requests, and so cost, on a queue that is often empty. When it is not set, the wait time of the queue is used. | integer |  | 20 |

## Dependencies

At runtime, the `aws-s3-event-based-source` Kamelet relies upon the presence of the following dependencies:

-   camel:aws2-sqs
    
-   camel:aws2-s3
    
-   camel:jsonpath
    
-   camel:kamelet
    
-   camel:jackson3
    

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
      uri: "kamelet:aws-s3-event-based-source"
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

## AWS S3 Event based Source Kamelet Description

### Authentication methods

The Kamelet logs in with the same credentials to the SQS queue and, when `getObject` is true, to the bucket. It can use:

-   an access key and a secret key, in `accessKey` and `secretKey`;
    
-   temporary credentials, such as the ones AWS STS gives when you assume an IAM role, with `useSessionCredentials` set to `true` and `accessKey`, `secretKey` and `sessionToken`;
    
-   the credentials of the environment, with `useDefaultCredentialsProvider` set to `true`, and no keys;
    
-   a profile of the AWS credentials file (`~/.aws/credentials`), with `useProfileCredentialsProvider` set to `true` and the name of the profile in `profileCredentialsName`, and no keys.
    

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS, which is how an IAM role reaches a pod on Amazon EKS (IRSA).
    
-   The shared credentials and config files.
    
-   Container credentials - loaded when the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` (Amazon ECS) or `AWS_CONTAINER_CREDENTIALS_FULL_URI` (EKS Pod Identity) is set.
    
-   Amazon EC2 Instance profile credentials.
    

For more information, see the [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Example with the IAM Role of the Pod

On Kubernetes, with an IAM role given to the pod through IRSA or EKS Pod Identity, no keys are needed:

```yaml
- route:
    from:
      uri: "kamelet:aws-s3-event-based-source"
      parameters:
        queueNameOrArn: "s3-events"
        region: "eu-west-1"
        useDefaultCredentialsProvider: true
        getObject: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The role needs the permission to receive and delete the messages of the queue and, with `getObject`, to read the files of the bucket.

### Example with Long Polling and a Longer Visibility Timeout

By default, the Kamelet asks the queue for events every `delay` milliseconds, and each request returns at once, even when the queue is empty. With **waitTimeSeconds**, a request waits up to that many seconds for an event to arrive, so an empty queue costs far fewer requests, and a new event is still received as soon as it arrives. **maxMessagesPerPoll** is the most events received in one request (1 to 10; 10 when it is not set). **visibilityTimeout** is how long a received event stays hidden from other readers: set it longer than processing one event takes, such as fetching a large file with `getObject`, or the event is received a second time while it is still being processed. An event that fails stays in the queue and is received again when this time ends.

```yaml
- route:
    from:
      uri: "kamelet:aws-s3-event-based-source"
      parameters:
        queueNameOrArn: "s3-events"
        region: "eu-west-1"
        useDefaultCredentialsProvider: true
        getObject: true
        waitTimeSeconds: 20
        maxMessagesPerPoll: 5
        visibilityTimeout: 300
      steps:
        - to:
            uri: "kamelet:log-sink"
```

When they are not set, the wait time and the visibility timeout of the queue are used.

### Required Setup

To use this Kamelet you’ll need to set up Eventbridge on your bucket and subscribe Eventbridge bus to an SQS Queue.

For doing this you’ll need to enable Eventbridge notification on your bucket and creating a rule on Eventbridge console related to all the events on S3 bucket and pointing to the SQS Queue specified as parameter in this Kamelet.

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password. Both the calls to SQS and, with `getObject`, the calls to S3 go through the proxy.

```yaml
- route:
    from:
      uri: "kamelet:aws-s3-event-based-source"
      parameters:
        accessKey: "{{aws.access.key}}"
        secretKey: "{{aws.secret.key}}"
        queueNameOrArn: "s3-events"
        region: "eu-west-1"
        proxyHost: "proxy.example.com"
        proxyPort: 3128
        proxyProtocol: "HTTP"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-event-based-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-event-based-source.kamelet.yaml)