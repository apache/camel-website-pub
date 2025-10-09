# Google Firestore

**Since Camel 4.19**

**Both producer and consumer are supported**

The Google Firestore component provides access to [Google Cloud Firestore](https://cloud.google.com/firestore) via the [Google Cloud Firestore Java library](https://github.com/googleapis/java-firestore).

Firestore is a flexible, scalable NoSQL cloud database for mobile, web, and server development. It keeps your data in sync across client apps through realtime listeners and offers offline support.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-firestore</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

## Authentication Configuration

Google Firestore component authentication is targeted for use with GCP Service Accounts. For more information, please refer to [Google Firestore Quickstart](https://cloud.google.com/firestore/docs/quickstart-servers).

When you have the **service account key**, you can provide authentication credentials to your application code. Google security credentials can be set through the component endpoint:

```java
String endpoint = "google-firestore://myCollection?serviceAccountKey=/home/user/Downloads/my-key.json&projectId=my-project";
```

Or by providing the path to the GCP credentials file location:

Provide authentication credentials to your application code by setting the environment variable `GOOGLE_APPLICATION_CREDENTIALS`:

export GOOGLE\_APPLICATION\_CREDENTIALS="/home/user/Downloads/my-key.json"

## URI Format

google-firestore://collectionName?\[options\]

You can append query options to the URI in the following format: `?options=value&option2=value&…​`

For example, to get a document from the `users` collection:

```java
from("direct:start")
    .setHeader("CamelGoogleFirestoreDocumentId", constant("user123"))
    .to("google-firestore://users?operation=getDocumentById&serviceAccountKey=/path/to/key.json&projectId=my-project")
    .to("log:result");
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

The Google Firestore component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | The component configuration. |  | GoogleFirestoreConfiguration |
| **databaseId** (common) | The Firestore database ID. If not specified, the default database '(default)' will be used. |  | String |
| **firestoreClient** (common) | **Autowired** The Firestore client to use for operations. |  | Firestore |
| **projectId** (common) | The Google Cloud project ID. If not specified, it will be determined from the service account key or environment. |  | String |
| **serviceAccountKey** (common) | The Service account key that can be used as credentials for the Firestore client. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **realtimeUpdates** (consumer) | When true, the consumer will listen for real-time updates on the collection. | false | boolean |
| **documentId** (producer) | The document ID to use for document-specific operations. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
Set the operation for the producer.

Enum values:

-   setDocument
    
-   getDocumentById
    
-   updateDocument
    
-   deleteDocument
    
-   queryCollection
    
-   listDocuments
    
-   listCollections
    
-   createDocument
    





 |  | GoogleFirestoreOperations |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Google Firestore endpoint is configured using URI syntax:

google-firestore:collectionName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collectionName** (common) | **Required** The collection name to use. |  | String |

### Query Parameters (27 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **databaseId** (common) | The Firestore database ID. If not specified, the default database '(default)' will be used. |  | String |
| **firestoreClient** (common) | **Autowired** The Firestore client to use for operations. |  | Firestore |
| **projectId** (common) | The Google Cloud project ID. If not specified, it will be determined from the service account key or environment. |  | String |
| **serviceAccountKey** (common) | The Service account key that can be used as credentials for the Firestore client. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **realtimeUpdates** (consumer) | When true, the consumer will listen for real-time updates on the collection. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **documentId** (producer) | The document ID to use for document-specific operations. |  | String |
| **operation** (producer) | 

Set the operation for the producer.

Enum values:

-   setDocument
    
-   getDocumentById
    
-   updateDocument
    
-   deleteDocument
    
-   queryCollection
    
-   listDocuments
    
-   listCollections
    
-   createDocument
    





 |  | GoogleFirestoreOperations |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |

## Message Headers

The Google Firestore component supports 16 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleFirestoreOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   setDocument
    
-   getDocumentById
    
-   updateDocument
    
-   deleteDocument
    
-   queryCollection
    
-   listDocuments
    
-   listCollections
    
-   createDocument
    





 |  | GoogleFirestoreOperations |
| **CamelGoogleFirestoreCollectionName** (producer) Constant: [`COLLECTION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#COLLECTION_NAME) | The collection name to use for the operation. |  | String |
| **CamelGoogleFirestoreDocumentId** (producer) Constant: [`DOCUMENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#DOCUMENT_ID) | The document ID to use for the operation. |  | String |
| **CamelGoogleFirestoreQueryField** (producer) Constant: [`QUERY_FIELD`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#QUERY_FIELD) | The field name for query filtering. |  | String |
| **CamelGoogleFirestoreQueryOperator** (producer) Constant: [`QUERY_OPERATOR`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#QUERY_OPERATOR) | The operator for query filtering (e.g., ==, , =, !=, array-contains, in, array-contains-any, not-in). |  | String |
| **CamelGoogleFirestoreQueryValue** (producer) Constant: [`QUERY_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#QUERY_VALUE) | The value for query filtering. |  | Object |
| **CamelGoogleFirestoreQueryLimit** (producer) Constant: [`QUERY_LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#QUERY_LIMIT) | The maximum number of documents to return in a query. |  | Integer |
| **CamelGoogleFirestoreQueryOrderBy** (producer) Constant: [`QUERY_ORDER_BY`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#QUERY_ORDER_BY) | The field to order the query results by. |  | String |
| **CamelGoogleFirestoreQueryOrderDirection** (producer) Constant: [`QUERY_ORDER_DIRECTION`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#QUERY_ORDER_DIRECTION) | 

The direction to order the query results (ASCENDING or DESCENDING).

Enum values:

-   ASCENDING
    
-   DESCENDING
    





 |  | Query$Direction |
| **CamelGoogleFirestoreResponseDocumentId** (consumer) Constant: [`RESPONSE_DOCUMENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#RESPONSE_DOCUMENT_ID) | The document ID from the response. |  | String |
| **CamelGoogleFirestoreResponseDocumentPath** (consumer) Constant: [`RESPONSE_DOCUMENT_PATH`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#RESPONSE_DOCUMENT_PATH) | The document path from the response. |  | String |
| **CamelGoogleFirestoreResponseCreateTime** (consumer) Constant: [`RESPONSE_CREATE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#RESPONSE_CREATE_TIME) | The document create time. |  | Timestamp |
| **CamelGoogleFirestoreResponseUpdateTime** (consumer) Constant: [`RESPONSE_UPDATE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#RESPONSE_UPDATE_TIME) | The document update time. |  | Timestamp |
| **CamelGoogleFirestoreResponseReadTime** (consumer) Constant: [`RESPONSE_READ_TIME`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#RESPONSE_READ_TIME) | The document read time. |  | Timestamp |
| **CamelGoogleFirestoreMerge** (producer) Constant: [`MERGE`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#MERGE) | When true, merge the data with existing document data instead of overwriting. | false | Boolean |
| **CamelGoogleFirestoreMergeFields** (producer) Constant: [`MERGE_FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-google-firestore/latest/org/apache/camel/component/google/firestore/GoogleFirestoreConstants.html#MERGE_FIELDS) | List of field paths to merge when using merge option. |  | List |

## Usage

### Google Firestore Producer Operations

Google Firestore component provides the following operations on the producer side:

-   `setDocument` - Create or overwrite a document with a specific ID
    
-   `createDocument` - Create a new document with an auto-generated ID
    
-   `getDocumentById` - Retrieve a document by its ID
    
-   `updateDocument` - Update specific fields of a document
    
-   `deleteDocument` - Delete a document
    
-   `queryCollection` - Query documents with filters
    
-   `listDocuments` - List all documents in a collection
    
-   `listCollections` - List all collections
    

If you don’t specify an operation explicitly, the producer will perform a `setDocument` operation.

### Supported Input Formats

For operations that require document data (`setDocument`, `createDocument`, `updateDocument`), the component accepts the following input formats:

-   **Map<String, Object>** - Java Map with field names as keys
    
-   **JSON String** - A valid JSON object string (e.g., `{"name": "John", "age": 30}`)
    
-   **Any object** - Convertible to Map via Camel’s type converter
    

JSON String Example:

```java
// Using JSON string as input
String json = """
    {
        "name": "John Doe",
        "email": "john@example.com",
        "age": 30,
        "active": true
    }
    """;

from("direct:start")
    .setBody(constant(json))
    .setHeader("CamelGoogleFirestoreDocumentId", constant("user123"))
    .to("google-firestore://users?operation=setDocument");
```

### Google Firestore Consumer

The consumer can poll documents from a collection or listen for real-time updates.

-   **Polling mode** (default): Periodically polls the collection for all documents
    
-   **Real-time mode**: Listens for document changes using Firestore’s real-time listeners
    

To enable real-time updates:

```java
from("google-firestore://myCollection?realtimeUpdates=true")
    .to("log:changes");
```

### Advanced Component Configuration

If you need more control over the `Firestore` client instance configuration, you can create your own instance and refer to it in your Camel google-firestore component configuration:

```java
from("google-firestore://myCollection?firestoreClient=#myFirestoreClient")
    .to("mock:result");
```

## Producer Operation Examples

### Create Document with Auto-Generated ID

This operation creates a new document with an auto-generated unique ID:

```java
Map<String, Object> document = new HashMap<>();
document.put("name", "John Doe");
document.put("email", "john@example.com");
document.put("age", 30);

from("direct:start")
    .setBody(constant(document))
    .to("google-firestore://users?operation=createDocument")
    .log("Created document with ID: ${header.CamelGoogleFirestoreResponseDocumentId}");
```

### Set Document with Specific ID

This operation creates or overwrites a document with a specific ID:

```java
Map<String, Object> document = new HashMap<>();
document.put("name", "Jane Doe");
document.put("email", "jane@example.com");

from("direct:start")
    .setBody(constant(document))
    .setHeader("CamelGoogleFirestoreDocumentId", constant("user123"))
    .to("google-firestore://users?operation=setDocument")
    .log("Document saved");
```

### Set Document with Merge

To merge data with an existing document instead of overwriting:

```java
Map<String, Object> updates = new HashMap<>();
updates.put("lastLogin", new Date());

from("direct:start")
    .setBody(constant(updates))
    .setHeader("CamelGoogleFirestoreDocumentId", constant("user123"))
    .setHeader("CamelGoogleFirestoreMerge", constant(true))
    .to("google-firestore://users?operation=setDocument")
    .log("Document merged");
```

### Get Document by ID

This operation retrieves a document by its ID:

```java
from("direct:start")
    .setHeader("CamelGoogleFirestoreDocumentId", constant("user123"))
    .to("google-firestore://users?operation=getDocumentById")
    .log("Document data: ${body}");
```

The response body will contain a `Map<String, Object>` with the document data, or `null` if the document doesn’t exist.

### Update Document

This operation updates specific fields without overwriting the entire document:

```java
Map<String, Object> updates = new HashMap<>();
updates.put("status", "active");
updates.put("updatedAt", new Date());

from("direct:start")
    .setBody(constant(updates))
    .setHeader("CamelGoogleFirestoreDocumentId", constant("user123"))
    .to("google-firestore://users?operation=updateDocument")
    .log("Document updated");
```

### Delete Document

This operation deletes a document:

```java
from("direct:start")
    .setHeader("CamelGoogleFirestoreDocumentId", constant("user123"))
    .to("google-firestore://users?operation=deleteDocument")
    .log("Document deleted: ${body}");
```

### List Documents

This operation lists all documents in a collection:

```java
from("direct:start")
    .to("google-firestore://users?operation=listDocuments")
    .log("Found ${body.size()} documents");
```

The response body will contain a `List<Map<String, Object>>` with each document’s data. Each document includes `_id` and `_path` fields with the document ID and path.

### Query Collection

This operation queries documents with filters:

```java
from("direct:start")
    .setHeader("CamelGoogleFirestoreQueryField", constant("age"))
    .setHeader("CamelGoogleFirestoreQueryOperator", constant(">="))
    .setHeader("CamelGoogleFirestoreQueryValue", constant(21))
    .setHeader("CamelGoogleFirestoreQueryLimit", constant(10))
    .setHeader("CamelGoogleFirestoreQueryOrderBy", constant("age"))
    .to("google-firestore://users?operation=queryCollection")
    .log("Found ${body.size()} matching documents");
```

Supported query operators:

-   `==` or `eq` - Equal to
    
-   `!=` or `ne` - Not equal to
    
-   `<` or `lt` - Less than
    
-   `⇐` or `lte` - Less than or equal to
    
-   `>` or `gt` - Greater than
    
-   `>=` or `gte` - Greater than or equal to
    
-   `array-contains` - Array contains value
    
-   `in` - Value in list
    
-   `array-contains-any` - Array contains any value in list
    
-   `not-in` - Value not in list
    

### List Collections

This operation lists all collections in the database:

```java
from("direct:start")
    .to("google-firestore://anyCollection?operation=listCollections")
    .log("Collections: ${body}");
```

To list subcollections under a specific document:

```java
from("direct:start")
    .setHeader("CamelGoogleFirestoreDocumentId", constant("user123"))
    .to("google-firestore://users?operation=listCollections")
    .log("Subcollections: ${body}");
```

## Consumer Examples

### Poll Documents

Poll all documents from a collection every 30 seconds:

```java
from("google-firestore://users?delay=30000")
    .log("Document ID: ${header.CamelGoogleFirestoreResponseDocumentId}")
    .log("Document data: ${body}")
    .to("mock:result");
```

### Real-time Updates

Listen for document changes in real-time:

```java
from("google-firestore://users?realtimeUpdates=true")
    .log("Change type: ${header.CamelGoogleFirestoreChangeType}")
    .log("Document ID: ${header.CamelGoogleFirestoreResponseDocumentId}")
    .log("Document data: ${body}")
    .to("mock:result");
```

The `CamelGoogleFirestoreChangeType` header indicates the type of change: `ADDED`, `MODIFIED`, or `REMOVED`.

## Data Types

### Input Data Formats

For write operations (`setDocument`, `createDocument`, `updateDocument`), the component accepts the following input formats in the message body:

  
| Format | Description | Example |
| --- | --- | --- |
| `Map<String, Object>` | Java Map with field names as keys | `Map.of("name", "John", "age", 30)` |
| JSON String | Valid JSON object string | `{"name": "John", "age": 30}` |
| POJO | Any object convertible to Map via Camel’s type converter | Custom Java beans |

#### JSON String Input

You can send a JSON string directly as the message body. The component will automatically parse it:

```java
// Simple JSON
from("direct:start")
    .setBody(constant("{\"name\": \"John\", \"age\": 30}"))
    .setHeader("CamelGoogleFirestoreDocumentId", constant("user123"))
    .to("google-firestore://users?operation=setDocument");

// Multi-line JSON with text blocks (Java 15+)
String json = """
    {
        "name": "John Doe",
        "email": "john@example.com",
        "age": 30,
        "active": true,
        "tags": ["admin", "user"],
        "address": {
            "street": "123 Main St",
            "city": "New York",
            "zip": "10001"
        }
    }
    """;

from("direct:start")
    .setBody(constant(json))
    .to("google-firestore://users?operation=createDocument");
```

#### Reading JSON from Files

```java
// Read JSON files and store in Firestore
from("file:data/users?noop=true&include=.*\\.json")
    .setHeader("CamelGoogleFirestoreDocumentId", simple("${file:name.noext}"))
    .to("google-firestore://users?operation=setDocument")
    .log("Imported: ${file:name}");
```

#### REST API Integration

```java
// Receive JSON from REST endpoint and store in Firestore
from("rest:post:/api/users")
    .to("google-firestore://users?operation=createDocument")
    .setBody(simple("{\"id\": \"${header.CamelGoogleFirestoreResponseDocumentId}\"}"));
```

### Supported Firestore Data Types

The following Java types are automatically converted to Firestore data types:

  
| Java Type | Firestore Type | Notes |
| --- | --- | --- |
| `String` | String | Text data |
| `Integer`, `Long` | Integer | 64-bit signed integer |
| `Double`, `Float` | Floating-point | 64-bit double precision |
| `Boolean` | Boolean | `true` or `false` |
| `Date`, `java.sql.Timestamp` | Timestamp | Converted to Firestore Timestamp |
| `com.google.cloud.Timestamp` | Timestamp | Native Firestore Timestamp |
| `List<?>` | Array | Ordered list, nested types supported |
| `Map<String, ?>` | Map | Nested document/object |
| `null` | Null | Null value |
| `byte[]` | Bytes | Binary data (max 1MB) |
| `com.google.cloud.firestore.GeoPoint` | GeoPoint | Latitude/longitude coordinates |
| `com.google.cloud.firestore.DocumentReference` | Reference | Reference to another document |

### Output Data Formats

#### Single Document Operations

For `getDocumentById`, the response body is:

-   `Map<String, Object>` - Document data if found
    
-   `null` - If document does not exist
    

#### List/Query Operations

For `listDocuments` and `queryCollection`, the response body is:

-   `List<Map<String, Object>>` - List of documents
    

Each document Map includes additional metadata fields:

-   `_id` - The document ID
    
-   `_path` - The full document path (e.g., `users/user123`)
    

#### Delete Operation

For `deleteDocument`, the response body is:

-   `Boolean` - Always `true` (Firestore delete is idempotent)
    

#### List Collections Operation

For `listCollections`, the response body is:

-   `List<String>` - List of collection IDs
    

### Error Handling

If the input body cannot be converted to a Map (e.g., invalid JSON), an `InvalidPayloadException` is thrown:

```text
org.apache.camel.InvalidPayloadException: No body available of type: java.util.Map
  ...Caused by: Unexpected character ('x' (code 120)): was expecting...
```

## Message Headers

The component uses the following headers:

### Producer Headers (Input)

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelGoogleFirestoreOperation` | `GoogleFirestoreOperations` | The operation to perform |
| `CamelGoogleFirestoreCollectionName` | `String` | Override the collection name |
| `CamelGoogleFirestoreDocumentId` | `String` | The document ID for document operations |
| `CamelGoogleFirestoreQueryField` | `String` | Field name for query filtering |
| `CamelGoogleFirestoreQueryOperator` | `String` | Operator for query filtering |
| `CamelGoogleFirestoreQueryValue` | `Object` | Value for query filtering |
| `CamelGoogleFirestoreQueryLimit` | `Integer` | Maximum documents to return |
| `CamelGoogleFirestoreQueryOrderBy` | `String` | Field to order results by |
| `CamelGoogleFirestoreQueryOrderDirection` | `Query.Direction` | Order direction (ASCENDING/DESCENDING) |
| `CamelGoogleFirestoreMerge` | `Boolean` | Merge data with existing document |
| `CamelGoogleFirestoreMergeFields` | `List<String>` | Specific fields to merge |

### Consumer/Response Headers (Output)

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelGoogleFirestoreResponseDocumentId` | `String` | The document ID |
| `CamelGoogleFirestoreResponseDocumentPath` | `String` | The full document path |
| `CamelGoogleFirestoreResponseCreateTime` | `Timestamp` | Document creation time |
| `CamelGoogleFirestoreResponseUpdateTime` | `Timestamp` | Document last update time |
| `CamelGoogleFirestoreResponseReadTime` | `Timestamp` | Document read time |
| `CamelGoogleFirestoreChangeType` | `String` | Change type for real-time updates (ADDED, MODIFIED, REMOVED) |

## Spring Boot Auto-Configuration

When using google-firestore with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-firestore-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-firestore.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-firestore.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-firestore.configuration** | The component configuration. The option is a org.apache.camel.component.google.firestore.GoogleFirestoreConfiguration type. |  | GoogleFirestoreConfiguration |
| **camel.component.google-firestore.database-id** | The Firestore database ID. If not specified, the default database '(default)' will be used. |  | String |
| **camel.component.google-firestore.document-id** | The document ID to use for document-specific operations. |  | String |
| **camel.component.google-firestore.enabled** | Whether to enable auto configuration of the google-firestore component. This is enabled by default. |  | Boolean |
| **camel.component.google-firestore.firestore-client** | The Firestore client to use for operations. The option is a com.google.cloud.firestore.Firestore type. |  | Firestore |
| **camel.component.google-firestore.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.google-firestore.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.google-firestore.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-firestore.operation** | Set the operation for the producer. |  | GoogleFirestoreOperations |
| **camel.component.google-firestore.project-id** | The Google Cloud project ID. If not specified, it will be determined from the service account key or environment. |  | String |
| **camel.component.google-firestore.realtime-updates** | When true, the consumer will listen for real-time updates on the collection. | false | Boolean |
| **camel.component.google-firestore.service-account-key** | The Service account key that can be used as credentials for the Firestore client. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |