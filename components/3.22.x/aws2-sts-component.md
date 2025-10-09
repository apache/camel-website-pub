# AWS Security Token Service (STS)

**Since Camel 3.5**

**Only producer is supported**

The AWS2 STS component supports assumeRole operation. [AWS STS](https://aws.amazon.com/sts/).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon STS. More information is available at [Amazon STS](https://aws.amazon.com/sts/).

> **Note**
> The AWS2 STS component works on the aws-global region and it has aws-global as default region

## URI Format

aws2-sts://label\[?options\]

You can append query options to the URI in the following format, ?options=value&option2=value&…​

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The AWS Security Token Service (STS) component supports 16 options, which are listed below.

   
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
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the STS client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the STS client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the STS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which STS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). | aws-global | String |
| **stsClient** (producer) | **Autowired** To use a existing configured AWS STS as client. |  | StsClient |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the STS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS Security Token Service (STS) endpoint is configured using URI syntax:

aws2-sts:label

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   assumeRole
    
-   getSessionToken
    
-   getFederationToken
    





 | assumeRole | STS2Operations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the STS client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the STS client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the STS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which STS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). | aws-global | String |
| **stsClient** (producer) | **Autowired** To use a existing configured AWS STS as client. |  | StsClient |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the STS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

Required STS component options

You have to provide the amazonSTSClient in the Registry or your accessKey and secretKey to access the [Amazon STS](https://aws.amazon.com/sts/) service.

## Usage

### Static credentials vs Default Credential Provider

You have the possibility of avoiding the usage of explicit static credentials, by specifying the useDefaultCredentialsProvider option and set it to true.

-   Java system properties - aws.accessKeyId and aws.secretKey
    
-   Environment variables - AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable AWS\_CONTAINER\_CREDENTIALS\_RELATIVE\_URI is set.
    
-   Amazon EC2 Instance profile credentials.
    

## Message Headers

The AWS Security Token Service (STS) component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsStsOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsStsRoleArn** (producer) Constant: [`ROLE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#ROLE_ARN) | The Amazon Resource Name (ARN) of the role to assume. |  | String |
| **CamelAwsStsRoleSessionName** (producer) Constant: [`ROLE_SESSION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#ROLE_SESSION_NAME) | An identifier for the assumed role session. |  | String |
| **CamelAwsStsFederatedName** (producer) Constant: [`FEDERATED_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sts/latest/org/apache/camel/component/aws2/sts/STS2Constants.html#FEDERATED_NAME) | The name of the federated user. |  | String |

### STS Producer operations

Camel-AWS STS component provides the following operation on the producer side:

-   assumeRole
    
-   getSessionToken
    
-   getFederationToken
    

## Producer Examples

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

## Using a POJO as body

Sometimes build an AWS Request can be complex, because of multiple options. We introduce the possibility to use a POJO as body. In AWS STS, as example for Assume Role request, you can do something like:

```java
from("direct:createUser")
     .setBody(AssumeRoleRequest.builder().roleArn("arn:123").roleSessionName("groot").build())
    .to("aws2-sts://test?stsClient=#amazonSTSClient&operation=assumeRole&pojoRequest=true")
```

In this way you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

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

The component supports 17 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-sts.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-sts.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-sts.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.sts.STS2Configuration type. |  | STS2Configuration |
| **camel.component.aws2-sts.enabled** | Whether to enable auto configuration of the aws2-sts component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-sts.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-sts.operation** | The operation to perform. |  | STS2Operations |
| **camel.component.aws2-sts.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-sts.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-sts.proxy-host** | To define a proxy host when instantiating the STS client. |  | String |
| **camel.component.aws2-sts.proxy-port** | To define a proxy port when instantiating the STS client. |  | Integer |
| **camel.component.aws2-sts.proxy-protocol** | To define a proxy protocol when instantiating the STS client. |  | Protocol |
| **camel.component.aws2-sts.region** | The region in which STS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). | aws-global | String |
| **camel.component.aws2-sts.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-sts.sts-client** | To use a existing configured AWS STS as client. The option is a software.amazon.awssdk.services.sts.StsClient type. |  | StsClient |
| **camel.component.aws2-sts.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-sts.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-sts.use-default-credentials-provider** | Set whether the STS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |