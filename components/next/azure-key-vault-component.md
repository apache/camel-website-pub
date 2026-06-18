# Azure Key Vault

**Since Camel 3.17**

**Only producer is supported**

The azure-key-vault component that integrates [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault/).

Prerequisites

You must have a valid Windows Azure Key Vault account. More information is available at [Azure Documentation Portal](https://docs.microsoft.com/azure/).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-key-vault</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

```text
azure-key-vault://vaultName[?options]
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

The Azure Key Vault component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Azure Key Vault endpoint is configured using URI syntax:

azure-key-vault:vaultName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **vaultName** (producer) | Vault Name to be used. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **credentialType** (common) | 
Determines the credential strategy to adopt.

Enum values:

-   CLIENT\_SECRET
    
-   AZURE\_IDENTITY
    





 | CLIENT\_SECRET | CredentialType |
| **operation** (producer) | 

Operation to be performed.

Enum values:

-   createSecret
    
-   getSecret
    
-   updateSecretProperties
    
-   deleteSecret
    
-   purgeDeletedSecret
    





 |  | KeyVaultOperation |
| **secretClient** (producer) | **Autowired** Instance of Secret client. |  | SecretClient |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **clientId** (security) | Client Id to be used. |  | String |
| **clientSecret** (security) | Client Secret to be used. |  | String |
| **tenantId** (security) | Tenant Id to be used. |  | String |

## Message Headers

The Azure Key Vault component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureKeyVaultProducerOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-key-vault/latest/org/apache/camel/component/azure/key/vault/KeyVaultConstants.html#OPERATION) | Overrides the desired operation to be used in the producer. |  | KeyVaultOperationDefinition |
| **CamelAzureKeyVaultSecretName** (producer) Constant: [`SECRET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-key-vault/latest/org/apache/camel/component/azure/key/vault/KeyVaultConstants.html#SECRET_NAME) | The secret name to be used in Key Vault. |  | String |
| **CamelAzureKeyVaultSecretProperties** (producer) Constant: [`SECRET_PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-azure-key-vault/latest/org/apache/camel/component/azure/key/vault/KeyVaultConstants.html#SECRET_PROPERTIES) | The secret properties to be used in Key Vault for updating a secret. |  | String |

## Usage

### Using Azure Key Vault Property Function

To use this function, you’ll need to provide credentials to Azure Key Vault Service as environment variables:

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

> **Note**
> if you’re running the application on a Kubernetes based cloud platform, you can initialize the environment variables from a Secret or Configmap to enhance security. You can also enhance security by [setting a Secret property placeholder](../../manual/using-propertyplaceholder.html#_resolving_property_placeholders_on_cloud) which will be initialized at application runtime only.

Or you can enable the usage of Azure Identity in the following way:

```bash
export $CAMEL_VAULT_AZURE_IDENTITY_ENABLED=true
export $CAMEL_VAULT_AZURE_VAULT_NAME=vaultName
```

You can also enable the usage of Azure Identity in the `application.properties` file such as:

```properties
camel.vault.azure.azureIdentityEnabled = true
camel.vault.azure.vaultName = vaultName
```

> **Note**
> `camel.vault.azure` configuration only applies to the Azure Key Vault properties function (E.g when resolving properties). When using the `operation` option to create, get, list secrets etc., you should provide the usual options for connecting to Azure Services.

At this point, you’ll be able to reference a property in the following way:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{azure:route}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{azure:route}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{azure:route}}"
```

Where route will be the name of the secret stored in the Azure Key Vault Service.

You could specify a default value in case the secret is not present on Azure Key Vault Service:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{azure:route:default}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{azure:route:default}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{azure:route:default}}"
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
    .log("Username is {{azure:database#username}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{azure:database#username}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{azure:database#username}}"
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on Azure Key Vault:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{azure:database#username:admin}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{azure:database#username:admin}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{azure:database#username:admin}}"
```

In this case, if the secret doesn’t exist or the secret exists, but the username field is not part of the secret, the property will fall back to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approach, with field/default value specified or only with secret:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{azure:route@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{azure:route@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{azure:route@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"
```

This approach will return the RAW route secret with the version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451'.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{azure:route:default@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{azure:route:default@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{azure:route:default@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"
```

This approach will return the route secret value with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451' or default value in case the secret doesn’t exist or the version doesn’t exist.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{azure:database#username:admin@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{azure:database#username:admin@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{azure:database#username:admin@bf9b4f4b-8e63-43fd-a73c-3e2d3748b451}}"
```

This approach will return the username field of the database secret with version 'bf9b4f4b-8e63-43fd-a73c-3e2d3748b451' or admin in case the secret doesn’t exist or the version doesn’t exist.

For the moment we are not considering the rotation function if any are applied, but it is in the work to be done.

The only requirement is adding the camel-azure-key-vault jar to your Camel application.

### Automatic Camel context reloading on Secret Refresh

Being able to reload Camel context on a Secret Refresh could be done by specifying the usual credentials (the same used for Azure Key Vault Property Function).

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

If you want to use Azure Identity with environment variables, you can do in the following way:

```bash
export $CAMEL_VAULT_AZURE_IDENTITY_ENABLED=true
export $CAMEL_VAULT_AZURE_VAULT_NAME=vaultName
```

You can also enable the usage of Azure Identity in the `application.properties` file such as:

```properties
camel.vault.azure.azureIdentityEnabled = true
camel.vault.azure.vaultName = vaultName
```

To enable the automatic refresh, you’ll need additional properties to set:

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

### Automatic Camel context reloading on Secret Refresh - Required Infrastructure’s creation

First, we need to create an application

```none
az ad app create --display-name test-app-key-vault
```

Then we need to obtain the credentials

```none
az ad app credential reset --id <appId> --append --display-name 'Description: Key Vault app client' --end-date '2024-12-31'
```

This will return a result like this

```none
{
  "appId": "appId",
  "password": "pwd",
  "tenant": "tenantId"
}
```

You should take note of the password and use it as clientSecret parameter, together with the clientId and tenantId.

Now create the key vault

```none
az keyvault create --name <vaultName> --resource-group <resourceGroup>
```

Create a service principal associated with the application Id

```none
az ad sp create --id <appId>
```

At this point we need to add a role to the application with role assignment

```none
az role assignment create --assignee <appId> --role "Key Vault Administrator" --scope /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.KeyVault/vaults/<vaultName>
```

The last step is to create a policy on what can be or cannot be done with the application. In this case, we just want to read the secret value. So This should be enough.

```none
az keyvault set-policy --name <vaultName> --spn <appId> --secret-permissions get
```

You can create a secret through Azure CLI with the following command:

```none
az keyvault secret set --name <secret_name> --vault-name <vaultName> -f <json-secret>
```

Now we need to setup the Eventhub/EventGrid notification for being informed about secrets updates.

First of all we’ll need a Blob account and Blob container, to track Eventhub consuming activities.

```none
az storage account create --name <blobAccountName> --resource-group <resourceGroup>
```

Then create a container

```none
az storage container create --account-name <blobAccountName> --name <blobContainerName>
```

Then recover the access key for this purpose

```none
az storage account keys list -g <resourceGroup> -n <blobAccountName>
```

Take note of the blob Account name, blob Container name and Blob Access Key to be used for setting up the vault.

Let’s now create the Eventhub side

Create the namespace first

```none
az eventhubs namespace create --resource-group <resourceGroup> --name <eventhub-namespace> --location westus --sku Standard --enable-auto-inflate --maximum-throughput-units 20
```

Now create the resource

```none
az eventhubs eventhub create --resource-group <resourceGroup> --namespace-name <eventhub-namespace> --name <eventhub-name> --cleanup-policy Delete --partition-count 15
```

Now we need to create a shared policy to access Event Hub.

```none
az eventhubs eventhub authorization-rule create --resource-group <resourceGroup> --namespace-name <eventhub-namespace> --eventhub-name <eventhub-name>  --name <auth_rule_name> --rights Listen Send Manage
```

Now we are ready to get the connection string

```none
az eventhubs eventhub authorization-rule keys list --resource-group <resourceGroup> --namespace-name <eventhub-namespace> --eventhub-name <eventhub-name> --name <auth_rule_name>
```

This will return the following output

```none
{
  "keyName": "<auth_rule_name>",
  "primaryConnectionString": "<primary_conn_string>",
  "primaryKey": "<primary_key>",
  "secondaryConnectionString": "<second_conn_string>",
  "secondaryKey": "<secondary_key>"
}
```

Substitute the connection string field with <primary\_conn\_string> as Event Hub connection string.

Get back to the Azure Portal, and go to Key Vault service.

Select the Key Vault just created. In the menu select "Events".

Then Select the Event Hub icon.

In the page that will open, define a name for the event subscription, for example, "keyvault-to-eh".

In the System topic name field add `keyvault-to-eh-topic` for example.

In the "Filter to Event Types" leave the default value of 9.

In the configure endpoint section for Eventhub, in the Event Hub namespace section you should notice the namespace you’ve created through the AZ CLI. Select that and in the Event Hub dropdown menu select the Event Hub you’ve created through the AZ CLI. Press confirm selection.

Leave everything as it is and press "Create".

You now have all the required parameters to set up the vault.

### Azure Key Vault Producer operations

Azure Key Vault component provides the following operation on the producer side:

-   createSecret
    
-   getSecret
    
-   deleteSecret
    
-   purgeDeletedSecret
    

## Examples

### Producer Examples

-   createSecret: this operation will create a secret in Azure Key Vault
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createSecret")
    .setHeader("CamelAzureKeyVaultSecretName", constant("Test"))
    .setBody(constant("Test"))
    .to("azure-key-vault://test123?clientId=RAW({{clientId}})&clientSecret=RAW({{clientSecret}})&tenantId=RAW({{tenantId}})");
```

```xml
<route>
  <from uri="direct:createSecret"/>
  <setHeader name="CamelAzureKeyVaultSecretName">
    <constant>Test</constant>
  </setHeader>
  <setBody>
    <constant>Test</constant>
  </setBody>
  <to uri="azure-key-vault://test123?clientId=RAW({{clientId}})&amp;clientSecret=RAW({{clientSecret}})&amp;tenantId=RAW({{tenantId}})"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createSecret
      steps:
        - setHeader:
            name: CamelAzureKeyVaultSecretName
            constant: Test
        - setBody:
            constant: Test
        - to:
            uri: azure-key-vault://test123
            parameters:
              clientId: "RAW({{clientId}})"
              clientSecret: "RAW({{clientSecret}})"
              tenantId: "RAW({{tenantId}})"
```

-   getSecret: this operation will get a secret from Azure Key Vault
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getSecret")
    .setHeader("CamelAzureKeyVaultSecretName", constant("Test"))
    .to("azure-key-vault://test123?clientId=RAW({{clientId}})&clientSecret=RAW({{clientSecret}})&tenantId=RAW({{tenantId}})&operation=getSecret");
```

```xml
<route>
  <from uri="direct:getSecret"/>
  <setHeader name="CamelAzureKeyVaultSecretName">
    <constant>Test</constant>
  </setHeader>
  <to uri="azure-key-vault://test123?clientId=RAW({{clientId}})&amp;clientSecret=RAW({{clientSecret}})&amp;tenantId=RAW({{tenantId}})&amp;operation=getSecret"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getSecret
      steps:
        - setHeader:
            name: CamelAzureKeyVaultSecretName
            constant: Test
        - to:
            uri: azure-key-vault://test123
            parameters:
              clientId: "RAW({{clientId}})"
              clientSecret: "RAW({{clientSecret}})"
              tenantId: "RAW({{tenantId}})"
              operation: getSecret
```

-   deleteSecret: this operation will delete a Secret from Azure Key Vault
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:deleteSecret")
    .setHeader("CamelAzureKeyVaultSecretName", constant("Test"))
    .to("azure-key-vault://test123?clientId=RAW({{clientId}})&clientSecret=RAW({{clientSecret}})&tenantId=RAW({{tenantId}})&operation=deleteSecret");
```

```xml
<route>
  <from uri="direct:deleteSecret"/>
  <setHeader name="CamelAzureKeyVaultSecretName">
    <constant>Test</constant>
  </setHeader>
  <to uri="azure-key-vault://test123?clientId=RAW({{clientId}})&amp;clientSecret=RAW({{clientSecret}})&amp;tenantId=RAW({{tenantId}})&amp;operation=deleteSecret"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:deleteSecret
      steps:
        - setHeader:
            name: CamelAzureKeyVaultSecretName
            constant: Test
        - to:
            uri: azure-key-vault://test123
            parameters:
              clientId: "RAW({{clientId}})"
              clientSecret: "RAW({{clientSecret}})"
              tenantId: "RAW({{tenantId}})"
              operation: deleteSecret
```

-   purgeDeletedSecret: this operation will purge a deleted Secret from Azure Key Vault
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:purgeDeletedSecret")
    .setHeader("CamelAzureKeyVaultSecretName", constant("Test"))
    .to("azure-key-vault://test123?clientId=RAW({{clientId}})&clientSecret=RAW({{clientSecret}})&tenantId=RAW({{tenantId}})&operation=purgeDeletedSecret");
```

```xml
<route>
  <from uri="direct:purgeDeletedSecret"/>
  <setHeader name="CamelAzureKeyVaultSecretName">
    <constant>Test</constant>
  </setHeader>
  <to uri="azure-key-vault://test123?clientId=RAW({{clientId}})&amp;clientSecret=RAW({{clientSecret}})&amp;tenantId=RAW({{tenantId}})&amp;operation=purgeDeletedSecret"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:purgeDeletedSecret
      steps:
        - setHeader:
            name: CamelAzureKeyVaultSecretName
            constant: Test
        - to:
            uri: azure-key-vault://test123
            parameters:
              clientId: "RAW({{clientId}})"
              clientSecret: "RAW({{clientSecret}})"
              tenantId: "RAW({{tenantId}})"
              operation: purgeDeletedSecret
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

### Using Azure Key Vault Property Function in Spring Boot for Early resolving properties

Azure Key Vault Spring Boot component starter offers the ability to early resolve properties, so the end user could resolve properties directly in the application.properties before both Spring Boot runtime and Camel context will start.

This could be done in the following way. You should specify this property in your `application.properties` file:

```bash
camel.component.azure-key-vault.early-resolve-properties=true=true
```

This will enable the feature, so you’ll be able to resolve properties, in your application.properties file, like:

```bash
foo = azure:databaseprod#password
```