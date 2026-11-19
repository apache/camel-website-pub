# ![aws ddb sink](_images/kamelets/aws-ddb-sink.svg) AWS DynamoDB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Writes each message as an item into an Amazon DynamoDB table: it creates or replaces, updates or deletes the item, depending on the operation.

Use it to store events or records, such as orders, sensor readings or user profiles, as items of a DynamoDB table, or to delete items. To receive the changes made to a table, use `aws-ddb-streams-source`.

Input: the body is a JSON object, as JSON text, whose fields are the attributes of the item, such as `{"id":"A-1","customer":"Alice","total":42}`; it must hold the key attributes of the table. Text becomes a string attribute, a number a number, true or false a boolean, an object a map, and a list a set of strings or of numbers. With `DeleteItem` the body only needs the key. With `UpdateItem` the body holds a `key` object with the key attributes and an `item` object with the attributes to set, such as `{"key":{"id":"A-1"},"item":{"status":"shipped"}}`. The optional `CamelAwsDdbOperation` header chooses the operation for one message.

Output: the body is unchanged. The `CamelAwsDdbAttributes` header holds the attributes of the item before the change (`PutItem`, `DeleteItem`) or after it (`UpdateItem`).

Good to know: `PutItem`, the default, replaces the whole item that has the same key, so the attributes missing from the body are lost; use `UpdateItem` to change some attributes only. A body without the key of the table fails. Do not choose the operation with an `operation` field in the body: depending on the Camel version it is ignored, and the item is then replaced as with `PutItem`, or the message fails. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid. Headers that start with `CamelAwsDdb`, except `CamelAwsDdbOperation` and `CamelAwsDdbReturnValues`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `aws-ddb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region of the table, such as `eu-west-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **table** | Table Name | **Required** The name of the DynamoDB table to write the items to. The table must exist: the Kamelet does not start when it does not. | string |  | orders |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **operation** | Operation | What to do with each message: `PutItem` creates the item, or replaces the item with the same key; `UpdateItem` changes only the given attributes of an item; `DeleteItem` deletes the item. The `CamelAwsDdbOperation` header overrides it for one message. Enum values: \* PutItem \* UpdateItem \* DeleteItem | string | PutItem | PutItem |
| **overrideEndpoint** | Endpoint Overwrite | If true, the requests go to the address in `uriEndpointOverride` instead of AWS, for example to test against LocalStack. | boolean | false |  |
| **profileCredentialsName** | Profile Credentials Name | The name of the profile to use from the AWS credentials file. Only used when `useProfileCredentialsProvider` is true. | string |  |  |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the calls to AWS through, such as the proxy of a company network. Used only together with `proxyPort`. When it is not set, the calls go straight to AWS. | string |  | proxy.example.com |
| **proxyPort** | Proxy Port | The port of the proxy in `proxyHost`, such as `3128` for Squid. Used only together with `proxyHost`. | integer |  | 3128 |
| **proxyProtocol** | Proxy Protocol | How to talk to the proxy itself: `HTTP` or `HTTPS`. It is not the protocol of the calls to AWS, which stay encrypted, as the proxy only passes them on. When it is not set, it is `HTTPS`, which needs a proxy that takes TLS connections. Most company proxies, such as Squid, take plain HTTP: set `HTTP` for them. With the wrong one, every call fails, for example with `Unsupported or unrecognized SSL message`. Enum values: \* HTTP \* HTTPS | string |  | HTTP |
| **secretKey** | Secret Key | The secret access key that goes with `accessKey`. AWS shows it only once, when the access key is created. | string |  |  |
| **sessionToken** | Session Token | The session token of temporary credentials, which AWS gives together with their access key and secret key. Only used when `useSessionCredentials` is true. | string |  |  |
| **uriEndpointOverride** | Overwrite Endpoint URI | The address to send the requests to instead of the usual AWS address, such as `[http://localhost:4566](http://localhost:4566)` for LocalStack. Only used when `overrideEndpoint` is true. | string |  | http://localhost:4566 |
| **useDefaultCredentialsProvider** | Default Credentials Provider | If true, the credentials are found the way the AWS SDK finds them: from the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables, the shared credentials file, or the IAM role of the machine, container or pod it runs on. Then `accessKey` and `secretKey` are not needed. | boolean | false |  |
| **useProfileCredentialsProvider** | Profile Credentials Provider | If true, the credentials are read from a profile of the AWS credentials file (`~/.aws/credentials`), the one named in `profileCredentialsName`. | boolean | false |  |
| **useSessionCredentials** | Session Credentials | If true, it logs in with temporary credentials, such as those of an assumed IAM role: `accessKey`, `secretKey` and `sessionToken` together. | boolean | false |  |

## Dependencies

At runtime, the `aws-ddb-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:aws-ddb-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS DynamoDB Sink Kamelet Description

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

### Expected Data format for sink

This Kamelet expects a JSON object, as JSON text, and it must include the primary key values that define the DynamoDB item. The mapping between the JSON fields and table attribute values is done by key. For example, for the input `{"username":"oscerd", "city":"Rome"}`, the Kamelet inserts or replaces an item in the specified AWS DynamoDB table and sets the values for the `username` and `city` attributes.

For PutItem operation the Json body defines all item attributes. For DeleteItem operation the Json body defines only the primary key attributes that identify the item to delete. For UpdateItem operation the Json body defines both key attributes to identify the item to be updated and all item attributes that get updated on the item.

The given JSON body can use `key` and `item` as top level properties that are mapped to the respective attribute value maps:

```json
{
  "key": {"username": "oscerd"},
  "item": {"city": "Rome"}
}
```

Choose the operation with the `operation` option, or for one message with the `CamelAwsDdbOperation` header. Do not put an `operation` field in the body: depending on the Camel version it is ignored, and the item is then replaced as with PutItem, or the message fails.

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-ddb-sink"
    parameters:
      table: "orders"
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ddb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ddb-sink.kamelet.yaml)