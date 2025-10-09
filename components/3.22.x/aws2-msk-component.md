# AWS Managed Streaming for Apache Kafka (MSK)

**Since Camel 3.1**

**Only producer is supported**

The AWS2 MSK component supports create, run, start, stop and terminate [AWS MSK](https://aws.amazon.com/msk/) instances.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon MSK. More information is available at [Amazon MSK](https://aws.amazon.com/msk/).

## URI Format

aws2-msk://label\[?options\]

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

The AWS Managed Streaming for Apache Kafka (MSK) component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | MSK2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **mskClient** (producer) | **Autowired** To use a existing configured AWS MSK as client. |  | KafkaClient |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   listClusters
    
-   createCluster
    
-   deleteCluster
    
-   describeCluster
    





 |  | MSK2Operations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the MSK client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the MSK client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the MSK client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which MSK client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Kafka client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS Managed Streaming for Apache Kafka (MSK) endpoint is configured using URI syntax:

aws2-msk:label

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **mskClient** (producer) | **Autowired** To use a existing configured AWS MSK as client. |  | KafkaClient |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   listClusters
    
-   createCluster
    
-   deleteCluster
    
-   describeCluster
    





 |  | MSK2Operations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the MSK client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the MSK client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the MSK client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which MSK client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Kafka client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

Required MSK component options

You have to provide the amazonMskClient in the Registry or your accessKey and secretKey to access the [Amazon MSK](https://aws.amazon.com/msk/) service.

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

The AWS Managed Streaming for Apache Kafka (MSK) component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsMSKOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsMSKClusterFilter** (producer) Constant: [`CLUSTERS_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#CLUSTERS_FILTER) | The cluster name filter for list operation. |  | String |
| **CamelAwsMSKClusterName** (producer) Constant: [`CLUSTER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#CLUSTER_NAME) | The cluster name for list and create operation. |  | String |
| **CamelAwsMSKClusterArn** (producer) Constant: [`CLUSTER_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#CLUSTER_ARN) | The cluster arn for delete operation. |  | String |
| **CamelAwsMSKClusterKafkaVersion** (producer) Constant: [`CLUSTER_KAFKA_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#CLUSTER_KAFKA_VERSION) | The Kafka for the cluster during create operation. |  | String |
| **CamelAwsMSKBrokerNodesNumber** (producer) Constant: [`BROKER_NODES_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#BROKER_NODES_NUMBER) | The number of nodes for the cluster during create operation. |  | Integer |
| **CamelAwsMSKBrokerNodesGroupInfo** (producer) Constant: [`BROKER_NODES_GROUP_INFO`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#BROKER_NODES_GROUP_INFO) | The Broker nodes group info to provide during the create operation. |  | BrokerNodeGroupInfo |

### MSK Producer operations

Camel-AWS MSK component provides the following operation on the producer side:

-   listClusters
    
-   createCluster
    
-   deleteCluster
    
-   describeCluster
    

## Examples

### Producer Examples

-   listClusters: this operation will list the available MSK Brokers in AWS
    

```java
from("direct:listClusters")
    .to("aws2-msk://test?mskClient=#amazonMskClient&operation=listClusters")
```

-   createCluster: this operation will create an MSK Cluster in AWS
    

```java
from("direct:createCluster")
    .process(new Processor() {
       @Override
       public void process(Exchange exchange) throws Exception {
                exchange.getIn().setHeader(MSK2Constants.CLUSTER_NAME, "test-kafka");
                exchange.getIn().setHeader(MSK2Constants.CLUSTER_KAFKA_VERSION, "2.1.1");
                exchange.getIn().setHeader(MSK2Constants.BROKER_NODES_NUMBER, 2);
                BrokerNodeGroupInfo groupInfo = BrokerNodeGroupInfo.builder().build();
                exchange.getIn().setHeader(MSK2Constants.BROKER_NODES_GROUP_INFO, groupInfo);
       }
    })
    .to("aws2-msk://test?mskClient=#amazonMskClient&operation=createCluster")
```

-   deleteCluster: this operation will delete an MSK Cluster in AWS
    

```java
from("direct:deleteCluster")
    .setHeader(MSK2Constants.CLUSTER_ARN, constant("test-kafka"));
    .to("aws2-msk://test?mskClient=#amazonMskClient&operation=deleteCluster")
```

```java
from("direct:createCluster")
    .process(new Processor() {
       @Override
       public void process(Exchange exchange) throws Exception {
                exchange.getIn().setHeader(MSK2Constants.CLUSTER_NAME, "test-kafka");
                exchange.getIn().setHeader(MSK2Constants.CLUSTER_KAFKA_VERSION, "2.1.1");
                exchange.getIn().setHeader(MSK2Constants.BROKER_NODES_NUMBER, 2);
                BrokerNodeGroupInfo groupInfo = BrokerNodeGroupInfo.builder().build();
                exchange.getIn().setHeader(MSK2Constants.BROKER_NODES_GROUP_INFO, groupInfo);
       }
    })
    .to("aws2-msk://test?mskClient=#amazonMskClient&operation=deleteCluster")
```

## Using a POJO as body

Sometimes build an AWS Request can be complex, because of multiple options. We introduce the possibility to use a POJO as body. In AWS MSK there are multiple operations you can submit, as an example for List clusters request, you can do something like:

```java
from("direct:aws2-msk")
     .setBody(ListClustersRequest.builder().maxResults(10).build())
     .to("aws2-msk://test?mskClient=#amazonMskClient&operation=listClusters&pojoRequest=true")
```

In this way you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-msk</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-msk with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-msk-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 17 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-msk.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-msk.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-msk.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.msk.MSK2Configuration type. |  | MSK2Configuration |
| **camel.component.aws2-msk.enabled** | Whether to enable auto configuration of the aws2-msk component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-msk.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-msk.msk-client** | To use a existing configured AWS MSK as client. The option is a software.amazon.awssdk.services.kafka.KafkaClient type. |  | KafkaClient |
| **camel.component.aws2-msk.operation** | The operation to perform. |  | MSK2Operations |
| **camel.component.aws2-msk.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-msk.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-msk.proxy-host** | To define a proxy host when instantiating the MSK client. |  | String |
| **camel.component.aws2-msk.proxy-port** | To define a proxy port when instantiating the MSK client. |  | Integer |
| **camel.component.aws2-msk.proxy-protocol** | To define a proxy protocol when instantiating the MSK client. |  | Protocol |
| **camel.component.aws2-msk.region** | The region in which MSK client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-msk.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-msk.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-msk.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-msk.use-default-credentials-provider** | Set whether the Kafka client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |