# AWS Parameter Store

**Since Camel 4.17**

**Only producer is supported**

The AWS Parameter Store component supports [AWS Systems Manager Parameter Store](https://aws.amazon.com/systems-manager/features/#Parameter_Store) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Systems Manager Parameter Store. More information is available at [AWS Systems Manager Parameter Store](https://aws.amazon.com/systems-manager/features/#Parameter_Store).

## URI Format

aws-parameter-store://label\[?options\]

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

The AWS Parameter Store component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | ParameterStoreConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   getParameter
    
-   getParameters
    
-   getParametersByPath
    
-   putParameter
    
-   deleteParameter
    
-   deleteParameters
    
-   describeParameters
    
-   getParameterHistory
    





 |  | ParameterStoreOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which the SSM client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useProfileCredentialsProvider** (producer) | Set whether the SSM client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **ssmClient** (advanced) | **Autowired** To use an existing configured AWS SSM client. |  | SsmClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SSM client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the SSM client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the SSM client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the SSM client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useSessionCredentials** (security) | Set whether the SSM client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in SSM. | false | boolean |

## Endpoint Options

The AWS Parameter Store endpoint is configured using URI syntax:

aws-parameter-store:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   getParameter
    
-   getParameters
    
-   getParametersByPath
    
-   putParameter
    
-   deleteParameter
    
-   deleteParameters
    
-   describeParameters
    
-   getParameterHistory
    





 |  | ParameterStoreOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which the SSM client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useProfileCredentialsProvider** (producer) | Set whether the SSM client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **ssmClient** (advanced) | **Autowired** To use an existing configured AWS SSM client. |  | SsmClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SSM client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the SSM client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the SSM client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the SSM client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useSessionCredentials** (security) | Set whether the SSM client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in SSM. | false | boolean |

## Message Headers

The AWS Parameter Store component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsParameterStoreOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsParameterStoreMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#MAX_RESULTS) | The number of results to include in the response. |  | Integer |
| **CamelAwsParameterStoreName** (producer) Constant: [`PARAMETER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#PARAMETER_NAME) | The name of the parameter. |  | String |
| **CamelAwsParameterStoreNames** (producer) Constant: [`PARAMETER_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#PARAMETER_NAMES) | A comma separated list of parameter names. |  | String |
| **CamelAwsParameterStoreDescription** (producer) Constant: [`PARAMETER_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#PARAMETER_DESCRIPTION) | The description of the parameter. |  | String |
| **CamelAwsParameterStoreValue** (producer) Constant: [`PARAMETER_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#PARAMETER_VALUE) | The value of the parameter. |  | String |
| **CamelAwsParameterStoreType** (producer) Constant: [`PARAMETER_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#PARAMETER_TYPE) | The type of the parameter (String, StringList, SecureString). |  | String |
| **CamelAwsParameterStorePath** (producer) Constant: [`PARAMETER_PATH`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#PARAMETER_PATH) | The hierarchy path for the parameter. |  | String |
| **CamelAwsParameterStoreWithDecryption** (producer) Constant: [`WITH_DECRYPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#WITH_DECRYPTION) | Whether to decrypt SecureString values. |  | Boolean |
| **CamelAwsParameterStoreRecursive** (producer) Constant: [`RECURSIVE`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#RECURSIVE) | Whether to retrieve all parameters within a hierarchy recursively. |  | Boolean |
| **CamelAwsParameterStoreOverwrite** (producer) Constant: [`OVERWRITE`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#OVERWRITE) | Whether to overwrite an existing parameter. |  | Boolean |
| **CamelAwsParameterStoreVersion** (producer) Constant: [`PARAMETER_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#PARAMETER_VERSION) | The version of the parameter. |  | Long |
| **CamelAwsParameterStoreKmsKeyId** (producer) Constant: [`KMS_KEY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#KMS_KEY_ID) | The KMS Key ID to use for SecureString encryption. |  | String |
| **CamelAwsParameterStoreTier** (producer) Constant: [`PARAMETER_TIER`](https://javadoc.io/doc/org.apache.camel/camel-aws-parameter-store/latest/org/apache/camel/component/aws/parameterstore/ParameterStoreConstants.html#PARAMETER_TIER) | The tier for the parameter (Standard, Advanced, Intelligent-Tiering). |  | String |

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

### Using AWS Parameter Store Property Function

To use this function, you’ll need to provide credentials to AWS Systems Manager Parameter Store as environment variables:

```bash
export CAMEL_VAULT_AWS_ACCESS_KEY=accessKey
export CAMEL_VAULT_AWS_SECRET_KEY=secretKey
export CAMEL_VAULT_AWS_REGION=region
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.aws.accessKey = accessKey
camel.vault.aws.secretKey = secretKey
camel.vault.aws.region = region
```

> **Note**
> if you’re running the application on a Kubernetes based cloud platform, you can initialize the environment variables from a Secret or Configmap to enhance security. You can also enhance security by [setting a Secret property placeholder](../../manual/using-propertyplaceholder.html#_resolving_property_placeholders_on_cloud) which will be initialized at application runtime only.

If you want instead to use the [AWS default credentials provider](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md), you’ll need to provide the following env variables:

```bash
export CAMEL_VAULT_AWS_USE_DEFAULT_CREDENTIALS_PROVIDER=true
export CAMEL_VAULT_AWS_REGION=region
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.aws.defaultCredentialsProvider = true
camel.vault.aws.region = region
```

It is also possible to specify a particular profile name for accessing AWS Parameter Store:

```bash
export CAMEL_VAULT_AWS_USE_PROFILE_CREDENTIALS_PROVIDER=true
export CAMEL_VAULT_AWS_PROFILE_NAME=test-account
export CAMEL_VAULT_AWS_REGION=region
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.aws.profileCredentialsProvider = true
camel.vault.aws.profileName = test-account
camel.vault.aws.region = region
```

> **Note**
> `camel.vault.aws` configuration only applies to the AWS Parameter Store properties function (E.g when resolving properties). When using the `operation` option to create, get, list parameters etc., you should provide the usual options for connecting to AWS Services.

At this point, you’ll be able to reference a property in the following way:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{aws-parameterstore:/myapp/config/endpoint}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws-parameterstore:/myapp/config/endpoint}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{aws-parameterstore:/myapp/config/endpoint}}"
```

Where `/myapp/config/endpoint` will be the name (path) of the parameter stored in the AWS Systems Manager Parameter Store.

You could specify a default value in case the parameter is not present on AWS Parameter Store:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{aws-parameterstore:/myapp/config/endpoint:http://localhost:8080}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws-parameterstore:/myapp/config/endpoint:http://localhost:8080}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{aws-parameterstore:/myapp/config/endpoint:http://localhost:8080}}"
```

In this case, if the parameter doesn’t exist, the property will fall back to "http://localhost:8080" as value.

### Parameter Store Hierarchies

AWS Parameter Store supports hierarchical parameter names. You can organize parameters into hierarchies using forward slashes:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Database host is {{aws-parameterstore:/myapp/database/host}}")
    .log("Database port is {{aws-parameterstore:/myapp/database/port}}")
    .log("Database user is {{aws-parameterstore:/myapp/database/username}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Database host is {{aws-parameterstore:/myapp/database/host}}"/>
        <log message="Database port is {{aws-parameterstore:/myapp/database/port}}"/>
        <log message="Database user is {{aws-parameterstore:/myapp/database/username}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Database host is {{aws-parameterstore:/myapp/database/host}}"
        - log:
            message: "Database port is {{aws-parameterstore:/myapp/database/port}}"
        - log:
            message: "Database user is {{aws-parameterstore:/myapp/database/username}}"
```

### SecureString Parameters

AWS Parameter Store supports SecureString parameters which are encrypted using AWS KMS. The Parameter Store properties function automatically decrypts SecureString parameters:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("API Key is {{aws-parameterstore:/myapp/secrets/api-key}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="API Key is {{aws-parameterstore:/myapp/secrets/api-key}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "API Key is {{aws-parameterstore:/myapp/secrets/api-key}}"
```

The only requirement is adding the camel-aws-parameter-store jar to your Camel application.

### Testing AWS Parameter Store Property Function with Localstack

For testing purpose you might want to test the function on Localstack. To make this easier you can use the following two properties in combination with the others:

```properties
camel.vault.aws.overrideEndpoint = true
camel.vault.aws.uriEndpointOverride = <localstack_url>
```

With this you could be able to retrieve parameters with the function directly from the Localstack instance.

### Parameter Store Producer operations

Camel-AWS-Parameter-Store component provides the following operation on the producer side:

-   getParameter
    
-   getParameters
    
-   getParametersByPath
    
-   putParameter
    
-   deleteParameter
    
-   deleteParameters
    
-   describeParameters
    
-   getParameterHistory
    

#### getParameter

This operation retrieves a single parameter value by name.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getParameter")
    .setHeader(ParameterStoreConstants.PARAMETER_NAME, constant("/myapp/config/endpoint"))
    .to("aws-parameter-store://test?operation=getParameter");
```

```xml
<route>
    <from uri="direct:getParameter"/>
    <setHeader name="CamelAwsParameterStoreName">
        <constant>/myapp/config/endpoint</constant>
    </setHeader>
    <to uri="aws-parameter-store://test?operation=getParameter"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getParameter
    steps:
      - setHeader:
          name: CamelAwsParameterStoreName
          constant: /myapp/config/endpoint
      - to:
          uri: aws-parameter-store://test
          parameters:
            operation: getParameter
```

#### getParameters

This operation retrieves multiple parameters by their names.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getParameters")
    .setHeader(ParameterStoreConstants.PARAMETER_NAMES, constant("/myapp/config/host,/myapp/config/port"))
    .to("aws-parameter-store://test?operation=getParameters");
```

```xml
<route>
    <from uri="direct:getParameters"/>
    <setHeader name="CamelAwsParameterStoreNames">
        <constant>/myapp/config/host,/myapp/config/port</constant>
    </setHeader>
    <to uri="aws-parameter-store://test?operation=getParameters"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getParameters
    steps:
      - setHeader:
          name: CamelAwsParameterStoreNames
          constant: "/myapp/config/host,/myapp/config/port"
      - to:
          uri: aws-parameter-store://test
          parameters:
            operation: getParameters
```

#### getParametersByPath

This operation retrieves all parameters within a hierarchy.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getParametersByPath")
    .setHeader(ParameterStoreConstants.PARAMETER_PATH, constant("/myapp/config"))
    .setHeader(ParameterStoreConstants.RECURSIVE, constant(true))
    .to("aws-parameter-store://test?operation=getParametersByPath");
```

```xml
<route>
    <from uri="direct:getParametersByPath"/>
    <setHeader name="CamelAwsParameterStorePath">
        <constant>/myapp/config</constant>
    </setHeader>
    <setHeader name="CamelAwsParameterStoreRecursive">
        <constant>true</constant>
    </setHeader>
    <to uri="aws-parameter-store://test?operation=getParametersByPath"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getParametersByPath
    steps:
      - setHeader:
          name: CamelAwsParameterStorePath
          constant: /myapp/config
      - setHeader:
          name: CamelAwsParameterStoreRecursive
          constant: "true"
      - to:
          uri: aws-parameter-store://test
          parameters:
            operation: getParametersByPath
```

#### putParameter

This operation creates or updates a parameter.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:putParameter")
    .setHeader(ParameterStoreConstants.PARAMETER_NAME, constant("/myapp/config/endpoint"))
    .setHeader(ParameterStoreConstants.PARAMETER_TYPE, constant("String"))
    .setBody(constant("http://localhost:8080"))
    .to("aws-parameter-store://test?operation=putParameter");
```

```xml
<route>
    <from uri="direct:putParameter"/>
    <setHeader name="CamelAwsParameterStoreName">
        <constant>/myapp/config/endpoint</constant>
    </setHeader>
    <setHeader name="CamelAwsParameterStoreType">
        <constant>String</constant>
    </setHeader>
    <setBody>
        <constant>http://localhost:8080</constant>
    </setBody>
    <to uri="aws-parameter-store://test?operation=putParameter"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:putParameter
    steps:
      - setHeader:
          name: CamelAwsParameterStoreName
          constant: /myapp/config/endpoint
      - setHeader:
          name: CamelAwsParameterStoreType
          constant: String
      - setBody:
          constant: "http://localhost:8080"
      - to:
          uri: aws-parameter-store://test
          parameters:
            operation: putParameter
```

For SecureString parameters:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:putSecureParameter")
    .setHeader(ParameterStoreConstants.PARAMETER_NAME, constant("/myapp/secrets/api-key"))
    .setHeader(ParameterStoreConstants.PARAMETER_TYPE, constant("SecureString"))
    .setBody(constant("my-secret-api-key"))
    .to("aws-parameter-store://test?operation=putParameter");
```

```xml
<route>
    <from uri="direct:putSecureParameter"/>
    <setHeader name="CamelAwsParameterStoreName">
        <constant>/myapp/secrets/api-key</constant>
    </setHeader>
    <setHeader name="CamelAwsParameterStoreType">
        <constant>SecureString</constant>
    </setHeader>
    <setBody>
        <constant>my-secret-api-key</constant>
    </setBody>
    <to uri="aws-parameter-store://test?operation=putParameter"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:putSecureParameter
    steps:
      - setHeader:
          name: CamelAwsParameterStoreName
          constant: /myapp/secrets/api-key
      - setHeader:
          name: CamelAwsParameterStoreType
          constant: SecureString
      - setBody:
          constant: my-secret-api-key
      - to:
          uri: aws-parameter-store://test
          parameters:
            operation: putParameter
```

#### deleteParameter

This operation deletes a single parameter.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deleteParameter")
    .setHeader(ParameterStoreConstants.PARAMETER_NAME, constant("/myapp/config/old-endpoint"))
    .to("aws-parameter-store://test?operation=deleteParameter");
```

```xml
<route>
    <from uri="direct:deleteParameter"/>
    <setHeader name="CamelAwsParameterStoreName">
        <constant>/myapp/config/old-endpoint</constant>
    </setHeader>
    <to uri="aws-parameter-store://test?operation=deleteParameter"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deleteParameter
    steps:
      - setHeader:
          name: CamelAwsParameterStoreName
          constant: /myapp/config/old-endpoint
      - to:
          uri: aws-parameter-store://test
          parameters:
            operation: deleteParameter
```

#### deleteParameters

This operation deletes multiple parameters.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deleteParameters")
    .setHeader(ParameterStoreConstants.PARAMETER_NAMES, constant("/myapp/config/old1,/myapp/config/old2"))
    .to("aws-parameter-store://test?operation=deleteParameters");
```

```xml
<route>
    <from uri="direct:deleteParameters"/>
    <setHeader name="CamelAwsParameterStoreNames">
        <constant>/myapp/config/old1,/myapp/config/old2</constant>
    </setHeader>
    <to uri="aws-parameter-store://test?operation=deleteParameters"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deleteParameters
    steps:
      - setHeader:
          name: CamelAwsParameterStoreNames
          constant: "/myapp/config/old1,/myapp/config/old2"
      - to:
          uri: aws-parameter-store://test
          parameters:
            operation: deleteParameters
```

#### describeParameters

This operation lists parameter metadata.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:describeParameters")
    .setHeader(ParameterStoreConstants.MAX_RESULTS, constant(10))
    .to("aws-parameter-store://test?operation=describeParameters");
```

```xml
<route>
    <from uri="direct:describeParameters"/>
    <setHeader name="CamelAwsParameterStoreMaxResults">
        <constant>10</constant>
    </setHeader>
    <to uri="aws-parameter-store://test?operation=describeParameters"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:describeParameters
    steps:
      - setHeader:
          name: CamelAwsParameterStoreMaxResults
          constant: "10"
      - to:
          uri: aws-parameter-store://test
          parameters:
            operation: describeParameters
```

#### getParameterHistory

This operation retrieves the history of a parameter.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getParameterHistory")
    .setHeader(ParameterStoreConstants.PARAMETER_NAME, constant("/myapp/config/endpoint"))
    .to("aws-parameter-store://test?operation=getParameterHistory");
```

```xml
<route>
    <from uri="direct:getParameterHistory"/>
    <setHeader name="CamelAwsParameterStoreName">
        <constant>/myapp/config/endpoint</constant>
    </setHeader>
    <to uri="aws-parameter-store://test?operation=getParameterHistory"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getParameterHistory
    steps:
      - setHeader:
          name: CamelAwsParameterStoreName
          constant: /myapp/config/endpoint
      - to:
          uri: aws-parameter-store://test
          parameters:
            operation: getParameterHistory
```

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws-parameter-store</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.