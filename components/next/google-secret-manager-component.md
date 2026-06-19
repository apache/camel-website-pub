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

Google Secret Manager component authentication is targeted for use with the GCP Service Accounts. For more information, please refer to [Google Cloud Authentication](https://github.com/googleapis/google-cloud-java#authentication).

When you have the **service account key**, you can provide authentication credentials to your application code. Google security credentials can be set through the component endpoint:

_Java-only: setting the endpoint URI with service account key_

```java
String endpoint = "google-secret-manager://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json";
```

Or by setting the environment variable `GOOGLE_APPLICATION_CREDENTIALS` :

export GOOGLE\_APPLICATION\_CREDENTIALS="/home/user/Downloads/my-key.json"

## URI Format

google-secret-manager://functionName\[?options\]

You can append query options to the URI in the following format, `?options=value&option2=value&…​`

For example, in order to call the function `myCamelFunction` from the project `myProject` and location `us-central1`, use the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=createSecret")
    .to("direct:test");
```

```xml
<route>
  <from uri="google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&amp;operation=createSecret"/>
  <to uri="direct:test"/>
</route>
```

```yaml
- route:
    from:
      uri: google-secret-manager://myProject
      parameters:
        serviceAccountKey: /home/user/Downloads/my-key.json
        operation: createSecret
      steps:
        - to:
            uri: direct:test
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

The Google Secret Manager component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Google Secret Manager endpoint is configured using URI syntax:

google-secret-manager:project

With the following _path_ and _query_ parameters:

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
| **CamelGoogleSecretManagerOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-secret-manager/latest/org/apache/camel/component/google/secret/manager/GoogleSecretManagerConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   createSecret
    
-   getSecretVersion
    
-   deleteSecret
    
-   listSecrets
    





 |  | GoogleSecretManagerOperations |
| **CamelGoogleSecretManagerSecretId** (producer) Constant: [`SECRET_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-secret-manager/latest/org/apache/camel/component/google/secret/manager/GoogleSecretManagerConstants.html#SECRET_ID) | The id of the secret. |  | String |
| **CamelGoogleSecretManagerVersionId** (producer) Constant: [`VERSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-secret-manager/latest/org/apache/camel/component/google/secret/manager/GoogleSecretManagerConstants.html#VERSION_ID) | The version of the secret. | latest | String |

### Using GCP Secret Manager Property Function

To use GCP Secret Manager, you need to provide `serviceAccountKey` file and GCP `projectId`. This can be done using environmental variables before starting the application:

```bash
export $CAMEL_VAULT_GCP_SERVICE_ACCOUNT_KEY=file:////path/to/service.accountkey
export $CAMEL_VAULT_GCP_PROJECT_ID=projectId
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.gcp.serviceAccountKey = serviceAccountKey
camel.vault.gcp.projectId = projectId
```

> **Note**
> if you’re running the application on a Kubernetes based cloud platform, you can initialize the environment variables from a Secret or Configmap to enhance security. You can also enhance security by [setting a Secret property placeholder](../../manual/using-propertyplaceholder.html#_resolving_property_placeholders_on_cloud) which will be initialized at application runtime only.

If you want instead to use the [GCP default client instance](https://cloud.google.com/docs/authentication/production), you’ll need to provide the following env variables:

```bash
export $CAMEL_VAULT_GCP_USE_DEFAULT_INSTANCE=true
export $CAMEL_VAULT_GCP_PROJECT_ID=projectId
```

You can also configure the credentials in the `application.properties` file such as:

```properties
camel.vault.gcp.useDefaultInstance = true
camel.vault.gcp.projectId = region
```

> **Note**
> `camel.vault.gcp` configuration only applies to the Google Secret Manager properties function (E.g when resolving properties). When using the `operation` option to create, get, list secrets etc., you should provide the usual options for connecting to GCP Services.

At this point you’ll be able to reference a property in the following way by using `gcp:` as prefix in the `{{ }}` syntax:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{gcp:route}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{gcp:route}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{gcp:route}}"
```

Where `route` will be the name of the secret stored in the GCP Secret Manager Service.

You could specify a default value in case the secret is not present on GCP Secret Manager:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{gcp:route:default}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{gcp:route:default}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{gcp:route:default}}"
```

In this case, if the secret doesn’t exist, the property will fall back to `default` as value.

Also, you are able to get a particular field of the secret, if you have, for example, a secret named database of this form:

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

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{gcp:database#username}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{gcp:database#username}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{gcp:database#username}}"
```

Or re-use the property as part of an endpoint.

You could specify a default value in case the particular field of secret is not present on GCP Secret Manager:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{gcp:database#username:admin}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{gcp:database#username:admin}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{gcp:database#username:admin}}"
```

In this case, if the secret doesn’t exist or the secret exists, but the username field is not part of the secret, the property will fall back to "admin" as value.

There is also the syntax to get a particular version of the secret for both the approach, with field/default value specified or only with secret:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{gcp:route@1}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{gcp:route@1}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{gcp:route@1}}"
```

This approach will return the RAW route secret with version '1'.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{gcp:route:default@1}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <to uri="{{gcp:route:default@1}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{gcp:route:default@1}}"
```

This approach will return the route secret value with version '1' or default value in case the secret doesn’t exist or the version doesn’t exist.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .log("Username is {{gcp:database#username:admin@1}}");
```

```xml
<camelContext>
    <route>
        <from uri="direct:start"/>
        <log message="Username is {{gcp:database#username:admin@1}}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - log:
            message: "Username is {{gcp:database#username:admin@1}}"
```

This approach will return the username field of the database secret with version '1' or admin in case the secret doesn’t exist or the version doesn’t exist.

There are only two requirements: - Adding `camel-google-secret-manager` JAR to your Camel application. - Give the service account used permissions to do operation at secret management level, (for example, accessing the secret payload, or being admin of secret manager service)

### Automatic `CamelContext` reloading on Secret Refresh

Being able to reload Camel context on a Secret Refresh could be done by specifying the usual credentials (the same used for Google Secret Manager Property Function).

With Environment variables:

```bash
export $CAMEL_VAULT_GCP_USE_DEFAULT_INSTANCE=true
export $CAMEL_VAULT_GCP_PROJECT_ID=projectId
```

or as plain Camel main properties:

```properties
camel.vault.gcp.useDefaultInstance = true
camel.vault.gcp.projectId = projectId
```

Or by specifying a path to a service account key file, instead of using the default instance.

To enable the automatic refresh, you’ll need additional properties to set:

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

This mechanism while making use of the notification system related to Google Secret Manager: through this feature, every secret could be associated with one up to ten Google Pubsub Topics. These topics will receive events related to the life cycle of the secret.

There are only two requirements: - Adding `camel-google-secret-manager` JAR to your Camel application. - Give the service account used permissions to do operation at secret management level, (for example, accessing the secret payload, or being admin of secret manager service and also have permission over the Pubsub service)

### Automatic `CamelContext` reloading on Secret Refresh - Required infrastructure’s creation

You’ll need to install the gcloud cli from [https://cloud.google.com/sdk/docs/install](https://cloud.google.com/sdk/docs/install)

Once the Cli has been installed we can proceed to log in and to set up the project with the following commands:

```none
gcloud auth login
```

and

```none
gcloud projects create <projectId> --name="GCP Secret Manager Refresh"
```

The project will need a service identity for using secret manager service and we’ll be able to have that through the command:

```none
gcloud beta services identity create --service "secretmanager.googleapis.com" --project <project_id>
```

The latter command will provide a service account name that we need to export

```none
export SM_SERVICE_ACCOUNT="service-...."
```

Since we want to have notifications about events related to a specific secret through a Google Pubsub topic we’ll need to create a topic for this purpose with the following command:

```none
gcloud pubsub topics create "projects/<project_id>/topics/pubsub-gcp-sec-refresh"
```

The service account will need Secret Manager authorization to publish messages on the topic just created, so we’ll need to add an iam policy binding with the following command:

```none
gcloud pubsub topics add-iam-policy-binding pubsub-gcp-sec-refresh --member "serviceAccount:${SM_SERVICE_ACCOUNT}" --role "roles/pubsub.publisher" --project <project_id>
```

We now need to create a subscription to the pubsub-gcp-sec-refresh just created and we’re going to call it sub-gcp-sec-refresh with the following command:

```none
gcloud pubsub subscriptions create "projects/<project_id>/subscriptions/sub-gcp-sec-refresh" --topic "projects/<project_id>/topics/pubsub-gcp-sec-refresh"
```

Now we need to create a service account for running our application:

```none
gcloud iam service-accounts create gcp-sec-refresh-sa --description="GCP Sec Refresh SA" --project <project_id>
```

Let’s give the SA an owner role:

```none
gcloud projects add-iam-policy-binding <project_id> --member="serviceAccount:gcp-sec-refresh-sa@<project_id>.iam.gserviceaccount.com" --role="roles/owner"
```

Now we should create a Service account key file for the just create SA:

```none
gcloud iam service-accounts keys create <project_id>.json --iam-account=gcp-sec-refresh-sa@<project_id>.iam.gserviceaccount.com
```

Let’s enable the Secret Manager API for our project

```none
gcloud services enable secretmanager.googleapis.com --project <project_id>
```

Also the PubSub API needs to be enabled

```none
gcloud services enable pubsub.googleapis.com --project <project_id>
```

If needed enable also the Billing API.

Now it’s time to create our secret, with topic notification:

```none
gcloud secrets create <secret_name> --topics=projects/<project_id>/topics/pubsub-gcp-sec-refresh --project=<project_id>
```

And let’s add the value

```none
gcloud secrets versions add <secret_name> --data-file=<json_secret> --project=<project_id>
```

You could now use the projectId and the service account json file to recover the secret.

### Google Secret Manager Producer operations

Google Functions component provides the following operation on the producer side:

-   `createSecret`
    
-   `getSecretVersion`
    
-   `deleteSecret`
    
-   `listSecrets`
    

If you don’t specify an operation by default, the producer will use the `createSecret` operation.

### Google Secret Manager Producer Operation examples

-   `createSecret`: This operation will create a secret in the Secret Manager service
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelGoogleSecretManagerSecretId", constant("test"))
    .setBody(constant("hello"))
    .to("google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=createSecret")
    .log("body:${body}");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelGoogleSecretManagerSecretId">
    <constant>test</constant>
  </setHeader>
  <setBody>
    <constant>hello</constant>
  </setBody>
  <to uri="google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&amp;operation=createSecret"/>
  <log message="body:${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelGoogleSecretManagerSecretId
            constant: test
        - setBody:
            constant: hello
        - to:
            uri: google-secret-manager://myProject
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
              operation: createSecret
        - log:
            message: "body:${body}"
```

-   `getSecretVersion`: This operation will retrieve a secret value with the latest version in the Secret Manager service
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelGoogleSecretManagerSecretId", constant("test"))
    .to("google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=getSecretVersion")
    .log("body:${body}");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelGoogleSecretManagerSecretId">
    <constant>test</constant>
  </setHeader>
  <to uri="google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&amp;operation=getSecretVersion"/>
  <log message="body:${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelGoogleSecretManagerSecretId
            constant: test
        - to:
            uri: google-secret-manager://myProject
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
              operation: getSecretVersion
        - log:
            message: "body:${body}"
```

This will log the value of the secret "test".

-   `deleteSecret`: This operation will delete a secret
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelGoogleSecretManagerSecretId", constant("test"))
    .to("google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=deleteSecret");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelGoogleSecretManagerSecretId">
    <constant>test</constant>
  </setHeader>
  <to uri="google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&amp;operation=deleteSecret"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelGoogleSecretManagerSecretId
            constant: test
        - to:
            uri: google-secret-manager://myProject
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
              operation: deleteSecret
```

-   `listSecrets`: This operation will return the secrets' list for the project myProject
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelGoogleSecretManagerSecretId", constant("test"))
    .to("google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&operation=listSecrets");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelGoogleSecretManagerSecretId">
    <constant>test</constant>
  </setHeader>
  <to uri="google-secret-manager://myProject?serviceAccountKey=/home/user/Downloads/my-key.json&amp;operation=listSecrets"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelGoogleSecretManagerSecretId
            constant: test
        - to:
            uri: google-secret-manager://myProject
            parameters:
              serviceAccountKey: /home/user/Downloads/my-key.json
              operation: listSecrets
```

### Using Google Secret Manager Property Function in Spring Boot for Early resolving properties

Google Secret Manager Spring Boot component starter offers the ability to early resolve properties, so the end user could resolve properties directly in the application.properties before both Spring Boot runtime and Camel context will start.

This could be accomplished in the following way. You should specified this property in your application.properties file:

```bash
camel.component.google-secret-manager.early-resolve-properties=true
```

This will enable the feature so you’ll be able to resolved properties, in your application.properties file, like:

```bash
foo = gcp:databaseprod#password
```

Please note that for making this feature work you’ll need to set the following two properties inside your application.properties

```bash
camel.vault.gcp.projectId=projectId
camel.vault.gcp.useDefaultInstance=true
```

Then you’ll need to export the environment variable `GOOGLE_APPLICATION_CREDENTIALS` and make it point to your service account key file.