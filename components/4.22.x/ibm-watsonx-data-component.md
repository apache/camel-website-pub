# IBM watsonx.data

**Since Camel 4.19**

**Only producer is supported**

The IBM watsonx.data component provides integration with [IBM watsonx.data](https://www.ibm.com/products/watsonx-data), an open lakehouse platform for data analytics and AI workloads. It allows you to manage catalogs, schemas, tables, query engines, and storage registrations programmatically.

This component is built on top of the [IBM watsonx.data Java SDK](https://github.com/IBM/watsonxdata-java-sdk).

## Prerequisites

You must have a valid IBM Cloud account with access to watsonx.data services. More information is available at [IBM watsonx.data](https://www.ibm.com/products/watsonx-data).

To use this component, you need:

-   An IBM Cloud API key
    
-   The watsonx.data service URL for your region
    

## URI Format

ibm-watsonx-data:label\[?options\]

Where `label` is a logical name for the endpoint.

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

The IBM watsonx.data component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **authInstanceId** (common) | The watsonx.data instance CRN for API authorization. |  | String |
| **serviceUrl** (common) | **Required** The watsonx.data service URL (e.g., [https://region.lakehouse.cloud.ibm.com/lakehouse/api/v2](https://region.lakehouse.cloud.ibm.com/lakehouse/api/v2)). |  | String |
| **catalogName** (producer) | The catalog name for catalog, schema, and table operations. |  | String |
| **configuration** (producer) | The component configuration. |  | WatsonxDataConfiguration |
| **engineId** (producer) | The engine ID for engine operations and schema/table queries. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   listCatalogs
    
-   getCatalog
    
-   deleteCatalog
    
-   listSchemas
    
-   createSchema
    
-   deleteSchema
    
-   listTables
    
-   getTable
    
-   deleteTable
    
-   updateTable
    
-   registerTable
    
-   getAllColumns
    
-   listPrestoEngines
    
-   getPrestoEngine
    
-   listPrestissimoEngines
    
-   getPrestissimoEngine
    
-   listStorageRegistrations
    
-   createStorageRegistration
    





 |  | WatsonxDataOperations |
| **schemaName** (producer) | The schema name for schema and table operations. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **apiKey** (security) | **Required** IBM Cloud API key for authentication. |  | String |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as apiKey. Requires camel-oauth on the classpath. |  | String |

## Endpoint Options

The IBM watsonx.data endpoint is configured using URI syntax:

ibm-watsonx-data:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name for the endpoint. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **authInstanceId** (common) | The watsonx.data instance CRN for API authorization. |  | String |
| **serviceUrl** (common) | **Required** The watsonx.data service URL (e.g., [https://region.lakehouse.cloud.ibm.com/lakehouse/api/v2](https://region.lakehouse.cloud.ibm.com/lakehouse/api/v2)). |  | String |
| **catalogName** (producer) | The catalog name for catalog, schema, and table operations. |  | String |
| **engineId** (producer) | The engine ID for engine operations and schema/table queries. |  | String |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   listCatalogs
    
-   getCatalog
    
-   deleteCatalog
    
-   listSchemas
    
-   createSchema
    
-   deleteSchema
    
-   listTables
    
-   getTable
    
-   deleteTable
    
-   updateTable
    
-   registerTable
    
-   getAllColumns
    
-   listPrestoEngines
    
-   getPrestoEngine
    
-   listPrestissimoEngines
    
-   getPrestissimoEngine
    
-   listStorageRegistrations
    
-   createStorageRegistration
    





 |  | WatsonxDataOperations |
| **schemaName** (producer) | The schema name for schema and table operations. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiKey** (security) | **Required** IBM Cloud API key for authentication. |  | String |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as apiKey. Requires camel-oauth on the classpath. |  | String |

## Message Headers

The IBM watsonx.data component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIBMWatsonxDataOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#OPERATION) | The operation to perform. |  | WatsonxDataOperations |
| **CamelIBMWatsonxDataCatalogName** (producer) Constant: [`CATALOG_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#CATALOG_NAME) | The catalog name. |  | String |
| **CamelIBMWatsonxDataSchemaName** (producer) Constant: [`SCHEMA_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#SCHEMA_NAME) | The schema name. |  | String |
| **CamelIBMWatsonxDataCustomPath** (producer) Constant: [`CUSTOM_PATH`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#CUSTOM_PATH) | The custom path for schema creation. |  | String |
| **CamelIBMWatsonxDataTableName** (producer) Constant: [`TABLE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#TABLE_NAME) | The table name. |  | String |
| **CamelIBMWatsonxDataMetadataLocation** (producer) Constant: [`METADATA_LOCATION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#METADATA_LOCATION) | The metadata location for table registration (e.g., S3 path to Iceberg metadata). |  | String |
| **CamelIBMWatsonxDataCatalogId** (producer) Constant: [`CATALOG_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#CATALOG_ID) | The catalog ID for table registration. |  | String |
| **CamelIBMWatsonxDataSchemaId** (producer) Constant: [`SCHEMA_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#SCHEMA_ID) | The schema ID for table registration. |  | String |
| **CamelIBMWatsonxDataEngineId** (producer) Constant: [`ENGINE_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#ENGINE_ID) | The engine ID. |  | String |
| **CamelIBMWatsonxDataStorageDescription** (producer) Constant: [`STORAGE_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#STORAGE_DESCRIPTION) | The storage description for registration. |  | String |
| **CamelIBMWatsonxDataStorageDisplayName** (producer) Constant: [`STORAGE_DISPLAY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#STORAGE_DISPLAY_NAME) | The storage display name for registration. |  | String |
| **CamelIBMWatsonxDataStorageManagedBy** (producer) Constant: [`STORAGE_MANAGED_BY`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#STORAGE_MANAGED_BY) | The storage managed by value (e.g., ibm, customer). |  | String |
| **CamelIBMWatsonxDataStorageType** (producer) Constant: [`STORAGE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#STORAGE_TYPE) | The storage type (e.g., ibm\_cos, aws\_s3, google\_cs). |  | String |
| **CamelIBMWatsonxDataAuthInstanceId** (producer) Constant: [`AUTH_INSTANCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-data/latest/org/apache/camel/component/ibm/watsonx/data/WatsonxDataConstants.html#AUTH_INSTANCE_ID) | The auth instance ID for watsonx.data API calls. |  | String |

## Authentication

The component supports authentication via IBM Cloud API Key:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("ibm-watsonx-data:myLakehouse?apiKey=YOUR_API_KEY&serviceUrl=https://us-south.lakehouse.cloud.ibm.com/lakehouse/api/v2&operation=listCatalogs");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="ibm-watsonx-data:myLakehouse?apiKey=YOUR_API_KEY&amp;serviceUrl=https://us-south.lakehouse.cloud.ibm.com/lakehouse/api/v2&amp;operation=listCatalogs"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: ibm-watsonx-data:myLakehouse
            parameters:
              apiKey: YOUR_API_KEY
              serviceUrl: "https://us-south.lakehouse.cloud.ibm.com/lakehouse/api/v2"
              operation: listCatalogs
```

OAuth 2.0 Client Credentials grant is also supported when `camel-oauth` is on the classpath:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("ibm-watsonx-data:myLakehouse?oauthProfile=ibm&serviceUrl=https://us-south.lakehouse.cloud.ibm.com/lakehouse/api/v2&operation=listCatalogs");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="ibm-watsonx-data:myLakehouse?oauthProfile=ibm&amp;serviceUrl=https://us-south.lakehouse.cloud.ibm.com/lakehouse/api/v2&amp;operation=listCatalogs"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: ibm-watsonx-data:myLakehouse
            parameters:
              oauthProfile: ibm
              serviceUrl: "https://us-south.lakehouse.cloud.ibm.com/lakehouse/api/v2"
              operation: listCatalogs
```

## Operations

The component supports the following operations:

### Catalog Operations

 
| Operation | Description |
| --- | --- |
| `listCatalogs` | List all catalogs in the watsonx.data instance. |
| `getCatalog` | Get details of a specific catalog. Requires `catalogName`. |
| `deleteCatalog` | Delete a catalog. Requires `catalogName`. |

### Schema Operations

 
| Operation | Description |
| --- | --- |
| `listSchemas` | List schemas in a catalog. Requires `catalogName` and `engineId`. |
| `createSchema` | Create a new schema. Requires `catalogName`, `engineId`, `CamelIBMWatsonxDataSchemaName` header, and `CamelIBMWatsonxDataCustomPath` header. |
| `deleteSchema` | Delete a schema. Requires `catalogName`, `engineId`, and `schemaName`. |

### Table Operations

 
| Operation | Description |
| --- | --- |
| `listTables` | List tables in a schema. Requires `catalogName`, `schemaName`, and `engineId`. |
| `getTable` | Get table details. Requires `catalogName`, `schemaName`, `engineId`, and `CamelIBMWatsonxDataTableName` header. |
| `deleteTable` | Delete a table. Requires `catalogName`, `schemaName`, `engineId`, and `CamelIBMWatsonxDataTableName` header. |
| `updateTable` | Update table properties. Requires `catalogName`, `schemaName`, `engineId`, `CamelIBMWatsonxDataTableName` header, and a `Map` body with patch data. |
| `registerTable` | Register an external Iceberg table. Requires `CamelIBMWatsonxDataCatalogId`, `CamelIBMWatsonxDataSchemaId`, `CamelIBMWatsonxDataMetadataLocation`, and `CamelIBMWatsonxDataTableName` headers. |
| `getAllColumns` | Get all columns for a catalog. Requires `catalogName`. Optionally filter by `schemaName` and `CamelIBMWatsonxDataTableName`. |

### Engine Operations

 
| Operation | Description |
| --- | --- |
| `listPrestoEngines` | List all Presto query engines. |
| `getPrestoEngine` | Get details of a Presto engine. Requires `engineId`. |
| `listPrestissimoEngines` | List all Prestissimo query engines. |
| `getPrestissimoEngine` | Get details of a Prestissimo engine. Requires `engineId`. |

### Storage Operations

 
| Operation | Description |
| --- | --- |
| `listStorageRegistrations` | List all registered storage locations. |
| `createStorageRegistration` | Register a new storage location. Requires `CamelIBMWatsonxDataStorageDescription`, `CamelIBMWatsonxDataStorageDisplayName`, `CamelIBMWatsonxDataStorageManagedBy`, and `CamelIBMWatsonxDataStorageType` headers. |

## Examples

### List Catalogs

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listCatalogs")
    .to("ibm-watsonx-data:lakehouse?apiKey={{ibm.apiKey}}&serviceUrl={{ibm.watsonxdata.url}}&operation=listCatalogs")
    .log("Catalogs: ${body}");
```

```xml
<route>
  <from uri="direct:listCatalogs"/>
  <to uri="ibm-watsonx-data:lakehouse?apiKey={{ibm.apiKey}}&amp;serviceUrl={{ibm.watsonxdata.url}}&amp;operation=listCatalogs"/>
  <log message="Catalogs: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:listCatalogs
      steps:
        - to:
            uri: ibm-watsonx-data:lakehouse
            parameters:
              apiKey: "{{ibm.apiKey}}"
              serviceUrl: "{{ibm.watsonxdata.url}}"
              operation: listCatalogs
        - log:
            message: "Catalogs: ${body}"
```

### List Tables in a Schema

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:listTables")
    .to("ibm-watsonx-data:lakehouse?apiKey={{ibm.apiKey}}&serviceUrl={{ibm.watsonxdata.url}}&catalogName=my-catalog&schemaName=my-schema&engineId=my-presto-engine&operation=listTables")
    .log("Tables: ${body}");
```

```xml
<route>
  <from uri="direct:listTables"/>
  <to uri="ibm-watsonx-data:lakehouse?apiKey={{ibm.apiKey}}&amp;serviceUrl={{ibm.watsonxdata.url}}&amp;catalogName=my-catalog&amp;schemaName=my-schema&amp;engineId=my-presto-engine&amp;operation=listTables"/>
  <log message="Tables: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:listTables
      steps:
        - to:
            uri: ibm-watsonx-data:lakehouse
            parameters:
              apiKey: "{{ibm.apiKey}}"
              serviceUrl: "{{ibm.watsonxdata.url}}"
              catalogName: my-catalog
              schemaName: my-schema
              engineId: my-presto-engine
              operation: listTables
        - log:
            message: "Tables: ${body}"
```

### Create a Schema

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createSchema")
    .setHeader("CamelIBMWatsonxDataSchemaName", constant("new_schema"))
    .setHeader("CamelIBMWatsonxDataCustomPath", constant("s3a://my-bucket/new_schema"))
    .to("ibm-watsonx-data:lakehouse?apiKey={{ibm.apiKey}}&serviceUrl={{ibm.watsonxdata.url}}&catalogName=my-catalog&engineId=my-engine&operation=createSchema")
    .log("Schema created: ${body}");
```

```xml
<route>
  <from uri="direct:createSchema"/>
  <setHeader name="CamelIBMWatsonxDataSchemaName">
    <constant>new_schema</constant>
  </setHeader>
  <setHeader name="CamelIBMWatsonxDataCustomPath">
    <constant>s3a://my-bucket/new_schema</constant>
  </setHeader>
  <to uri="ibm-watsonx-data:lakehouse?apiKey={{ibm.apiKey}}&amp;serviceUrl={{ibm.watsonxdata.url}}&amp;catalogName=my-catalog&amp;engineId=my-engine&amp;operation=createSchema"/>
  <log message="Schema created: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createSchema
      steps:
        - setHeader:
            name: CamelIBMWatsonxDataSchemaName
            constant: new_schema
        - setHeader:
            name: CamelIBMWatsonxDataCustomPath
            constant: "s3a://my-bucket/new_schema"
        - to:
            uri: ibm-watsonx-data:lakehouse
            parameters:
              apiKey: "{{ibm.apiKey}}"
              serviceUrl: "{{ibm.watsonxdata.url}}"
              catalogName: my-catalog
              engineId: my-engine
              operation: createSchema
        - log:
            message: "Schema created: ${body}"
```

### Using Dynamic Operations via Headers

_Java-only: requires Java enum WatsonxDataOperations constant_

```java
from("direct:dynamic")
    .setHeader("CamelIBMWatsonxDataOperation", constant(WatsonxDataOperations.listPrestoEngines))
    .to("ibm-watsonx-data:lakehouse?apiKey={{ibm.apiKey}}&serviceUrl={{ibm.watsonxdata.url}}")
    .log("Engines: ${body}");
```