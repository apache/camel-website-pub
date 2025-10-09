# Google Cloud Functions

**Since Camel 3.9**

**Only producer is supported**

The Google Functions component provides access to [Google Cloud Functions](https://cloud.google.com/functions/) via the [Google Cloud Functions Client for Java](https://github.com/googleapis/java-functions).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-functions</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

## Authentication Configuration

Google Functions component authentication is targeted for use with the GCP Service Accounts. For more information, please refer to [Google Cloud Authentication](https://github.com/googleapis/google-cloud-java#authentication).

When you have the **service account key**, you can provide authentication credentials to your application code. Google security credentials can be set through the component endpoint:

```java
String endpoint = "google-functions://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json";
```

Or by setting the environment variable `GOOGLE_APPLICATION_CREDENTIALS` :

export GOOGLE\_APPLICATION\_CREDENTIALS="/home/user/Downloads/my-key.json"

## URI Format

google-functions://functionName\[?options\]

You can append query options to the URI in the following format, `?options=value&option2=value&…​`

For example, to call the function `myCamelFunction` from the project `myProject` and location `us-central1`, use the following snippet:

```java
from("direct:start")
    .to("google-functions://myCamelFunction?project=myProject&location=us-central1&operation=callFunction&serviceAccountKey=/home/user/Downloads/my-key.json");
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

The Google Cloud Functions component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Google Cloud Functions endpoint is configured using URI syntax:

google-functions:functionName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **functionName** (common) | **Required** The user-defined name of the function. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceAccountKey** (common) | Service account key to authenticate an application as a service account. |  | String |
| **location** (producer) | The Google Cloud Location (Region) where the Function is located. |  | String |
| **operation** (producer) | 
The operation to perform on the producer.

Enum values:

-   listFunctions
    
-   getFunction
    
-   callFunction
    
-   generateDownloadUrl
    
-   generateUploadUrl
    
-   createFunction
    
-   updateFunction
    
-   deleteFunction
    





 |  | GoogleCloudFunctionsOperations |
| **pojoRequest** (producer) | Specifies if the request is a pojo request. | false | boolean |
| **project** (producer) | The Google Cloud Project name where the Function is located. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (advanced) | **Autowired** The client to use during service invocation. |  | CloudFunctionsServiceClient |

## Usage

## Message Headers

The Google Cloud Functions component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **GoogleCloudFunctionsOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-functions/latest/org/apache/camel/component/google/functions/GoogleCloudFunctionsConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   listFunctions
    
-   getFunction
    
-   callFunction
    
-   generateDownloadUrl
    
-   generateUploadUrl
    
-   createFunction
    
-   updateFunction
    
-   deleteFunction
    





 |  | GoogleCloudFunctionsOperations |
| **GoogleCloudFunctionsEntryPoint** (producer) Constant: [`ENTRY_POINT`](https://javadoc.io/doc/org.apache.camel/camel-google-functions/latest/org/apache/camel/component/google/functions/GoogleCloudFunctionsConstants.html#ENTRY_POINT) | The name of the function (as defined in source code) that will be executed. Used for createFunction operation. |  | String |
| **GoogleCloudFunctionsRuntime** (producer) Constant: [`RUNTIME`](https://javadoc.io/doc/org.apache.camel/camel-google-functions/latest/org/apache/camel/component/google/functions/GoogleCloudFunctionsConstants.html#RUNTIME) | The runtime in which to run the function. Possible values are: nodejs10 nodejs12 nodejs14 python37 python38 python39 go111 go113 java11 dotnet3 ruby26 nodejs6 nodejs8 Used for createFunction operation. |  | String |
| **GoogleCloudFunctionsSourceArchiveUrl** (producer) Constant: [`SOURCE_ARCHIVE_URL`](https://javadoc.io/doc/org.apache.camel/camel-google-functions/latest/org/apache/camel/component/google/functions/GoogleCloudFunctionsConstants.html#SOURCE_ARCHIVE_URL) | The Google Cloud Storage URL, starting with gs://, pointing to the zip archive which contains the function. Used for createFunction operation. |  | String |
| **GoogleCloudFunctionsResponseObject** (producer) Constant: [`RESPONSE_OBJECT`](https://javadoc.io/doc/org.apache.camel/camel-google-functions/latest/org/apache/camel/component/google/functions/GoogleCloudFunctionsConstants.html#RESPONSE_OBJECT) | The response object resulting from the Google Functions Client invocation. |  | Object |

### Google Functions Producer operations

Google Functions component provides the following operation on the producer side:

-   listFunctions
    
-   getFunction
    
-   callFunction
    
-   generateDownloadUrl
    
-   generateUploadUrl
    
-   createFunction
    
-   updateFunction
    
-   deleteFunction
    

If you don’t specify an operation by default, the producer will use the `callFunction` operation.

### Advanced component configuration

If you need to have more control over the `client` instance configuration, you can create your own instance and refer to it in your Camel google-functions component configuration:

```java
from("direct:start")
    .to("google-functions://myCamelFunction?client=#myClient");
```

### Google Functions Producer Operation examples

-   `ListFunctions`: This operation invokes the Google Functions client and gets the list of cloud Functions
    

```java
//list functions
from("direct:start")
    .to("google-functions://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json&project=myProject&location=us-central1&operation=listFunctions")
    .log("body:${body}")
```

This operation will get the list of cloud functions for the project `myProject` and location `us-central1`.

-   `GetFunction`: this operation gets the Cloud Functions object
    

```java
//get function
from("direct:start")
    .to("google-functions://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json&project=myProject&location=us-central1&operation=getFunction")
    .log("body:${body}")
    .to("mock:result");
```

This operation will get the `CloudFunction` object for the project `myProject`, location `us-central1` and functionName `myCamelFunction`.

-   `CallFunction`: this operation calls the function using an HTTP request
    

```java
//call function
from("direct:start")
    .process(exchange -> {
      exchange.getIn().setBody("just a message");
    })
    .to("google-functions://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json&project=myProject&location=us-central1&operation=callFunction")
    .log("body:${body}")
    .to("mock:result");
```

-   `GenerateDownloadUrl`: this operation generates the signed URL for downloading deployed function source code.
    

```java
//generate download url
from("direct:start")
    .to("google-functions://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json&project=myProject&location=us-central1&operation=generateDownloadUrl")
    .log("body:${body}")
    .to("mock:result");
```

-   `GenerateUploadUrl`: this operation generates a signed URL for uploading a function source code.
    

```java
from("direct:start")
    .to("google-functions://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json&project=myProject&location=us-central1&operation=generateUploadUrl")
    .log("body:${body}")
    .to("mock:result");
```

-   `createFunction`: this operation creates a new function.
    

```java
from("direct:start")
    .process(exchange -> {
      exchange.getIn().setHeader(GoogleCloudFunctionsConstants.ENTRY_POINT, "com.example.Example");
      exchange.getIn().setHeader(GoogleCloudFunctionsConstants.RUNTIME, "java11");
      exchange.getIn().setHeader(GoogleCloudFunctionsConstants.SOURCE_ARCHIVE_URL, "gs://myBucket/source.zip");
    })
    .to("google-functions://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json&project=myProject&location=us-central1&operation=createFunction")
    .log("body:${body}")
    .to("mock:result");
```

-   `updateFunction`: this operation updates existing function.
    

```java
from("direct:start")
    .process(exchange -> {
      UpdateFunctionRequest request = UpdateFunctionRequest.newBuilder()
        .setFunction(CloudFunction.newBuilder().build())
        .setUpdateMask(FieldMask.newBuilder().build()).build();
      exchange.getIn().setBody(request);
    })
    .to("google-functions://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json&project=myProject&location=us-central1&operation=updateFunction&pojoRequest=true")
    .log("body:${body}")
    .to("mock:result");
```

-   `deleteFunction`: this operation Deletes a function with the given name from the specified project.
    

```java
from("direct:start")
    .to("google-functions://myCamelFunction?serviceAccountKey=/home/user/Downloads/my-key.json&project=myProject&location=us-central1&operation=deleteFunction")
    .log("body:${body}")
    .to("mock:result");
```

## Spring Boot Auto-Configuration

When using google-functions with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-functions-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-functions.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-functions.enabled** | Whether to enable auto configuration of the google-functions component. This is enabled by default. |  | Boolean |
| **camel.component.google-functions.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |