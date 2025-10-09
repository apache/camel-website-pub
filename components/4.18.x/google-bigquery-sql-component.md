# Google BigQuery Standard SQL

**Since Camel 2.23**

**Only producer is supported**

The Google BigQuery SQL component provides access to [Cloud BigQuery Infrastructure](https://cloud.google.com/bigquery/) via the [Google Client Services API](https://developers.google.com/apis-explorer/#p/bigquery/v2/bigquery.jobs.query).

The current implementation supports only standard SQL [DML queries](https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-bigquery</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

## Authentication Configuration

Google BigQuery component authentication is targeted for use with the GCP Service Accounts. For more information please refer to [Google Cloud Platform Auth Guide](https://cloud.google.com/docs/authentication)

Google security credentials can be set explicitly by providing the path to the GCP credentials file location.

Or they are set implicitly, where the connection factory falls back on [Application Default Credentials](https://developers.google.com/identity/protocols/application-default-credentials#howtheywork).

When you have the **service account key** you can provide authentication credentials to your application code. Google security credentials can be set through the component endpoint:

```java
String endpoint = "google-bigquery-sql://project-id:query?serviceAccountKey=/home/user/Downloads/my-key.json";
```

You can also use the base64 encoded content of the authentication credentials file if you don’t want to set a file system path.

```java
String endpoint = "google-bigquery-sql://project-id:query?serviceAccountKey=base64:<base64 encoded>";
```

Or by setting the environment variable `GOOGLE_APPLICATION_CREDENTIALS` :

export GOOGLE\_APPLICATION\_CREDENTIALS="/home/user/Downloads/my-key.json"

## URI Format

google-bigquery-sql://project-id:query?\[options\]

Examples:

google-bigquery-sql://project-17248459:delete \* from test.table where id=@myId

google-bigquery-sql://project-17248459:delete \* from ${datasetId}.${tableId} where id=@myId

where

-   parameters in form ${name} are extracted from message headers and formed the translated query.
    
-   parameters in form @name are extracted from body or message headers and sent to Google Bigquery. The `com.google.cloud.bigquery.StandardSQLTypeName` of the parameter is detected from the type of the parameter using `<T> QueryParameterValue<T>.of(T value, Class<T> type)`
    

You can externalize your SQL queries to files in the classpath or file system as shown:

google-bigquery-sql://project-17248459::classpath:delete.sql

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

The Google BigQuery Standard SQL component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionFactory** (producer) | **Autowired** ConnectionFactory to obtain connection to Bigquery Service. If not provided the default one will be used. |  | GoogleBigQueryConnectionFactory |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **projectId** (producer) | Google Cloud Project Id. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Google BigQuery Standard SQL endpoint is configured using URI syntax:

google-bigquery-sql:projectId:queryString

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **projectId** (common) | **Required** Google Cloud Project Id. |  | String |
| **queryString** (common) | **Required** BigQuery standard SQL query. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionFactory** (producer) | **Autowired** ConnectionFactory to obtain connection to Bigquery Service. If not provided the default one will be used. |  | GoogleBigQueryConnectionFactory |
| **outputType** (producer) | 
Output mode type for select queries.

Enum values:

-   SELECT\_LIST
    
-   STREAM\_LIST
    





 | SELECT\_LIST | OutputType |
| **pageSize** (producer) | Size of a page to request. Unset by default. | 0 | long |
| **pageToken** (producer) | Page token, returned by a previous call, to request the next page of results. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account to google cloud platform. |  | String |

## Message Headers

The Google BigQuery Standard SQL component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleBigQueryTranslatedQuery** (producer) Constant: [`TRANSLATED_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-google-bigquery/latest/org/apache/camel/component/google/bigquery/GoogleBigQueryConstants.html#TRANSLATED_QUERY) | Preprocessed query text. |  | String |
| **CamelGoogleBigQueryJobId** (producer) Constant: [`JOB_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-bigquery/latest/org/apache/camel/component/google/bigquery/GoogleBigQueryConstants.html#JOB_ID) | A custom JobId to use. |  | JobId |
| **CamelGoogleBigQueryPageToken** (producer) Constant: [`PAGE_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-google-bigquery/latest/org/apache/camel/component/google/bigquery/GoogleBigQueryConstants.html#PAGE_TOKEN) | The page token to retrieve a specific page of results from BigQuery. If not set, the first page is returned. |  | String |
| **CamelGoogleBigQueryNextPageToken** (producer) Constant: [`NEXT_PAGE_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-google-bigquery/latest/org/apache/camel/component/google/bigquery/GoogleBigQueryConstants.html#NEXT_PAGE_TOKEN) | The next page token returned by BigQuery. Use this token in the CamelGoogleBigQueryPageToken header of a subsequent request to retrieve the next page of results. |  | String |

## Producer Endpoints

Google BigQuery SQL endpoint expects the payload to be either empty or a map of query parameters.

## Query Types

The component supports both SELECT and DML (INSERT, UPDATE, DELETE) queries:

-   **SELECT queries** - Return data based on configured `outputType` (SELECT\_LIST or STREAM\_LIST)
    
-   **DML queries** - Return the number of affected rows as `Long`
    

## Output Types

The component supports two output types for SELECT queries, configured using the `outputType` parameter

### SELECT\_LIST (default)

Returns all query results as a `List<Map<String, Object>>` loaded into memory.

**Characteristics:**

-   All rows from current page loaded into memory
    
-   Message body: `List<Map<String, Object>>`
    
-   Manual pagination via `pageSize` and `pageToken` parameters
    
-   Sets `CamelGoogleBigQueryNextPageToken` header for next page
    
-   Sets `CamelGoogleBigQueryJobId` header for continued pagination with same job
    
-   Results can be accessed multiple times
    

### STREAM\_LIST

Returns an `Iterator<Map<String, Object>>` for memory-efficient streaming of large result sets. Rows are loaded lazily as the iterator is consumed.

**Characteristics:**

-   Message body: `Iterator<Map<String, Object>>`
    
-   Pagination handled automatically by BigQuery SDK using `pageSize` for internal page fetching
    
-   Does NOT set `CamelGoogleBigQueryNextPageToken` or `CamelGoogleBigQueryJobId` headers
    
-   Does NOT support manual `pageToken` control
    
-   Memory-efficient - only current page in memory
    
-   Iterator can only be consumed once
    

**Note:** The `.streaming()` modifier on Split EIP is required to prevent loading all rows into memory before splitting.

**When to use STREAM\_LIST:**

-   Result sets with millions of rows
    
-   Memory-constrained environments
    
-   One-time sequential processing of rows
    
-   When using Split EIP in streaming mode
    

## Data Type Mapping

BigQuery result types are mapped to Java types:

  
| BigQuery Type | Java Type | Notes |
| --- | --- | --- |
| INT64 | Long |  |
| FLOAT64 | Double |  |
| NUMERIC | BigDecimal |  |
| STRING | String |  |
| BOOL | Boolean |  |
| BYTES | byte\[\] |  |
| DATE | String | ISO 8601 format |
| DATETIME | String | ISO 8601 format |
| TIME | String | ISO 8601 format |
| TIMESTAMP | String | ISO 8601 format with timezone |
| STRUCT (RECORD) | Map<String, Object> | Recursively converted to nested maps |
| ARRAY (REPEATED) | List<Object> | Elements recursively converted based on their type |
| RANGE | Map<String, Object> | Map with range start and end values |
| NULL | null |  |

## Spring Boot Auto-Configuration

When using google-bigquery-sql with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-bigquery-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-bigquery-sql.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-bigquery-sql.connection-factory** | ConnectionFactory to obtain connection to Bigquery Service. If not provided the default one will be used. The option is a org.apache.camel.component.google.bigquery.GoogleBigQueryConnectionFactory type. |  | GoogleBigQueryConnectionFactory |
| **camel.component.google-bigquery-sql.enabled** | Whether to enable auto configuration of the google-bigquery-sql component. This is enabled by default. |  | Boolean |
| **camel.component.google-bigquery-sql.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-bigquery-sql.project-id** | Google Cloud Project Id. |  | String |
| **camel.component.google-bigquery.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-bigquery.connection-factory** | ConnectionFactory to obtain connection to Bigquery Service. If not provided the default one will be used. The option is a org.apache.camel.component.google.bigquery.GoogleBigQueryConnectionFactory type. |  | GoogleBigQueryConnectionFactory |
| **camel.component.google-bigquery.dataset-id** | BigQuery Dataset Id. |  | String |
| **camel.component.google-bigquery.enabled** | Whether to enable auto configuration of the google-bigquery component. This is enabled by default. |  | Boolean |
| **camel.component.google-bigquery.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-bigquery.project-id** | Google Cloud Project Id. |  | String |