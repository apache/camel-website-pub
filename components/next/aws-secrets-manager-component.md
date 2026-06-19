# AWS Secrets Manager

**Since Camel 3.9**

**Only producer is supported**

The AWS Secrets Manager component supports [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Secrets Manager. More information is available at [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/).

## URI Format

aws-secrets-manager://label\[?options\]

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

The AWS Secrets Manager component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **binaryPayload** (producer) | Set if the secret is binary or not. | false | boolean |
| **configuration** (producer) | Component configuration. |  | SecretsManagerConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   listSecrets
    
-   createSecret
    
-   getSecret
    
-   batchGetSecret
    
-   describeSecret
    
-   deleteSecret
    
-   rotateSecret
    
-   updateSecret
    
-   restoreSecret
    
-   replicateSecretToRegions
    
-   putSecretValue
    





 |  | SecretsManagerOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which a Secrets Manager client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useProfileCredentialsProvider** (producer) | Set whether the Secrets Manager client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **secretsManagerClient** (advanced) | **Autowired** To use an existing configured AWS Secrets Manager client. |  | SecretsManagerClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Secrets Manager client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Secrets Manager client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Secrets Manager client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Secrets Manager client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Secrets Manager client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Secrets Manager. | false | boolean |

## Endpoint Options

The AWS Secrets Manager endpoint is configured using URI syntax:

aws-secrets-manager:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **binaryPayload** (producer) | Set if the secret is binary or not. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   listSecrets
    
-   createSecret
    
-   getSecret
    
-   batchGetSecret
    
-   describeSecret
    
-   deleteSecret
    
-   rotateSecret
    
-   updateSecret
    
-   restoreSecret
    
-   replicateSecretToRegions
    
-   putSecretValue
    





 |  | SecretsManagerOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which a Secrets Manager client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useProfileCredentialsProvider** (producer) | Set whether the Secrets Manager client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **secretsManagerClient** (advanced) | **Autowired** To use an existing configured AWS Secrets Manager client. |  | SecretsManagerClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Secrets Manager client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Secrets Manager client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Secrets Manager client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Secrets Manager client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Secrets Manager client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Secrets Manager. | false | boolean |

## Message Headers

The AWS Secrets Manager component supports 11 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsSecretsManagerOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsSecretsManagerMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#MAX_RESULTS) | The number of results to include in the response. |  | Integer |
| **CamelAwsSecretsManagerSecretName** (producer) Constant: [`SECRET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_NAME) | The name of the secret. |  | String |
| **CamelAwsSecretsManagerSecretDescription** (producer) Constant: [`SECRET_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_DESCRIPTION) | The description of the secret. |  | String |
| **CamelAwsSecretsManagerSecretId** (producer) Constant: [`SECRET_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_ID) | The ARN or name of the secret. |  | String |
| **CamelAwsSecretsManagerSecretIds** (producer) Constant: [`SECRET_IDS`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_IDS) | A comma separated list of the ARN or name of the secrets. |  | String |
| **CamelAwsSecretsManagerLambdaRotationFunctionArn** (producer) Constant: [`LAMBDA_ROTATION_FUNCTION_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#LAMBDA_ROTATION_FUNCTION_ARN) | The ARN of the Lambda rotation function that can rotate the secret. |  | String |
| **CamelAwsSecretsManagerSecretVersionId** (producer) Constant: [`SECRET_VERSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_VERSION_ID) | The unique identifier of the version of the secret. |  | String |
| **CamelAwsSecretsManagerSecretVersionIds** (producer) Constant: [`SECRET_VERSION_IDS`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_VERSION_IDS) | The unique identifier of the version of the secrets in batch operation. |  | String |
| **CamelAwsSecretsManagerSecretReplicationRegions** (producer) Constant: [`SECRET_REPLICATION_REGIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_REPLICATION_REGIONS) | A comma separated list of Regions in which to replicate the secret. |  | String |
| **CamelAwsSecretsManagerSecretForceDeletion** (producer) Constant: [`SECRET_FORCE_DELETION`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_FORCE_DELETION) | If this header is set to true, the deleted secret won’t have any retention period. |  | Boolean |

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

### Using AWS Secrets Manager Property Function

To use this function, you’ll need to provide credentials to AWS Secrets Manager Service as environment variables:

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

It is also possible to specify a particular profile name for accessing AWS Secrets Manager

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
> `camel.vault.aws` configuration only applies to the AWS Secrets Manager properties function (E.g when resolving properties). When using the `operation` option to create, get, list secrets etc., you should provide the usual options for connecting to AWS Services.

At this point, you’ll be able to reference a property in the following way:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{aws:route}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws:route}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{aws:route}}"
```

Where route will be the name of the secret stored in the AWS Secrets Manager Service.

You could specify a default value in case the secret is not present on AWS Secret Manager:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{aws:route:default}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws:route:default}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{aws:route:default}}"
```

In this case, if the secret doesn’t exist, the property will fall back to "default" as value.

Also, you are able to get a particular field of the secret, if you have, for example, a secret named database of this form:

```bash
{
  "username": "admin",
  "password": "password123",
  "engine": "postgres",
  "host": "127.0.0.1",
  "port": "3128",
  "dbname": "db"
}
```

