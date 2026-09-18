# IBM Watson Discovery

**Since Camel 4.16**

**Only producer is supported**

The IBM Watson Discovery component provides document understanding and intelligent search capabilities using [IBM Watson Discovery](https://www.ibm.com/cloud/watson-discovery).

Prerequisites

You must have a valid IBM Cloud account and have provisioned a Watson Discovery service instance with a project.

## URI Format

ibm-watson-discovery:label\[?options\]

Where `label` is a logical name for the endpoint.

You can append query options to the URI in the following format:

`?option1=value&option2=value&…​`

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

The IBM Watson Discovery component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **projectId** (common) | **Required** The Watson Discovery project ID. |  | String |
| **serviceUrl** (common) | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **version** (common) | The API version date (format: YYYY-MM-DD). | 2023-03-31 | String |
| **collectionId** (producer) | The collection ID for operations that require it. |  | String |
| **configuration** (producer) | The component configuration. |  | WatsonDiscoveryConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   query
    
-   listCollections
    
-   createCollection
    
-   deleteCollection
    
-   addDocument
    
-   updateDocument
    
-   deleteDocument
    





 |  | WatsonDiscoveryOperations |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **apiKey** (security) | **Required** The IBM Cloud API key for authentication. |  | String |

## Endpoint Options

The IBM Watson Discovery endpoint is configured using URI syntax:

ibm-watson-discovery:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **projectId** (common) | **Required** The Watson Discovery project ID. |  | String |
| **serviceUrl** (common) | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **version** (common) | The API version date (format: YYYY-MM-DD). | 2023-03-31 | String |
| **collectionId** (producer) | The collection ID for operations that require it. |  | String |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   query
    
-   listCollections
    
-   createCollection
    
-   deleteCollection
    
-   addDocument
    
-   updateDocument
    
-   deleteDocument
    





 |  | WatsonDiscoveryOperations |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiKey** (security) | **Required** The IBM Cloud API key for authentication. |  | String |

## Message Headers

The IBM Watson Discovery component supports 11 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIBMWatsonDiscoveryOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#OPERATION) | The operation to perform. |  | WatsonDiscoveryOperations |
| **CamelIBMWatsonDiscoveryQuery** (producer) Constant: [`QUERY`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#QUERY) | The natural language query to execute. |  | String |
| **CamelIBMWatsonDiscoveryCount** (producer) Constant: [`COUNT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#COUNT) | The number of results to return. |  | Integer |
| **CamelIBMWatsonDiscoveryFilter** (producer) Constant: [`FILTER`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#FILTER) | The filter to apply to the query. |  | String |
| **CamelIBMWatsonDiscoveryCollectionId** (producer) Constant: [`COLLECTION_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#COLLECTION_ID) | The collection ID. |  | String |
| **CamelIBMWatsonDiscoveryCollectionName** (producer) Constant: [`COLLECTION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#COLLECTION_NAME) | The collection name. |  | String |
| **CamelIBMWatsonDiscoveryCollectionDescription** (producer) Constant: [`COLLECTION_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#COLLECTION_DESCRIPTION) | The collection description. |  | String |
| **CamelIBMWatsonDiscoveryDocumentId** (producer) Constant: [`DOCUMENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#DOCUMENT_ID) | The document ID. |  | String |
| **CamelIBMWatsonDiscoveryDocumentFile** (producer) Constant: [`DOCUMENT_FILE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#DOCUMENT_FILE) | The document file. |  | InputStream |
| **CamelIBMWatsonDiscoveryDocumentFilename** (producer) Constant: [`DOCUMENT_FILENAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#DOCUMENT_FILENAME) | The document filename. |  | String |
| **CamelIBMWatsonDiscoveryDocumentContentType** (producer) Constant: [`DOCUMENT_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-discovery/latest/org/apache/camel/component/ibm/watson/discovery/WatsonDiscoveryConstants.html#DOCUMENT_CONTENT_TYPE) | The document content type. |  | String |

Required IBM Watson Discovery component options

You must provide the `apiKey` for authentication, `projectId` for your Watson Discovery project, and optionally the `serviceUrl` for your Watson service instance.

## Usage

### IBM Watson Discovery

This component integrates with IBM Watson Discovery service to perform intelligent document search, natural language querying, and document management operations.

### Authentication

IBM Watson services use IBM Cloud IAM (Identity and Access Management) for authentication. You need to provide:

-   `apiKey`: Your IBM Cloud API key
    
-   `projectId`: Your Watson Discovery project ID
    
-   `serviceUrl`: The endpoint URL for your Watson service instance (optional, defaults to the public endpoint)
    

You can find your service credentials and project ID in the IBM Cloud console.

### Operations

1.  `query` - Perform natural language queries against your document collections
    
2.  `listCollections` - List all collections in your project
    
3.  `createCollection` - Create a new document collection
    
4.  `deleteCollection` - Delete a collection
    
5.  `addDocument` - Add a document to a collection
    
6.  `updateDocument` - Update an existing document
    
7.  `deleteDocument` - Delete a document from a collection
    

## Examples

### Query Documents

Search for documents using natural language:

-   Java
    
-   YAML
    

```java
from("direct:search")
    .setBody(constant("What is artificial intelligence?"))
    .to("ibm-watson-discovery:default?apiKey=RAW(yourApiKey)&projectId=yourProjectId&operation=query")
    .process(exchange -> {
        QueryResponse response = exchange.getIn().getBody(QueryResponse.class);
        System.out.println("Found " + response.getMatchingResults() + " results");
        response.getResults().forEach(result -> {
            System.out.println("Document: " + result);
        });
    });
```

```yaml
- from:
    uri: direct:search
    steps:
      - setBody:
          constant: "What is artificial intelligence?"
      - to:
          uri: ibm-watson-discovery:default
          parameters:
            apiKey: RAW(yourApiKey)
            projectId: yourProjectId
            operation: query
      - log: "Found ${body.matchingResults} results"
```

### Query with Filters

Apply filters to narrow down search results:

-   Java
    
-   YAML
    

```java
from("direct:searchFiltered")
    .process(exchange -> {
        exchange.getIn().setBody("cloud computing");
        exchange.getIn().setHeader(WatsonDiscoveryConstants.FILTER, "enriched_text.entities.type:Company");
        exchange.getIn().setHeader(WatsonDiscoveryConstants.COUNT, 10);
    })
    .to("ibm-watson-discovery:default?apiKey=RAW(yourApiKey)&projectId=yourProjectId&operation=query");
```

```yaml
- from:
    uri: direct:searchFiltered
    steps:
      - setBody:
          constant: "cloud computing"
      - setHeader:
          name: CamelIBMWatsonDiscoveryFilter
          constant: "enriched_text.entities.type:Company"
      - setHeader:
          name: CamelIBMWatsonDiscoveryCount
          constant: 10
      - to:
          uri: ibm-watson-discovery:default
          parameters:
            apiKey: RAW(yourApiKey)
            projectId: yourProjectId
            operation: query
```

### List Collections

List all collections in your project:

-   Java
    
-   YAML
    

```java
from("direct:listCollections")
    .to("ibm-watson-discovery:default?apiKey=RAW(yourApiKey)&projectId=yourProjectId&operation=listCollections")
    .process(exchange -> {
        ListCollectionsResponse response = exchange.getIn().getBody(ListCollectionsResponse.class);
        response.getCollections().forEach(collection -> {
            System.out.println("Collection: " + collection.getName() + " (ID: " + collection.getCollectionId() + ")");
        });
    });
```

```yaml
- from:
    uri: direct:listCollections
    steps:
      - to:
          uri: ibm-watson-discovery:default
          parameters:
            apiKey: RAW(yourApiKey)
            projectId: yourProjectId
            operation: listCollections
      - log: "Collections: ${body}"
```

### Create Collection

Create a new document collection:

-   Java
    
-   YAML
    

```java
from("direct:createCollection")
    .process(exchange -> {
        exchange.getIn().setHeader(WatsonDiscoveryConstants.COLLECTION_NAME, "My Documents");
        exchange.getIn().setHeader(WatsonDiscoveryConstants.COLLECTION_DESCRIPTION, "Collection for project documents");
    })
    .to("ibm-watson-discovery:default?apiKey=RAW(yourApiKey)&projectId=yourProjectId&operation=createCollection")
    .process(exchange -> {
        CollectionDetails collection = exchange.getIn().getBody(CollectionDetails.class);
        String collectionId = exchange.getIn().getHeader(WatsonDiscoveryConstants.COLLECTION_ID, String.class);
        System.out.println("Created collection with ID: " + collectionId);
    });
```

```yaml
- from:
    uri: direct:createCollection
    steps:
      - setHeader:
          name: CamelIBMWatsonDiscoveryCollectionName
          constant: "My Documents"
      - setHeader:
          name: CamelIBMWatsonDiscoveryCollectionDescription
          constant: "Collection for project documents"
      - to:
          uri: ibm-watson-discovery:default
          parameters:
            apiKey: RAW(yourApiKey)
            projectId: yourProjectId
            operation: createCollection
      - log: "Created collection: ${header.CamelIBMWatsonDiscoveryCollectionId}"
```

### Add Document

Add a document to a collection:

-   Java
    
-   YAML
    

```java
from("file:input?noop=true")
    .process(exchange -> {
        exchange.getIn().setHeader(WatsonDiscoveryConstants.COLLECTION_ID, "your-collection-id");
        exchange.getIn().setHeader(WatsonDiscoveryConstants.DOCUMENT_FILENAME, exchange.getIn().getHeader(Exchange.FILE_NAME));
        exchange.getIn().setHeader(WatsonDiscoveryConstants.DOCUMENT_CONTENT_TYPE, "application/pdf");
        // Body is already the file InputStream
    })
    .to("ibm-watson-discovery:default?apiKey=RAW(yourApiKey)&projectId=yourProjectId&operation=addDocument")
    .process(exchange -> {
        String documentId = exchange.getIn().getHeader(WatsonDiscoveryConstants.DOCUMENT_ID, String.class);
        System.out.println("Added document with ID: " + documentId);
    });
```

```yaml
- from:
    uri: file:input?noop=true
    steps:
      - setHeader:
          name: CamelIBMWatsonDiscoveryCollectionId
          constant: "your-collection-id"
      - setHeader:
          name: CamelIBMWatsonDiscoveryDocumentFilename
          simple: "${header.CamelFileName}"
      - setHeader:
          name: CamelIBMWatsonDiscoveryDocumentContentType
          constant: "application/pdf"
      - to:
          uri: ibm-watson-discovery:default
          parameters:
            apiKey: RAW(yourApiKey)
            projectId: yourProjectId
            operation: addDocument
      - log: "Added document: ${header.CamelIBMWatsonDiscoveryDocumentId}"
```

### Delete Document

Delete a document from a collection:

-   Java
    
-   YAML
    

```java
from("direct:deleteDoc")
    .process(exchange -> {
        exchange.getIn().setHeader(WatsonDiscoveryConstants.COLLECTION_ID, "your-collection-id");
        exchange.getIn().setHeader(WatsonDiscoveryConstants.DOCUMENT_ID, "document-to-delete");
    })
    .to("ibm-watson-discovery:default?apiKey=RAW(yourApiKey)&projectId=yourProjectId&operation=deleteDocument")
    .log("Document deleted successfully");
```

```yaml
- from:
    uri: direct:deleteDoc
    steps:
      - setHeader:
          name: CamelIBMWatsonDiscoveryCollectionId
          constant: "your-collection-id"
      - setHeader:
          name: CamelIBMWatsonDiscoveryDocumentId
          constant: "document-to-delete"
      - to:
          uri: ibm-watson-discovery:default
          parameters:
            apiKey: RAW(yourApiKey)
            projectId: yourProjectId
            operation: deleteDocument
      - log: "Document deleted successfully"
```

### Custom Service URL

If your Watson service is in a specific region, specify the service URL:

-   Java
    
-   YAML
    

```java
from("direct:search")
    .to("ibm-watson-discovery:default?apiKey=RAW(yourApiKey)&projectId=yourProjectId&serviceUrl=https://api.us-south.discovery.watson.cloud.ibm.com&operation=query");
```

```yaml
- from:
    uri: direct:search
    steps:
      - to:
          uri: ibm-watson-discovery:default
          parameters:
            apiKey: RAW(yourApiKey)
            projectId: yourProjectId
            serviceUrl: "https://api.us-south.discovery.watson.cloud.ibm.com"
            operation: query
```

## Dependencies

Maven users will need to add the following dependency to their `pom.xml`.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ibm-watson-discovery</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

where `x.x.x` is the version number of Camel.

## Spring Boot Auto-Configuration

When using ibm-watson-discovery with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ibm-watson-discovery-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.ibm-watson-discovery.api-key** | The IBM Cloud API key for authentication. |  | String |
| **camel.component.ibm-watson-discovery.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ibm-watson-discovery.collection-id** | The collection ID for operations that require it. |  | String |
| **camel.component.ibm-watson-discovery.configuration** | The component configuration. The option is a org.apache.camel.component.ibm.watson.discovery.WatsonDiscoveryConfiguration type. |  | WatsonDiscoveryConfiguration |
| **camel.component.ibm-watson-discovery.enabled** | Whether to enable auto configuration of the ibm-watson-discovery component. This is enabled by default. |  | Boolean |
| **camel.component.ibm-watson-discovery.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ibm-watson-discovery.operation** | The operation to perform. |  | WatsonDiscoveryOperations |
| **camel.component.ibm-watson-discovery.project-id** | The Watson Discovery project ID. |  | String |
| **camel.component.ibm-watson-discovery.service-url** | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **camel.component.ibm-watson-discovery.version** | The API version date (format: YYYY-MM-DD). | 2023-03-31 | String |