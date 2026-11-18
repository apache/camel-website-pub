# ![aws kinesis source](_images/kamelets/aws-kinesis-source.svg) AWS Kinesis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the records of an Amazon Kinesis data stream, one message per record.

Use it to process a stream of events that other applications write to Kinesis, such as clicks, logs or readings from devices, for example with `aws-kinesis-sink`.

Output: the body is the data of the record, as bytes. The headers give the partition key, the sequence number, the shard ID and the arrival time of the record.

Good to know: by default it reads the stream from its oldest record, and again from the oldest record each time the integration starts: it does not remember where it stopped, so records are read again after a restart. Set `iteratorType` to `LATEST` to read only the records written after it started; the records written while it was stopped are then not read. `iteratorType` can also start at a sequence number or at a time, again on each start. Records are not removed: Kinesis keeps them for the retention period of the stream. With `useKclConsumers` it reads through the Kinesis Client Library instead, which keeps where it stopped in a DynamoDB table and does not use `iteratorType`, and the body is a `ByteBuffer` rather than bytes. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. With `useKclConsumers`, the calls of the KCL to DynamoDB and CloudWatch go straight to AWS, without the proxy and without `uriEndpointOverride`.

## Configuration Options

The following table summarizes the configuration options available for the `aws-kinesis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region of the stream, as a region code such as `eu-west-1` or `us-east-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **stream** | Stream Name | **Required** The name of the Kinesis data stream, such as `clickstream`. The stream must exist. | string |  | clickstream |
| **accessKey** | Access Key | The access key ID of an IAM user, which you create in the AWS console under IAM, Users, Security credentials. Use it together with `secretKey`. Leave both out when `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` is true. | string |  |  |
| **asyncClient** | Async Client | If true, it uses the asynchronous Kinesis client of the AWS SDK. `useKclConsumers` needs it. | boolean | false |  |
| **delay** | Delay | How long to wait between two polls of the stream, in milliseconds. | integer | 500 |  |
| **iteratorType** | Start Position | Where in the stream it starts reading each time the integration starts. `TRIM_HORIZON` starts at the oldest record the stream still keeps, so the records are read again after each restart. `LATEST` reads only the records written after it started. `AT_SEQUENCE_NUMBER` and `AFTER_SEQUENCE_NUMBER` start at, or just after, the record whose sequence number is in `sequenceNumber`. `AT_TIMESTAMP` starts at the first record that arrived at or after the time in `messageTimestamp`. Not used when `useKclConsumers` is true. Enum values: \* TRIM\_HORIZON \* LATEST \* AT\_SEQUENCE\_NUMBER \* AFTER\_SEQUENCE\_NUMBER \* AT\_TIMESTAMP | string | TRIM\_HORIZON |  |
| **kclDisableCloudwatchMetricsExport** | KCL Disable CloudWatch Metrics | If true, the Kinesis Client Library does not send its metrics to CloudWatch. Only used when `useKclConsumers` is true. | boolean | false |  |
| **messageTimestamp** | Start Time | The time to start reading at, either as an ISO 8601 date and time in UTC, such as `2026-11-17T08:00:00Z`, or as milliseconds since 1970-01-01 UTC, such as `1794902400000`. It starts at the first record that arrived in the stream at or after this time. Required, and only used, when `iteratorType` is `AT_TIMESTAMP`. | string |  | 2026-11-17T08:00:00Z |
| **overrideEndpoint** | Endpoint Overwrite | If true, it connects to the address in `uriEndpointOverride` instead of to AWS. Use it for a local stand-in of AWS such as LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile in the AWS credentials file. Only used when `useProfileCredentialsProvider` is true; when it is not set, the default profile is used. | string |  | production |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **secretKey** | Secret Key | The secret access key that belongs to `accessKey`. The AWS console shows it only once, when the access key is created. | string |  |  |
| **sequenceNumber** | Sequence Number | The sequence number of the record to start at, as Kinesis gives it, such as the value of the `CamelAwsKinesisSequenceNumber` header of a record read earlier. Required, and only used, when `iteratorType` is `AT_SEQUENCE_NUMBER` or `AFTER_SEQUENCE_NUMBER`. | string |  | 49655467183424123548936502291338416434578112145614569474 |
| **sessionToken** | Session Token | The session token of temporary credentials, which comes with their access key and secret key, for example from AWS STS when you assume an IAM role. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to connect to instead of AWS, as a URL such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found in the environment instead of in `accessKey` and `secretKey`: the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the `~/.aws/credentials` file, or the IAM role of the EC2 instance, ECS task or Kubernetes pod the integration runs on. | boolean | false |  |
| **useKclConsumers** | KCL Consumer | If true, it reads the stream with the Kinesis Client Library (KCL), which shares the shards between the running copies of the integration. The KCL also uses DynamoDB and CloudWatch in the same account, so the credentials need access to them. Set `asyncClient` to true too. The calls of the KCL to DynamoDB and CloudWatch always go straight to AWS, without the proxy and without `uriEndpointOverride`. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a named profile in the AWS credentials file (`~/.aws/credentials`), as the AWS CLI does. Name the profile in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials: `accessKey`, `secretKey` and `sessionToken`, such as the ones AWS STS gives when you assume an IAM role. | boolean | false |  |

