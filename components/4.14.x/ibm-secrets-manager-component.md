# IBM Secrets Manager

**Since Camel 4.11**

**Only producer is supported**

The ibm-secrets-manager component that integrates [IBM Cloud Secrets Manager](https://www.ibm.com/products/secrets-manager).

## URI Format

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ibm-secrets-manager</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The IBM Secrets Manager component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The IBM Secrets Manager endpoint is configured using URI syntax:

ibm-secrets-manager:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
Operation to be performed.

Enum values:

-   createArbitrarySecret
    
-   createKVSecret
    
-   getSecret
    
-   deleteSecret
    
-   listSecrets
    





 |  | IBMSecretsManagerOperation |
| **serviceUrl** (producer) | Service URL for IBM Secrets Manager. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **token** (security) | IBM Cloud API Token for IBM Secrets Manager. |  | String |

## Message Headers

The IBM Secrets Manager component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIbmSecretsManagerProducerOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-secrets-manager/latest/org/apache/camel/component/ibm/secrets/manager/IBMSecretsManagerConstants.html#OPERATION) | Overrides the desired operation to be used in the producer. |  | String |
| **CamelIbmSecretsManagerSecretName** (producer) Constant: [`SECRET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-secrets-manager/latest/org/apache/camel/component/ibm/secrets/manager/IBMSecretsManagerConstants.html#SECRET_NAME) | Set the desired secret path as header. |  | String |
| **CamelIbmSecretsManagerSecretVersion** (producer) Constant: [`SECRET_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-secrets-manager/latest/org/apache/camel/component/ibm/secrets/manager/IBMSecretsManagerConstants.html#SECRET_VERSION) | Set the desired secret version as header. |  | String |
| **CamelIbmSecretsManagerSecretId** (producer) Constant: [`SECRET_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-secrets-manager/latest/org/apache/camel/component/ibm/secrets/manager/IBMSecretsManagerConstants.html#SECRET_ID) | Set the desired secret version as header. |  | String |

## Functionalities

The component supports operations at the producer level. Specifically, it provides the following functionalities:

-   `createArbitrarySecret`
    
-   `createKVSecret`
    
-   `getSecret`
    
-   `deleteSecret`
    

## Examples

### Using IBM Secrets Manager Vault Property Function

To use this function, you’ll need to provide credentials for IBM Secrets Manager vault as environment variables:

```bash
export CAMEL_VAULT_IBM_TOKEN=token
export CAMEL_VAULT_IBM_SERVICE_URL=serviceUrl
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.ibm.token = token
camel.vault.ibm.serviceUrl = serviceUrl
```

> **Note**
> if you’re running the application on a Kubernetes based cloud platform, you can initialize the environment variables from a Secret or Configmap to enhance security. You can also enhance security by [setting a Secret property placeholder](../../manual/using-propertyplaceholder.html#_resolving_property_placeholders_on_cloud) which will be initialized at application runtime only.

> **Note**
> `camel.vault.ibm` configuration only applies to the IBM Secrets Manager Vault properties function (E.g when resolving properties). When using the `operation` option to create, get, list secrets etc., you should provide the `token` and `serviceUrl` options.

At this point, you’ll be able to reference a property in the following way:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{ibm:default:route}}"/>
    </route>
</camelContext>
```

Where route will be the name of the secret stored in the IBM Secrets Manager Vault instance, in the 'default' secret group.

You could specify a default value in case the secret is not present on IBM Secrets Manager Vault instance:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{ibm:default:route:default}}"/>
    </route>
</camelContext>
```

In this case, if the secret doesn’t exist in the 'default' secret group, the property will fall back to "default" as value.

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

You’re able to do get single secret value in your route, in the 'default' secret group, like for example:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{ibm:default:database#username}}"/>
    </route>
</camelContext>
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on IBM Secrets Manager Vault instance, in the 'secret' engine:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{ibm:default:database#username:admin}}"/>
    </route>
</camelContext>
```

In this case, if the secret doesn’t exist or the secret exists (in the 'default' secret group) but the username field is not part of the secret, the property will fall back to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approaches, with field/default value specified or only with secret:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{ibm:default:route@2}}"/>
    </route>
</camelContext>
```

This approach will return the RAW route secret with version '2', in the 'default' secret group.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{ibm:default:route:default@2}}"/>
    </route>
</camelContext>
```

This approach will return the route secret value with version '2' or default value in case the secret doesn’t exist or the version doesn’t exist (in the 'default' secret group).

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{ibm:default:database#username:admin@2}}"/>
    </route>
</camelContext>
```

This approach will return the username field of the database secret with version '2' or admin in case the secret doesn’t exist or the version doesn’t exist (in the 'default' secret group).

The only requirement is adding the camel-ibm-secrets-manager jar to your Camel application.

### Automatic Camel context reloading on Secret Refresh

Being able to reload Camel context on a Secret Refresh could be done by specifying the IBM Event Streams credentials combined with the IBM Secrets Manager one (the same used for IBM Secrets Manager Property Function).

With Environment variables:

```bash
export CAMEL_VAULT_IBM_TOKEN=token
export CAMEL_VAULT_IBM_SERVICE_URL=serviceUrl
export CAMEL_VAULT_IBM_EVENTSTREAM_BOOTSTRAP_SERVERS=bootstrapServers
export CAMEL_VAULT_IBM_EVENTSTREAM_TOPIC=topic
export CAMEL_VAULT_IBM_EVENTSTREAM_USERNAME=token
export CAMEL_VAULT_IBM_EVENTSTREAM_PASSWORD=password
export CAMEL_VAULT_IBM_EVENTSTREAM_CONSUMER_GROUP_ID=groupId
export CAMEL_VAULT_IBM_EVENTSTREAM_CONSUMER_POLL_TIMEOUT=3000
```

or as plain Camel main properties:

```properties
camel.vault.ibm.token = token
camel.vault.ibm.serviceUrl = serviceUrl
camel.vault.ibm.eventStreamBootstrapServers = bootstrapServers
camel.vault.ibm.eventStreamTopic = topic
camel.vault.ibm.eventStreamUsername = token
camel.vault.ibm.eventStreamPassword = password
camel.vault.ibm.eventStreamGroupId = groupId
camel.vault.ibm.eventStreamConsumerPollTimeout=3000
```

To enable the automatic refresh, you’ll need additional properties to set:

```properties
camel.vault.ibm.refreshEnabled=true
camel.vault.ibm.secrets=Secret
camel.main.context-reload-enabled = true
```

where `camel.vault.ibm.refreshEnabled` will enable the automatic context reload and `camel.vault.ibm.secrets` is a regex representing the secrets we want to track for updates.

where `camel.vault.ibm.eventStreamBootstrapServers` is the comma-separated list of Bootstrap Servers for IBM Event Stream, `camel.vault.ibm.eventStreamTopic`, `camel.vault.ibm.eventStreamUsername`, `camel.vault.ibm.eventStreamPassword`, `camel.vault.ibm.eventStreamGroupId` and `camel.vault.ibm.eventStreamConsumerPollTimeout` are the IBM Event Stream parameters for connecting and consuming events related to Secrets.

Note that `camel.vault.ibm.secrets` is not mandatory: if not specified the task responsible for checking updates events will take into accounts or the properties with an `ibm:` prefix.

## Spring Boot Auto-Configuration

When using ibm-secrets-manager with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ibm-secrets-manager-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.ibm-secrets-manager.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ibm-secrets-manager.enabled** | Whether to enable auto configuration of the ibm-secrets-manager component. This is enabled by default. |  | Boolean |
| **camel.component.ibm-secrets-manager.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |