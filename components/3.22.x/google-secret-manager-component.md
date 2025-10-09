# Google Secret Manager

**Since Camel 3.16**

**Only producer is supported**

The Google Secret Manager component provides access to [Google Cloud Secret Manager](https://cloud.google.com/secret-manager/)

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-secret-manager</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

## Authentication Configuration

Google Secret Manager component authentication is targeted for use with the GCP Service Accounts. For more information please refer to [Google Cloud Authentication](https://github.com/googleapis/google-cloud-java#authentication).

When you have the **service account key** you can provide authentication credentials to your application code. Google security credentials can be set through the component endpoint:

```java
String endpoint = "google-secret-manager://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json";
```

Or by setting the environment variable `GOOGLE_APPLICATION_CREDENTIALS` :

export GOOGLE\_APPLICATION\_CREDENTIALS="/home/user/Downloads/my-key.json"

## URI Format

google-secret-manager://functionName\[?options\]

You can append query options to the URI in the following format, `?options=value&option2=value&…​`

For example in order to call the function `myCamelFunction` from the project `myProject` and location `us-central1`, use the following snippet:

```java
from("google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=createSecret")
  .to("direct:test");
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

The Google Secret Manager component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Google Secret Manager endpoint is configured using URI syntax:

google-secret-manager:project

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **project** (common) | **Required** The Google Cloud Project Id name related to the Secret Manager. |  | String |

### Query Parameters (5 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceAccountKey** (common) | Service account key to authenticate an application as a service account. |  | String |
| **operation** (producer) | 
The operation to perform on the producer.

Enum values:

-   createSecret
    





 |  | GoogleSecretManagerOperations |
| **pojoRequest** (producer) | Specifies if the request is a pojo request. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (advanced) | **Autowired** The client to use during service invocation. |  | SecretManagerServiceClient |

## Message Headers

The Google Secret Manager component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **GoogleSecretManagerOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-secret-manager/latest/org/apache/camel/component/google/secret/manager/GoogleSecretManagerConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   createSecret
    
-   getSecretVersion
    
-   deleteSecret
    
-   listSecrets
    





 |  | GoogleSecretManagerOperations |
| **CamelGoogleSecretManagerSecretId** (producer) Constant: [`SECRET_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-secret-manager/latest/org/apache/camel/component/google/secret/manager/GoogleSecretManagerConstants.html#SECRET_ID) | The id of the secret. |  | String |
| **CamelGoogleSecretManagerVersionId** (producer) Constant: [`VERSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-secret-manager/latest/org/apache/camel/component/google/secret/manager/GoogleSecretManagerConstants.html#VERSION_ID) | The version of the secret. | latest | String |

### Using GCP Secret Manager Properties Source

To use GCP Secret Manager you need to provide _serviceAccountKey_ file and GCP _projectId_. This can be done using environmental variables before starting the application:

```bash
export $CAMEL_VAULT_GCP_SERVICE_ACCOUNT_KEY=file:////path/to/service.accountkey
export $CAMEL_VAULT_GCP_PROJECT_ID=projectId
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.gcp.serviceAccountKey = serviceAccountKey
camel.vault.gcp.projectId = projectId
```

If you want instead to use the [GCP default client instance](https://cloud.google.com/docs/authentication/production), you’ll need to provide the following env variables:

```bash
export $CAMEL_VAULT_GCP_USE_DEFAULT_INSTANCE=true
export $CAMEL_VAULT_GCP_PROJECT_ID=projectId
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.gcp.useDefaultInstance = true
camel.vault.aws.projectId = region
```

At this point you’ll be able to reference a property in the following way by using `gcp:` as prefix in the `{{ }}` syntax:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{gcp:route}}"/>
    </route>
</camelContext>
```

Where `route` will be the name of the secret stored in the GCP Secret Manager Service.

You could specify a default value in case the secret is not present on GCP Secret Manager:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{gcp:route:default}}"/>
    </route>
</camelContext>
```

In this case if the secret doesn’t exist, the property will fallback to "default" as value.

Also, you are able to get particular field of the secret, if you have for example a secret named database of this form:

```json
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
        <log message="Username is {{gcp:database/username}}"/>
    </route>
</camelContext>
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on GCP Secret Manager:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{gcp:database/username:admin}}"/>
    </route>
</camelContext>
```

In this case if the secret doesn’t exist or the secret exists, but the username field is not part of the secret, the property will fallback to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approach, with field/default value specified or only with secret:

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{gcp:route@1}}"/>
    </route>
</camelContext>
```

This approach will return the RAW route secret with version '1'.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{gcp:route:default@1}}"/>
    </route>
</camelContext>
```

This approach will return the route secret value with version '1' or default value in case the secret doesn’t exist or the version doesn’t exist.

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{gcp:database/username:admin@1}}"/>
    </route>
</camelContext>
```

This approach will return the username field of the database secret with version '1' or admin in case the secret doesn’t exist or the version doesn’t exist.

There are only two requirements: - Adding `camel-google-secret-manager` JAR to your Camel application. - Give the service account used permissions to do operation at secret management level (for example accessing the secret payload, or being admin of secret manager service)

### Automatic Camel context reloading on Secret Refresh

Being able to reload Camel context on a Secret Refresh, could be done by specifying the usual credentials (the same used for Google Secret Manager Property Function).

With Environment variables:

```bash
export $CAMEL_VAULT_GCP_USE_DEFAULT_INSTANCE=true
export $CAMEL_VAULT_GCP_PROJECT_ID=projectId
```

or as plain Camel main properties:

```properties
camel.vault.gcp.useDefaultInstance = true
camel.vault.aws.projectId = projectId
```

Or by specifying a path to a service account key file, instead of using the default instance.

To enable the automatic refresh you’ll need additional properties to set:

```properties
camel.vault.gcp.projectId= projectId
camel.vault.gcp.refreshEnabled=true
camel.vault.gcp.refreshPeriod=60000
camel.vault.gcp.secrets=hello*
camel.vault.gcp.subscriptionName=subscriptionName
camel.main.context-reload-enabled = true
```

where `camel.vault.gcp.refreshEnabled` will enable the automatic context reload, `camel.vault.gcp.refreshPeriod` is the interval of time between two different checks for update events and `camel.vault.gcp.secrets` is a regex representing the secrets we want to track for updates.

Note that `camel.vault.gcp.secrets` is not mandatory: if not specified the task responsible for checking updates events will take into accounts or the properties with an `gcp:` prefix.

The `camel.vault.gcp.subscriptionName` is the subscription name created in relation to the Google PubSub topic associated with the tracked secrets.

This mechanism while make use of the notification system related to Google Secret Manager: through this feature, every secret could be associated to one up to ten Google Pubsub Topics. These topics will receive events related to life cycle of the secret.

There are only two requirements: - Adding `camel-google-secret-manager` JAR to your Camel application. - Give the service account used permissions to do operation at secret management level (for example accessing the secret payload, or being admin of secret manager service and also have permission over the Pubsub service)

### Google Secret Manager Producer operations

Google Functions component provides the following operation on the producer side:

-   createSecret
    
-   getSecretVersion
    
-   deleteSecret
    
-   listSecrets
    

If you don’t specify an operation by default the producer will use the `createSecret` operation.

### Google Secret Manager Producer Operation examples

-   createSecret: This operation will create a secret in the Secret Manager service
    

```java
from("direct:start")
    .setHeader("GoogleSecretManagerConstants.SECRET_ID, constant("test"))
    .setBody(constant("hello"))
    .to("google-functions://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=createSecret")
    .log("body:${body}")
```

-   getSecretVersion: This operation will retrieve a secret value with latest version in the Secret Manager service
    

```java
from("direct:start")
    .setHeader("GoogleSecretManagerConstants.SECRET_ID, constant("test"))
    .to("google-functions://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=getSecretVersion")
    .log("body:${body}")
```

This will log the value of the secret "test".

-   deleteSecret: This operation will delete a secret
    

```java
from("direct:start")
    .setHeader("GoogleSecretManagerConstants.SECRET_ID, constant("test"))
    .to("google-functions://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=deleteSecret")
```

-   listSecrets: This operation will return the secrets list for the project myProject
    

```java
from("direct:start")
    .setHeader("GoogleSecretManagerConstants.SECRET_ID, constant("test"))
    .to("google-functions://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=listSecrets")
```

## Spring Boot Auto-Configuration

When using google-secret-manager with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-secret-manager-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-secret-manager.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-secret-manager.enabled** | Whether to enable auto configuration of the google-secret-manager component. This is enabled by default. |  | Boolean |
| **camel.component.google-secret-manager.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |