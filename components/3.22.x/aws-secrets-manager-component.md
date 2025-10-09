# AWS Secrets Manager

**Since Camel 3.9**

**Only producer is supported**

The AWS Secrets Manager component supports list secret [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Secrets Manager. More information is available at [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/).

## URI Format

aws-secrets-manager://label\[?options\]

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

The AWS Secrets Manager component supports 17 options, which are listed below.

   
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
    
-   describeSecret
    
-   deleteSecret
    
-   rotateSecret
    
-   updateSecret
    
-   restoreSecret
    
-   replicateSecretToRegions
    





 |  | SecretsManagerOperations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the Secrets Manager client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Secrets Manager client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Secrets Manager client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which Secrets Manager client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **secretsManagerClient** (producer) | **Autowired** To use a existing configured AWS Secrets Manager as client. |  | SecretsManagerClient |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Translate client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS Secrets Manager endpoint is configured using URI syntax:

aws-secrets-manager:label

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (15 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **binaryPayload** (producer) | Set if the secret is binary or not. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   listSecrets
    
-   createSecret
    
-   getSecret
    
-   describeSecret
    
-   deleteSecret
    
-   rotateSecret
    
-   updateSecret
    
-   restoreSecret
    
-   replicateSecretToRegions
    





 |  | SecretsManagerOperations |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **proxyHost** (producer) | To define a proxy host when instantiating the Secrets Manager client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Secrets Manager client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Secrets Manager client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which Secrets Manager client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **secretsManagerClient** (producer) | **Autowired** To use a existing configured AWS Secrets Manager as client. |  | SecretsManagerClient |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Translate client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

### Using AWS Secrets Manager Property Function

To use this function you’ll need to provide credentials to AWS Secrets Manager Service as environment variables:

```bash
export $CAMEL_VAULT_AWS_ACCESS_KEY=accessKey
export $CAMEL_VAULT_AWS_SECRET_KEY=secretKey
export $CAMEL_VAULT_AWS_REGION=region
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.aws.accessKey = accessKey
camel.vault.aws.secretKey = secretKey
camel.vault.aws.region = region
```

If you want instead to use the [AWS default credentials provider](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md), you’ll need to provide the following env variables:

```bash
export $CAMEL_VAULT_AWS_USE_DEFAULT_CREDENTIALS_PROVIDER=true
export $CAMEL_VAULT_AWS_REGION=region
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.aws.defaultCredentialsProvider = true
camel.vault.aws.region = region
```

It is also possible to specify a particular profile name for accessing AWS Secrets Manager

```bash
export $CAMEL_VAULT_AWS_USE_PROFILE_CREDENTIALS_PROVIDER=true
export $CAMEL_VAULT_AWS_PROFILE_NAME=test-account
export $CAMEL_VAULT_AWS_REGION=region
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.aws.profileCredentialsProvider = true
camel.vault.aws.profileName = test-account
camel.vault.aws.region = region
```

At this point you’ll be able to reference a property in the following way:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws:route}}"/>
    </route>
</camelContext>
```

Where route will be the name of the secret stored in the AWS Secrets Manager Service.

You could specify a default value in case the secret is not present on AWS Secret Manager:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws:route:default}}"/>
    </route>
</camelContext>
```

In this case if the secret doesn’t exist, the property will fallback to "default" as value.

Also you are able to get particular field of the secret, if you have for example a secret named database of this form:

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

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{aws:database/username}}"/>
    </route>
</camelContext>
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on AWS Secret Manager:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{aws:database/username:admin}}"/>
    </route>
