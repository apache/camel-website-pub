# Azure Key Vault

**Since Camel 3.17**

**Only producer is supported**

The azure-key-vault component that integrates [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault/).

Prerequisites

You must have a valid Windows Azure Key Vault account. More information is available at [Azure Documentation Portal](https://docs.microsoft.com/azure/).

## URI Format

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-key-vault</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The Azure Key Vault component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Azure Key Vault endpoint is configured using URI syntax:

azure-key-vault:vaultName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **vaultName** (producer) | Vault Name to be used. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
Operation to be performed.

Enum values:

-   createSecret
    
-   getSecret
    
-   deleteSecret
    
-   purgeDeletedSecret
    





 |  | KeyVaultOperation |
| **secretClient** (producer) | **Autowired** Instance of Secret client. |  | SecretClient |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **clientId** (security) | Client Id to be used. |  | String |
| **clientSecret** (security) | Client Secret to be used. |  | String |
| **tenantId** (security) | Tenant Id to be used. |  | String |

## Usage

### Using Azure Key Vault Property Function

To use this function you’ll need to provide credentials to Azure Key Vault Service as environment variables:

```bash
export $CAMEL_VAULT_AZURE_TENANT_ID=tenantId
export $CAMEL_VAULT_AZURE_CLIENT_ID=clientId
export $CAMEL_VAULT_AZURE_CLIENT_SECRET=clientSecret
export $CAMEL_VAULT_AZURE_VAULT_NAME=vaultName
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.azure.tenantId = accessKey
camel.vault.azure.clientId = clientId
camel.vault.azure.clientSecret = clientSecret
camel.vault.azure.vaultName = vaultName
```

At this point you’ll be able to reference a property in the following way:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{azure:route}}"/>
    </route>
</camelContext>
```

Where route will be the name of the secret stored in the Azure Key Vault Service.

You could specify a default value in case the secret is not present on Azure Key Vault Service:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{azure:route:default}}"/>
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
        <log message="Username is {{azure:database/username}}"/>
    </route>
</camelContext>
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on Azure Key Vault:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{azure:database/username:admin}}"/>
    </route>
</camelContext>
```

In this case if the secret doesn’t exist or the secret exists, but the username field is not part of the secret, the property will fallback to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approach, with field/default value specified or only with secret:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{azure:route@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

This approach will return the RAW route secret with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451'.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{azure:route:default@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

This approach will return the route secret value with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451' or default value in case the secret doesn’t exist or the version doesn’t exist.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{azure:database/username:admin@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

This approach will return the username field of the database secret with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451' or admin in case the secret doesn’t exist or the version doesn’t exist.

For the moment we are not considering the rotation function, if any will be applied, but it is in the work to be done.

The only requirement is adding the camel-azure-key-vault jar to your Camel application.

### Automatic Camel context reloading on Secret Refresh

Being able to reload Camel context on a Secret Refresh, could be done by specifying the usual credentials (the same used for Azure Key Vault Property Function).

With Environment variables:

```bash
export $CAMEL_VAULT_AZURE_TENANT_ID=tenantId
export $CAMEL_VAULT_AZURE_CLIENT_ID=clientId
export $CAMEL_VAULT_AZURE_CLIENT_SECRET=clientSecret
export $CAMEL_VAULT_AZURE_VAULT_NAME=vaultName
```

or as plain Camel main properties:

```properties
camel.vault.azure.tenantId = accessKey
camel.vault.azure.clientId = clientId
camel.vault.azure.clientSecret = clientSecret
camel.vault.azure.vaultName = vaultName
```

To enable the automatic refresh you’ll need additional properties to set:

```properties
camel.vault.azure.refreshEnabled=true
camel.vault.azure.refreshPeriod=60000
camel.vault.azure.secrets=Secret
camel.vault.azure.eventhubConnectionString=eventhub_conn_string
camel.vault.azure.blobAccountName=blob_account_name
camel.vault.azure.blobContainerName=blob_container_name
camel.vault.azure.blobAccessKey=blob_access_key
camel.main.context-reload-enabled = true
```

where `camel.vault.azure.refreshEnabled` will enable the automatic context reload, `camel.vault.azure.refreshPeriod` is the interval of time between two different checks for update events and `camel.vault.azure.secrets` is a regex representing the secrets we want to track for updates.

where `camel.vault.azure.eventhubConnectionString` is the eventhub connection string to get notification from, `camel.vault.azure.blobAccountName`, `camel.vault.azure.blobContainerName` and `camel.vault.azure.blobAccessKey` are the Azure Storage Blob parameters for the checkpoint store needed by Azure Eventhub.

Note that `camel.vault.azure.secrets` is not mandatory: if not specified the task responsible for checking updates events will take into accounts or the properties with an `azure:` prefix.

The only requirement is adding the camel-azure-key-vault jar to your Camel application.

## Message Headers

The Azure Key Vault component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureKeyVaultProducerOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-key-vault/latest/org/apache/camel/component/azure/key/vault/KeyVaultConstants.html#OPERATION) | Overrides the desired operation to be used in the producer. |  | KeyVaultOperationDefinition |
| **CamelAzureKeyVaultSecretName** (producer) Constant: [`SECRET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-key-vault/latest/org/apache/camel/component/azure/key/vault/KeyVaultConstants.html#SECRET_NAME) | The secret name to be used in Key Vault. |  | String |

### Azure Key Vault Producer operations

Azure Key Vault component provides the following operation on the producer side:

-   createSecret
    
-   getSecret
    
-   deleteSecret
    
-   purgeDeletedSecret
    

## Examples

### Producer Examples

-   createSecret: this operation will create a secret in Azure Key Vault
    

```java
from("direct:createSecret")
    .setHeader(KeyVaultConstants.SECRET_NAME, "Test")
    .setBody(constant("Test"))
    .to("azure-key-vault://test123?clientId=RAW({{clientId}})&clientSecret=RAW({{clientSecret}})&tenantId=RAW({{tenantId}})")
```

-   getSecret: this operation will get a secret from Azure Key Vault
    

```java
from("direct:getSecret")
    .setHeader(KeyVaultConstants.SECRET_NAME, "Test")
    .to("azure-key-vault://test123?clientId=RAW({{clientId}})&clientSecret=RAW({{clientSecret}})&tenantId=RAW({{tenantId}})&operation=getSecret")
```

-   deleteSecret: this operation will delete a Secret from Azure Key Vault
    

```java
from("direct:deleteSecret")
    .setHeader(KeyVaultConstants.SECRET_NAME, "Test")
    .to("azure-key-vault://test123?clientId=RAW({{clientId}})&clientSecret=RAW({{clientSecret}})&tenantId=RAW({{tenantId}})&operation=deleteSecret")
```

-   purgeDeletedSecret: this operation will purge a deleted Secret from Azure Key Vault
    

```java
from("direct:purgeDeletedSecret")
    .setHeader(KeyVaultConstants.SECRET_NAME, "Test")
    .to("azure-key-vault://test123?clientId=RAW({{clientId}})&clientSecret=RAW({{clientSecret}})&tenantId=RAW({{tenantId}})&operation=purgeDeletedSecret")
```

## Spring Boot Auto-Configuration

When using azure-key-vault with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-azure-key-vault-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.azure-key-vault.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.azure-key-vault.enabled** | Whether to enable auto configuration of the azure-key-vault component. This is enabled by default. |  | Boolean |
| **camel.component.azure-key-vault.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |