# AWS CloudWatch

**Since Camel 3.1**

**Only producer is supported**

The AWS2 Cloudwatch component allows messages to be sent to an [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) metrics. The implementation of the Amazon API is provided by the [AWS SDK](https://aws.amazon.com/sdkforjava/).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon CloudWatch. More information is available at [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/).

## URI Format

aws2-cw://namespace\[?options\]

The metrics will be created if they don’t already exist.

You can append query options to the URI in the following format: `?options=value&option2=value&…​`

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

The AWS CloudWatch component supports 25 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The component configuration. |  | Cw2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **name** (producer) | The metric name. |  | String |
| **operation** (producer) | 
The operation to perform. Defaults to putMetricData.

Enum values:

-   putMetricData
    
-   listMetrics
    
-   describeAlarms
    
-   describeAlarmsForMetric
    





 | putMetricData | Cw2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **region** (producer) | 

The region in which CW client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **timestamp** (producer) | The metric timestamp. |  | Instant |
| **unit** (producer) | The metric unit. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **value** (producer) | The metric value. |  | Double |
| **amazonCwClient** (advanced) | **Autowired** To use the AmazonCloudWatch as the client. |  | CloudWatchClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the CW client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the CW client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the CW client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Cloudwatch client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the CloudWatch client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in CloudWatch. | false | boolean |

## Endpoint Options

The AWS CloudWatch endpoint is configured using URI syntax:

aws2-cw:namespace

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **namespace** (producer) | **Required** The metric namespace. |  | String |

### Query Parameters (21 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | The metric name. |  | String |
| **operation** (producer) | 
The operation to perform. Defaults to putMetricData.

Enum values:

-   putMetricData
    
-   listMetrics
    
-   describeAlarms
    
-   describeAlarmsForMetric
    





 | putMetricData | Cw2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **region** (producer) | 

The region in which CW client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **timestamp** (producer) | The metric timestamp. |  | Instant |
| **unit** (producer) | The metric unit. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **value** (producer) | The metric value. |  | Double |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **amazonCwClient** (advanced) | **Autowired** To use the AmazonCloudWatch as the client. |  | CloudWatchClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the CW client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the CW client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the CW client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Cloudwatch client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the CloudWatch client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in CloudWatch. | false | boolean |

## Message Headers

The AWS CloudWatch component supports 14 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsCwOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#OPERATION) | The operation to perform. |  | String |
| **CamelAwsCwMetricNamespace** (producer) Constant: [`METRIC_NAMESPACE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_NAMESPACE) | The Amazon CW metric namespace. |  | String |
| **CamelAwsCwMetricName** (producer) Constant: [`METRIC_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_NAME) | The Amazon CW metric name. |  | String |
| **CamelAwsCwMetricValue** (producer) Constant: [`METRIC_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_VALUE) | The Amazon CW metric value. |  | Double |
| **CamelAwsCwMetricUnit** (producer) Constant: [`METRIC_UNIT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_UNIT) | The Amazon CW metric unit. |  | String |
| **CamelAwsCwMetricTimestamp** (producer) Constant: [`METRIC_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_TIMESTAMP) | The Amazon CW metric timestamp. |  | Date |
| **CamelAwsCwMetricDimensions** (producer) Constant: [`METRIC_DIMENSIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_DIMENSIONS) | A map of dimension names and dimension values. |  | Map |
| **CamelAwsCwMetricDimensionName** (producer) Constant: [`METRIC_DIMENSION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_DIMENSION_NAME) | The Amazon CW metric dimension name. |  | String |
| **CamelAwsCwMetricDimensionValue** (producer) Constant: [`METRIC_DIMENSION_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_DIMENSION_VALUE) | The Amazon CW metric dimension value. |  | String |
| **CamelAwsCwAlarmName** (producer) Constant: [`ALARM_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#ALARM_NAME) | The name of the alarm. |  | String |
| **CamelAwsCwAlarmState** (producer) Constant: [`ALARM_STATE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#ALARM_STATE) | The state value for the alarm (OK, ALARM, INSUFFICIENT\_DATA). |  | String |
| **CamelAwsCwNextToken** (producer) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#NEXT_TOKEN) | The token for the next set of results. |  | String |
| **CamelAwsCwMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#MAX_RESULTS) | The maximum number of results to return. |  | Integer |
| **CamelAwsCwIsTruncated** (producer) Constant: [`IS_TRUNCATED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#IS_TRUNCATED) | Whether the response has more results (is truncated). |  | Boolean |

Required CW component options

You have to provide the amazonCwClient in the Registry or your accessKey and secretKey to access the [Amazon’s CloudWatch](https://aws.amazon.com/cloudwatch/).

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

### Advanced CloudWatchClient configuration

If you need more control over the `CloudWatchClient` instance configuration you can create your own instance and refer to it from the URI:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("aws2-cw://namespace?amazonCwClient=#client");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="aws2-cw://namespace?amazonCwClient=#client"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: aws2-cw://namespace
            parameters:
              amazonCwClient: "#client"
```

The `#client` refers to a `CloudWatchClient` in the Registry.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-cw</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version`} must be replaced by the actual version of Camel.

## Examples

### Producer Example

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("aws2-cw://http://camel.apache.org/aws-cw");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="aws2-cw://http://camel.apache.org/aws-cw"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: aws2-cw://http://camel.apache.org/aws-cw
```

and sends something like

_Java-only: setting CloudWatch metric headers programmatically_

```java
exchange.getIn().setHeader(Cw2Constants.METRIC_NAME, "ExchangesCompleted");
exchange.getIn().setHeader(Cw2Constants.METRIC_VALUE, "2.0");
exchange.getIn().setHeader(Cw2Constants.METRIC_UNIT, "Count");
```

## Spring Boot Auto-Configuration

When using aws2-cw with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-cw-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 26 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-cw.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-cw.amazon-cw-client** | To use the AmazonCloudWatch as the client. The option is a software.amazon.awssdk.services.cloudwatch.CloudWatchClient type. |  | CloudWatchClient |
| **camel.component.aws2-cw.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-cw.configuration** | The component configuration. The option is a org.apache.camel.component.aws2.cw.Cw2Configuration type. |  | Cw2Configuration |
| **camel.component.aws2-cw.enabled** | Whether to enable auto configuration of the aws2-cw component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-cw.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws2-cw.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws2-cw.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-cw.name** | The metric name. |  | String |
| **camel.component.aws2-cw.operation** | The operation to perform. Defaults to putMetricData. | putmetricdata | Cw2Operations |
| **camel.component.aws2-cw.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-cw.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **camel.component.aws2-cw.proxy-host** | To define a proxy host when instantiating the CW client. |  | String |
| **camel.component.aws2-cw.proxy-port** | To define a proxy port when instantiating the CW client. |  | Integer |
| **camel.component.aws2-cw.proxy-protocol** | To define a proxy protocol when instantiating the CW client. | https | Protocol |
| **camel.component.aws2-cw.region** | The region in which CW client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-cw.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-cw.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws2-cw.timestamp** | The metric timestamp. |  | Instant |
| **camel.component.aws2-cw.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-cw.unit** | The metric unit. |  | String |
| **camel.component.aws2-cw.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-cw.use-default-credentials-provider** | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-cw.use-profile-credentials-provider** | Set whether the Cloudwatch client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-cw.use-session-credentials** | Set whether the CloudWatch client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in CloudWatch. | false | Boolean |
| **camel.component.aws2-cw.value** | The metric value. |  | Double |