# ![aws ec2 sink](_images/kamelets/aws-ec2-sink.svg) AWS EC2 Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Asks Amazon EC2 for the status of virtual machines (instances), such as whether they run and pass their health checks, each time a message arrives, or starts, stops or reboots them.

Use it to check regularly that your EC2 instances are running and healthy, for example every few minutes from `timer-source`, and raise an alert when a check fails, or to start and stop test machines on a schedule.

Input: the body is not used. The `instanceIds` header (or `ce-instanceids`) is a comma-separated list of the IDs of the instances, such as `i-0abc123,i-0def456`. For the status, it is optional; without it, the status of all the running instances of the region is returned. To start, stop or reboot, it is required.

Output: the body is the answer of AWS, an object of the AWS SDK for Java (not JSON text). By default, a `DescribeInstanceStatusResponse`, with for each instance its ID, availability zone, state (such as `running`) and the results of the instance and system status checks. When there are more results than fit, the `CamelAwsEC2NextToken` header holds the token of the next page. `describeInstances` gives a `DescribeInstancesResponse`, and `startInstances` and `stopInstances` a `StartInstancesResponse` or `StopInstancesResponse` with the previous and the new state of each instance, such as `stopped` and `pending`. `rebootInstances` leaves the body as it was.

Good to know: by default it only reads, and never starts, stops or changes an instance; `operation` chooses another action. It cannot create or terminate instances. With Camel 4.23, the `instanceIds` header is ignored: the status of all the instances is returned, and start, stop and reboot reach no instance. To reach AWS through an HTTP proxy, set `proxyHost` and `proxyPort`, and set `proxyProtocol` to `HTTP` for a proxy that takes plain HTTP, such as Squid.

## Configuration Options

The following table summarizes the configuration options available for the `aws-ec2-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **region** | AWS Region | **Required** The AWS region of the instances, such as `eu-west-1`. Enum values: \* ap-south-1 \* eu-south-1 \* us-gov-east-1 \* me-central-1 \* ca-central-1 \* eu-central-1 \* us-iso-west-1 \* us-west-1 \* us-west-2 \* af-south-1 \* eu-north-1 \* eu-west-3 \* eu-west-2 \* eu-west-1 \* ap-northeast-3 \* ap-northeast-2 \* ap-northeast-1 \* me-south-1 \* sa-east-1 \* ap-east-1 \* cn-north-1 \* us-gov-west-1 \* ap-southeast-1 \* ap-southeast-2 \* us-iso-east-1 \* ap-southeast-3 \* us-east-1 \* us-east-2 \* cn-northwest-1 \* us-isob-east-1 \* aws-global \* aws-cn-global \* aws-us-gov-global \* aws-iso-global \* aws-iso-b-global | string |  | eu-west-1 |
| **accessKey** | Access Key | The access key ID of an IAM user, which AWS gives when you create an access key for the user (in the AWS console: IAM, Users, Security credentials). Use it together with `secretKey`, or leave both empty and set `useDefaultCredentialsProvider` or `useProfileCredentialsProvider` instead. | string |  |  |
| **operation** | Operation | What to do with each message: `describeInstancesStatus` gives the status of the instances and the results of their status checks; `describeInstances` gives their full details, such as type, image, IP addresses and tags; `startInstances`, `stopInstances` and `rebootInstances` start, stop or reboot the instances in the `instanceIds` header, which is then required. Enum values: \* describeInstancesStatus \* describeInstances \* startInstances \* stopInstances \* rebootInstances | string | describeInstancesStatus | stopInstances |
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

At runtime, the `aws-ec2-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:aws2-ec2
    
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
            uri: "kamelet:aws-ec2-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## AWS EC2 Sink Kamelet Description

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

The Kamelet reads the following optional header:

-   `instanceIds` / `ce-instanceids`: as a comma separated list of EC2 instance ids. Without it, the status of all the running instances of the region is returned. To start, stop or reboot, it is required.
    

### Starting, Stopping and Rebooting Instances

By default, the Kamelet only reads the status of the instances. Set `operation` to choose another action:

-   `describeInstancesStatus` (the default): the status of the instances and the results of their status checks.
    
-   `describeInstances`: the full details of the instances, such as their type, image, IP addresses and tags.
    
-   `startInstances`, `stopInstances` and `rebootInstances`: start, stop or reboot the instances in the `instanceIds` header. Without the header, the message fails with `Instances Ids must be specified`.
    

The Kamelet cannot create or terminate instances.

For example, to stop test machines every evening, a route sends a message with the `instanceIds` header to this step:

```yaml
- to:
    uri: "kamelet:aws-ec2-sink"
    parameters:
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      operation: "stopInstances"
```

### Through an HTTP Proxy

Where AWS can be reached only through an HTTP proxy, as in many company networks, set `proxyHost` and `proxyPort` to the proxy. `proxyProtocol` is how the Kamelet talks to the proxy itself, not to AWS: it is `HTTPS` when it is not set, so set it to `HTTP` for a proxy that takes plain HTTP, such as Squid. The calls to AWS stay encrypted, as the proxy only passes them on. The Kamelet has no option for a proxy user or password.

The step that sends to the Kamelet, in a route:

```yaml
- to:
    uri: "kamelet:aws-ec2-sink"
    parameters:
      region: "eu-west-1"
      useDefaultCredentialsProvider: true
      proxyHost: "proxy.example.com"
      proxyPort: 3128
      proxyProtocol: "HTTP"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ec2-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/aws-ec2-sink.kamelet.yaml)