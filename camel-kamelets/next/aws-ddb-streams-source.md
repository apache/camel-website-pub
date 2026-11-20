# ![aws ddb streams source](_images/kamelets/aws-ddb-streams-source.svg) AWS DynamoDB Streams Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the changes made to the items of an Amazon DynamoDB table from its stream, one message per inserted, modified or removed item.

Use it to react when data changes in a table, for example to copy new orders to another system, keep a search index or a cache up to date, or record an audit trail. To write items into a table, use `aws-ddb-sink`.

Output: the body is a JSON object, as JSON text in bytes with the `Content-Type` header `application/json`, that describes one change: `eventName` is `INSERT`, `MODIFY` or `REMOVE`, and `dynamodb` holds the key of the item (`keys`) and, depending on the view type of the stream, the item before (`oldImage`) and after (`newImage`) the change, with the type of each attribute. The headers give the ID and the name of the event.

Good to know: DynamoDB Streams must be enabled on the table, with the view type that holds the images you need, such as new and old images. By default it reads only the changes made after it starts, up to 100 in one poll; set `maxResultsPerRequest` to read fewer at a time. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid.

## Configuration Options

The following table summarizes the configuration options available for the `aws-ddb-streams-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region of the table, such as `eu-west-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **table** | Table Name | **Required** The name of the DynamoDB table to receive the changes of. DynamoDB Streams must be enabled on the table. | string |  | orders |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **delay** | Delay | How long to wait between two reads of the stream, in milliseconds. | integer | 500 |  |
| **maxResultsPerRequest** | Max Changes Per Poll | The most changes it reads in one poll, from 1 to 1000. The number is shared between the shards of the stream that it reads, at least 1 each. When it is not set, it is 100. With a lower number, a burst of changes takes more polls, `delay` apart, to read. | integer |  | 50 |
| **overrideEndpoint** | Endpoint Overwrite | If true, the requests go to the address in `uriEndpointOverride` instead of AWS, for example to test against LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile to use from the AWS credentials file. Only used when `useProfileCredentialsProvider` is true. | string |  |  |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **secretKey** | Secret Key | The secret access key that goes with `accessKey`. AWS shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which AWS gives together with their access key and secret key. Only used when `useSessionCredentials` is true. | string |  |  |
| **streamIteratorType** | Stream Iterator Type | Where to start reading: `FROM_LATEST` receives only the changes made after the Kamelet starts; `FROM_START` first receives all the changes still kept in the stream, which can take a while before it catches up. Enum values: \* FROM\_LATEST \* FROM\_START | string | FROM\_LATEST |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to send the requests to instead of the usual AWS address, such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found the way the AWS SDK finds them: from the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the shared credentials file, or the IAM role of the machine, container or pod it runs on. Then `accessKey` and `secretKey` are not needed. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a profile of the AWS credentials file (`~/.aws/credentials`), the one named in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials, such as those of an assumed IAM role: `accessKey`, `secretKey` and `sessionToken` together. | boolean | false |  |

## Dependencies

At runtime, the `aws-ddb-streams-source` Kamelet relies upon the presence of the following dependencies:

-   camel:gson
    
-   camel:aws2-ddb
    
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
      uri: "kamelet:aws-ddb-streams-source"
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

## AWS DynamoDB Streams Source Kamelet Description

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

### Fewer Changes in One Poll

The Kamelet reads up to 100 changes in one poll, and polls again `delay` milliseconds later. To read fewer at a time, for example so that a slow route behind it is not handed a large burst at once, set `maxResultsPerRequest`. The number is shared between the shards of the stream. Here a burst of 1000 changes is read 50 at a time, one poll a second:

```yaml
- route:
    from:
      uri: "kamelet:aws-ddb-streams-source"
      parameters:
        table: "orders"
        region: "eu-west-1"
        useDefaultCredentialsProvider: true
        maxResultsPerRequest: 50
        delay: 1000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

```yaml
- route:
    from:
      uri: "kamelet:aws-ddb-streams-source"
      parameters:
        table: "orders"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ddb-streams-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ddb-streams-source.kamelet.yaml)