## Dependencies

At runtime, the `aws-kinesis-source` Kamelet relies upon the presence of the following dependencies:

-   camel:aws2-kinesis
    
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
      uri: "kamelet:aws-kinesis-source"
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

## AWS Kinesis Source Kamelet Description

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

### Usage example with plain consumer

You could consume the stream content directly

```yaml
- route:
    from:
      uri: "kamelet:aws-kinesis-source"
      parameters:
        useDefaultCredentialsProvider: true
        region: "eu-west-1"
        stream: "kamelets"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Where it starts reading

By default (`iteratorType` is `TRIM_HORIZON`) the Kamelet reads the stream from its oldest record each time the integration starts, so the records are read again after a restart. To read only the records written after the integration started, set `iteratorType` to `LATEST`:

```yaml
- route:
    from:
      uri: "kamelet:aws-kinesis-source"
      parameters:
        useDefaultCredentialsProvider: true
        region: "eu-west-1"
        stream: "kamelets"
        iteratorType: "LATEST"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The records written while the integration was stopped are then not read. To start at a given record, set `iteratorType` to `AT_SEQUENCE_NUMBER` or `AFTER_SEQUENCE_NUMBER` and `sequenceNumber` to its sequence number; to start at a given time, set `iteratorType` to `AT_TIMESTAMP` and `messageTimestamp` to the time, such as `2026-11-17T08:00:00Z`. The Kamelet does not remember where it stopped: it starts at the same place on each start. The KCL consumer below does not use `iteratorType`.

### Usage example with KCL Consumer

You could consume the stream content with the KCL support

```yaml
- route:
    from:
      uri: "kamelet:aws-kinesis-source"
      parameters:
        stream: "kamelets"
        useDefaultCredentialsProvider: true
        region: "eu-west-1"
        asyncClient: true
        useKclConsumers: true
      steps:
      - to:
          uri: "kamelet:log-sink"
          parameters:
            showHeaders: true
```

With the `useKclConsumers` enabled, you won’t have to deal with shard iteration directly. Everything is managed by the AWS Kinesis client library and the KCL layer.

As a side note you need to remember that the KCL consumer will need access to DynamoDB and Cloudwatch services from AWS, so it will create clients to these services under the hood and it will use them.

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

```yaml
- route:
    from:
      uri: "kamelet:aws-kinesis-source"
      parameters:
        stream: "clickstream"
        region: "eu-west-1"
        useDefaultCredentialsProvider: true
        proxyHost: "proxy.example.com"
        proxyPort: 3128
        proxyProtocol: "HTTP"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

With `useKclConsumers`, the calls of the KCL to DynamoDB and CloudWatch go straight to AWS, without the proxy: the network must let them through.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-kinesis-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-kinesis-source.kamelet.yaml)