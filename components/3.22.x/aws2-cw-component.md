# AWS CloudWatch

**Since Camel 3.1**

**Only producer is supported**

The AWS2 Cloudwatch component allows messages to be sent to an [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) metrics. The implementation of the Amazon API is provided by the [AWS SDK](https://aws.amazon.com/sdkforjava/).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon CloudWatch. More information is available at [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/).

## URI Format

aws2-cw://namespace\[?options\]

The metrics will be created if they don’t already exists.  
You can append query options to the URI in the following format, `?options=value&option2=value&…​`

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

The AWS CloudWatch component supports 18 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonCwClient** (producer) | **Autowired** To use the AmazonCloudWatch as the client. |  | CloudWatchClient |
| **configuration** (producer) | The component configuration. |  | Cw2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **name** (producer) | The metric name. |  | String |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the CW client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the CW client. |  | Integer |
| **proxyProtocol** (producer) | 
To define a proxy protocol when instantiating the CW client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which CW client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **timestamp** (producer) | The metric timestamp. |  | Instant |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **unit** (producer) | The metric unit. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **value** (producer) | The metric value. |  | Double |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS CloudWatch endpoint is configured using URI syntax:

aws2-cw:namespace

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **namespace** (producer) | **Required** The metric namespace. |  | String |

### Query Parameters (16 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonCwClient** (producer) | **Autowired** To use the AmazonCloudWatch as the client. |  | CloudWatchClient |
| **name** (producer) | The metric name. |  | String |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the CW client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the CW client. |  | Integer |
| **proxyProtocol** (producer) | 
To define a proxy protocol when instantiating the CW client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which CW client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **timestamp** (producer) | The metric timestamp. |  | Instant |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **unit** (producer) | The metric unit. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **value** (producer) | The metric value. |  | Double |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

Required CW component options

You have to provide the amazonCwClient in the Registry or your accessKey and secretKey to access the [Amazon’s CloudWatch](https://aws.amazon.com/cloudwatch/).

## Usage

### Static credentials vs Default Credential Provider

You have the possibility of avoiding the usage of explicit static credentials, by specifying the useDefaultCredentialsProvider option and set it to true.

-   Java system properties - aws.accessKeyId and aws.secretKey
    
-   Environment variables - AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable AWS\_CONTAINER\_CREDENTIALS\_RELATIVE\_URI is set.
    
-   Amazon EC2 Instance profile credentials.
    

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

## Message Headers

The AWS CloudWatch component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsCwMetricNamespace** (producer) Constant: [`METRIC_NAMESPACE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_NAMESPACE) | The Amazon CW metric namespace. |  | String |
| **CamelAwsCwMetricName** (producer) Constant: [`METRIC_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_NAME) | The Amazon CW metric name. |  | String |
| **CamelAwsCwMetricValue** (producer) Constant: [`METRIC_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_VALUE) | The Amazon CW metric value. |  | Double |
| **CamelAwsCwMetricUnit** (producer) Constant: [`METRIC_UNIT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_UNIT) | The Amazon CW metric unit. |  | String |
| **CamelAwsCwMetricTimestamp** (producer) Constant: [`METRIC_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_TIMESTAMP) | The Amazon CW metric timestamp. |  | Date |
| **CamelAwsCwMetricDimensions** (producer) Constant: [`METRIC_DIMENSIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_DIMENSIONS) | A map of dimension names and dimension values. |  | Map |
| **CamelAwsCwMetricDimensionName** (producer) Constant: [`METRIC_DIMENSION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_DIMENSION_NAME) | The Amazon CW metric dimension name. |  | String |
| **CamelAwsCwMetricDimensionValue** (producer) Constant: [`METRIC_DIMENSION_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-cw/latest/org/apache/camel/component/aws2/cw/Cw2Constants.html#METRIC_DIMENSION_VALUE) | The Amazon CW metric dimension value. |  | String |

### Advanced CloudWatchClient configuration

If you need more control over the `CloudWatchClient` instance configuration you can create your own instance and refer to it from the URI:

```java
from("direct:start")
.to("aws2-cw://namespace?amazonCwClient=#client");
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

```java
from("direct:start")
  .to("aws2-cw://http://camel.apache.org/aws-cw");
```

and sends something like

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

The component supports 19 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-cw.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-cw.amazon-cw-client** | To use the AmazonCloudWatch as the client. The option is a software.amazon.awssdk.services.cloudwatch.CloudWatchClient type. |  | CloudWatchClient |
| **camel.component.aws2-cw.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-cw.configuration** | The component configuration. The option is a org.apache.camel.component.aws2.cw.Cw2Configuration type. |  | Cw2Configuration |
| **camel.component.aws2-cw.enabled** | Whether to enable auto configuration of the aws2-cw component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-cw.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-cw.name** | The metric name. |  | String |
| **camel.component.aws2-cw.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-cw.proxy-host** | To define a proxy host when instantiating the CW client. |  | String |
| **camel.component.aws2-cw.proxy-port** | To define a proxy port when instantiating the CW client. |  | Integer |
| **camel.component.aws2-cw.proxy-protocol** | To define a proxy protocol when instantiating the CW client. |  | Protocol |
| **camel.component.aws2-cw.region** | The region in which CW client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-cw.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-cw.timestamp** | The metric timestamp. The option is a java.time.Instant type. |  | Instant |
| **camel.component.aws2-cw.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-cw.unit** | The metric unit. |  | String |
| **camel.component.aws2-cw.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-cw.use-default-credentials-provider** | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-cw.value** | The metric value. |  | Double |