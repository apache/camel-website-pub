# AWS Bedrock Agent Runtime

**Since Camel 4.5**

**Only producer is supported**

The AWS2 Bedrock component supports invoking a supported LLM model from [AWS Bedrock](https://aws.amazon.com/bedrock/) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Bedrock. More information is available at [Amazon Bedrock](https://aws.amazon.com/bedrock/).

## URI Format

aws-bedrock-agent-runtime://label\[?options\]

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

The AWS Bedrock Agent Runtime component supports 24 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | BedrockAgentRuntimeConfiguration |
| **knowledgeBaseId** (producer) | **Required** Define the Knowledge Base Id we are going to use. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **modelId** (producer) | 
**Required** Define the model Id we are going to use.

Enum values:

-   anthropic.claude-instant-v1
    
-   anthropic.claude-v2
    
-   anthropic.claude-v2:1
    





 |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   retrieveAndGenerate
    





 |  | BedrockAgentRuntimeOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which Bedrock Agent Runtime client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   us-east-1
    
-   us-west-1
    
-   ap-southeast-1
    
-   ap-northeast-1
    
-   eu-central-1
    





 |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Bedrock Agent Runtime client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Bedrock Agent Runtime client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **bedrockAgentRuntimeClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Agent Runtime client. |  | BedrockAgentRuntimeClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock Agent Runtime client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock Agent Runtime client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock Agent Runtime client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock Agent Runtime client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

## Endpoint Options

The AWS Bedrock Agent Runtime endpoint is configured using URI syntax:

aws-bedrock-agent-runtime:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (20 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **knowledgeBaseId** (producer) | **Required** Define the Knowledge Base Id we are going to use. |  | String |
| **modelId** (producer) | 
**Required** Define the model Id we are going to use.

Enum values:

-   anthropic.claude-instant-v1
    
-   anthropic.claude-v2
    
-   anthropic.claude-v2:1
    





 |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   retrieveAndGenerate
    





 |  | BedrockAgentRuntimeOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which Bedrock Agent Runtime client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   us-east-1
    
-   us-west-1
    
-   ap-southeast-1
    
-   ap-northeast-1
    
-   eu-central-1
    





 |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Bedrock Agent Runtime client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Bedrock Agent Runtime client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **bedrockAgentRuntimeClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Agent Runtime client. |  | BedrockAgentRuntimeClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock Agent Runtime client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock Agent Runtime client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock Agent Runtime client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock Agent Runtime client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

Required Bedrock component options

You have to provide the bedrockRuntimeClient in the Registry or your accessKey and secretKey to access the [Amazon Bedrock](https://aws.amazon.com/bedrock/) service.

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

## Message Headers

The AWS Bedrock Agent Runtime component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsBedrockAgentRuntimeOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsBedrockAgentRuntimeCitations** (producer) Constant: [`CITATIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#CITATIONS) | When retrieving and generating a response, this header will contain the citations. |  | String |
| **CamelAwsBedrockAgentRuntimeSessionId** (producer) Constant: [`SESSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#SESSION_ID) | When retrieving and generating a response, this header will contain he unique identifier of the session. Reuse the same value to continue the same session with the knowledge base. |  | String |

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws-bedrock</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws-bedrock-agent-runtime with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws-bedrock-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 77 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws-bedrock-agent-runtime.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-bedrock-agent-runtime.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-bedrock-agent-runtime.bedrock-agent-runtime-client** | To use an existing configured AWS Bedrock Agent Runtime client. The option is a software.amazon.awssdk.services.bedrockagentruntime.BedrockAgentRuntimeClient type. |  | BedrockAgentRuntimeClient |
| **camel.component.aws-bedrock-agent-runtime.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.bedrock.agentruntime.BedrockAgentRuntimeConfiguration type. |  | BedrockAgentRuntimeConfiguration |
| **camel.component.aws-bedrock-agent-runtime.enabled** | Whether to enable auto configuration of the aws-bedrock-agent-runtime component. This is enabled by default. |  | Boolean |
| **camel.component.aws-bedrock-agent-runtime.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws-bedrock-agent-runtime.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws-bedrock-agent-runtime.knowledge-base-id** | Define the Knowledge Base Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent-runtime.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.model-id** | Define the model Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent-runtime.operation** | The operation to perform. |  | BedrockAgentRuntimeOperations |
| **camel.component.aws-bedrock-agent-runtime.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws-bedrock-agent-runtime.proxy-host** | To define a proxy host when instantiating the Bedrock Agent Runtime client. |  | String |
| **camel.component.aws-bedrock-agent-runtime.proxy-port** | To define a proxy port when instantiating the Bedrock Agent Runtime client. |  | Integer |
| **camel.component.aws-bedrock-agent-runtime.proxy-protocol** | To define a proxy protocol when instantiating the Bedrock Agent Runtime client. | https | Protocol |
| **camel.component.aws-bedrock-agent-runtime.region** | The region in which Bedrock Agent Runtime client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-bedrock-agent-runtime.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-bedrock-agent-runtime.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws-bedrock-agent-runtime.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-bedrock-agent-runtime.use-default-credentials-provider** | Set whether the Bedrock Agent Runtime client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.use-profile-credentials-provider** | Set whether the Bedrock Agent Runtime client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.use-session-credentials** | Set whether the Bedrock Agent Runtime client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | Boolean |
| **camel.component.aws-bedrock-agent.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-bedrock-agent.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-bedrock-agent.bedrock-agent-client** | To use an existing configured AWS Bedrock Agent client. The option is a software.amazon.awssdk.services.bedrockagent.BedrockAgentClient type. |  | BedrockAgentClient |
| **camel.component.aws-bedrock-agent.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws-bedrock-agent.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.bedrock.agent.BedrockAgentConfiguration type. |  | BedrockAgentConfiguration |
| **camel.component.aws-bedrock-agent.data-source-id** | Define the Data source Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent.enabled** | Whether to enable auto configuration of the aws-bedrock-agent component. This is enabled by default. |  | Boolean |
| **camel.component.aws-bedrock-agent.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws-bedrock-agent.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws-bedrock-agent.ingestion-job-id** | Define the Ingestion Job Id we want to track. |  | String |
| **camel.component.aws-bedrock-agent.knowledge-base-id** | Define the Knowledge Base Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-bedrock-agent.model-id** | Define the model Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent.operation** | The operation to perform. |  | BedrockAgentOperations |
| **camel.component.aws-bedrock-agent.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-bedrock-agent.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-bedrock-agent.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws-bedrock-agent.proxy-host** | To define a proxy host when instantiating the Bedrock Agent client. |  | String |
| **camel.component.aws-bedrock-agent.proxy-port** | To define a proxy port when instantiating the Bedrock Agent client. |  | Integer |
| **camel.component.aws-bedrock-agent.proxy-protocol** | To define a proxy protocol when instantiating the Bedrock Agent client. | https | Protocol |
| **camel.component.aws-bedrock-agent.region** | The region in which Bedrock Agent client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-bedrock-agent.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-bedrock-agent.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws-bedrock-agent.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-bedrock-agent.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-bedrock-agent.use-default-credentials-provider** | Set whether the Bedrock Agent client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws-bedrock-agent.use-profile-credentials-provider** | Set whether the Bedrock Agent client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws-bedrock-agent.use-session-credentials** | Set whether the Bedrock Agent client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | Boolean |
| **camel.component.aws-bedrock.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-bedrock.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-bedrock.bedrock-runtime-client** | To use an existing configured AWS Bedrock Runtime client. The option is a software.amazon.awssdk.services.bedrockruntime.BedrockRuntimeClient type. |  | BedrockRuntimeClient |
| **camel.component.aws-bedrock.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.bedrock.runtime.BedrockConfiguration type. |  | BedrockConfiguration |
| **camel.component.aws-bedrock.enabled** | Whether to enable auto configuration of the aws-bedrock component. This is enabled by default. |  | Boolean |
| **camel.component.aws-bedrock.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws-bedrock.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws-bedrock.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-bedrock.model-id** | Define the model Id we are going to use. |  | String |
| **camel.component.aws-bedrock.operation** | The operation to perform. |  | BedrockOperations |
| **camel.component.aws-bedrock.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-bedrock.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-bedrock.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws-bedrock.proxy-host** | To define a proxy host when instantiating the Bedrock client. |  | String |
| **camel.component.aws-bedrock.proxy-port** | To define a proxy port when instantiating the Bedrock client. |  | Integer |
| **camel.component.aws-bedrock.proxy-protocol** | To define a proxy protocol when instantiating the Bedrock client. | https | Protocol |
| **camel.component.aws-bedrock.region** | The region in which Bedrock client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-bedrock.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-bedrock.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws-bedrock.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-bedrock.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-bedrock.use-default-credentials-provider** | Set whether the Bedrock client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws-bedrock.use-profile-credentials-provider** | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws-bedrock.use-session-credentials** | Set whether the Bedrock client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | Boolean |