</camelContext>
```

In this case if the secret doesn’t exist or the secret exists, but the username field is not part of the secret, the property will fallback to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approach, with field/default value specified or only with secret:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws:route@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

This approach will return the RAW route secret with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451'.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{aws:route:default@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

This approach will return the route secret value with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451' or default value in case the secret doesn’t exist or the version doesn’t exist.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{aws:database/username:admin@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

This approach will return the username field of the database secret with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451' or admin in case the secret doesn’t exist or the version doesn’t exist.

For the moment we are not considering the rotation function, if any will be applied, but it is in the work to be done.

The only requirement is adding the camel-aws-secrets-manager jar to your Camel application.

### Automatic Camel context reloading on Secret Refresh

Being able to reload Camel context on a Secret Refresh, could be done by specifying the usual credentials (the same used for AWS Secret Manager Property Function).

With Environment variables:

```bash
export $CAMEL_VAULT_AWS_USE_DEFAULT_CREDENTIALS_PROVIDER=accessKey
export $CAMEL_VAULT_AWS_REGION=region
```

or as plain Camel main properties:

```properties
camel.vault.aws.useDefaultCredentialProvider = true
camel.vault.aws.region = region
```

Or by specifying accessKey/SecretKey and region, instead of using the default credentials provider chain.

To enable the automatic refresh you’ll need additional properties to set:

```properties
camel.vault.aws.refreshEnabled=true
camel.vault.aws.refreshPeriod=60000
camel.vault.aws.secrets=Secret
camel.main.context-reload-enabled = true
```

where `camel.vault.aws.refreshEnabled` will enable the automatic context reload, `camel.vault.aws.refreshPeriod` is the interval of time between two different checks for update events and `camel.vault.aws.secrets` is a regex representing the secrets we want to track for updates.

Note that `camel.vault.aws.secrets` is not mandatory: if not specified the task responsible for checking updates events will take into accounts or the properties with an `aws:` prefix.

## Message Headers

The AWS Secrets Manager component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsSecretsManagerOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsSecretsManagerMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#MAX_RESULTS) | The number of results to include in the response. |  | Integer |
| **CamelAwsSecretsManagerSecretName** (producer) Constant: [`SECRET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_NAME) | The name of the secret. |  | String |
| **CamelAwsSecretsManagerSecretDescription** (producer) Constant: [`SECRET_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_DESCRIPTION) | The description of the secret. |  | String |
| **CamelAwsSecretsManagerSecretId** (producer) Constant: [`SECRET_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_ID) | The ARN or name of the secret. |  | String |
| **CamelAwsSecretsManagerLambdaRotationFunctionArn** (producer) Constant: [`LAMBDA_ROTATION_FUNCTION_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#LAMBDA_ROTATION_FUNCTION_ARN) | The ARN of the Lambda rotation function that can rotate the secret. |  | String |
| **CamelAwsSecretsManagerSecretVersionId** (producer) Constant: [`SECRET_VERSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_VERSION_ID) | The unique identifier of the version of the secret. |  | String |
| **CamelAwsSecretsManagerSecretReplicationRegions** (producer) Constant: [`SECRET_REPLICATION_REGIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws-secrets-manager/latest/org/apache/camel/component/aws/secretsmanager/SecretsManagerConstants.html#SECRET_REPLICATION_REGIONS) | A comma separated list of Regions in which to replicate the secret. |  | String |

### Secrets Manager Producer operations

Camel-AWS-Secrets-manager component provides the following operation on the producer side:

-   listSecrets
    
-   createSecret
    
-   deleteSecret
    
-   describeSecret
    
-   rotateSecret
    
-   getSecret
    
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

## Spring Boot Auto-Configuration

When using aws-secrets-manager with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws-secrets-manager-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 18 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws-secrets-manager.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-secrets-manager.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-secrets-manager.binary-payload** | Set if the secret is binary or not. | false | Boolean |
| **camel.component.aws-secrets-manager.configuration** | Component configuration. The option is a org.apache.camel.component.aws.secretsmanager.SecretsManagerConfiguration type. |  | SecretsManagerConfiguration |
| **camel.component.aws-secrets-manager.enabled** | Whether to enable auto configuration of the aws-secrets-manager component. This is enabled by default. |  | Boolean |
| **camel.component.aws-secrets-manager.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-secrets-manager.operation** | The operation to perform. |  | SecretsManagerOperations |
| **camel.component.aws-secrets-manager.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-secrets-manager.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-secrets-manager.proxy-host** | To define a proxy host when instantiating the Secrets Manager client. |  | String |
| **camel.component.aws-secrets-manager.proxy-port** | To define a proxy port when instantiating the Secrets Manager client. |  | Integer |
| **camel.component.aws-secrets-manager.proxy-protocol** | To define a proxy protocol when instantiating the Secrets Manager client. |  | Protocol |
| **camel.component.aws-secrets-manager.region** | The region in which Secrets Manager client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-secrets-manager.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-secrets-manager.secrets-manager-client** | To use a existing configured AWS Secrets Manager as client. The option is a software.amazon.awssdk.services.secretsmanager.SecretsManagerClient type. |  | SecretsManagerClient |
| **camel.component.aws-secrets-manager.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-secrets-manager.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-secrets-manager.use-default-credentials-provider** | Set whether the Translate client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |