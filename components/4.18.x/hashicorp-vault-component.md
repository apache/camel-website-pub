# Hashicorp Vault

**Since Camel 3.18**

**Only producer is supported**

The hashicorp-vault component that integrates [Hashicorp Vault](https://www.vaultproject.io/).

## URI Format

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-hashicorp-vault</artifactId>
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

The Hashicorp Vault component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Hashicorp Vault endpoint is configured using URI syntax:

hashicorp-vault:secretsEngine

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **secretsEngine** (producer) | Vault Name to be used. |  | String |

### Query Parameters (10 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cloud** (producer) | Determine if the Hashicorp Vault is deployed on Hashicorp Cloud or not. | false | boolean |
| **host** (producer) | Hashicorp Vault instance host to be used. |  | String |
| **namespace** (producer) | If the Hashicorp Vault instance is deployed on Hashicorp Cloud, this field will determine the namespace. |  | String |
| **operation** (producer) | 
Operation to be performed.

Enum values:

-   createSecret
    
-   getSecret
    
-   deleteSecret
    
-   listSecrets
    





 |  | HashicorpVaultOperation |
| **port** (producer) | Hashicorp Vault instance port to be used. | 8200 | String |
| **scheme** (producer) | Hashicorp Vault instance scheme to be used. | https | String |
| **secretPath** (producer) | Hashicorp Vault instance secret Path to be used. |  | String |
| **vaultTemplate** (producer) | **Autowired** Instance of Vault template. |  | VaultTemplate |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **token** (security) | Token to be used. |  | String |

## Message Headers

The Hashicorp Vault component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHashicorpVaultProducerOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-hashicorp-vault/latest/org/apache/camel/component/hashicorp/vault/HashicorpVaultConstants.html#OPERATION) | Overrides the desired operation to be used in the producer. |  | String |
| **CamelHashicorpVaultSecretPath** (producer) Constant: [`SECRET_PATH`](https://javadoc.io/doc/org.apache.camel/camel-hashicorp-vault/latest/org/apache/camel/component/hashicorp/vault/HashicorpVaultConstants.html#SECRET_PATH) | Set the desired secret path as header. |  | String |
| **CamelHashicorpVaultSecretVersion** (producer) Constant: [`SECRET_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-hashicorp-vault/latest/org/apache/camel/component/hashicorp/vault/HashicorpVaultConstants.html#SECRET_VERSION) | Set the desired secret version as header. |  | String |

## Authentication and Hashicorp vault on-premise vs Hashicorp Cloud

The component supports operations at the producer level. Specifically, it provides the following functionalities:

-   `createSecret`
    
-   `getSecret`
    
-   `deleteSecret`
    
-   `listSecrets`
    

The component can interact with HashiCorp Vault, which may be deployed either as an on-premise/local instance or as a HashiCorp Vault Cloud instance (Enterprise version).

### Configuration for HashiCorp Vault Cloud

When using a HashiCorp Vault Cloud instance, in addition to the standard parameters such as `host`, `port`, `scheme`, and `token`, you must configure the following additional parameters:

-   `cloud`:: A boolean flag that must be explicitly set to `true` to indicate that the HashiCorp Vault instance is hosted in the cloud.
    
-   `namespace`:: The namespace of your secrets engine.
    

## Examples

### Using Hashicorp Vault Property Function

To use this function, you’ll need to provide credentials for Hashicorp vault as environment variables:

```bash
export CAMEL_VAULT_HASHICORP_TOKEN=token
export CAMEL_VAULT_HASHICORP_HOST=host
export CAMEL_VAULT_HASHICORP_PORT=port
export CAMEL_VAULT_HASHICORP_SCHEME=http/https
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.hashicorp.token = token
camel.vault.hashicorp.host = host
camel.vault.hashicorp.port = port
camel.vault.hashicorp.scheme = scheme
```

In case the running Hashicorp Vault instance you’re pointing is running on Hashicorp Cloud, the configuration will require two additional parameters:

```bash
export CAMEL_VAULT_HASHICORP_TOKEN=token
export CAMEL_VAULT_HASHICORP_HOST=host
export CAMEL_VAULT_HASHICORP_PORT=port
export CAMEL_VAULT_HASHICORP_SCHEME=http/https
export CAMEL_HASHICORP_VAULT_CLOUD=true
export CAMEL_HASHICORP_VAULT_NAMESPACE=namespace
```

You can also set the same in the `application.properties` file such as:

```properties
camel.vault.hashicorp.token = token
camel.vault.hashicorp.host = host
camel.vault.hashicorp.port = port
camel.vault.hashicorp.scheme = scheme
camel.vault.hashicorp.cloud = true
camel.vault.hashicorp.namespace = namespace
```

This will make the Properties function works even in the Hashicorp Cloud deployment option.

> **Note**
> if you’re running the application on a Kubernetes based cloud platform, you can initialize the environment variables from a Secret or Configmap to enhance security. You can also enhance security by [setting a Secret property placeholder](../../manual/using-propertyplaceholder.html#_resolving_property_placeholders_on_cloud) which will be initialized at application runtime only.

> **Note**
> `camel.vault.hashicorp` configuration only applies to the Hashicorp Vault properties function (E.g when resolving properties). When using the `operation` option to create, get, list secrets etc., you should provide the `host`, `port`, `scheme` (if required) & `token` options.

At this point, you’ll be able to reference a property in the following way:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:secret:route}}"/>
    </route>
</camelContext>
```

Where route will be the name of the secret stored in the Hashicorp Vault instance, in the 'secret' engine.

You could specify a default value in case the secret is not present on Hashicorp Vault instance:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:secret:route:default}}"/>
    </route>
</camelContext>
```

In this case, if the secret doesn’t exist in the 'secret' engine, the property will fall back to "default" as value.

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

You’re able to do get single secret value in your route, in the 'secret' engine, like for example:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{hashicorp:secret:database#username}}"/>
    </route>
</camelContext>
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on Hashicorp Vault instance, in the 'secret' engine:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{hashicorp:secret:database#username:admin}}"/>
    </route>
</camelContext>
```

In this case, if the secret doesn’t exist or the secret exists (in the 'secret' engine) but the username field is not part of the secret, the property will fall back to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approach, with field/default value specified or only with secret:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:secret:route@2}}"/>
    </route>
</camelContext>
```

This approach will return the RAW route secret with version '2', in the 'secret' engine.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{hashicorp:route:default@2}}"/>
    </route>
</camelContext>
```

This approach will return the route secret value with version '2' or default value in case the secret doesn’t exist or the version doesn’t exist (in the 'secret' engine).

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{hashicorp:secret:database#username:admin@2}}"/>
    </route>
</camelContext>
```

This approach will return the username field of the database secret with version '2' or admin in case the secret doesn’t exist or the version doesn’t exist (in the 'secret' engine).

The only requirement is adding the camel-hashicorp-vault jar to your Camel application.

### Automatic Camel context reloading on Secret Refresh

Being able to reload Camel context on a Secret Refresh could be done by specifying the usual credentials (the same used for Hashicorp Vault Property Function).

With Environment variables:

```bash
export CAMEL_HASHICORP_VAULT_TOKEN=token
export CAMEL_HASHICORP_VAULT_HOST=host
export CAMEL_HASHICORP_VAULT_PORT=port
export CAMEL_HASHICORP_VAULT_SCHEME=http/https
```

or as plain Camel main properties:

```properties
camel.vault.hashicorp.token = token
camel.vault.hashicorp.host = host
camel.vault.hashicorp.port = port
camel.vault.hashicorp.scheme = scheme
```

To enable the automatic refresh, you’ll need additional properties to set:

```properties
camel.vault.hashicorp.refreshEnabled=true
camel.vault.hashicorp.refreshPeriod=60000
camel.vault.hashicorp.secrets=database,api-keys
camel.main.context-reload-enabled = true
```

where `camel.vault.hashicorp.refreshEnabled` will enable the automatic context reload, `camel.vault.hashicorp.refreshPeriod` is the interval of time between two different checks for update events (default 60000ms), and `camel.vault.hashicorp.secrets` is a comma-separated list of secret names (or patterns) to check for updates.

The secret names should use the following format: - `mysecret` or `path/to/secret` - tracks a secret in the default `secret` engine - `myengine:mysecret` or `myengine:path/to/secret` - tracks a secret in the `myengine` engine (use `:` to separate engine from path) - You can use patterns like `database*` to match multiple secrets

Note that `camel.vault.hashicorp.secrets` is not mandatory: if not specified the task responsible for checking updates events will take into account all the properties with a `hashicorp:` prefix.

#### How the Refresh Mechanism Works

Unlike cloud-based secret managers (AWS, GCP, Azure) that provide event-driven notifications, Hashicorp Vault does not have a native event notification system for secret changes. Therefore, this implementation uses a **polling-based approach**:

1.  **Metadata Polling**: The refresh task periodically queries the Hashicorp Vault metadata endpoint (`/v1/<engine>/metadata/<secret>`) for each tracked secret.
    
2.  **Version Tracking**: It compares the `current_version` field to detect changes.
    
3.  **Change Detection**: When a version change is detected, it triggers a Camel context reload.
    
4.  **Efficiency**: Only metadata is queried (not the full secret content), making this approach lightweight.
    

For example, if a secret named `database` is updated in Vault: - The metadata endpoint returns `"current_version": 5` - On the next check, if `current_version` changes to `6`, a reload is triggered - The refresh period (default 60 seconds) determines how quickly changes are detected

This polling approach works with all Hashicorp Vault deployments (on-premise, cloud, enterprise, and open-source) without requiring additional infrastructure.

## Spring Boot Auto-Configuration

When using hashicorp-vault with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-hashicorp-vault-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.hashicorp-vault.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hashicorp-vault.enabled** | Whether to enable auto configuration of the hashicorp-vault component. This is enabled by default. |  | Boolean |
| **camel.component.hashicorp-vault.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |

### Using Hashicorp Vault Property Function in Spring Boot for Early resolving properties

Hashicorp Vault Spring Boot component starter offers the ability to early resolve properties, so the end user could resolve properties directly in the application.properties before both Spring Boot runtime and Camel context will start.

This could be accomplished in the following way. You should specified this property in your application.properties file:

```bash
camel.component.hashicorp-vault.early-resolve-properties=true
```

This will enable the feature so you’ll be able to resolved properties, in your application.properties file, like:

```bash
foo = hashicorp:secret:database/password#string
```