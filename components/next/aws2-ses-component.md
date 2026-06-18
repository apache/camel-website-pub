# AWS Simple Email Service (SES)

**Since Camel 3.1**

**Only producer is supported**

The AWS2 SES component supports sending emails with [Amazon’s SES](https://aws.amazon.com/ses) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon SES. More information is available at [Amazon SES](https://aws.amazon.com/ses).

## URI Format

aws2-ses://from\[?options\]

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

The AWS Simple Email Service (SES) component supports 27 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bcc** (producer) | List of comma-separated destination blind carbon copy (bcc) email address. Can be overridden with 'CamelAwsSesBcc' header. |  | String |
| **cc** (producer) | List of comma-separated destination carbon copy (cc) email address. Can be overridden with 'CamelAwsSesCc' header. |  | String |
| **configuration** (producer) | component configuration. |  | Ses2Configuration |
| **configurationSet** (producer) | Set the configuration set to send with every request. Override it with 'CamelAwsSesConfigurationSet' header. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **region** (producer) | 
The region in which SES client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
    
-   eu-isoe-west-1
    
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
    
-   ca-west-1
    
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
    





 |  | String |
| **replyToAddresses** (producer) | List of comma separated reply-to email address(es) for the message, override it using 'CamelAwsSesReplyToAddresses' header. |  | String |
| **returnPath** (producer) | The email address to which bounce notifications are to be forwarded, override it using 'CamelAwsSesReturnPath' header. |  | String |
| **subject** (producer) | The subject which is used if the message header 'CamelAwsSesSubject' is not present. |  | String |
| **to** (producer) | List of comma separated destination email address. Can be overridden with 'CamelAwsSesTo' header. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **amazonSESClient** (advanced) | **Autowired** To use the AmazonSimpleEmailService as the client. |  | SesClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SES client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the SES client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the SES client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Ses client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the SES client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the SES client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in SES. | false | boolean |

## Endpoint Options

The AWS Simple Email Service (SES) endpoint is configured using URI syntax:

aws2-ses:from

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **from** (producer) | **Required** The sender’s email address. |  | String |

### Query Parameters (23 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bcc** (producer) | List of comma-separated destination blind carbon copy (bcc) email address. Can be overridden with 'CamelAwsSesBcc' header. |  | String |
| **cc** (producer) | List of comma-separated destination carbon copy (cc) email address. Can be overridden with 'CamelAwsSesCc' header. |  | String |
| **configurationSet** (producer) | Set the configuration set to send with every request. Override it with 'CamelAwsSesConfigurationSet' header. |  | String |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **region** (producer) | 
The region in which SES client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
    
-   eu-isoe-west-1
    
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
    
-   ca-west-1
    
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
    





 |  | String |
| **replyToAddresses** (producer) | List of comma separated reply-to email address(es) for the message, override it using 'CamelAwsSesReplyToAddresses' header. |  | String |
| **returnPath** (producer) | The email address to which bounce notifications are to be forwarded, override it using 'CamelAwsSesReturnPath' header. |  | String |
| **subject** (producer) | The subject which is used if the message header 'CamelAwsSesSubject' is not present. |  | String |
| **to** (producer) | List of comma separated destination email address. Can be overridden with 'CamelAwsSesTo' header. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **amazonSESClient** (advanced) | **Autowired** To use the AmazonSimpleEmailService as the client. |  | SesClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SES client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the SES client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the SES client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Ses client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the SES client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the SES client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in SES. | false | boolean |

## Message Headers

The AWS Simple Email Service (SES) component supports 11 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsSesFrom** (producer) Constant: [`FROM`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#FROM) | The sender’s email address. |  | String |
| **CamelAwsSesMessageId** (producer) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#MESSAGE_ID) | The Amazon SES message ID. |  | String |
| **CamelAwsSesReplyToAddresses** (producer) Constant: [`REPLY_TO_ADDRESSES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#REPLY_TO_ADDRESSES) | The reply-to email address(es) for the message. Use comma to separate multiple values. |  | String |
| **CamelAwsSesReturnPath** (producer) Constant: [`RETURN_PATH`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#RETURN_PATH) | The email address to which bounce notifications are to be forwarded. |  | String |
| **CamelAwsSesSubject** (producer) Constant: [`SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#SUBJECT) | The subject of the message. |  | String |
| **CamelAwsSesTo** (producer) Constant: [`TO`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#TO) | List of comma separated destination email address. |  | String |
| **CamelAwsSesCc** (producer) Constant: [`CC`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#CC) | List of comma separated destination carbon copy (cc) email address. |  | String |
| **CamelAwsSesBcc** (producer) Constant: [`BCC`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#BCC) | List of comma separated destination blind carbon copy (bcc) email address. |  | String |
| **CamelAwsSesTags** (producer) Constant: [`TAGS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#TAGS) | A collection of name/value pairs to apply when sending the email. Tags are user-defined properties that are included in published email sending events. |  | Map |
| **CamelAwsSesHtmlEmail** (producer) Constant: [`HTML_EMAIL`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#HTML_EMAIL) | The flag to show if email content is HTML. |  | Boolean |
| **CamelAwsSesConfigurationSet** (producer) Constant: [`CONFIGURATION_SET`](https://javadoc.io/doc/org.apache.camel/camel-aws2-ses/latest/org/apache/camel/component/aws2/ses/Ses2Constants.html#CONFIGURATION_SET) | TThe configuration set to send. |  | String |

Required SES component options

You have to provide the amazonSESClient in the Registry or your accessKey and secretKey to access the [Amazon’s SES](https://aws.amazon.com/ses).

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

### Advanced SesClient configuration

If you need more control over the `SesClient` instance configuration you can create your own instance and refer to it from the URI:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("aws2-ses://example@example.com?amazonSESClient=#client");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="aws2-ses://example@example.com?amazonSESClient=#client"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: aws2-ses://example@example.com
            parameters:
              amazonSESClient: "#client"
```

The `#client` refers to a `SesClient` in the Registry.

## Examples

### Producer Examples

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader(SesConstants.SUBJECT, constant("This is my subject"))
    .setHeader(SesConstants.TO, constant(Collections.singletonList("to@example.com"))
    .setBody(constant("This is my message text."))
    .to("aws2-ses://from@example.com?accessKey=xxx&secretKey=yyy");
```

```xml
<route>
    <from uri="direct:start"/>
    <setHeader name="CamelAwsSesSubject">
        <constant>This is my subject</constant>
    </setHeader>
    <setHeader name="CamelAwsSesTo">
        <constant>to@example.com</constant>
    </setHeader>
    <setBody>
        <constant>This is my message text.</constant>
    </setBody>
    <to uri="aws2-ses://from@example.com?accessKey=xxx&amp;secretKey=yyy"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAwsSesSubject
            constant: "This is my subject"
        - setHeader:
            name: CamelAwsSesTo
            constant: "to@example.com"
        - setBody:
            constant: "This is my message text."
        - to:
            uri: aws2-ses://from@example.com
            parameters:
              accessKey: xxx
              secretKey: yyy
```

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-ses</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-ses with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-ses-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 28 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-ses.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-ses.amazon-s-e-s-client** | To use the AmazonSimpleEmailService as the client. The option is a software.amazon.awssdk.services.ses.SesClient type. |  | SesClient |
| **camel.component.aws2-ses.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-ses.bcc** | List of comma-separated destination blind carbon copy (bcc) email address. Can be overridden with 'CamelAwsSesBcc' header. |  | String |
| **camel.component.aws2-ses.cc** | List of comma-separated destination carbon copy (cc) email address. Can be overridden with 'CamelAwsSesCc' header. |  | String |
| **camel.component.aws2-ses.configuration** | component configuration. The option is a org.apache.camel.component.aws2.ses.Ses2Configuration type. |  | Ses2Configuration |
| **camel.component.aws2-ses.configuration-set** | Set the configuration set to send with every request. Override it with 'CamelAwsSesConfigurationSet' header. |  | String |
| **camel.component.aws2-ses.enabled** | Whether to enable auto configuration of the aws2-ses component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-ses.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws2-ses.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws2-ses.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-ses.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-ses.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **camel.component.aws2-ses.proxy-host** | To define a proxy host when instantiating the SES client. |  | String |
| **camel.component.aws2-ses.proxy-port** | To define a proxy port when instantiating the SES client. |  | Integer |
| **camel.component.aws2-ses.proxy-protocol** | To define a proxy protocol when instantiating the SES client. | https | Protocol |
| **camel.component.aws2-ses.region** | The region in which SES client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-ses.reply-to-addresses** | List of comma separated reply-to email address(es) for the message, override it using 'CamelAwsSesReplyToAddresses' header. |  | String |
| **camel.component.aws2-ses.return-path** | The email address to which bounce notifications are to be forwarded, override it using 'CamelAwsSesReturnPath' header. |  | String |
| **camel.component.aws2-ses.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-ses.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws2-ses.subject** | The subject which is used if the message header 'CamelAwsSesSubject' is not present. |  | String |
| **camel.component.aws2-ses.to** | List of comma separated destination email address. Can be overridden with 'CamelAwsSesTo' header. |  | String |
| **camel.component.aws2-ses.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-ses.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-ses.use-default-credentials-provider** | Set whether the Ses client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-ses.use-profile-credentials-provider** | Set whether the SES client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-ses.use-session-credentials** | Set whether the SES client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in SES. | false | Boolean |