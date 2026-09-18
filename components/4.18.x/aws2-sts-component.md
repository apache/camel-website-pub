# AWS Security Token Service (STS)

**Since Camel 3.5**

**Only producer is supported**

The AWS2 STS component supports assumeRole operation. [AWS STS](https://aws.amazon.com/sts/).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon STS. More information is available at [Amazon STS](https://aws.amazon.com/sts/).

> **Note**
> The AWS2 STS component works on the aws-global region, and it has aws-global as the default region.

## URI Format

aws2-sts://label\[?options\]

You can append query options to the URI in the following format:

`?options=value&option2=value&…​`

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The AWS Security Token Service (STS) component supports 18 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | STS2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   assumeRole
    
-   getSessionToken
    
-   getFederationToken
    





 | assumeRole | STS2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the STS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 | aws-global | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **stsClient** (advanced) | **Autowired** To use an existing configured AWS STS client. |  | StsClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the STS client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the STS client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the STS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the STS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the STS client should expect to load credentials through a profile credentials provider. | false | boolean |

## Endpoint Options

The AWS Security Token Service (STS) endpoint is configured using URI syntax:

aws2-sts:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (16 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   assumeRole
    
-   getSessionToken
    
-   getFederationToken
    





 | assumeRole | STS2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the STS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 | aws-global | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **stsClient** (advanced) | **Autowired** To use an existing configured AWS STS client. |  | StsClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the STS client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the STS client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the STS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the STS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the STS client should expect to load credentials through a profile credentials provider. | false | boolean |

## Message Headers

The AWS Security Token Service (STS) component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsStsOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsStsRoleArn** (producer) Constant: [`ROLE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#ROLE_ARN) | The Amazon Resource Name (ARN) of the role to assume. |  | String |
| **CamelAwsStsRoleSessionName** (producer) Constant: [`ROLE_SESSION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#ROLE_SESSION_NAME) | An identifier for the assumed role session. |  | String |
| **CamelAwsStsFederatedName** (producer) Constant: [`FEDERATED_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#FEDERATED_NAME) | The name of the federated user. |  | String |
| **CamelAwsStsAssumeRoleDurationSeconds** (producer) Constant: [`ASSUME_ROLE_DURATION_SECONDS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#ASSUME_ROLE_DURATION_SECONDS) | The duration, in seconds, of the role session. It could go from 900 seconds, to 1 to 12 hours (dependent on administrator settings. The default if not specified is 3600 seconds. |  | Integer |
| **CamelAwsStsAccessKeyId** (assumeRole getSessionToken getFederationToken) Constant: [`ACCESS_KEY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#ACCESS_KEY_ID) | The temporary access key ID. |  | String |
| **CamelAwsStsSecretKey** (assumeRole getSessionToken getFederationToken) Constant: [`SECRET_KEY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#SECRET_KEY_ID) | The temporary secret access key. |  | String |
| **CamelAwsStsSessionToken** (assumeRole getSessionToken getFederationToken) Constant: [`SESSION_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#SESSION_TOKEN) | The temporary session token. |  | String |
| **CamelAwsStsExpiration** (assumeRole getSessionToken getFederationToken) Constant: [`EXPIRATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#EXPIRATION) | The expiration date and time of the credentials. |  | Instant |
| **CamelAwsStsAssumedRoleArn** (assumeRole) Constant: [`ASSUMED_ROLE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#ASSUMED_ROLE_ARN) | The Amazon Resource Name (ARN) of the assumed role. |  | String |

Required STS component options

You have to provide the amazonSTSClient in the Registry or your accessKey and secretKey to access the [Amazon STS](https://aws.amazon.com/sts/) service.

## Usage

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### STS Producer operations

Camel-AWS STS component provides the following operation on the producer side:

-   assumeRole
    
-   getSessionToken
    
-   getFederationToken
    

## Examples

### Producer Examples

-   assumeRole: this operation will make an AWS user assume a different role temporary
    

```java
from("direct:assumeRole")
    .setHeader(STS2Constants.ROLE_ARN, constant("arn:123"))
    .setHeader(STS2Constants.ROLE_SESSION_NAME, constant("groot"))
    .to("aws2-sts://test?stsClient=#amazonSTSClient&operation=assumeRole")
```

-   getSessionToken: this operation will return a temporary session token
    

```java
from("direct:getSessionToken")
    .to("aws2-sts://test?stsClient=#amazonSTSClient&operation=getSessionToken")
```

-   getFederationToken: this operation will return a temporary federation token
    

```java
from("direct:getFederationToken")
    .setHeader(STS2Constants.FEDERATED_NAME, constant("federation-account"))
    .to("aws2-sts://test?stsClient=#amazonSTSClient&operation=getSessionToken")
```

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as the body. In AWS STS, as an example for Assume Role request, you can do something like:

```java
from("direct:createUser")
     .setBody(AssumeRoleRequest.builder().roleArn("arn:123").roleSessionName("groot").build())
    .to("aws2-sts://test?stsClient=#amazonSTSClient&operation=assumeRole&pojoRequest=true")
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-sts</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-sts with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-sts-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 19 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-sts.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-sts.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-sts.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.sts.STS2Configuration type. |  | STS2Configuration |
| **camel.component.aws2-sts.enabled** | Whether to enable auto configuration of the aws2-sts component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-sts.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-sts.operation** | The operation to perform. | assumerole | STS2Operations |
| **camel.component.aws2-sts.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-sts.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-sts.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **camel.component.aws2-sts.proxy-host** | To define a proxy host when instantiating the STS client. |  | String |
| **camel.component.aws2-sts.proxy-port** | To define a proxy port when instantiating the STS client. |  | Integer |
| **camel.component.aws2-sts.proxy-protocol** | To define a proxy protocol when instantiating the STS client. | https | Protocol |
| **camel.component.aws2-sts.region** | The region in which the STS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). | aws-global | String |
| **camel.component.aws2-sts.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-sts.sts-client** | To use an existing configured AWS STS client. The option is a software.amazon.awssdk.services.sts.StsClient type. |  | StsClient |
| **camel.component.aws2-sts.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-sts.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-sts.use-default-credentials-provider** | Set whether the STS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-sts.use-profile-credentials-provider** | Set whether the STS client should expect to load credentials through a profile credentials provider. | false | Boolean |