You’re able to do get single secret value in your route, like for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{aws:database#username}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{aws:database#username}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{aws:database#username}}"
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on AWS Secret Manager:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{aws:database#username:admin}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{aws:database#username:admin}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{aws:database#username:admin}}"
```

In this case, if the secret doesn’t exist or the secret exists, but the username field is not part of the secret, the property will fall back to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approach, with field/default value specified or only with secret:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{aws:route@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws:route@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{aws:route@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"
```

This approach will return the RAW route secret with the version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451'.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{aws:route:default@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws:route:default@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{aws:route:default@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"
```

This approach will return the route secret value with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451' or default value in case the secret doesn’t exist or the version doesn’t exist.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{aws:database#username:admin@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{aws:database#username:admin@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{aws:database#username:admin@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"
```

This approach will return the username field of the database secret with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451' or admin in case the secret doesn’t exist or the version doesn’t exist.

For the moment we are not considering the rotation function if any are applied, but it is in the work to be done.

The only requirement is adding the camel-aws-secrets-manager jar to your Camel application.

### Testing AWS Secrets Manager Property Function with Localstack

For testing purpose you might want to test the function on Localstack. To make this easier you can use the following two properties in combination with the others:

```properties
camel.vault.aws.overrideEndpoint = true
camel.vault.aws.uriEndpointOverride = <localstack_url>
```

With this you could be able to retrieve secret with the function directly from the Localstack instance.

### Automatic Camel context reloading on Secret Refresh

Being able to reload Camel context on a Secret Refresh could be done by specifying the usual credentials (the same used for AWS Secret Manager Property Function).

With Environment variables:

```bash
export CAMEL_VAULT_AWS_USE_DEFAULT_CREDENTIALS_PROVIDER=accessKey
export CAMEL_VAULT_AWS_REGION=region
```

or as plain Camel main properties:

```properties
camel.vault.aws.useDefaultCredentialProvider = true
camel.vault.aws.region = region
```

Or by specifying accessKey/SecretKey and region, instead of using the default credentials provider chain.

To enable the automatic refresh, you’ll need additional properties to set:

```properties
camel.vault.aws.refreshEnabled=true
camel.vault.aws.refreshPeriod=60000
camel.vault.aws.secrets=Secret
camel.main.context-reload-enabled = true
```

where `camel.vault.aws.refreshEnabled` will enable the automatic context reload, `camel.vault.aws.refreshPeriod` is the interval of time between two different checks for update events and `camel.vault.aws.secrets` is a regex representing the secrets we want to track for updates.

Note that `camel.vault.aws.secrets` is not mandatory: if not specified the task responsible for checking updates events will take into accounts or the properties with an `aws:` prefix.

### Automatic Camel context reloading on Secret Refresh with Eventbridge and AWS SQS Services

Another option is to use AWS EventBridge in conjunction with the AWS SQS service.

On the AWS side, the following resources need to be created:

-   an AWS Couldtrail trail
    
-   an AWS SQS Queue
    
-   an Eventbridge rule of the following kind
    

```json
{
  "source": ["aws.secretsmanager"],
  "detail-type": ["AWS API Call via CloudTrail"],
  "detail": {
    "eventSource": ["secretsmanager.amazonaws.com"]
  }
}
```

This rule will make the event related to AWS Secrets Manager filtered

-   You need to set the a Rule target to the AWS SQS Queue for Eventbridge rule
    
-   You need to give permission to the Eventbrige rule, to write on the above SQS Queue. For doing this you’ll need to define a json file like this:
    

```json
{
    "Policy": "{\"Version\":\"2012-10-17\",\"Id\":\"<queue_arn>/SQSDefaultPolicy\",\"Statement\":[{\"Sid\": \"EventsToMyQueue\", \"Effect\": \"Allow\", \"Principal\": {\"Service\": \"events.amazonaws.com\"}, \"Action\": \"sqs:SendMessage\", \"Resource\": \"<queue_arn>\", \"Condition\": {\"ArnEquals\": {\"aws:SourceArn\": \"<eventbridge_rule_arn>\"}}}]}"
}
```

Change the values for queue\_arn and eventbridge\_rule\_arn, save the file with policy.json name and run the following command with AWS CLI

```bash
aws sqs set-queue-attributes --queue-url <queue_url> --attributes file://policy.json
```

where queue\_url is the AWS SQS Queue URL of the just created Queue.

Now you should be able to set up the configuration on the Camel side. To enable the SQS notification add the following properties:

```properties
camel.vault.aws.refreshEnabled=true
camel.vault.aws.refreshPeriod=60000
camel.vault.aws.secrets=Secret
camel.main.context-reload-enabled = true
camel.vault.aws.useSqsNotification=true
camel.vault.aws.sqsQueueUrl=<queue_url>
```

where queue\_url is the AWS SQS Queue URL of the just created Queue.

Whenever an event of PutSecretValue for the Secret named 'Secret' will happen, a message will be enqueued in the AWS SQS Queue and consumed on the Camel side and a context reload will be triggered.

### Secrets Manager Producer operations

Camel-AWS-Secrets-manager component provides the following operation on the producer side:

-   listSecrets
    
-   createSecret
    
-   deleteSecret
    
-   describeSecret
    
-   rotateSecret
    
-   getSecret
    
-   batchGetSecret
    
-   updateSecret
    
-   replicateSecretToRegions
    

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws-secrets-manager</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

### Using AWS Secrets Manager Property Function in Spring Boot for Early resolving properties

AWS Secrets Manager Spring Boot component starter offers the ability to early resolve properties, so the end user could resolve properties directly in the application.properties before both Spring Boot runtime and Camel context will start.

This could be accomplished in the following way. You should specified this property in your application.properties file:

```bash
camel.component.aws-secrets-manager.early-resolve-properties=true
```

This will enable the feature so you’ll be able to resolved properties, in your application.properties file, like:

```bash
foo = aws:database/prod#password
```