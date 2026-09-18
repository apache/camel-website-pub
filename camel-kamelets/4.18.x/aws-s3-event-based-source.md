# ![aws s3 event based source](_images/kamelets/aws-s3-event-based-source.svg) AWS S3 Event Based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from AWS SQS subscribed to Eventbridge Bus reporting events related to an S3 bucket or multiple buckets.

## Configuration Options

The following table summarizes the configuration options available for the `aws-s3-event-based-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The access key obtained from AWS. | string |  |  |
| **queueNameOrArn** | Queue Name | **Required** The SQS Queue Name or ARN. | string |  |  |
| **region** | AWS Region | **Required** The AWS region to access. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  |  |
| **secretKey** | Secret Key | **Required** The secret key obtained from AWS. | string |  |  |
| **amazonAWSHost** | AWS Host | The hostname of the Amazon AWS cloud. | string | amazonaws.com |  |
| **autoCreateQueue** | Autocreate Queue | Setting the autocreation of the SQS queue. | boolean | false |  |
| **delay** | Delay | The number of milliseconds before the next poll of the selected stream. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Messages | Delete messages after consuming them. | boolean | true |  |
| **getObject** | Greedy Object in Bucket | If `getObject` is enabled, then the file created in the bucket is retrieved and returned as body. If not, only the event will returned as body. | boolean | false |  |
| **greedy** | Greedy Scheduler | If greedy is enabled, then the polling will happen immediately again, if the previous run polled 1 or more messages. | boolean | false |  |
| **overrideEndpoint** | Endpoint Overwrite | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | boolean | false |  |
| **protocol** | Protocol | The underlying protocol used to communicate with SQS. | string | https | http or https |
| **queueURL** | Queue URL | The full SQS Queue URL. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. | string |  |  |

## Dependencies

At runtime, the `aws-s3-event-based-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:aws2-sqs
    
-   camel:aws2-s3
    
-   camel:jsonpath
    
-   camel:kamelet
    
-   camel:jackson
    

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