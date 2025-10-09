# Azure Functions

**Since Camel 4.19**

**Only producer is supported**

The azure-functions component enables integration with [Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/). Azure Functions is a serverless compute service that enables you to run code on-demand without having to explicitly provision or manage infrastructure.

This component supports:

-   Invoking HTTP-triggered Azure Functions
    
-   Managing Azure Function Apps (list, create, delete, start, stop, restart)
    
-   Managing function app configuration and tags
    

Prerequisites

You must have a valid Azure subscription. More information is available at [Azure Documentation Portal](https://docs.microsoft.com/azure/).

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-functions</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

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

The Azure Functions component supports 21 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The component configuration. |  | FunctionsConfiguration |
| **connectionTimeout** (producer) | Connection timeout in milliseconds for HTTP invocation. | 30000 | int |
| **httpMethod** (producer) | HTTP method for function invocation (GET, POST, PUT, DELETE, etc.). | POST | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **location** (producer) | Azure region for creating function app (e.g., eastus, westeurope). |  | String |
| **operation** (producer) | 
The operation to be performed.

Enum values:

-   invokeFunction
    
-   listFunctionApps
    
-   getFunctionApp
    
-   createFunctionApp
    
-   deleteFunctionApp
    
-   startFunctionApp
    
-   stopFunctionApp
    
-   restartFunctionApp
    
-   listFunctions
    
-   getFunction
    
-   getFunctionKeys
    
-   getFunctionAppConfiguration
    
-   updateFunctionAppConfiguration
    
-   listTags
    
-   tagResource
    
-   untagResource
    





 | invokeFunction | FunctionsOperations |
| **readTimeout** (producer) | Read timeout in milliseconds for HTTP invocation. | 60000 | int |
| **runtime** (producer) | Runtime stack (java, node, python, dotnet). |  | String |
| **runtimeVersion** (producer) | Runtime version. |  | String |
| **storageAccountConnectionString** (producer) | Storage account connection string for function app. |  | String |
| **appServiceManager** (advanced) | **Autowired** An AppServiceManager instance for management operations. |  | AppServiceManager |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientId** (security) | Azure AD Client ID for service principal authentication. |  | String |
| **clientSecret** (security) | Azure AD Client Secret for service principal authentication. |  | String |
| **credentialType** (security) | 

Determines the credential strategy to adopt.

Enum values:

-   AZURE\_IDENTITY
    
-   FUNCTION\_KEY
    
-   TOKEN\_CREDENTIAL
    





 | AZURE\_IDENTITY | CredentialType |
| **functionKey** (security) | The function key for direct HTTP invocation. |  | String |
| **hostKey** (security) | The host key for the function app (used if function key is not provided). |  | String |
| **resourceGroup** (security) | The resource group name containing the function app (required for management operations). |  | String |
| **subscriptionId** (security) | The Azure subscription ID (required for management operations). |  | String |
| **tenantId** (security) | Azure AD Tenant ID. |  | String |
| **tokenCredential** (security) | **Autowired** A TokenCredential instance for Azure AD authentication. |  | TokenCredential |

## Endpoint Options

The Azure Functions endpoint is configured using URI syntax:

azure-functions:functionApp/functionName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **functionApp** (producer) | **Required** The Azure Function App name. |  | String |
| **functionName** (producer) | The function name within the app (required for invokeFunction operation). |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (producer) | Connection timeout in milliseconds for HTTP invocation. | 30000 | int |
| **httpMethod** (producer) | HTTP method for function invocation (GET, POST, PUT, DELETE, etc.). | POST | String |
| **location** (producer) | Azure region for creating function app (e.g., eastus, westeurope). |  | String |
| **operation** (producer) | 
The operation to be performed.

Enum values:

-   invokeFunction
    
-   listFunctionApps
    
-   getFunctionApp
    
-   createFunctionApp
    
-   deleteFunctionApp
    
-   startFunctionApp
    
-   stopFunctionApp
    
-   restartFunctionApp
    
-   listFunctions
    
-   getFunction
    
-   getFunctionKeys
    
-   getFunctionAppConfiguration
    
-   updateFunctionAppConfiguration
    
-   listTags
    
-   tagResource
    
-   untagResource
    





 | invokeFunction | FunctionsOperations |
| **readTimeout** (producer) | Read timeout in milliseconds for HTTP invocation. | 60000 | int |
| **runtime** (producer) | Runtime stack (java, node, python, dotnet). |  | String |
| **runtimeVersion** (producer) | Runtime version. |  | String |
| **storageAccountConnectionString** (producer) | Storage account connection string for function app. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **appServiceManager** (advanced) | **Autowired** An AppServiceManager instance for management operations. |  | AppServiceManager |
| **clientId** (security) | Azure AD Client ID for service principal authentication. |  | String |
| **clientSecret** (security) | Azure AD Client Secret for service principal authentication. |  | String |
| **credentialType** (security) | 

Determines the credential strategy to adopt.

Enum values:

-   AZURE\_IDENTITY
    
-   FUNCTION\_KEY
    
-   TOKEN\_CREDENTIAL
    





 | AZURE\_IDENTITY | CredentialType |
| **functionKey** (security) | The function key for direct HTTP invocation. |  | String |
| **hostKey** (security) | The host key for the function app (used if function key is not provided). |  | String |
| **resourceGroup** (security) | The resource group name containing the function app (required for management operations). |  | String |
| **subscriptionId** (security) | The Azure subscription ID (required for management operations). |  | String |
| **tenantId** (security) | Azure AD Tenant ID. |  | String |
| **tokenCredential** (security) | **Autowired** A TokenCredential instance for Azure AD authentication. |  | TokenCredential |

## Message Headers

The Azure Functions component supports 18 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureFunctionsOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#OPERATION) | 
The operation to perform. Overrides the operation in the endpoint.

Enum values:

-   invokeFunction
    
-   listFunctionApps
    
-   getFunctionApp
    
-   createFunctionApp
    
-   deleteFunctionApp
    
-   startFunctionApp
    
-   stopFunctionApp
    
-   restartFunctionApp
    
-   listFunctions
    
-   getFunction
    
-   getFunctionKeys
    
-   getFunctionAppConfiguration
    
-   updateFunctionAppConfiguration
    
-   listTags
    
-   tagResource
    
-   untagResource
    





 |  | FunctionsOperations |
| **CamelAzureFunctionsFunctionApp** (producer) Constant: [`FUNCTION_APP`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#FUNCTION_APP) | The function app name. |  | String |
| **CamelAzureFunctionsFunctionName** (producer) Constant: [`FUNCTION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#FUNCTION_NAME) | The function name within the app. |  | String |
| **CamelAzureFunctionsResourceGroup** (producer) Constant: [`RESOURCE_GROUP`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#RESOURCE_GROUP) | The resource group name. |  | String |
| **CamelAzureFunctionsHttpMethod** (producer) Constant: [`HTTP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#HTTP_METHOD) | The HTTP method for function invocation (GET, POST, PUT, DELETE, etc.). |  | String |
| **CamelAzureFunctionsHttpHeaders** (producer) Constant: [`HTTP_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#HTTP_HEADERS) | Custom HTTP headers for function invocation. |  | Map |
| **CamelAzureFunctionsStatusCode** (producer) Constant: [`STATUS_CODE`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#STATUS_CODE) | The HTTP status code from the response. |  | Integer |
| **CamelAzureFunctionsResponseHeaders** (producer) Constant: [`RESPONSE_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#RESPONSE_HEADERS) | The response headers from function invocation. |  | Map |
| **CamelAzureFunctionsFunctionAppState** (producer) Constant: [`FUNCTION_APP_STATE`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#FUNCTION_APP_STATE) | The function app state (Running, Stopped, etc.). |  | String |
| **CamelAzureFunctionsResourceId** (producer) Constant: [`RESOURCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#RESOURCE_ID) | The function app resource ID. |  | String |
| **CamelAzureFunctionsDefaultHostname** (producer) Constant: [`DEFAULT_HOSTNAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#DEFAULT_HOSTNAME) | The default hostname of the function app. |  | String |
| **CamelAzureFunctionsAppSettings** (producer) Constant: [`APP_SETTINGS`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#APP_SETTINGS) | App settings to update (for updateFunctionAppConfiguration). |  | Map |
| **CamelAzureFunctionsResourceTags** (producer) Constant: [`RESOURCE_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#RESOURCE_TAGS) | Tags to apply to the resource (for tagResource). |  | Map |
| **CamelAzureFunctionsTagKeys** (producer) Constant: [`TAG_KEYS`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#TAG_KEYS) | Tag keys to remove from the resource (for untagResource). |  | List |
| **CamelAzureFunctionsLocation** (producer) Constant: [`LOCATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#LOCATION) | Azure region for creating the function app (e.g., eastus, westeurope). |  | String |
| **CamelAzureFunctionsRuntime** (producer) Constant: [`RUNTIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#RUNTIME) | Runtime stack for the function app (java, node, python, dotnet). |  | String |
| **CamelAzureFunctionsRuntimeVersion** (producer) Constant: [`RUNTIME_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#RUNTIME_VERSION) | Runtime version for the function app. |  | String |
| **CamelAzureFunctionsStorageConnectionString** (producer) Constant: [`STORAGE_CONNECTION_STRING`](https://javadoc.io/doc/org.apache.camel/camel-azure-functions/latest/org/apache/camel/component/azure/functions/FunctionsConstants.html#STORAGE_CONNECTION_STRING) | Storage account connection string for the function app. |  | String |

## URI Format

```none
azure-functions:functionApp[/functionName]
```

Where:

-   `functionApp` is the name of your Azure Function App
    
-   `functionName` is the name of the function within the app (required for `invokeFunction` operation)
    

## Usage

### Authentication Information

There are three different Credential Types: `AZURE_IDENTITY`, `FUNCTION_KEY`, and `TOKEN_CREDENTIAL`.

**AZURE\_IDENTITY** (default):

This will use `com.azure.identity.DefaultAzureCredentialBuilder().build()` instance. This follows the Default Azure Credential Chain which tries multiple authentication methods:

-   Environment variables
    
-   Managed Identity
    
-   Azure CLI
    
-   Visual Studio Code
    
-   IntelliJ IDEA
    

See the documentation [here about Azure AD authentication](https://docs.microsoft.com/en-us/azure/active-directory/authentication/overview-authentication).

**FUNCTION\_KEY**:

For invoking HTTP-triggered functions, you can use function keys or host keys:

```java
from("direct:invoke")
    .to("azure-functions:myFunctionApp/myFunction?credentialType=FUNCTION_KEY&functionKey=your-function-key");
```

**TOKEN\_CREDENTIAL**:

Provide an implementation of `com.azure.core.credential.TokenCredential` into the Camel Registry:

```java
from("direct:invoke")
    .to("azure-functions:myFunctionApp/myFunction?credentialType=TOKEN_CREDENTIAL&tokenCredential=#myCredential");
```

### Service Principal Authentication

For service principal authentication, provide the client credentials:

```java
from("direct:manage")
    .to("azure-functions:myFunctionApp?operation=listFunctionApps"
        + "&subscriptionId=your-subscription-id"
        + "&resourceGroup=your-resource-group"
        + "&clientId=your-client-id"
        + "&clientSecret=your-client-secret"
        + "&tenantId=your-tenant-id");
```

## Operations

The component supports the following operations:

### Function Invocation

 
| Operation | Description |
| --- | --- |
| `invokeFunction` | Invokes an HTTP-triggered Azure Function (default operation) |

### Function App Management

 
| Operation | Description |
| --- | --- |
| `listFunctionApps` | List all function apps in the subscription or resource group |
| `getFunctionApp` | Get details of a specific function app |
| `createFunctionApp` | Create a new function app |
| `deleteFunctionApp` | Delete a function app |
| `startFunctionApp` | Start a stopped function app |
| `stopFunctionApp` | Stop a running function app |
| `restartFunctionApp` | Restart a function app |

### Function Operations

 
| Operation | Description |
| --- | --- |
| `listFunctions` | List all functions within a function app |
| `getFunction` | Get details of a specific function |
| `getFunctionKeys` | Get the master key for the function app |

### Configuration Operations

 
| Operation | Description |
| --- | --- |
| `getFunctionAppConfiguration` | Get app settings/configuration |
| `updateFunctionAppConfiguration` | Update app settings |

### Tag Operations

 
| Operation | Description |
| --- | --- |
| `listTags` | List tags on the function app resource |
| `tagResource` | Add tags to the function app |
| `untagResource` | Remove tags from the function app |

## Examples

### Invoke a Function

```java
from("direct:invoke")
    .setBody(constant("{\"name\": \"World\"}"))
    .to("azure-functions:myFunctionApp/HelloFunction?functionKey=your-key")
    .log("Response: ${body}");
```

### List Function Apps

```java
from("direct:list")
    .to("azure-functions:myFunctionApp?operation=listFunctionApps"
        + "&subscriptionId=xxx&resourceGroup=myResourceGroup")
    .log("Function Apps: ${body}");
```

### Stop a Function App

```java
from("direct:stop")
    .to("azure-functions:myFunctionApp?operation=stopFunctionApp"
        + "&subscriptionId=xxx&resourceGroup=myResourceGroup")
    .log("Function App stopped");
```

### Update Configuration

```java
from("direct:updateConfig")
    .setHeader("CamelAzureFunctionsAppSettings", constant(Map.of("MY_SETTING", "value")))
    .to("azure-functions:myFunctionApp?operation=updateFunctionAppConfiguration"
        + "&subscriptionId=xxx&resourceGroup=myResourceGroup")
    .log("Configuration updated: ${body}");
```

### Create a Function App

```java
from("direct:create")
    .to("azure-functions:newFunctionApp?operation=createFunctionApp"
        + "&subscriptionId=xxx"
        + "&resourceGroup=myResourceGroup"
        + "&location=eastus"
        + "&runtime=java"
        + "&storageAccountConnectionString=DefaultEndpointsProtocol=https;...")
    .log("Created function app: ${header.CamelAzureFunctionsResourceId}");
```

## Spring Boot Auto-Configuration

When using azure-functions with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-azure-functions-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.azure-functions.app-service-manager** | An AppServiceManager instance for management operations. The option is a com.azure.resourcemanager.appservice.AppServiceManager type. |  | AppServiceManager |
| **camel.component.azure-functions.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.azure-functions.client-id** | Azure AD Client ID for service principal authentication. |  | String |
| **camel.component.azure-functions.client-secret** | Azure AD Client Secret for service principal authentication. |  | String |
| **camel.component.azure-functions.configuration** | The component configuration. The option is a org.apache.camel.component.azure.functions.FunctionsConfiguration type. |  | FunctionsConfiguration |
| **camel.component.azure-functions.connection-timeout** | Connection timeout in milliseconds for HTTP invocation. | 30000 | Integer |
| **camel.component.azure-functions.credential-type** | Determines the credential strategy to adopt. | azure-identity | CredentialType |
| **camel.component.azure-functions.enabled** | Whether to enable auto configuration of the azure-functions component. This is enabled by default. |  | Boolean |
| **camel.component.azure-functions.function-key** | The function key for direct HTTP invocation. |  | String |
| **camel.component.azure-functions.host-key** | The host key for the function app (used if function key is not provided). |  | String |
| **camel.component.azure-functions.http-method** | HTTP method for function invocation (GET, POST, PUT, DELETE, etc.). | POST | String |
| **camel.component.azure-functions.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.azure-functions.location** | Azure region for creating function app (e.g., eastus, westeurope). |  | String |
| **camel.component.azure-functions.operation** | The operation to be performed. | invokefunction | FunctionsOperations |
| **camel.component.azure-functions.read-timeout** | Read timeout in milliseconds for HTTP invocation. | 60000 | Integer |
| **camel.component.azure-functions.resource-group** | The resource group name containing the function app (required for management operations). |  | String |
| **camel.component.azure-functions.runtime** | Runtime stack (java, node, python, dotnet). |  | String |
| **camel.component.azure-functions.runtime-version** | Runtime version. |  | String |
| **camel.component.azure-functions.storage-account-connection-string** | Storage account connection string for function app. |  | String |
| **camel.component.azure-functions.subscription-id** | The Azure subscription ID (required for management operations). |  | String |
| **camel.component.azure-functions.tenant-id** | Azure AD Tenant ID. |  | String |
| **camel.component.azure-functions.token-credential** | A TokenCredential instance for Azure AD authentication. The option is a com.azure.core.credential.TokenCredential type. |  | TokenCredential |