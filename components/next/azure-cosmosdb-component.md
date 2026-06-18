# Azure CosmosDB

**Since Camel 3.10**

**Both producer and consumer are supported**

[Azure Cosmos DB](https://azure.microsoft.com/en-us/services/cosmos-db/) is Microsoft’s globally distributed, multimodel database service for operational and analytics workloads. It offers multi-mastering feature by automatically scaling throughput, compute, and storage. This component interacts with Azure CosmosDB through Azure SQL API.

Prerequisites

You must have a valid Windows Azure Storage account. More information is available at [Azure Documentation Portal](https://docs.microsoft.com/azure/).

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-cosmosdb</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

```text
azure-cosmosdb://[databaseName][/containerName][?options]
```

In case of the consumer, `databaseName`, `containerName` are required, In case of the producer, it depends on the operation that being requested, for example if operation is on a database level, e.b: deleteDatabase, only `databaseName` is required, but in case of operation being requested in container level, e.g: readItem, then `databaseName` and `containerName` are required.

You can append query options to the URI in the following format, `?options=value&option2=value&`…​

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

The Azure CosmosDB component supports 31 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientTelemetryEnabled** (common) | Sets the flag to enable client telemetry which will periodically collect database operations aggregation statistics, system information like cpu/memory and send it to cosmos monitoring service, which will be helpful during debugging. DEFAULT value is false indicating this is an opt-in feature, by default no telemetry collection. | false | boolean |
| **configuration** (common) | The component configurations. |  | CosmosDbConfiguration |
| **connectionSharingAcrossClientsEnabled** (common) | Enables connections sharing across multiple Cosmos Clients. The default is false. When you have multiple instances of Cosmos Client in the same JVM interacting with multiple Cosmos accounts, enabling this allows connection sharing in Direct mode if possible between instances of Cosmos Client. Please note, when setting this option, the connection configuration (e.g., socket timeout config, idle timeout config) of the first instantiated client will be used for all other client instances. | false | boolean |
| **consistencyLevel** (common) | 
Sets the consistency levels supported for Azure Cosmos DB client operations in the Azure Cosmos DB service. The requested ConsistencyLevel must match or be weaker than that provisioned for the database account. Consistency levels by order of strength are STRONG, BOUNDED\_STALENESS, SESSION and EVENTUAL. Refer to consistency level documentation for additional details: [https://docs.microsoft.com/en-us/azure/cosmos-db/consistency-levels](https://docs.microsoft.com/en-us/azure/cosmos-db/consistency-levels).

Enum values:

-   Strong
    
-   BoundedStaleness
    
-   Session
    
-   Eventual
    
-   ConsistentPrefix
    





 | SESSION | ConsistencyLevel |
| **containerPartitionKeyPath** (common) | Sets the container partition key path. |  | String |
| **contentResponseOnWriteEnabled** (common) | Sets the boolean to only return the headers and status code in Cosmos DB response in case of Create, Update and Delete operations on CosmosItem. In Consumer, it is enabled by default because of the ChangeFeed in the consumer that needs this flag to be enabled, and thus it shouldn’t be overridden. In Producer, it is advised to disable it since it reduces the network overhead. | true | boolean |
| **cosmosAsyncClient** (common) | **Autowired** Inject an external CosmosAsyncClient into the component which provides a client-side logical representation of the Azure Cosmos DB service. This asynchronous client is used to configure and execute requests against the service. |  | CosmosAsyncClient |
| **createContainerIfNotExists** (common) | Sets if the component should create the Cosmos container automatically in case it doesn’t exist in the Cosmos database. | false | boolean |
| **createDatabaseIfNotExists** (common) | Sets if the component should create the Cosmos database automatically in case it doesn’t exist in the Cosmos account. | false | boolean |
| **databaseEndpoint** (common) | **Required** Sets the Azure Cosmos database endpoint the component will connect to. |  | String |
| **multipleWriteRegionsEnabled** (common) | Sets the flag to enable writes on any regions for geo-replicated database accounts in the Azure Cosmos DB service. When the value of this property is true, the SDK will direct write operations to available writable regions of geo-replicated database account. Writable regions are ordered by PreferredRegions property. Setting the property value to true has no effect until EnableMultipleWriteRegions in DatabaseAccount is also set to true. DEFAULT value is true indicating that writes are directed to available writable regions of geo-replicated database account. | true | boolean |
| **preferredRegions** (common) | Sets the comma separated preferred regions for geo-replicated database accounts. For example, East US as the preferred region. When EnableEndpointDiscovery is true and PreferredRegions is non-empty, the SDK will prefer to use the regions in the container in the order they are specified to perform operations. |  | String |
| **readRequestsFallbackEnabled** (common) | Sets whether to allow for reads to go to multiple regions configured on an account of Azure Cosmos DB service. DEFAULT value is true. If this property is not set, the default is true for all Consistency Levels other than Bounded Staleness, The default is false for Bounded Staleness. 1. endpointDiscoveryEnabled is true 2. the Azure Cosmos DB account has more than one region. | true | boolean |
| **throughputProperties** (common) | Sets throughput of the resources in the Azure Cosmos DB service. |  | ThroughputProperties |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **changeFeedProcessorOptions** (consumer) | Sets the ChangeFeedProcessorOptions to be used. Unless specifically set the default values that will be used are: maximum items per page or FeedResponse: 100 lease renew interval: 17 seconds lease acquire interval: 13 seconds lease expiration interval: 60 seconds feed poll delay: 5 seconds maximum scale count: unlimited. |  | ChangeFeedProcessorOptions |
| **createLeaseContainerIfNotExists** (consumer) | Sets if the component should create Cosmos lease container for the consumer automatically in case it doesn’t exist in Cosmos database. | false | boolean |
| **createLeaseDatabaseIfNotExists** (consumer) | Sets if the component should create the Cosmos lease database for the consumer automatically in case it doesn’t exist in the Cosmos account. | false | boolean |
| **hostName** (consumer) | Sets the hostname. The host: a host is an application instance that uses the change feed processor to listen for changes. Multiple instances with the same lease configuration can run in parallel, but each instance should have a different instance name. If not specified, this will be a generated random hostname. |  | String |
| **leaseContainerName** (consumer) | Sets the lease container which acts as a state storage and coordinates processing the change feed across multiple workers. The lease container can be stored in the same account as the monitored container or in a separate account. It will be auto-created if createLeaseContainerIfNotExists is set to true. | camel-lease | String |
| **leaseDatabaseName** (consumer) | Sets the lease database where the leaseContainerName will be stored. If it is not specified, this component will store the lease container in the same database that is specified in databaseName. It will be auto-created if createLeaseDatabaseIfNotExists is set to true. |  | String |
| **itemId** (producer) | Sets the itemId in case needed for operation on item like delete, replace. |  | String |
| **itemPartitionKey** (producer) | Sets partition key. Represents a partition key value in the Azure Cosmos DB database service. A partition key identifies the partition where the item is stored in. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 

The CosmosDB operation that can be used with this component on the producer.

Enum values:

-   listDatabases
    
-   createDatabase
    
-   queryDatabases
    
-   deleteDatabase
    
-   createContainer
    
-   replaceDatabaseThroughput
    
-   listContainers
    
-   queryContainers
    
-   deleteContainer
    
-   replaceContainerThroughput
    
-   createItem
    
-   upsertItem
    
-   deleteItem
    
-   replaceItem
    
-   readItem
    
-   readAllItems
    
-   queryItems
    





 | listDatabases | CosmosDbOperationsDefinition |
| **query** (producer) | An SQL query to execute on a given resources. To learn more about Cosmos SQL API, check this link \\{link [https://docs.microsoft.com/en-us/azure/cosmos-db/sql-query-getting-started}](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-query-getting-started}). |  | String |
| **queryRequestOptions** (producer) | Set additional QueryRequestOptions that can be used with queryItems, queryContainers, queryDatabases, listDatabases, listItems, listContainers operations. |  | CosmosQueryRequestOptions |
| **indexingPolicy** ( advanced) | The CosmosDB Indexing Policy that will be set in case of container creation, this option is related to createLeaseContainerIfNotExists and it will be taken into account when the latter is true. |  | IndexingPolicy |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accountKey** (security) | Sets either a master or readonly key used to perform authentication for accessing resource. |  | String |
| **credentialType** (security) | 

Determines the credential strategy to adopt.

Enum values:

-   SHARED\_ACCOUNT\_KEY
    
-   AZURE\_IDENTITY
    





 | SHARED\_ACCOUNT\_KEY | CredentialType |

## Endpoint Options

The Azure CosmosDB endpoint is configured using URI syntax:

azure-cosmosdb:databaseName/containerName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **databaseName** (common) | The name of the Cosmos database that component should connect to. In case you are producing data and have createDatabaseIfNotExists=true, the component will automatically auto create a Cosmos database. |  | String |
| **containerName** (common) | The name of the Cosmos container that component should connect to. In case you are producing data and have createContainerIfNotExists=true, the component will automatically auto create a Cosmos container. |  | String |

### Query Parameters (31 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientTelemetryEnabled** (common) | Sets the flag to enable client telemetry which will periodically collect database operations aggregation statistics, system information like cpu/memory and send it to cosmos monitoring service, which will be helpful during debugging. DEFAULT value is false indicating this is an opt-in feature, by default no telemetry collection. | false | boolean |
| **connectionSharingAcrossClientsEnabled** (common) | Enables connections sharing across multiple Cosmos Clients. The default is false. When you have multiple instances of Cosmos Client in the same JVM interacting with multiple Cosmos accounts, enabling this allows connection sharing in Direct mode if possible between instances of Cosmos Client. Please note, when setting this option, the connection configuration (e.g., socket timeout config, idle timeout config) of the first instantiated client will be used for all other client instances. | false | boolean |
| **consistencyLevel** (common) | 
Sets the consistency levels supported for Azure Cosmos DB client operations in the Azure Cosmos DB service. The requested ConsistencyLevel must match or be weaker than that provisioned for the database account. Consistency levels by order of strength are STRONG, BOUNDED\_STALENESS, SESSION and EVENTUAL. Refer to consistency level documentation for additional details: [https://docs.microsoft.com/en-us/azure/cosmos-db/consistency-levels](https://docs.microsoft.com/en-us/azure/cosmos-db/consistency-levels).

Enum values:

-   Strong
    
-   BoundedStaleness
    
-   Session
    
-   Eventual
    
-   ConsistentPrefix
    





 | SESSION | ConsistencyLevel |
| **containerPartitionKeyPath** (common) | Sets the container partition key path. |  | String |
| **contentResponseOnWriteEnabled** (common) | Sets the boolean to only return the headers and status code in Cosmos DB response in case of Create, Update and Delete operations on CosmosItem. In Consumer, it is enabled by default because of the ChangeFeed in the consumer that needs this flag to be enabled, and thus it shouldn’t be overridden. In Producer, it is advised to disable it since it reduces the network overhead. | true | boolean |
| **cosmosAsyncClient** (common) | **Autowired** Inject an external CosmosAsyncClient into the component which provides a client-side logical representation of the Azure Cosmos DB service. This asynchronous client is used to configure and execute requests against the service. |  | CosmosAsyncClient |
| **createContainerIfNotExists** (common) | Sets if the component should create the Cosmos container automatically in case it doesn’t exist in the Cosmos database. | false | boolean |
| **createDatabaseIfNotExists** (common) | Sets if the component should create the Cosmos database automatically in case it doesn’t exist in the Cosmos account. | false | boolean |
| **databaseEndpoint** (common) | **Required** Sets the Azure Cosmos database endpoint the component will connect to. |  | String |
| **multipleWriteRegionsEnabled** (common) | Sets the flag to enable writes on any regions for geo-replicated database accounts in the Azure Cosmos DB service. When the value of this property is true, the SDK will direct write operations to available writable regions of geo-replicated database account. Writable regions are ordered by PreferredRegions property. Setting the property value to true has no effect until EnableMultipleWriteRegions in DatabaseAccount is also set to true. DEFAULT value is true indicating that writes are directed to available writable regions of geo-replicated database account. | true | boolean |
| **preferredRegions** (common) | Sets the comma separated preferred regions for geo-replicated database accounts. For example, East US as the preferred region. When EnableEndpointDiscovery is true and PreferredRegions is non-empty, the SDK will prefer to use the regions in the container in the order they are specified to perform operations. |  | String |
| **readRequestsFallbackEnabled** (common) | Sets whether to allow for reads to go to multiple regions configured on an account of Azure Cosmos DB service. DEFAULT value is true. If this property is not set, the default is true for all Consistency Levels other than Bounded Staleness, The default is false for Bounded Staleness. 1. endpointDiscoveryEnabled is true 2. the Azure Cosmos DB account has more than one region. | true | boolean |
| **throughputProperties** (common) | Sets throughput of the resources in the Azure Cosmos DB service. |  | ThroughputProperties |
| **changeFeedProcessorOptions** (consumer) | Sets the ChangeFeedProcessorOptions to be used. Unless specifically set the default values that will be used are: maximum items per page or FeedResponse: 100 lease renew interval: 17 seconds lease acquire interval: 13 seconds lease expiration interval: 60 seconds feed poll delay: 5 seconds maximum scale count: unlimited. |  | ChangeFeedProcessorOptions |
| **createLeaseContainerIfNotExists** (consumer) | Sets if the component should create Cosmos lease container for the consumer automatically in case it doesn’t exist in Cosmos database. | false | boolean |
| **createLeaseDatabaseIfNotExists** (consumer) | Sets if the component should create the Cosmos lease database for the consumer automatically in case it doesn’t exist in the Cosmos account. | false | boolean |
| **hostName** (consumer) | Sets the hostname. The host: a host is an application instance that uses the change feed processor to listen for changes. Multiple instances with the same lease configuration can run in parallel, but each instance should have a different instance name. If not specified, this will be a generated random hostname. |  | String |
| **leaseContainerName** (consumer) | Sets the lease container which acts as a state storage and coordinates processing the change feed across multiple workers. The lease container can be stored in the same account as the monitored container or in a separate account. It will be auto-created if createLeaseContainerIfNotExists is set to true. | camel-lease | String |
| **leaseDatabaseName** (consumer) | Sets the lease database where the leaseContainerName will be stored. If it is not specified, this component will store the lease container in the same database that is specified in databaseName. It will be auto-created if createLeaseDatabaseIfNotExists is set to true. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **itemId** (producer) | Sets the itemId in case needed for operation on item like delete, replace. |  | String |
| **itemPartitionKey** (producer) | Sets partition key. Represents a partition key value in the Azure Cosmos DB database service. A partition key identifies the partition where the item is stored in. |  | String |
| **operation** (producer) | 

The CosmosDB operation that can be used with this component on the producer.

Enum values:

-   listDatabases
    
-   createDatabase
    
-   queryDatabases
    
-   deleteDatabase
    
-   createContainer
    
-   replaceDatabaseThroughput
    
-   listContainers
    
-   queryContainers
    
-   deleteContainer
    
-   replaceContainerThroughput
    
-   createItem
    
-   upsertItem
    
-   deleteItem
    
-   replaceItem
    
-   readItem
    
-   readAllItems
    
-   queryItems
    





 | listDatabases | CosmosDbOperationsDefinition |
| **query** (producer) | An SQL query to execute on a given resources. To learn more about Cosmos SQL API, check this link \\{link [https://docs.microsoft.com/en-us/azure/cosmos-db/sql-query-getting-started}](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-query-getting-started}). |  | String |
| **queryRequestOptions** (producer) | Set additional QueryRequestOptions that can be used with queryItems, queryContainers, queryDatabases, listDatabases, listItems, listContainers operations. |  | CosmosQueryRequestOptions |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **indexingPolicy** ( advanced) | The CosmosDB Indexing Policy that will be set in case of container creation, this option is related to createLeaseContainerIfNotExists and it will be taken into account when the latter is true. |  | IndexingPolicy |
| **accountKey** (security) | Sets either a master or readonly key used to perform authentication for accessing resource. |  | String |
| **credentialType** (security) | 

Determines the credential strategy to adopt.

Enum values:

-   SHARED\_ACCOUNT\_KEY
    
-   AZURE\_IDENTITY
    





 | SHARED\_ACCOUNT\_KEY | CredentialType |

## Usage

### Authentication Information

To use this component, you have two options to provide the required Azure authentication information:

-   Provide `accountKey` and `databaseEndpoint` for your Azure CosmosDB account. The account key can be generated through your CosmosDB Azure portal.
    
-   Provide a [CosmosAsyncClient](https://docs.microsoft.com/en-us/java/api/com.azure.cosmos.cosmosasyncclient?view=azure-java-stable) instance which can be provided into `cosmosAsyncClient`.
    

### Async Consumer and Producer

This component implements the async Consumer and producer.

This allows camel route to consume and produce events asynchronously without blocking any threads.

### Message headers evaluated by the component producer

   
| Header | Variable Name | Type | Description |
| --- | --- | --- | --- |
| `CamelAzureCosmosDbDatabaseName` | `CosmosDbConstants.DATABASE_NAME` | `String` | Overrides the database name which is the name of the Cosmos database that component should connect to. In case you are producing data and have createDatabaseIfNotExists=true, the component will automatically auto create a Cosmos database. |
| `CamelAzureCosmosDbContainerName` | `CosmosDbConstants.CONTAINER_NAME` | `String` | Overrides the container name which is the name of the Cosmos container that component should connect to. In case you are producing data and have createContainerIfNotExists=true, the component will automatically auto create a Cosmos container. |
| `CamelAzureCosmosDbOperation` | `CosmosDbConstants.OPERATION` | `CosmosDbOperationsDefinition` | Set the producer operation which can be used to execute a specific operation on the producer. |
| `CamelAzureCosmosDbQuery` | `CosmosDbConstants.QUERY` | `String` | Set the SQL query to execute on a given producer query operations. |
| `CamelAzureCosmosDbQueryRequestOptions` | `CosmosDbConstants.QUERY_REQUEST_OPTIONS` | `CosmosQueryRequestOptions` | Set additional QueryRequestOptions that can be used with queryItems, queryContainers, queryDatabases, listDatabases, listItems, listContainers operations. |
| `CamelAzureCosmosDbCreateDatabaseIfNotExist` | `CosmosDbConstants.CREATE_DATABASE_IF_NOT_EXIST` | `boolean` | Sets if the component should create the Cosmos database automatically in case it doesn’t exist in the Cosmos account. |
| `CamelAzureCosmosDbCreateContainerIfNotExist` | `CosmosDbConstants.CREATE_CONTAINER_IF_NOT_EXIST` | `boolean` | Sets if the component should create Cosmos container automatically in case it doesn’t exist in the Cosmos account. |
| `CamelAzureCosmosDbThroughputProperties` | `CosmosDbConstants.THROUGHPUT_PROPERTIES` | `ThroughputProperties` | Sets throughput of the resources in the Azure Cosmos DB service. |
| `CamelAzureCosmosDbDatabaseRequestOptions` | `CosmosDbConstants.DATABASE_REQUEST_OPTIONS` | `CosmosDatabaseRequestOptions` | Sets additional options to execute on database operations. |
| `CamelAzureCosmosDbContainerPartitionKeyPath` | `CosmosDbConstants.CONTAINER_PARTITION_KEY_PATH` | `String` | Set the container partition key path. |
| `CamelAzureCosmosDbContainerRequestOptions` | `CosmosDbConstants.CONTAINER_REQUEST_OPTIONS` | `CosmosContainerRequestOptions` | Set additional options to execute on container operations. |
| `CamelAzureCosmosDbItemPartitionKey` | `CosmosDbConstants.ITEM_PARTITION_KEY` | `String` | Set the partition key. Represents a partition key value in the Azure Cosmos DB database service. A partition key identifies the partition where the item is stored in. |
| `CamelAzureCosmosDbItemRequestOptions` | `CosmosDbConstants.ITEM_REQUEST_OPTIONS` | `CosmosItemRequestOptions` | Set additional options to execute on item operations. |
| `CamelAzureCosmosDbItemId` | `CosmosDbConstants.ITEM_ID` | `String` | Set the itemId in case needed for operation on item like _delete_, _replace_. |

### Message headers set by the component producer

   
| Header | Variable Name | Type | Description |
| --- | --- | --- | --- |
| `CamelAzureCosmosDbRecourseId` | `CosmosDbConstants.RESOURCE_ID` | `String` | The resource ID of the requested resource. |
| `CamelAzureCosmosDbEtag` | `CosmosDbConstants.E_TAG` | `String` | The Etag ID of the requested resource. |
| `CamelAzureCosmosDbTimestamp` | `CosmosDbConstants.TIMESTAMP` | `String` | The timestamp of the requested resource. |
| `CamelAzureCosmosDbResponseHeaders` | `CosmosDbConstants.RESPONSE_HEADERS` | `Map` | The response headers of the requested resource. |
| `CamelAzureCosmosDbStatusCode` | `CosmosDbConstants.STATUS_CODE` | `Integer` | The status code of the requested resource. |
| `CamelAzureCosmosDbDefaultTimeToLiveInSeconds` | `CosmosDbConstants.DEFAULT_TIME_TO_LIVE_SECONDS` | `Integer` | The TTL of the requested resource. |
| `CamelAzureCosmosDbManualThroughput` | `CosmosDbConstants.MANUAL_THROUGHPUT` | `Integer` | The manual throughput of the requested resource. |
| `CamelAzureCosmosDbAutoscaleMaxThroughput` | `CosmosDbConstants.AUTOSCALE_MAX_THROUGHPUT` | `Integer` | The AutoscaleMaxThroughput of the requested resource. |

### Azure CosmosDB Producer operations

Camel Azure CosmosDB component provides a wide range of operations on the producer side:

**Operations on the service level**

For these operations, `databaseName` is **required** except for `queryDatabases` and `listDatabases` operations.

 
| Operation | Description |
| --- | --- |
| `listDatabases` | Gets a list of all databases as `List<CosmosDatabaseProperties>` set in the exchange message body. |
| `createDatabase` | Create a database in the specified Azure CosmosDB account. |
| `queryDatabases` | **`query` is required** Execute an SQL query against the service level in order for example return only a small subset of the databases list. It will set `List<CosmosDatabaseProperties>` set in the exchange message body. |

**Operations on the database level**

For these operations, `databaseName` is **required** for all operations here and `containerName` only for `createContainer` and `queryContainers`.

 
| Operation | Description |
| --- | --- |
| `deleteDatabase` | Delete a database from the Azure CosmosDB account. |
| `createContainer` | Create a container in the specified Azure CosmosDB database. |
| `replaceDatabaseThroughput` | Replace the throughput for the specified Azure CosmosDB database. |
| `listContainers` | Gets a list of all containers in the specified database as `List<CosmosContainerProperties>` set in the exchange message body. |
| `queryContainers` | **`query` is required** Executes an SQL query against the database level in order for example return only a small subset of the container list for the specified database. It will set `List<CosmosContainerProperties>` set in the exchange message body. |

**Operations on the container level**

For these operations, `databaseName` and `containerName` is **required** for all operations here.

 
| Operation | Description |
| --- | --- |
| `deleteContainer` | Delete a container from the specified Azure CosmosDB database. |
| `replaceContainerThroughput` | Replace the throughput for the specified Azure CosmosDB container. |
| `createItem` | **`itemPartitionKey` is required** Creates an item in the specified container, it accepts POJO or key value as `Map<String, ?>`. |
| `upsertItem` | **`itemPartitionKey` is required** Creates an item in the specified container if it doesn’t exist otherwise overwrite it if it exists, it accepts POJO or key value as `Map<String, ?>`. |
| `replaceItem` | **`itemPartitionKey` and `itemId` are required** Overwrites an item in the specified container, it accepts POJO or key value as `Map<String, ?>`. |
| `deleteItem` | **`itemPartitionKey` and `itemId` are required** Deletes an item in the specified container. |
| `readItem` | **`itemPartitionKey` and `itemId` are required** Gets an item in the specified container as `Map<String,?>` set in the exchange body message. |
| `readItem` | **`itemPartitionKey`** Gets a list of items in the specified container per the `itemPartitionKey` as `List<Map<String,?>>` set in the exchange body message. |
| `queryItems` | **`query` is required** Execute an SQL query against the container level in order, for example, return only matching items per the SQL query. It will set `List<Map<String,>?>` in the exchange message body. |

Refer to the example section in this page to learn how to use these operations into your camel application.

## Examples

### Consuming records from a specific container

For example, to consume records from a specific container in a specific database to a file, use the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-cosmosdb://camelDb/myContainer?accountKey=MyaccountKey&databaseEndpoint=https//myazure.com:443&leaseDatabaseName=myLeaseDB&createLeaseDatabaseIfNotExists=true&createLeaseContainerIfNotExists=true")
    .to("file://directory");
```

```xml
<route>
    <from uri="azure-cosmosdb://camelDb/myContainer?accountKey=MyaccountKey&amp;databaseEndpoint=https//myazure.com:443&amp;leaseDatabaseName=myLeaseDB&amp;createLeaseDatabaseIfNotExists=true&amp;createLeaseContainerIfNotExists=true"/>
    <to uri="file://directory"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-cosmosdb://camelDb/myContainer
      parameters:
        accountKey: MyaccountKey
        databaseEndpoint: "https//myazure.com:443"
        leaseDatabaseName: myLeaseDB
        createLeaseDatabaseIfNotExists: true
        createLeaseContainerIfNotExists: true
    steps:
      - to:
          uri: file://directory
```

### Operations

-   `listDatabases`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("azure-cosmosdb://?operation=listDatabases")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="azure-cosmosdb://?operation=listDatabases"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: listDatabases
        - to:
            uri: mock:result
```

-   `createDatabase`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureCosmosDbDatabaseName", constant("myDb"))
    .to("azure-cosmosdb://?operation=createDatabase")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureCosmosDbDatabaseName">
    <constant>myDb</constant>
  </setHeader>
  <to uri="azure-cosmosdb://?operation=createDatabase"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureCosmosDbDatabaseName
            constant: myDb
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: createDatabase
        - to:
            uri: mock:result
```

-   `deleteDatabase`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureCosmosDbDatabaseName", constant("myDb"))
    .to("azure-cosmosdb://?operation=deleteDatabase")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureCosmosDbDatabaseName">
    <constant>myDb</constant>
  </setHeader>
  <to uri="azure-cosmosdb://?operation=deleteDatabase"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureCosmosDbDatabaseName
            constant: myDb
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: deleteDatabase
        - to:
            uri: mock:result
```

-   `createContainer`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureCosmosDbDatabaseName", constant("databaseName"))
    .setHeader("CamelAzureCosmosDbContainerName", constant("containerName"))
    .setHeader("CamelAzureCosmosDbContainerPartitionKeyPath", constant("path"))
    .setHeader("CamelAzureCosmosDbCreateDatabaseIfNotExist", constant(true))
    .to("azure-cosmosdb://?operation=createContainer")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureCosmosDbDatabaseName">
    <constant>databaseName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbContainerName">
    <constant>containerName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbContainerPartitionKeyPath">
    <constant>path</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbCreateDatabaseIfNotExist">
    <constant>true</constant>
  </setHeader>
  <to uri="azure-cosmosdb://?operation=createContainer"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureCosmosDbDatabaseName
            constant: databaseName
        - setHeader:
            name: CamelAzureCosmosDbContainerName
            constant: containerName
        - setHeader:
            name: CamelAzureCosmosDbContainerPartitionKeyPath
            constant: path
        - setHeader:
            name: CamelAzureCosmosDbCreateDatabaseIfNotExist
            constant: true
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: createContainer
        - to:
            uri: mock:result
```

-   `deleteContainer`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureCosmosDbDatabaseName", constant("databaseName"))
    .setHeader("CamelAzureCosmosDbContainerName", constant("containerName"))
    .to("azure-cosmosdb://?operation=deleteContainer")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureCosmosDbDatabaseName">
    <constant>databaseName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbContainerName">
    <constant>containerName</constant>
  </setHeader>
  <to uri="azure-cosmosdb://?operation=deleteContainer"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureCosmosDbDatabaseName
            constant: databaseName
        - setHeader:
            name: CamelAzureCosmosDbContainerName
            constant: containerName
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: deleteContainer
        - to:
            uri: mock:result
```

-   `replaceDatabaseThroughput`:
    

_Java-only: requires SDK ThroughputProperties object_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelAzureCosmosDbDatabaseName", "databaseName");
        exchange.getIn().setHeader("CamelAzureCosmosDbThroughputProperties",
                ThroughputProperties.createManualThroughput(700));
    })
    .to("azure-cosmosdb://?operation=replaceDatabaseThroughput")
    .to("mock:result");
```

-   `queryContainers`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureCosmosDbDatabaseName", constant("databaseName"))
    .setHeader("CamelAzureCosmosDbQuery", constant("SELECT * from c where c.id = 'myAwesomeContainer'"))
    .to("azure-cosmosdb://?operation=queryContainers")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureCosmosDbDatabaseName">
    <constant>databaseName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbQuery">
    <constant>SELECT * from c where c.id = 'myAwesomeContainer'</constant>
  </setHeader>
  <to uri="azure-cosmosdb://?operation=queryContainers"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureCosmosDbDatabaseName
            constant: databaseName
        - setHeader:
            name: CamelAzureCosmosDbQuery
            constant: "SELECT * from c where c.id = 'myAwesomeContainer'"
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: queryContainers
        - to:
            uri: mock:result
```

-   `createItem`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureCosmosDbDatabaseName", constant("databaseName"))
    .setHeader("CamelAzureCosmosDbContainerName", constant("containerName"))
    .setHeader("CamelAzureCosmosDbContainerPartitionKeyPath", constant("partition"))
    .setHeader("CamelAzureCosmosDbItemPartitionKey", constant("test-1"))
    .setBody(constant("{\"id\":\"test-id-1\",\"partition\":\"test-1\",\"field1\":\"awesome!\"}"))
    .to("azure-cosmosdb://?operation=createItem")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureCosmosDbDatabaseName">
    <constant>databaseName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbContainerName">
    <constant>containerName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbContainerPartitionKeyPath">
    <constant>partition</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbItemPartitionKey">
    <constant>test-1</constant>
  </setHeader>
  <setBody>
    <constant>{"id":"test-id-1","partition":"test-1","field1":"awesome!"}</constant>
  </setBody>
  <to uri="azure-cosmosdb://?operation=createItem"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureCosmosDbDatabaseName
            constant: databaseName
        - setHeader:
            name: CamelAzureCosmosDbContainerName
            constant: containerName
        - setHeader:
            name: CamelAzureCosmosDbContainerPartitionKeyPath
            constant: partition
        - setHeader:
            name: CamelAzureCosmosDbItemPartitionKey
            constant: "test-1"
        - setBody:
            constant: '{"id":"test-id-1","partition":"test-1","field1":"awesome!"}'
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: createItem
        - to:
            uri: mock:result
```

-   `replaceItem`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureCosmosDbDatabaseName", constant("databaseName"))
    .setHeader("CamelAzureCosmosDbContainerName", constant("containerName"))
    .setHeader("CamelAzureCosmosDbItemPartitionKey", constant("test-1"))
    .setHeader("CamelAzureCosmosDbItemId", constant("test-id-1"))
    .setBody(constant("{\"id\":\"test-id-1\",\"partition\":\"test-1\",\"field1\":\"awesome!\"}"))
    .to("azure-cosmosdb://?operation=replaceItem")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureCosmosDbDatabaseName">
    <constant>databaseName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbContainerName">
    <constant>containerName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbItemPartitionKey">
    <constant>test-1</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbItemId">
    <constant>test-id-1</constant>
  </setHeader>
  <setBody>
    <constant>{"id":"test-id-1","partition":"test-1","field1":"awesome!"}</constant>
  </setBody>
  <to uri="azure-cosmosdb://?operation=replaceItem"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureCosmosDbDatabaseName
            constant: databaseName
        - setHeader:
            name: CamelAzureCosmosDbContainerName
            constant: containerName
        - setHeader:
            name: CamelAzureCosmosDbItemPartitionKey
            constant: "test-1"
        - setHeader:
            name: CamelAzureCosmosDbItemId
            constant: "test-id-1"
        - setBody:
            constant: '{"id":"test-id-1","partition":"test-1","field1":"awesome!"}'
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: replaceItem
        - to:
            uri: mock:result
```

-   `deleteItem`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureCosmosDbDatabaseName", constant("databaseName"))
    .setHeader("CamelAzureCosmosDbContainerName", constant("containerName"))
    .setHeader("CamelAzureCosmosDbItemPartitionKey", constant("test-1"))
    .setHeader("CamelAzureCosmosDbItemId", constant("test-id-1"))
    .to("azure-cosmosdb://?operation=deleteItem")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureCosmosDbDatabaseName">
    <constant>databaseName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbContainerName">
    <constant>containerName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbItemPartitionKey">
    <constant>test-1</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbItemId">
    <constant>test-id-1</constant>
  </setHeader>
  <to uri="azure-cosmosdb://?operation=deleteItem"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureCosmosDbDatabaseName
            constant: databaseName
        - setHeader:
            name: CamelAzureCosmosDbContainerName
            constant: containerName
        - setHeader:
            name: CamelAzureCosmosDbItemPartitionKey
            constant: "test-1"
        - setHeader:
            name: CamelAzureCosmosDbItemId
            constant: "test-id-1"
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: deleteItem
        - to:
            uri: mock:result
```

-   `queryItems`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureCosmosDbDatabaseName", constant("databaseName"))
    .setHeader("CamelAzureCosmosDbContainerName", constant("containerName"))
    .setHeader("CamelAzureCosmosDbQuery", constant("SELECT c.id,c.field2,c.field1 from c where c.id = 'test-id-1'"))
    .to("azure-cosmosdb://?operation=queryItems")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureCosmosDbDatabaseName">
    <constant>databaseName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbContainerName">
    <constant>containerName</constant>
  </setHeader>
  <setHeader name="CamelAzureCosmosDbQuery">
    <constant>SELECT c.id,c.field2,c.field1 from c where c.id = 'test-id-1'</constant>
  </setHeader>
  <to uri="azure-cosmosdb://?operation=queryItems"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureCosmosDbDatabaseName
            constant: databaseName
        - setHeader:
            name: CamelAzureCosmosDbContainerName
            constant: containerName
        - setHeader:
            name: CamelAzureCosmosDbQuery
            constant: "SELECT c.id,c.field2,c.field1 from c where c.id = 'test-id-1'"
        - to:
            uri: azure-cosmosdb://
            parameters:
              operation: queryItems
        - to:
            uri: mock:result
```

### Azure CosmosDB Consumer

Camel Azure CosmosDB uses [ChangeFeed pattern](https://docs.microsoft.com/en-us/azure/cosmos-db/change-feed-design-patterns) to capture a feed of events and feed them into the Camel in an Async manner, something similar to the Change Data Capture (CDC) design pattern. However, it doesn’t capture deletions as these are removed from the feed as well.

To use the Camel Azure CosmosDB, `containerName` and `databaseName` are required. However, there are more options that need to be set to use this feature:

-   `leaseDatabaseName`: Sets the lease database where the `leaseContainerName` will be stored. If it is not specified, this component will store the lease container in the same database that is specified in databaseName. It will be auto-created if `createLeaseDatabaseIfNotExists` is set to true.
    
-   `leaseContainerName`: Sets the lease container which acts as a state storage and coordinates processing the change feed across multiple workers. The lease container can be stored in the same account as the monitored container or in a separate account. It will be auto-created if `createLeaseContainerIfNotExists` is set to true. If not specified, this component will create container called `camel-lease`.
    
-   `hostName`: Sets the hostname. The host: a host is an application instance that uses the change feed processor to listen for changes. Multiple instances with the same lease configuration can run in parallel, but each instance should have a different instance name. If not specified, this will be a generated random hostname.
    
-   `changeFeedProcessorOptions`: Sets additional options for the change feed processor.
    

The consumer will set `List<Map<String,>>` in exchange message body which reflect the list of items in a single feed.

#### Example

For example, to listen to the events in `myContainer` container in `myDb`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-cosmosdb://myDb/myContainer?leaseDatabaseName=myLeaseDb&createLeaseDatabaseIfNotExists=true&createLeaseContainerIfNotExists=true")
    .to("mock:result");
```

```xml
<route>
    <from uri="azure-cosmosdb://myDb/myContainer?leaseDatabaseName=myLeaseDb&amp;createLeaseDatabaseIfNotExists=true&amp;createLeaseContainerIfNotExists=true"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-cosmosdb://myDb/myContainer
      parameters:
        leaseDatabaseName: myLeaseDb
        createLeaseDatabaseIfNotExists: true
        createLeaseContainerIfNotExists: true
    steps:
      - to:
          uri: mock:result
```

## Important Development Notes

When developing on this component, you will need to obtain your Azure accessKey in order to run the integration tests. In addition to the mocked unit tests, you **will need to run the integration tests with every change you make or even client upgrade as the Azure client can break things even on minor versions upgrade.** To run the integration tests, on this component directory, run the following maven command:

```bash
mvn clean install -Dendpoint={{dbaddress}} -DaccessKey={{accessKey}}
```

Whereby `endpoint` is your Azure CosmosDB endpoint name and `accessKey` is the access key being generated from Azure CosmosDB portal.

## Spring Boot Auto-Configuration

When using azure-cosmosdb with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-azure-cosmosdb-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 32 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.azure-cosmosdb.account-key** | Sets either a master or readonly key used to perform authentication for accessing resource. |  | String |
| **camel.component.azure-cosmosdb.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.azure-cosmosdb.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.azure-cosmosdb.change-feed-processor-options** | Sets the ChangeFeedProcessorOptions to be used. Unless specifically set the default values that will be used are: maximum items per page or FeedResponse: 100 lease renew interval: 17 seconds lease acquire interval: 13 seconds lease expiration interval: 60 seconds feed poll delay: 5 seconds maximum scale count: unlimited. The option is a com.azure.cosmos.models.ChangeFeedProcessorOptions type. |  | ChangeFeedProcessorOptions |
| **camel.component.azure-cosmosdb.client-telemetry-enabled** | Sets the flag to enable client telemetry which will periodically collect database operations aggregation statistics, system information like cpu/memory and send it to cosmos monitoring service, which will be helpful during debugging. DEFAULT value is false indicating this is an opt-in feature, by default no telemetry collection. | false | Boolean |
| **camel.component.azure-cosmosdb.configuration** | The component configurations. The option is a org.apache.camel.component.azure.cosmosdb.CosmosDbConfiguration type. |  | CosmosDbConfiguration |
| **camel.component.azure-cosmosdb.connection-sharing-across-clients-enabled** | Enables connections sharing across multiple Cosmos Clients. The default is false. When you have multiple instances of Cosmos Client in the same JVM interacting with multiple Cosmos accounts, enabling this allows connection sharing in Direct mode if possible between instances of Cosmos Client. Please note, when setting this option, the connection configuration (e.g., socket timeout config, idle timeout config) of the first instantiated client will be used for all other client instances. | false | Boolean |
| **camel.component.azure-cosmosdb.consistency-level** | Sets the consistency levels supported for Azure Cosmos DB client operations in the Azure Cosmos DB service. The requested ConsistencyLevel must match or be weaker than that provisioned for the database account. Consistency levels by order of strength are STRONG, BOUNDED\_STALENESS, SESSION and EVENTUAL. Refer to consistency level documentation for additional details: [https://docs.microsoft.com/en-us/azure/cosmos-db/consistency-levels](https://docs.microsoft.com/en-us/azure/cosmos-db/consistency-levels). | session | ConsistencyLevel |
| **camel.component.azure-cosmosdb.container-partition-key-path** | Sets the container partition key path. |  | String |
| **camel.component.azure-cosmosdb.content-response-on-write-enabled** | Sets the boolean to only return the headers and status code in Cosmos DB response in case of Create, Update and Delete operations on CosmosItem. In Consumer, it is enabled by default because of the ChangeFeed in the consumer that needs this flag to be enabled, and thus it shouldn’t be overridden. In Producer, it is advised to disable it since it reduces the network overhead. | true | Boolean |
| **camel.component.azure-cosmosdb.cosmos-async-client** | Inject an external CosmosAsyncClient into the component which provides a client-side logical representation of the Azure Cosmos DB service. This asynchronous client is used to configure and execute requests against the service. The option is a com.azure.cosmos.CosmosAsyncClient type. |  | CosmosAsyncClient |
| **camel.component.azure-cosmosdb.create-container-if-not-exists** | Sets if the component should create the Cosmos container automatically in case it doesn’t exist in the Cosmos database. | false | Boolean |
| **camel.component.azure-cosmosdb.create-database-if-not-exists** | Sets if the component should create the Cosmos database automatically in case it doesn’t exist in the Cosmos account. | false | Boolean |
| **camel.component.azure-cosmosdb.create-lease-container-if-not-exists** | Sets if the component should create Cosmos lease container for the consumer automatically in case it doesn’t exist in Cosmos database. | false | Boolean |
| **camel.component.azure-cosmosdb.create-lease-database-if-not-exists** | Sets if the component should create the Cosmos lease database for the consumer automatically in case it doesn’t exist in the Cosmos account. | false | Boolean |
| **camel.component.azure-cosmosdb.credential-type** | Determines the credential strategy to adopt. | shared-account-key | CredentialType |
| **camel.component.azure-cosmosdb.database-endpoint** | Sets the Azure Cosmos database endpoint the component will connect to. |  | String |
| **camel.component.azure-cosmosdb.enabled** | Whether to enable auto configuration of the azure-cosmosdb component. This is enabled by default. |  | Boolean |
| **camel.component.azure-cosmosdb.host-name** | Sets the hostname. The host: a host is an application instance that uses the change feed processor to listen for changes. Multiple instances with the same lease configuration can run in parallel, but each instance should have a different instance name. If not specified, this will be a generated random hostname. |  | String |
| **camel.component.azure-cosmosdb.indexing-policy** | The CosmosDB Indexing Policy that will be set in case of container creation, this option is related to createLeaseContainerIfNotExists and it will be taken into account when the latter is true. The option is a com.azure.cosmos.models.IndexingPolicy type. |  | IndexingPolicy |
| **camel.component.azure-cosmosdb.item-id** | Sets the itemId in case needed for operation on item like delete, replace. |  | String |
| **camel.component.azure-cosmosdb.item-partition-key** | Sets partition key. Represents a partition key value in the Azure Cosmos DB database service. A partition key identifies the partition where the item is stored in. |  | String |
| **camel.component.azure-cosmosdb.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.azure-cosmosdb.lease-container-name** | Sets the lease container which acts as a state storage and coordinates processing the change feed across multiple workers. The lease container can be stored in the same account as the monitored container or in a separate account. It will be auto-created if createLeaseContainerIfNotExists is set to true. | camel-lease | String |
| **camel.component.azure-cosmosdb.lease-database-name** | Sets the lease database where the leaseContainerName will be stored. If it is not specified, this component will store the lease container in the same database that is specified in databaseName. It will be auto-created if createLeaseDatabaseIfNotExists is set to true. |  | String |
| **camel.component.azure-cosmosdb.multiple-write-regions-enabled** | Sets the flag to enable writes on any regions for geo-replicated database accounts in the Azure Cosmos DB service. When the value of this property is true, the SDK will direct write operations to available writable regions of geo-replicated database account. Writable regions are ordered by PreferredRegions property. Setting the property value to true has no effect until EnableMultipleWriteRegions in DatabaseAccount is also set to true. DEFAULT value is true indicating that writes are directed to available writable regions of geo-replicated database account. | true | Boolean |
| **camel.component.azure-cosmosdb.operation** | The CosmosDB operation that can be used with this component on the producer. | listdatabases | CosmosDbOperationsDefinition |
| **camel.component.azure-cosmosdb.preferred-regions** | Sets the comma separated preferred regions for geo-replicated database accounts. For example, East US as the preferred region. When EnableEndpointDiscovery is true and PreferredRegions is non-empty, the SDK will prefer to use the regions in the container in the order they are specified to perform operations. |  | String |
| **camel.component.azure-cosmosdb.query** | An SQL query to execute on a given resources. To learn more about Cosmos SQL API, check this link \\{link [https://docs.microsoft.com/en-us/azure/cosmos-db/sql-query-getting-started}](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-query-getting-started}). |  | String |
| **camel.component.azure-cosmosdb.query-request-options** | Set additional QueryRequestOptions that can be used with queryItems, queryContainers, queryDatabases, listDatabases, listItems, listContainers operations. The option is a com.azure.cosmos.models.CosmosQueryRequestOptions type. |  | CosmosQueryRequestOptions |
| **camel.component.azure-cosmosdb.read-requests-fallback-enabled** | Sets whether to allow for reads to go to multiple regions configured on an account of Azure Cosmos DB service. DEFAULT value is true. If this property is not set, the default is true for all Consistency Levels other than Bounded Staleness, The default is false for Bounded Staleness. 1. endpointDiscoveryEnabled is true 2. the Azure Cosmos DB account has more than one region. | true | Boolean |
| **camel.component.azure-cosmosdb.throughput-properties** | Sets throughput of the resources in the Azure Cosmos DB service. The option is a com.azure.cosmos.models.ThroughputProperties type. |  | ThroughputProperties |