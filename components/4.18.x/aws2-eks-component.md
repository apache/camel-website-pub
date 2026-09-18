# AWS Elastic Kubernetes Service (EKS)

**Since Camel 3.1**

**Only producer is supported**

The AWS2 EKS component supports create, delete, describe and list clusters [AWS EKS](https://aws.amazon.com/eks/) clusters instances.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon EKS. More information is available at [Amazon EKS](https://aws.amazon.com/eks/).

## URI Format

aws2-eks://label\[?options\]

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

The AWS Elastic Kubernetes Service (EKS) component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | EKS2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   listClusters
    
-   describeCluster
    
-   createCluster
    
-   deleteCluster
    





 |  | EKS2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which EKS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useDefaultCredentialsProvider** (producer) | Set whether the EKS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the EKS client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **eksClient** (advanced) | **Autowired** To use an existing configured AWS EKS client. |  | EksClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the EKS client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the EKS client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the EKS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the EKS client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in EKS. | false | boolean |

## Endpoint Options

The AWS Elastic Kubernetes Service (EKS) endpoint is configured using URI syntax:

aws2-eks:label

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
    
-   describeCluster
    
-   createCluster
    
-   deleteCluster
    





 |  | EKS2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which EKS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useDefaultCredentialsProvider** (producer) | Set whether the EKS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the EKS client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **eksClient** (advanced) | **Autowired** To use an existing configured AWS EKS client. |  | EksClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the EKS client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the EKS client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the EKS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the EKS client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in EKS. | false | boolean |

## Message Headers

The AWS Elastic Kubernetes Service (EKS) component supports 9 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsEKSOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eks/latest/org/apache/camel/component/aws2/eks/EKS2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsEKSMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eks/latest/org/apache/camel/component/aws2/eks/EKS2Constants.html#MAX_RESULTS) | The limit number of results while listing clusters. |  | Integer |
| **CamelAwsEKSDescription** (producer) Constant: [`DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eks/latest/org/apache/camel/component/aws2/eks/EKS2Constants.html#DESCRIPTION) | A key description to use while performing a createKey operation. |  | String |
| **CamelAwsEKSClusterName** (producer) Constant: [`CLUSTER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eks/latest/org/apache/camel/component/aws2/eks/EKS2Constants.html#CLUSTER_NAME) | The cluster name. |  | String |
| **CamelAwsEKSRoleARN** (producer) Constant: [`ROLE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eks/latest/org/apache/camel/component/aws2/eks/EKS2Constants.html#ROLE_ARN) | The role ARN to use while creating the cluster. |  | String |
| **CamelAwsEKSVPCConfig** (producer) Constant: [`VPC_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eks/latest/org/apache/camel/component/aws2/eks/EKS2Constants.html#VPC_CONFIG) | The VPC config for the creations of an EKS cluster. |  | VpcConfigRequest |
| **CamelAwsEKSNextToken** (listClusters) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eks/latest/org/apache/camel/component/aws2/eks/EKS2Constants.html#NEXT_TOKEN) | The token for the next set of results. |  | String |
| **CamelAwsEKSIsTruncated** (listClusters) Constant: [`IS_TRUNCATED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eks/latest/org/apache/camel/component/aws2/eks/EKS2Constants.html#IS_TRUNCATED) | Whether the response has more results (is truncated). |  | Boolean |
| **CamelAwsEKSClusterArn** (createCluster describeCluster deleteCluster) Constant: [`CLUSTER_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eks/latest/org/apache/camel/component/aws2/eks/EKS2Constants.html#CLUSTER_ARN) | The ARN of the cluster. |  | String |

Required EKS component options

You have to provide the amazonEKSClient in the Registry or your accessKey and secretKey to access the [Amazon EKS](https://aws.amazon.com/eks/) service.

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

### EKS Producer operations

Camel-AWS EKS component provides the following operation on the producer side:

-   listClusters
    
-   createCluster
    
-   describeCluster
    
-   deleteCluster
    

## Examples

### Producer Examples

-   listClusters: this operation will list the available clusters in EKS
    

```java
from("direct:listClusters")
    .to("aws2-eks://test?eksClient=#amazonEksClient&operation=listClusters")
```

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as a body. In AWS EKS there are multiple operations you can submit, as an example for List cluster request, you can do something like:

```java
from("direct:start")
  .setBody(ListClustersRequest.builder().maxResults(12).build())
  .to("aws2-eks://test?eksClient=#amazonEksClient&operation=listClusters&pojoRequest=true")
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-eks</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-eks with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-eks-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-eks.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-eks.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-eks.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.eks.EKS2Configuration type. |  | EKS2Configuration |
| **camel.component.aws2-eks.eks-client** | To use an existing configured AWS EKS client. The option is a software.amazon.awssdk.services.eks.EksClient type. |  | EksClient |
| **camel.component.aws2-eks.enabled** | Whether to enable auto configuration of the aws2-eks component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-eks.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws2-eks.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws2-eks.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-eks.operation** | The operation to perform. |  | EKS2Operations |
| **camel.component.aws2-eks.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-eks.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-eks.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws2-eks.proxy-host** | To define a proxy host when instantiating the EKS client. |  | String |
| **camel.component.aws2-eks.proxy-port** | To define a proxy port when instantiating the EKS client. |  | Integer |
| **camel.component.aws2-eks.proxy-protocol** | To define a proxy protocol when instantiating the EKS client. | https | Protocol |
| **camel.component.aws2-eks.region** | The region in which EKS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-eks.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-eks.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws2-eks.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-eks.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-eks.use-default-credentials-provider** | Set whether the EKS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-eks.use-profile-credentials-provider** | Set whether the EKS client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-eks.use-session-credentials** | Set whether the EKS client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in EKS. | false | Boolean |