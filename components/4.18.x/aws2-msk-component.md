# AWS Managed Streaming for Apache Kafka (MSK)

**Since Camel 3.1**

**Only producer is supported**

The AWS2 MSK component supports create, run, start, stop and terminate [AWS MSK](https://aws.amazon.com/msk/) instances.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon MSK. More information is available at [Amazon MSK](https://aws.amazon.com/msk/).

## URI Format

aws2-msk://label\[?options\]

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

The AWS Managed Streaming for Apache Kafka (MSK) component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | MSK2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   listClusters
    
-   createCluster
    
-   deleteCluster
    
-   describeCluster
    





 |  | MSK2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the MSK client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **mskClient** (advanced) | **Autowired** To use an existing configured AWS MSK client. |  | KafkaClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the MSK client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the MSK client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the MSK client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Kafka client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the MSK client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the MSK client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in MSK. | false | boolean |

## Endpoint Options

The AWS Managed Streaming for Apache Kafka (MSK) endpoint is configured using URI syntax:

aws2-msk:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (18 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   listClusters
    
-   createCluster
    
-   deleteCluster
    
-   describeCluster
    





 |  | MSK2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the MSK client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **mskClient** (advanced) | **Autowired** To use an existing configured AWS MSK client. |  | KafkaClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the MSK client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the MSK client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the MSK client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Kafka client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the MSK client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the MSK client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in MSK. | false | boolean |

## Message Headers

The AWS Managed Streaming for Apache Kafka (MSK) component supports 11 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsMSKOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsMSKClusterFilter** (producer) Constant: [`CLUSTERS_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#CLUSTERS_FILTER) | The cluster name filter for list operation. |  | String |
| **CamelAwsMSKClusterName** (producer) Constant: [`CLUSTER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#CLUSTER_NAME) | The cluster name for list and create operation. |  | String |
| **CamelAwsMSKClusterArn** (producer) Constant: [`CLUSTER_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#CLUSTER_ARN) | The cluster arn for delete operation. |  | String |
| **CamelAwsMSKClusterKafkaVersion** (producer) Constant: [`CLUSTER_KAFKA_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#CLUSTER_KAFKA_VERSION) | The Kafka for the cluster during create operation. |  | String |
| **CamelAwsMSKBrokerNodesNumber** (producer) Constant: [`BROKER_NODES_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#BROKER_NODES_NUMBER) | The number of nodes for the cluster during create operation. |  | Integer |
| **CamelAwsMSKBrokerNodesGroupInfo** (producer) Constant: [`BROKER_NODES_GROUP_INFO`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#BROKER_NODES_GROUP_INFO) | The Broker nodes group info to provide during the create operation. |  | BrokerNodeGroupInfo |
| **CamelAwsMSKNextToken** (listClusters) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#NEXT_TOKEN) | The token for the next set of results. |  | String |
| **CamelAwsMSKMaxResults** (listClusters) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#MAX_RESULTS) | The maximum number of results to return. |  | Integer |
| **CamelAwsMSKIsTruncated** (listClusters) Constant: [`IS_TRUNCATED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#IS_TRUNCATED) | Whether the response has more results (is truncated). |  | Boolean |
| **CamelAwsMSKClusterState** (createCluster describeCluster) Constant: [`CLUSTER_STATE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-msk/latest/org/apache/camel/component/aws2/msk/MSK2Constants.html#CLUSTER_STATE) | The state of the cluster. |  | String |

Required MSK component options

You have to provide the amazonMskClient in the Registry or your accessKey and secretKey to access the [Amazon MSK](https://aws.amazon.com/msk/) service.

## Usage

### Static credentials vs Default Credential Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

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

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as the body. In AWS MSK, there are multiple operations you can submit, as an example for List clusters request, you can do something like:

```java
from("direct:aws2-msk")
     .setBody(ListClustersRequest.builder().maxResults(10).build())
     .to("aws2-msk://test?mskClient=#amazonMskClient&operation=listClusters&pojoRequest=true")
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

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

The component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-msk.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-msk.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-msk.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.msk.MSK2Configuration type. |  | MSK2Configuration |
| **camel.component.aws2-msk.enabled** | Whether to enable auto configuration of the aws2-msk component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-msk.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws2-msk.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws2-msk.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-msk.msk-client** | To use an existing configured AWS MSK client. The option is a software.amazon.awssdk.services.kafka.KafkaClient type. |  | KafkaClient |
| **camel.component.aws2-msk.operation** | The operation to perform. |  | MSK2Operations |
| **camel.component.aws2-msk.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-msk.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-msk.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **camel.component.aws2-msk.proxy-host** | To define a proxy host when instantiating the MSK client. |  | String |
| **camel.component.aws2-msk.proxy-port** | To define a proxy port when instantiating the MSK client. |  | Integer |
| **camel.component.aws2-msk.proxy-protocol** | To define a proxy protocol when instantiating the MSK client. | https | Protocol |
| **camel.component.aws2-msk.region** | The region in which the MSK client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-msk.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-msk.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws2-msk.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-msk.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-msk.use-default-credentials-provider** | Set whether the Kafka client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-msk.use-profile-credentials-provider** | Set whether the MSK client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-msk.use-session-credentials** | Set whether the MSK client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in MSK. | false | Boolean |