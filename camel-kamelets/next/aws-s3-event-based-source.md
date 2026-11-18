# ![aws s3 event based source](_images/kamelets/aws-s3-event-based-source.svg) AWS S3 Event Based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives the events of an Amazon S3 bucket, such as a new or a deleted file, from the Amazon SQS queue that Amazon EventBridge sends them to, one message per event.

Use it to react to new files in a bucket as soon as they arrive, without listing the bucket again and again, for example to process uploaded documents or imported data files. To read the files of a bucket by polling it, use `aws-s3-source`.

Output: the body is the EventBridge event, as JSON text: `detail-type` says what happened (such as `Object Created` or `Object Deleted`), `detail.bucket.name` is the bucket and `detail.object.key` the key of the file. With `getObject` set to true, the event of a file uploaded with a simple upload (PutObject) carries the content of the file instead, as a stream, with the `CamelAwsS3ProducedBucketName` and `CamelAwsS3ProducedKey` headers; the other events then come as parsed JSON (a Jackson `JsonNode`).

Good to know: it needs a setup in AWS. In the properties of the bucket, turn on sending events to Amazon EventBridge; then create an EventBridge rule for the events of source `aws.s3` and that bucket, with the queue as its target. Each event is deleted from the queue once it has been processed, unless `deleteAfterRead` is false. The files stay in the bucket. `getObject` skips files created by a multipart upload or a copy, and never connects through `uriEndpointOverride`.

## Configuration Options

The following table summarizes the configuration options available for the `aws-s3-event-based-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. | string |  |  |
| **queueNameOrArn** | Queue Name | **Required** The name of the SQS queue that the EventBridge rule sends the S3 events to, such as `s3-events`, or its ARN (Amazon Resource Name). | string |  | s3-events |
| **region** | AWS Region | **Required** The AWS region of the queue and the bucket, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **secretKey** | Secret Key | **Required** The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **amazonAWSHost** | AWS Host | The host name of AWS. Leave it as `amazonaws.com` for AWS. Any other value is the address to connect to instead, as `host:port`, together with `protocol`; `uriEndpointOverride` does the same. | string | amazonaws.com |  |
| **autoCreateQueue** | Autocreate Queue | If true, the queue is created when it does not exist. A name that ends in `.fifo` creates a FIFO queue. The credentials need the permission to create queues. | boolean | false |  |
| **delay** | Delay | How long to wait between two polls of the queue, in milliseconds. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Messages | If true, each event is deleted from the queue once it has been processed. Set it to false to keep the events; they are then received again each time the visibility timeout of the queue ends. | boolean | true |  |
| **getObject** | Get Object | If true, for an event of a file uploaded with a simple upload (PutObject), it fetches the file and sends its content instead of the event. It connects to S3 with `accessKey`, `secretKey` and `region` only, not with `uriEndpointOverride`. | boolean | false |  |
| **greedy** | Greedy Scheduler | If true, it polls again right away when the last poll received messages, instead of waiting for `delay`. | boolean | false |  |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to SQS. Use it for a local stand-in of AWS such as LocalStack. | boolean | false |  |
| **protocol** | Protocol | `https` or `http`. Only used when `amazonAWSHost` is not `amazonaws.com`. | string | https | http |
| **queueURL** | Queue URL | The full address of the queue, as the SQS console shows it. When it is set, it is used as it is, and the queue is not looked up by name. | string |  | https://sqs.eu-west-1.amazonaws.com/123456789012/s3-events |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |

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

Access Key/Secret Key is the basic method for authenticating to the AWS SQS Service.

### Required Setup

To use this Kamelet you’ll need to set up Eventbridge on your bucket and subscribe Eventbridge bus to an SQS Queue.

For doing this you’ll need to enable Eventbridge notification on your bucket and creating a rule on Eventbridge console related to all the events on S3 bucket and pointing to the SQS Queue specified as parameter in this Kamelet.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-event-based-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-s3-event-based-source.kamelet.yaml)