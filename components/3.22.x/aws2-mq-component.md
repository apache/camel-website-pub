# AWS MQ

**Since Camel 3.1**

**Only producer is supported**

The AWS2 MQ component supports create, run, start, stop and terminate [AWS MQ](https://aws.amazon.com/amazon-mq/) instances.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon MQ. More information is available at [Amazon MQ](https://aws.amazon.com/amazon-mq/).

## URI Format

aws2-mq://label\[?options\]

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

The AWS MQ component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonMqClient** (producer) | **Autowired** To use a existing configured AmazonMQClient as client. |  | MqClient |
| **configuration** (producer) | Component configuration. |  | MQ2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform. It can be listBrokers,createBroker,deleteBroker.

Enum values:

-   listBrokers
    
-   createBroker
    
-   deleteBroker
    
-   rebootBroker
    
-   updateBroker
    
-   describeBroker
    





 |  | MQ2Operations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the MQ client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the MQ client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the MQ client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which MQ client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the MQ client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS MQ endpoint is configured using URI syntax:

aws2-mq:label

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonMqClient** (producer) | **Autowired** To use a existing configured AmazonMQClient as client. |  | MqClient |
| **operation** (producer) | 
**Required** The operation to perform. It can be listBrokers,createBroker,deleteBroker.

Enum values:

-   listBrokers
    
-   createBroker
    
-   deleteBroker
    
-   rebootBroker
    
-   updateBroker
    
-   describeBroker
    





 |  | MQ2Operations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the MQ client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the MQ client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the MQ client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which MQ client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the MQ client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

Required MQ component options

You have to provide the amazonMqClient in the Registry or your accessKey and secretKey to access the [Amazon MQ](https://aws.amazon.com/amazon-mq/) service.

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

The AWS MQ component supports 11 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsMQOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsMQMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#MAX_RESULTS) | The number of results that must be retrieved from listBrokers operation. |  | Integer |
| **CamelAwsMQBrokerName** (producer) Constant: [`BROKER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#BROKER_NAME) | The broker name. |  | String |
| **CamelAwsMQBrokerEngine** (producer) Constant: [`BROKER_ENGINE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#BROKER_ENGINE) | The Broker Engine for MQ. |  | String |
| **CamelAwsMQBrokerEngineVersion** (producer) Constant: [`BROKER_ENGINE_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#BROKER_ENGINE_VERSION) | The Broker Engine Version for MQ. Currently you can choose between 5.15.6 and 5.15.0 of ACTIVEMQ. |  | String |
| **CamelAwsMQBrokerID** (producer) Constant: [`BROKER_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#BROKER_ID) | The broker id. |  | String |
| **CamelAwsMQConfigurationID** (producer) Constant: [`CONFIGURATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#CONFIGURATION_ID) | A list of information about the configuration. |  | ConfigurationId |
| **CamelAwsMQBrokerDeploymentMode** (producer) Constant: [`BROKER_DEPLOYMENT_MODE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#BROKER_DEPLOYMENT_MODE) | The deployment mode for the broker in the createBroker operation. |  | String |
| **CamelAwsMQBrokerInstanceType** (producer) Constant: [`BROKER_INSTANCE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#BROKER_INSTANCE_TYPE) | The instance type for the MQ machine in the createBroker operation. |  | String |
| **CamelAwsMQBrokerUsers** (producer) Constant: [`BROKER_USERS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#BROKER_USERS) | The list of users for MQ. |  | List |
| **CamelAwsMQBrokerPubliclyAccessible** (producer) Constant: [`BROKER_PUBLICLY_ACCESSIBLE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-mq/latest/org/apache/camel/component/aws2/mq/MQ2Constants.html#BROKER_PUBLICLY_ACCESSIBLE) | If the MQ instance must be publicly available or not. | false | Boolean |

### MQ Producer operations

Camel-AWS MQ component provides the following operation on the producer side:

-   listBrokers
    
-   createBroker
    
-   deleteBroker
    
-   rebootBroker
    
-   updateBroker
    
-   describeBroker
    

## Examples

### Producer Examples

-   listBrokers: this operation will list the available MQ Brokers in AWS
    

```java
from("direct:listBrokers")
    .to("aws2-mq://test?amazonMqClient=#amazonMqClient&operation=listBrokers")
```

-   createBroker: this operation will create an MQ Broker in AWS
    

```java
from("direct:createBroker")
    .process(new Processor() {
       @Override
       public void process(Exchange exchange) throws Exception {
                exchange.getIn().setHeader(MQ2Constants.BROKER_NAME, "test");
                exchange.getIn().setHeader(MQ2Constants.BROKER_DEPLOYMENT_MODE, DeploymentMode.SINGLE_INSTANCE);
                exchange.getIn().setHeader(MQ2Constants.BROKER_INSTANCE_TYPE, "mq.t2.micro");
                exchange.getIn().setHeader(MQ2Constants.BROKER_ENGINE, EngineType.ACTIVEMQ.name());
                exchange.getIn().setHeader(MQ2Constants.BROKER_ENGINE_VERSION, "5.15.6");
                exchange.getIn().setHeader(MQ2Constants.BROKER_PUBLICLY_ACCESSIBLE, false);
                List<User> users = new ArrayList<>();
                User.Builder user = User.builder();
                user.username("camel");
                user.password("camelpwd");
                users.add(user.build());
                exchange.getIn().setHeader(MQ2Constants.BROKER_USERS, users);

       }
    })
    .to("aws2-mq://test?amazonMqClient=#amazonMqClient&operation=createBroker")
```

-   deleteBroker: this operation will delete an MQ Broker in AWS
    

```java
from("direct:listBrokers")
    .setHeader(MQ2Constants.BROKER_ID, constant("123")
    .to("aws2-mq://test?amazonMqClient=#amazonMqClient&operation=deleteBroker")
```

-   rebootBroker: this operation will delete an MQ Broker in AWS
    

```java
from("direct:listBrokers")
    .setHeader(MQ2Constants.BROKER_ID, constant("123")
    .to("aws2-mq://test?amazonMqClient=#amazonMqClient&operation=rebootBroker")
```

## Using a POJO as body

Sometimes build an AWS Request can be complex, because of multiple options. We introduce the possibility to use a POJO as body. In AWS MQ there are multiple operations you can submit, as an example for List brokers request, you can do something like:

```java
from("direct:aws2-mq")
     .setBody(ListBrokersRequest.builder().maxResults(10).build())
     .to("aws2-mq://test?amazonMqClient=#amazonMqClient&operation=listBrokers&pojoRequest=true")
```

In this way you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-mq</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-mq with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-mq-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 17 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-mq.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-mq.amazon-mq-client** | To use a existing configured AmazonMQClient as client. The option is a software.amazon.awssdk.services.mq.MqClient type. |  | MqClient |
| **camel.component.aws2-mq.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-mq.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.mq.MQ2Configuration type. |  | MQ2Configuration |
| **camel.component.aws2-mq.enabled** | Whether to enable auto configuration of the aws2-mq component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-mq.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-mq.operation** | The operation to perform. It can be listBrokers,createBroker,deleteBroker. |  | MQ2Operations |
| **camel.component.aws2-mq.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-mq.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-mq.proxy-host** | To define a proxy host when instantiating the MQ client. |  | String |
| **camel.component.aws2-mq.proxy-port** | To define a proxy port when instantiating the MQ client. |  | Integer |
| **camel.component.aws2-mq.proxy-protocol** | To define a proxy protocol when instantiating the MQ client. |  | Protocol |
| **camel.component.aws2-mq.region** | The region in which MQ client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-mq.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-mq.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-mq.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-mq.use-default-credentials-provider** | Set whether the MQ client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |