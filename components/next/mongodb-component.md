# MongoDB

**Since Camel 2.19**

**Both producer and consumer are supported**

According to Wikipedia: "NoSQL is a movement promoting a loosely defined class of non-relational data stores that break with a long history of relational databases and ACID guarantees." NoSQL solutions have grown in popularity in the last few years, and major extremely used sites and services such as Facebook, LinkedIn, Twitter, etc. are known to use them extensively to achieve scalability and agility.

Basically, NoSQL solutions differ from traditional RDBMS (Relational Database Management Systems) in that they don’t use SQL as their query language and generally don’t offer ACID-like transactional behaviour nor relational data. Instead, they are designed around the concept of flexible data structures and schemas (meaning that the traditional concept of a database table with a fixed schema is dropped), extreme scalability on commodity hardware and blazing-fast processing.

MongoDB is a very popular NoSQL solution. The camel-mongodb component integrates Camel with MongoDB, allowing you to interact with MongoDB collections both as a producer (performing operations on the collection) and as a consumer (consuming documents from a MongoDB collection).

MongoDB revolves around the concepts of documents (not as is office documents, but rather hierarchical data defined in JSON/BSON) and collections. This component page will assume you are familiar with them. Otherwise, visit [http://www.mongodb.org/](http://www.mongodb.org/).

> **Note**
> The MongoDB Camel component uses Mongo Java Driver 4.x.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-mongodb</artifactId>
    <version>x.y.z</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI formats

mongodb:connectionBean?database=databaseName&collection=collectionName&operation=operationName\[&moreOptions...\]
mongodb:dummy?hosts=hostnames&database=databaseName&collection=collectionName&operation=operationName\[&moreOptions...\]

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

The MongoDB component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **mongoConnection** (common) | **Autowired** Shared client used for connection. All endpoints generated from the component will share this connection client. |  | MongoClient |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The MongoDB endpoint is configured using URI syntax:

mongodb:connectionBean

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionBean** (common) | **Required** Sets the connection bean reference used to lookup a client for connecting to a database if no hosts parameter is present. |  | String |

### Query Parameters (56 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (common) | Sets the name of the MongoDB collection to bind to this endpoint. |  | String |
| **collectionIndex** (common) | Sets the collection index (JSON FORMAT : \\{ field1 : order1, field2 : order2}). |  | String |
| **connectionUriString** (common) | Set the whole Connection String/Uri for mongodb endpoint. |  | String |
| **createCollection** (common) | Create the collection during initialisation if it doesn’t exist. Default is true. | true | boolean |
| **database** (common) | Sets the name of the MongoDB database to target. |  | String |
| **hosts** (common) | Host address of mongodb server in host:port format. It’s possible to also use more than one address, as a comma separated list of hosts: host1:port1,host2:port2. If this parameter is specified, the provided connectionBean is ignored. |  | String |
| **mongoConnection** (common) | Sets the connection bean used as a client for connecting to a database. |  | MongoClient |
| **operation** (common) | 
Sets the operation this endpoint will execute against MongoDB.

Enum values:

-   findById
    
-   findOneAndDelete
    
-   findOneAndReplace
    
-   findOneAndUpdate
    
-   findOneByQuery
    
-   findAll
    
-   findDistinct
    
-   insert
    
-   save
    
-   update
    
-   remove
    
-   bulkWrite
    
-   aggregate
    
-   getDbStats
    
-   getColStats
    
-   count
    
-   command
    





 |  | MongoDbOperation |
| **outputType** (common) | 

Convert the output of the producer to the selected type: DocumentList Document or MongoIterable. DocumentList or MongoIterable applies to findAll and aggregate. Document applies to all other operations.

Enum values:

-   DocumentList
    
-   Document
    
-   MongoIterable
    





 |  | MongoDbOutputType |
| **consumerType** (consumer) | 

Consumer type.

Enum values:

-   tailable
    
-   changeStreams
    





 | tailable | String |
| **fullDocument** (consumer) | 

Specifies whether changeStream consumer include a copy of the full document when modified by update operations. Possible values are default, updateLookup, required and whenAvailable.

Enum values:

-   default
    
-   updateLookup
    
-   required
    
-   whenAvailable
    





 | default | FullDocument |
| **persistentId** (consumer) | One tail tracking collection can host many trackers for several tailable consumers. To keep them separate, each tracker should have its own unique persistentId. |  | String |
| **persistentTailTracking** (consumer) | Enable persistent tail tracking, which is a mechanism to keep track of the last consumed message across system restarts. The next time the system is up, the endpoint will recover the cursor from the point where it last stopped slurping records. | false | boolean |
| **tailTrackCollection** (consumer) | Collection where tail tracking information will be persisted. If not specified, MongoDbTailTrackingConfig#DEFAULT\_COLLECTION will be used by default. |  | String |
| **tailTrackDb** (consumer) | Indicates what database the tail tracking mechanism will persist to. If not specified, the current database will be picked by default. Dynamicity will not be taken into account even if enabled, i.e., the tail tracking database will not vary past endpoint initialization. |  | String |
| **tailTrackField** (consumer) | Field where the last tracked value will be placed. If not specified, MongoDbTailTrackingConfig#DEFAULT\_FIELD will be used by default. |  | String |
| **tailTrackIncreasingField** (consumer) | Correlation field in the incoming record which is of increasing nature and will be used to position the tailing cursor every time it is generated. The cursor will be (re)created with a query of type: tailTrackIncreasingField greater than lastValue (possibly recovered from persistent tail tracking). Can be of type Integer, Date, String, etc. NOTE: No support for dot notation at the current time, so the field should be at the top level of the document. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **appName** (advanced) | Sets the logical name of the application. The application name may be used by the client to identify the application to the server, for use in server logs, slow query logs, and profile collection. Default: null. |  | String |
| **compressors** (advanced) | Specifies one or more compression algorithms that the driver will attempt to use to compress requests sent to the connected MongoDB instance. Possible values include: zlib, snappy, and zstd. Default: null. |  | String |
| **connectTimeoutMS** (advanced) | Specifies the maximum amount of time, in milliseconds, the Java driver waits for a connection to open before timing out. A value of 0 instructs the driver to never time out while waiting for a connection to open. Default: 10000 (10 seconds). | 10000 | Integer |
| **cursorRegenerationDelay** (advanced) | MongoDB tailable cursors will block until new data arrives. If no new data is inserted, after some time the cursor will be automatically freed and closed by the MongoDB server. The client is expected to regenerate the cursor if needed. This value specifies the time to wait before attempting to fetch a new cursor, and if the attempt fails, how long before the next attempt is made. Default value is 1000ms. | 1000 | long |
| **directConnection** (advanced) | Specifies that the driver must connect to the host directly. Default: false. | false | boolean |
| **dynamicity** (advanced) | Sets whether this endpoint will attempt to dynamically resolve the target database and collection from the incoming Exchange properties. Can be used to override at runtime the database and collection specified on the otherwise static endpoint URI. It is disabled by default to boost performance. Enabling it will take a minimal performance hit. | false | boolean |
| **heartbeatFrequencyMS** (advanced) | heartbeatFrequencyMS controls when the driver checks the state of the MongoDB deployment. Specify the interval (in milliseconds) between checks, counted from the end of the previous check until the beginning of the next one. Default: Single-threaded drivers: 60 seconds. Multithreaded drivers: 10 seconds. |  | Integer |
| **loadBalanced** (advanced) | If true the driver will assume that it’s connecting to MongoDB through a load balancer. | false | boolean |
| **localThresholdMS** (advanced) | The size (in milliseconds) of the latency window for selecting among multiple suitable MongoDB instances. Default: 15 milliseconds. | 15 | Integer |
| **maxConnecting** (advanced) | Specifies the maximum number of connections a pool may be establishing concurrently. Default: 2. | 2 | Integer |
| **maxIdleTimeMS** (advanced) | Specifies the maximum amount of time, in milliseconds, the Java driver will allow a pooled connection to idle before closing the connection. A value of 0 indicates that there is no upper bound on how long the driver can allow a pooled collection to be idle. Default: 0. | 0 | Integer |
| **maxLifeTimeMS** (advanced) | Specifies the maximum amount of time, in milliseconds, the Java driver will continue to use a pooled connection before closing the connection. A value of 0 indicates that there is no upper bound on how long the driver can keep a pooled connection open. Default: 0. | 0 | Integer |
| **maxPoolSize** (advanced) | The maximum number of connections in the connection pool. The default value is 100. | 100 | Integer |
| **maxStalenessSeconds** (advanced) | Specifies, in seconds, how stale a secondary can be before the driver stops communicating with that secondary. The minimum value is either 90 seconds or the heartbeat frequency plus 10 seconds, whichever is greater. For more information, see the server documentation for the maxStalenessSeconds option. Not providing a parameter or explicitly specifying -1 indicates that there should be no staleness check for secondaries. Default: -1. | \-1 | Integer |
| **minPoolSize** (advanced) | Specifies the minimum number of connections that must exist at any moment in a single connection pool. Default: 0. | 0 | Integer |
| **readPreference** (advanced) | 

Configure how MongoDB clients route read operations to the members of a replica set. Possible values are PRIMARY, PRIMARY\_PREFERRED, SECONDARY, SECONDARY\_PREFERRED or NEAREST.

Enum values:

-   PRIMARY
    
-   PRIMARY\_PREFERRED
    
-   SECONDARY
    
-   SECONDARY\_PREFERRED
    
-   NEAREST
    





 | PRIMARY | String |
| **readPreferenceTags** (advanced) | A representation of a tag set as a comma-separated list of colon-separated key-value pairs, e.g. dc:ny,rack:1. Spaces are stripped from the beginning and end of all keys and values. To specify a list of tag sets, using multiple readPreferenceTags, e.g., readPreferenceTags=dc:ny,rack:1;readPreferenceTags=dc:ny;readPreferenceTags= Note the empty value for the last one, which means match any secondary as a last resort. Order matters when using multiple readPreferenceTags. |  | String |
| **replicaSet** (advanced) | Specifies that the connection string provided includes multiple hosts. When specified, the driver attempts to find all members of that set. |  | String |
| **retryReads** (advanced) | Specifies that the driver must retry supported read operations if they fail due to a network error. Default: true. | true | boolean |
| **retryWrites** (advanced) | Specifies that the driver must retry supported write operations if they fail due to a network error. Default: true. | true | boolean |
| **serverSelectionTimeoutMS** (advanced) | Specifies how long (in milliseconds) to block for server selection before throwing an exception. Default: 30,000 milliseconds. | 30000 | Integer |
| **socketTimeoutMS** (advanced) | Specifies the maximum amount of time, in milliseconds, the Java driver will wait to send or receive a request before timing out. A value of 0 instructs the driver to never time out while waiting to send or receive a request. Default: 0. | 0 | Integer |
| **srvMaxHosts** (advanced) | The maximum number of hosts from the SRV record to connect to. |  | Integer |
| **srvServiceName** (advanced) | Specifies the service name of the SRV resource recordsthe driver retrieves to construct your seed list. You must use the DNS Seed List Connection Format in your connection URI to use this option. Default: mongodb. | mongodb | String |
| **waitQueueTimeoutMS** (advanced) | Specifies the maximum amount of time, in milliseconds that a thread may wait for a connection to become available. Default: 120000 (120 seconds). | 120000 | Integer |
| **writeConcern** (advanced) | 

Configure the connection bean with the level of acknowledgment requested from MongoDB for write operations to a standalone mongod, replicaset or cluster. Possible values are ACKNOWLEDGED, W1, W2, W3, UNACKNOWLEDGED, JOURNALED or MAJORITY.

Enum values:

-   ACKNOWLEDGED
    
-   W1
    
-   W2
    
-   W3
    
-   UNACKNOWLEDGED
    
-   JOURNALED
    
-   MAJORITY
    





 | ACKNOWLEDGED | String |
| **writeResultAsHeader** (advanced) | In write operations, it determines whether instead of returning WriteResult as the body of the OUT message, we transfer the IN message to the OUT and attach the WriteResult as a header. | false | boolean |
| **zlibCompressionLevel** (advanced) | Specifies the degree of compression that Zlib should use to decrease the size of requests to the connected MongoDB instance. The level can range from -1 to 9, with lower values compressing faster (but resulting in larger requests) and larger values compressing slower (but resulting in smaller requests). Default: null. |  | Integer |
| **streamFilter** (changeStream) | Filter condition for change streams consumer. |  | String |
| **authSource** (security) | The database name associated with the user’s credentials. |  | String |
| **password** (security) | User password for mongodb connection. |  | String |
| **sslContextParameters** (security) | SSL configuration using a Camel SSLContextParameters object. When configured, TLS is automatically enabled on the connection. |  | SSLContextParameters |
| **tls** (security) | Specifies that all communication with MongoDB instances should use TLS. Supersedes the ssl option. Default: false. | false | boolean |
| **tlsAllowInvalidHostnames** (security) | Specifies that the driver should allow invalid hostnames in the certificate for TLS connections. Supersedes sslInvalidHostNameAllowed. Has the same effect as tlsInsecure by setting tlsAllowInvalidHostnames to true. Default: false. | false | boolean |
| **username** (security) | Username for mongodb connection. |  | String |

## Message Headers

The MongoDB component supports 26 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMongoDbOperation** (producer) Constant: [`OPERATION_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#OPERATION_HEADER) | The operation this endpoint will execute against MongoDB. |  | MongoDbOperation or String |
| **CamelMongoDbResultTotalSize** (producer findAll) Constant: [`RESULT_TOTAL_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#RESULT_TOTAL_SIZE) | Number of objects matching the query. This does not take limit/skip into consideration. |  | Integer |
| **CamelMongoDbResultPageSize** (producer findAll) Constant: [`RESULT_PAGE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#RESULT_PAGE_SIZE) | Number of objects matching the query. This does not take limit/skip into consideration. |  | Integer |
| **CamelMongoDbCriteria** (producer) Constant: [`CRITERIA`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#CRITERIA) | The query to execute against MongoDB. |  | Bson |
| **CamelMongoDbFieldsProjection** (producer) Constant: [`FIELDS_PROJECTION`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#FIELDS_PROJECTION) | The project document. |  | Bson |
| **CamelMongoDbBatchSize** (producer findAll aggregate) Constant: [`BATCH_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#BATCH_SIZE) | The number of documents per batch. |  | Integer |
| **CamelMongoDbNumToSkip** (producer findAll) Constant: [`NUM_TO_SKIP`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#NUM_TO_SKIP) | Discards a given number of elements at the beginning of the cursor. |  | Integer |
| **CamelMongoDbMultiUpdate** (producer update) Constant: [`MULTIUPDATE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#MULTIUPDATE) | If the update should be applied to all objects matching. See [http://www.mongodb.org/display/DOCS/AtomicOperationsAtomic](http://www.mongodb.org/display/DOCS/AtomicOperationsAtomic) Operations. |  | Boolean |
| **CamelMongoDbUpsert** (producer update) Constant: [`UPSERT`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#UPSERT) | If the database should create the element if it does not exist. |  | Boolean |
| **CamelMongoDbRecordsAffected** (producer) Constant: [`RECORDS_AFFECTED`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#RECORDS_AFFECTED) | The number of modified or deleted records. |  | long |
| **CamelMongoDbRecordsMatched** (producer) Constant: [`RECORDS_MATCHED`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#RECORDS_MATCHED) | The number of documents matched by the query. |  | long |
| **CamelMongoDbSortBy** (producer) Constant: [`SORT_BY`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#SORT_BY) | The sort criteria. |  | Bson or Document |
| **CamelMongoDbDatabase** (common) Constant: [`DATABASE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#DATABASE) | The name of the MongoDB database to target. |  | String |
| **CamelMongoDbCollection** (common) Constant: [`COLLECTION`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#COLLECTION) | The name of the MongoDB collection to bind to this endpoint. |  | String |
| **CamelMongoDbCollectionIndex** (producer) Constant: [`COLLECTION_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#COLLECTION_INDEX) | The list of dynamic indexes to create on the fly. |  | List |
| **CamelMongoDbLimit** (producer findAll) Constant: [`LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#LIMIT) | Limits the number of elements returned. |  | Integer |
| **CamelMongoDbTailable** (consumer) Constant: [`FROM_TAILABLE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#FROM_TAILABLE) | Is from tailable. |  | Boolean |
| **CamelMongoWriteResult** (producer) Constant: [`WRITERESULT`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#WRITERESULT) | The result of the write operation. |  | Object |
| **CamelMongoOid** (producer) Constant: [`OID`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#OID) | The OID(s) of the inserted record(s). |  | Object or List |
| **CamelMongoDbDistinctQueryField** (producer) Constant: [`DISTINCT_QUERY_FIELD`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#DISTINCT_QUERY_FIELD) | The specified field name fow which we want to get the distinct values. |  | String |
| **CamelMongoDbAllowDiskUse** (producer findAll aggregate) Constant: [`ALLOW_DISK_USE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#ALLOW_DISK_USE) | Sets allowDiskUse MongoDB flag. This is supported since MongoDB Server 4.3.1. Using this header with older MongoDB Server version can cause query to fail. |  | Boolean |
| **CamelMongoDbBulkOrdered** (producer bulkWrite) Constant: [`BULK_ORDERED`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#BULK_ORDERED) | Perform an ordered or unordered operation execution. | TRUE | Boolean |
| **\_id** (consumer changeStreams) Constant: [`MONGO_ID`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#MONGO_ID) | A document that contains the \_id of the document created or modified by the insert, replace, delete, update operations (i.e. CRUD operations). For sharded collections, also displays the full shard key for the document. The \_id field is not repeated if it is already a part of the shard key. |  | ObjectId |
| **CamelMongoDbStreamOperationType** (consumer changeStreams) Constant: [`STREAM_OPERATION_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#STREAM_OPERATION_TYPE) | The type of operation that occurred. Can be any of the following values: insert, delete, replace, update, drop, rename, dropDatabase, invalidate. |  | String |
| **CamelMongoDbReturnDocumentType** (producer update one and return) Constant: [`RETURN_DOCUMENT`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#RETURN_DOCUMENT) | 
Indicates which document to return, the document before or after an update and return atomic operation.

Enum values:

-   BEFORE
    
-   AFTER
    





 |  | ReturnDocument |
| **CamelMongoDbOperationOption** (producer update one and options) Constant: [`OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-mongodb/latest/org/apache/camel/component/mongodb/MongoDbConstants.html#OPTIONS) | Options to use. When set, options set in the headers will be ignored. |  | Object |

## Usage

### Configuration of a database in Spring XML

The following Spring XML creates a bean defining the connection to a MongoDB instance.

Since mongo java driver 3, the WriteConcern and readPreference options have not been dynamically modifiable. They are defined in the mongoClient object:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:mongo="http://www.springframework.org/schema/data/mongo"
xsi:schemaLocation="http://www.springframework.org/schema/context
      http://www.springframework.org/schema/context/spring-context.xsd
      http://www.springframework.org/schema/data/mongo
      http://www.springframework.org/schema/data/mongo/spring-mongo.xsd
      http://www.springframework.org/schema/beans
      http://www.springframework.org/schema/beans/spring-beans.xsd">

  <mongo:mongo-client id="mongoBean" host="${mongo.url}" port="${mongo.port}" credentials="${mongo.user}:${mongo.pass}@${mongo.dbname}">
    <mongo:client-options write-concern="NORMAL" />
  </mongo:mongo-client>
</beans>
```

### MongoDB operations - producer endpoints

#### Query operations

##### findById

This operation retrieves only one element from the collection whose \_id field matches the content of the IN message body. The incoming object can be anything that has an equivalent to a `Bson` type. See [http://bsonspec.org/spec.html](http://bsonspec.org/spec.md) and [http://www.mongodb.org/display/DOCS/Java+Types](http://www.mongodb.org/display/DOCS/Java+Types).

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:findById")
    .to("mongodb:myDb?database=flights&collection=tickets&operation=findById")
    .to("mock:resultFindById");
```

```xml
<route>
  <from uri="direct:findById"/>
  <to uri="mongodb:myDb?database=flights&amp;collection=tickets&amp;operation=findById"/>
  <to uri="mock:resultFindById"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:findById
      steps:
        - to:
            uri: mongodb:myDb
            parameters:
              database: flights
              collection: tickets
              operation: findById
        - to:
            uri: mock:resultFindById
```

Please note that the default \_id is treated by Mongo as and `ObjectId` type, so you may need to convert it properly.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:findById")
    .convertBodyTo(ObjectId.class)
    .to("mongodb:myDb?database=flights&collection=tickets&operation=findById")
    .to("mock:resultFindById");
```

```xml
<route>
  <from uri="direct:findById"/>
  <convertBodyTo type="org.bson.types.ObjectId"/>
  <to uri="mongodb:myDb?database=flights&amp;collection=tickets&amp;operation=findById"/>
  <to uri="mock:resultFindById"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:findById
      steps:
        - convertBodyTo:
            type: org.bson.types.ObjectId
        - to:
            uri: mongodb:myDb
            parameters:
              database: flights
              collection: tickets
              operation: findById
        - to:
            uri: mock:resultFindById
```

> **Tip**
> **Supports optional parameters**
>
> This operation supports projection operators. See [Specifying a `fields` filter (projection)](#_specifying_a_fields_filter_projection).

##### findOneByQuery

Retrieve the first element from a collection matching a MongoDB query selector. **If the `CamelMongoDbCriteria` header is set, then its value is used as the query selector**. If the `CamelMongoDbCriteria` header is _null_, then the IN message body is used as the query selector. In both cases, the query selector should be of type `Bson` or convertible to `Bson` (for instance, a JSON string or `HashMap`). See [Type conversions](#_type_conversions) for more info.

Create query selectors using the `Filters` provided by the MongoDB Driver.

###### Example without a query selector (returns the first document in a collection)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:findOneByQuery")
    .to("mongodb:myDb?database=flights&collection=tickets&operation=findOneByQuery")
    .to("mock:resultFindOneByQuery");
```

```xml
<route>
  <from uri="direct:findOneByQuery"/>
  <to uri="mongodb:myDb?database=flights&amp;collection=tickets&amp;operation=findOneByQuery"/>
  <to uri="mock:resultFindOneByQuery"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:findOneByQuery
      steps:
        - to:
            uri: mongodb:myDb
            parameters:
              database: flights
              collection: tickets
              operation: findOneByQuery
        - to:
            uri: mock:resultFindOneByQuery
```

###### Example with a query selector (returns the first matching document in a collection):

_Java-only: requires Bson Filters object_

```java
from("direct:findOneByQuery")
    .setHeader("CamelMongoDbCriteria", constant(Filters.eq("name", "Raul Kripalani")))
    .to("mongodb:myDb?database=flights&collection=tickets&operation=findOneByQuery")
    .to("mock:resultFindOneByQuery");
```

> **Tip**
> **Supports optional parameters**
>
> This operation supports projection operators and sort clauses. See [Specifying a `fields` filter (projection)](#_specifying_a_fields_filter_projection), [Specifying a sort clause](#_specifying_a_sort_clause).

##### findAll

The `findAll` operation returns all documents matching a query, or none at all, in which case all documents contained in the collection are returned. **The query object is extracted `CamelMongoDbCriteria` header**. if the CamelMongoDbCriteria header is null the query object is extracted message body, i.e., it should be of type `Bson` or convertible to `Bson`. It can be a JSON String or a Hashmap. See [Type conversions](#_type_conversions) for more info.

###### Example without a query selector (returns all documents in a collection)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:findAll")
    .to("mongodb:myDb?database=flights&collection=tickets&operation=findAll")
    .to("mock:resultFindAll");
```

```xml
<route>
  <from uri="direct:findAll"/>
  <to uri="mongodb:myDb?database=flights&amp;collection=tickets&amp;operation=findAll"/>
  <to uri="mock:resultFindAll"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:findAll
      steps:
        - to:
            uri: mongodb:myDb
            parameters:
              database: flights
              collection: tickets
              operation: findAll
        - to:
            uri: mock:resultFindAll
```

###### Example with a query selector (returns all matching documents in a collection)

_Java-only: requires Bson Filters object_

```java
from("direct:findAll")
    .setHeader("CamelMongoDbCriteria", constant(Filters.eq("name", "Raul Kripalani")))
    .to("mongodb:myDb?database=flights&collection=tickets&operation=findAll")
    .to("mock:resultFindAll");
```

###### Example with option _outputType=MongoIterable_ and batch size

_Java-only: requires Bson Filters object_

```java
from("direct:findAll")
    .setHeader("CamelMongoDbBatchSize", constant(10))
    .setHeader("CamelMongoDbCriteria", constant(Filters.eq("name", "Raul Kripalani")))
    .to("mongodb:myDb?database=flights&collection=tickets&operation=findAll&outputType=MongoIterable")
    .to("mock:resultFindAll");
```

> **Tip**
> **Supports optional parameters**
>
> This operation supports projection operators and sort clauses. See [Specifying a `fields` filter (projection)](#_specifying_a_fields_filter_projection), [Specifying a sort clause](#_specifying_a_sort_clause).

##### count

Returns the total number of objects in a collection, returning a Long as the OUT message body.  
The following example will count the number of records in the "dynamicCollectionName" collection. Notice how dynamicity is enabled, and as a result, the operation will not run against the "notableScientists" collection, but against the "dynamicCollectionName" collection.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:count")
    .to("mongodb:myDb?database=tickets&collection=flights&operation=count&dynamicity=true");
```

```xml
<route>
  <from uri="direct:count"/>
  <to uri="mongodb:myDb?database=tickets&amp;collection=flights&amp;operation=count&amp;dynamicity=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:count
      steps:
        - to:
            uri: mongodb:myDb
            parameters:
              database: tickets
              collection: flights
              operation: count
              dynamicity: true
```

To dynamically target a different collection, set the `CamelMongoDbCollection` header:

_Java-only: Java test API (ProducerTemplate)_

```java
Long result = template.requestBodyAndHeader("direct:count", "irrelevantBody",
        "CamelMongoDbCollection", "dynamicCollectionName");
```

You can provide a query **The query object is extracted `CamelMongoDbCriteria` header**. if the CamelMongoDbCriteria header is null the query object is extracted message body, i.e., it should be of type `Bson` or convertible to `Bson`., and operation will return the number of documents matching the criteria.

_Java-only: Java test API (ProducerTemplate)_

```java
Document query = ...
Long count = template.requestBodyAndHeader("direct:count", query,
        "CamelMongoDbCollection", "dynamicCollectionName");
```

##### Specifying a `fields` filter (projection)

Query operations will, by default, return the matching objects in their entirety (with all their fields). If your documents are large, and you only require retrieving a subset of their fields, you can specify a field filter in all query operations, simply by setting the relevant `Bson` (or type convertible to `Bson`, such as a JSON String, Map, etc.) on the `CamelMongoDbFieldsProjection` header.

Here is an example that uses MongoDB’s `Projections` to simplify the creation of Bson. It retrieves all fields except `_id` and `boringField`:

_Java-only: Java test API with Bson Projection_

```java
// route: from("direct:findAll").to("mongodb:myDb?database=flights&collection=tickets&operation=findAll")
Bson fieldProjection = Projection.exclude("_id", "boringField");
Object result = template.requestBodyAndHeader("direct:findAll", ObjectUtils.NULL,
        "CamelMongoDbFieldsProjection", fieldProjection);
```

##### Specifying a sort clause

There is often a requirement to fetch the min/max record from a collection based on sorting by a particular field that uses MongoDB’s `Sorts` to simplify the creation of Bson. It retrieves all fields except `_id` and `boringField`:

_Java-only: Java test API with Bson Sorts_

```java
// route: from("direct:findAll").to("mongodb:myDb?database=flights&collection=tickets&operation=findAll")
Bson sorts = Sorts.descending("_id");
Object result = template.requestBodyAndHeader("direct:findAll", ObjectUtils.NULL,
        "CamelMongoDbSortBy", sorts);
```

In a Camel route, the SORT\_BY header can be used with the findOneByQuery operation to achieve the same result. If the FIELDS\_PROJECTION header is also specified, the operation will return a single field/value pair that can be passed directly to another component (for example, a parameterized MyBatis SELECT query). This example demonstrates fetching the temporally newest document from a collection and reducing the result to a single field, based on the `documentTimestamp` field:

_Java-only: requires Bson Sorts and Projection objects_

```java
from("direct:someTriggeringEvent")
    .setHeader("CamelMongoDbSortBy", constant(Sorts.descending("documentTimestamp")))
    .setHeader("CamelMongoDbFieldsProjection", constant(Projection.include("documentTimestamp")))
    .setBody(constant("{}"))
    .to("mongodb:myDb?database=local&collection=myDemoCollection&operation=findOneByQuery")
    .to("direct:aMyBatisParameterizedSelect");
```

#### Create/update operations

##### insert

Insert a new object into the MongoDB collection, taken from the IN message body. Type conversion is attempted to turn it into `Document` or a `List`. Two modes are supported: single insert and multiple insert. For multiple insert, the endpoint will expect a List, Array or Collections of objects of any type, as long as they are - or can be converted to - `Document`. Example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:insert")
    .to("mongodb:myDb?database=flights&collection=tickets&operation=insert");
```

```xml
<route>
  <from uri="direct:insert"/>
  <to uri="mongodb:myDb?database=flights&amp;collection=tickets&amp;operation=insert"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:insert
      steps:
        - to:
            uri: mongodb:myDb
            parameters:
              database: flights
              collection: tickets
              operation: insert
```

The operation will return a WriteResult, and depending on the `WriteConcern` or the value of the `invokeGetLastError` option, `getLastError()` would have been called already or not. If you want to access the ultimate result of the write operation, you need to retrieve the `CommandResult` by calling `getLastError()` or `getCachedLastError()` on the `WriteResult`. Then you can verify the result by calling `CommandResult.ok()`, `CommandResult.getErrorMessage()` and/or `CommandResult.getException()`.

Note that the new object’s `_id` must be unique in the collection. If you don’t specify the value, MongoDB will automatically generate one for you. But if you do specify it, and it is not unique, the insert operation will fail (and for Camel to notice, you will need to enable invokeGetLastError or set a WriteConcern that waits for the write result).

This is not a limitation of the component, but it is how things work in MongoDB for higher throughput. If you are using a custom `_id`, you are expected to ensure at the application level that is unique (and this is a good practice too).

OID(s) of the inserted record(s) are stored in the message header under `CamelMongoOid` key. The value stored is `org.bson.types.ObjectId` for single insert or `java.util.List<org.bson.types.ObjectId>` if multiple records have been inserted.

In MongoDB Java Driver 3.x the insertOne and insertMany operation return void. The Camel insert operation return the document or list of documents inserted. Note that each document is updated by a new OID if needed.

##### save

The save operation is equivalent to an _upsert_ (UPdate, inSERT) operation, where the record will be updated, and if it doesn’t exist, it will be inserted, all in one atomic operation. MongoDB will perform the matching based on the `_id` field.

Beware that in case of an update, the object is replaced entirely and the usage of [MongoDB’s $modifiers](http://www.mongodb.org/display/DOCS/Updating#Updating-ModifierOperations) is not permitted. Therefore, if you want to manipulate the object if it already exists, you have two options:

1.  performing a query to retrieve the entire object first along with all its fields (may not be efficient), alter it inside Camel and then save it.
    
2.  using the update operation with [$modifiers](http://www.mongodb.org/display/DOCS/Updating#Updating-ModifierOperations), which will execute the update at the server-side instead. You can enable the upsert flag, in which case if an insert is required, MongoDB will apply the $modifiers to the filter query object and insert the result.
    

If the document to be saved does not contain the `_id` attribute, the operation will be an insert, and the new `_id` created will be placed in the `CamelMongoOid` header.

For example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:insert")
    .to("mongodb:myDb?database=flights&collection=tickets&operation=save");
```

```xml
<route>
  <from uri="direct:insert"/>
  <to uri="mongodb:myDb?database=flights&amp;collection=tickets&amp;operation=save"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:insert
      steps:
        - to:
            uri: mongodb:myDb
            parameters:
              database: flights
              collection: tickets
              operation: save
```

_Java-only: Java test API (ProducerTemplate)_

```java
// route: from("direct:insert").to("mongodb:myDb?database=flights&collection=tickets&operation=save");
Document docForSave = new Document();
docForSave.put("key", "value");
Object result = template.requestBody("direct:insert", docForSave);
```

##### update

Update one or multiple records in the collection. Requires a filter query and a update rules.

You can define the filter using `CamelMongoDbCriteria` header as `Bson` and define the update rules as `Bson` in Body.

> **Note**
> **Update after enrich**
>
> While defining the filter by using `CamelMongoDbCriteria` header as `Bson` to query mongodb before you do update, you should notice you need to remove it from the resulting Camel exchange during aggregation if you use the enrich pattern with an aggregation strategy and then apply mongodb update. If you don’t remove this header during aggregation and/or redefine `CamelMongoDbCriteria` header before sending Camel exchange to mongodb producer endpoint, you may end up with invalid Camel exchange payload while updating mongodb.

The second way requires a `List<Bson>` as the IN message body containing exactly two elements:

-   Element 1 (index 0) ⇒ filter query ⇒ determines what objects will be affected, same as a typical query object
    
-   Element 2 (index 1) ⇒ update rules ⇒ how matched objects will be updated. All [modifier operations](http://www.mongodb.org/display/DOCS/Updating#Updating-ModifierOperations) from MongoDB are supported.
    

> **Note**
> **Multiupdates**
>
> By default, MongoDB will only update 1 object even if multiple objects match the filter query. To instruct MongoDB to update **all** matching records, set the `CamelMongoDbMultiUpdate` IN message header to `true`.

A header with key `CamelMongoDbRecordsAffected` will be returned with the number of records updated (copied from `WriteResult.getN()`).

For example, the following will update **all** records whose filterField field equals true by setting the value of the "scientist" field to "Darwin":

_Java-only: Java test API with Bson filter and update_

```java
// route: from("direct:update").to("mongodb:myDb?database=science&collection=notableScientists&operation=update");
List<Bson> body = new ArrayList<>();
Bson filterField = Filters.eq("filterField", true);
body.add(filterField);
BsonDocument updateObj = new BsonDocument().append("$set", new BsonDocument("scientist", new BsonString("Darwin")));
body.add(updateObj);
Object result = template.requestBodyAndHeader("direct:update", body, "CamelMongoDbMultiUpdate", true);
```

_Java-only: Java test API with criteria header_

```java
// route: from("direct:update").to("mongodb:myDb?database=science&collection=notableScientists&operation=update");
Map<String, Object> headers = new HashMap<>(2);
headers.put("CamelMongoDbMultiUpdate", true);
headers.put("CamelMongoDbCriteria", Filters.eq("filterField", true));
Bson updateObj = Updates.set("scientist", "Darwin");
Object result = template.requestBodyAndHeaders("direct:update", updateObj, headers);
```

_Java-only: Java test API with JSON string_

```java
// route: from("direct:update").to("mongodb:myDb?database=science&collection=notableScientists&operation=update");
String updateObj = "[{\"filterField\": true}, {\"$set\", {\"scientist\", \"Darwin\"}}]";
Object result = template.requestBodyAndHeader("direct:update", updateObj, "CamelMongoDbMultiUpdate", true);
```

#### Delete operations

##### remove

Remove matching records from the collection. The IN message body will act as the removal filter query, and is expected to be of type `DBObject` or a type convertible to it.  
The following example will remove all objects whose field 'conditionField' equals true, in the science database, notableScientists collection:

_Java-only: Java test API with Bson filter_

```java
// route: from("direct:remove").to("mongodb:myDb?database=science&collection=notableScientists&operation=remove");
Bson conditionField = Filters.eq("conditionField", true);
Object result = template.requestBody("direct:remove", conditionField);
```

A header with key `CamelMongoDbRecordsAffected` is returned with type `int`, containing the number of records deleted (copied from `WriteResult.getN()`).

#### Bulk Write Operations

##### bulkWrite

Performs write operations in bulk with controls for order of execution. Requires a `List<WriteModel<Document>>` as the IN message body containing commands for insert, update, and delete operations.

The following example will insert a new scientist "Pierre Curie", update record with id "5" by setting the value of the "scientist" field to "Marie Curie" and delete record with id "3" :

_Java-only: Java test API with WriteModel objects_

```java
// route: from("direct:bulkWrite").to("mongodb:myDb?database=science&collection=notableScientists&operation=bulkWrite");
List<WriteModel<Document>> bulkOperations = Arrays.asList(
        new InsertOneModel<>(new Document("scientist", "Pierre Curie")),
        new UpdateOneModel<>(new Document("_id", "5"),
                new Document("$set", new Document("scientist", "Marie Curie"))),
        new DeleteOneModel<>(new Document("_id", "3")));

BulkWriteResult result = template.requestBody("direct:bulkWrite", bulkOperations, BulkWriteResult.class);
```

By default, operations are executed in order and interrupted on the first write error without processing any remaining write operations in the list. To instruct MongoDB to continue to process remaining write operations in the list, set the `CamelMongoDbBulkOrdered` IN message header to `false`. Unordered operations are executed in parallel, and this behavior is not guaranteed.

#### Other operations

##### aggregate

Perform an aggregation with the given pipeline contained in the body. **Aggregations could be long and heavy operations. Use with care.**

_Java-only: requires Bson aggregation pipeline_

```java
// route: from("direct:aggregate").to("mongodb:myDb?database=science&collection=notableScientists&operation=aggregate");
List<Bson> aggregate = Arrays.asList(match(or(eq("scientist", "Darwin"), eq("scientist", "Einstein"))),
        group("$scientist", sum("count", 1)));
from("direct:aggregate")
    .setBody(constant(aggregate))
    .to("mongodb:myDb?database=science&collection=notableScientists&operation=aggregate")
    .to("mock:resultAggregate");
```

By default, a List of all results is returned. This can be heavy on memory depending on the size of the results. A safer alternative is to set your outputType=MongoIterable. The next Processor will see an iterable in the message body allowing it to step through the results one by one. Thus, setting a batch size and returning an iterable allows for efficient retrieval and processing of the result.

An example would look like:

_Java-only: requires Bson aggregation pipeline_

```java
List<Bson> aggregate = Arrays.asList(match(or(eq("scientist", "Darwin"), eq("scientist", "Einstein"))),
        group("$scientist", sum("count", 1)));
from("direct:aggregate")
    .setHeader("CamelMongoDbBatchSize", constant(10))
    .setBody(constant(aggregate))
    .to("mongodb:myDb?database=science&collection=notableScientists&operation=aggregate&outputType=MongoIterable")
    .split(body())
    .streaming()
    .to("mock:resultAggregate");
```

Note that calling `.split(body())` is enough to send the entries down the route one-by-one, however it would still load all the entries into memory first. Calling `.streaming()` is thus required to load data into memory by batches.

##### getDbStats

Equivalent of running the `db.stats()` command in the MongoDB shell, which displays useful statistic figures about the database.  
For example:

\> db.stats();
{
    "db" : "test",
    "collections" : 7,
    "objects" : 719,
    "avgObjSize" : 59.73296244784423,
    "dataSize" : 42948,
    "storageSize" : 1000058880,
    "numExtents" : 9,
    "indexes" : 4,
    "indexSize" : 32704,
    "fileSize" : 1275068416,
    "nsSizeMB" : 16,
    "ok" : 1
}

Usage example:

_Java-only: Java test API (ProducerTemplate)_

```java
// from("direct:getDbStats").to("mongodb:myDb?database=flights&collection=tickets&operation=getDbStats");
Object result = template.requestBody("direct:getDbStats", "irrelevantBody");
assertTrue("Result is not of type Document", result instanceof Document);
```

The operation will return a data structure similar to the one displayed in the shell, in the form of a `Document` in the OUT message body.

##### getColStats

Equivalent of running the `db.collection.stats()` command in the MongoDB shell, which displays useful statistic figures about the collection.  
For example:

\> db.camelTest.stats();
{
    "ns" : "test.camelTest",
    "count" : 100,
    "size" : 5792,
    "avgObjSize" : 57.92,
    "storageSize" : 20480,
    "numExtents" : 2,
    "nindexes" : 1,
    "lastExtentSize" : 16384,
    "paddingFactor" : 1,
    "flags" : 1,
    "totalIndexSize" : 8176,
    "indexSizes" : {
        "\_id\_" : 8176
    },
    "ok" : 1
}

Usage example:

_Java-only: Java test API (ProducerTemplate)_

```java
// from("direct:getColStats").to("mongodb:myDb?database=flights&collection=tickets&operation=getColStats");
Object result = template.requestBody("direct:getColStats", "irrelevantBody");
assertTrue("Result is not of type Document", result instanceof Document);
```

The operation will return a data structure similar to the one displayed in the shell, in the form of a `Document` in the OUT message body.

##### command

Run the body as a command on the database. Useful for admin operation as getting host information, replication or sharding status.

Collection parameter is not used for this operation.

_Java-only: Java test API (ProducerTemplate)_

```java
// route: from("command").to("mongodb:myDb?database=science&operation=command");
DBObject commandBody = new BasicDBObject("hostInfo", "1");
Object result = template.requestBody("direct:command", commandBody);
```

#### Dynamic operations

An Exchange can override the endpoint’s fixed operation by setting the `CamelMongoDbOperation` header. The values supported are determined by the MongoDbOperation enumeration and match the accepted values for the `operation` parameter on the endpoint URI.

For example:

_Java-only: Java test API (ProducerTemplate)_

```java
// from("direct:insert").to("mongodb:myDb?database=flights&collection=tickets&operation=insert");
Object result = template.requestBodyAndHeader("direct:insert", "irrelevantBody", "CamelMongoDbOperation", "count");
assertTrue("Result is not of type Long", result instanceof Long);
```

### Consumers

There are several types of consumers:

1.  Tailable Cursor Consumer
    
2.  Change Streams Consumer
    

#### Tailable Cursor Consumer

MongoDB offers a mechanism to instantaneously consume ongoing data from a collection, by keeping the cursor open just like the `tail -f` command of \*nix systems. This mechanism is significantly more efficient than a scheduled poll, due to the fact that the server pushes new data to the client as it becomes available, rather than making the client ping back at scheduled intervals to fetch new data. It also reduces otherwise redundant network traffic.

There is only one requisite to use tailable cursors: the collection must be a "capped collection", meaning that it will only hold N objects, and when the limit is reached, MongoDB flushes old objects in the same order they were originally inserted. For more information, please refer to: [http://www.mongodb.org/display/DOCS/Tailable+Cursors](http://www.mongodb.org/display/DOCS/Tailable+Cursors).

The Camel MongoDB component implements a tailable cursor consumer, making this feature available for you to use in your Camel routes. As new objects are inserted, MongoDB will push them as `Document` in natural order to your tailable cursor consumer, who will transform them to an Exchange and will trigger your route logic.

### How the tailable cursor consumer works

To turn a cursor into a tailable cursor, a few special flags are to be signalled to MongoDB when first generating the cursor. Once created, the cursor will then stay open and will block upon calling the `MongoCursor.next()` method until new data arrives. However, the MongoDB server reserves itself the right to kill your cursor if new data doesn’t appear after an indeterminate period. If you are interested to continue consuming new data, you have to regenerate the cursor. And to do so, you will have to remember the position where you left off or else you will start consuming from the top again.

The Camel MongoDB tailable cursor consumer takes care of all these tasks for you. You will need to provide the key to some field in your data of increasing nature, which will act as a marker to position your cursor every time it is regenerated, e.g. a timestamp, a sequential ID, etc. It can be of any datatype supported by MongoDB. Date, Strings and Integers are found to work well. We call this mechanism "tail tracking" in the context of this component.

The consumer will remember the last value of this field, and whenever the cursor is to be regenerated, it will run the query with a filter like: `increasingField > lastValue`, so that only unread data is consumed.

**Setting the increasing field:** Set the key of the increasing field on the endpoint URI `tailTrackingIncreasingField` option. In Camel 2.10, it must be a top-level field in your data, as nested navigation for this field is not yet supported. That is, the "timestamp" field is okay, but `nested.timestamp` will not work. Please open a ticket in the Camel JIRA if you do require support for nested increasing fields.

**Cursor regeneration delay:** One thing to note is that if new data is not already available upon initialisation, MongoDB will kill the cursor instantly. Since we don’t want to overwhelm the server in this case, a `cursorRegenerationDelay` option has been introduced (with a default value of 1000ms.), which you can modify to suit your needs.

An example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("mongodb:myDb?database=flights&collection=cancellations&tailTrackIncreasingField=departureTime")
    .id("tailableCursorConsumer1")
    .autoStartup(false)
    .to("mock:test");
```

```xml
<route id="tailableCursorConsumer1" autoStartup="false">
  <from uri="mongodb:myDb?database=flights&amp;collection=cancellations&amp;tailTrackIncreasingField=departureTime"/>
  <to uri="mock:test"/>
</route>
```

```yaml
- route:
    id: tailableCursorConsumer1
    autoStartup: false
    from:
      uri: mongodb:myDb
      parameters:
        database: flights
        collection: cancellations
        tailTrackIncreasingField: departureTime
      steps:
        - to:
            uri: mock:test
```

The above route will consume from the `flights.cancellations` capped collection, using `departureTime` as the increasing field, with a default regeneration cursor delay of 1000ms.

### Persistent tail tracking

Standard tail tracking is volatile and the last value is only kept in memory. However, in practice, you will need to restart your Camel container sometimes. However, your last value would then be lost and your tailable cursor consumer would start consuming from the top again, very likely sending duplicate records into your route.

To overcome this situation, you can enable the **persistent tail tracking** feature to keep track of the last consumed increasing value in a special collection inside your MongoDB database too. When the consumer initialises again, it will restore the last tracked value and continue as if nothing happened.

The last read value is persisted on two occasions: every time the cursor is regenerated and when the consumer shuts down. We may consider persisting at regular intervals too in the future (flush every 5 seconds) for added robustness if the demand is there. To request this feature, please open a ticket in the Camel JIRA.

### Enabling persistent tail tracking

To enable this function, set at least the following options on the endpoint URI:

-   `persistentTailTracking` option to `true`
    
-   `persistentId` option to a unique identifier for this consumer, so that the same collection can be reused across many consumers
    

Additionally, you can set the `tailTrackDb`, `tailTrackCollection` and `tailTrackField` options to customise where the runtime information will be stored. Refer to the endpoint options table at the top of this page for descriptions of each option.

For example, the following route will consume from the "flights.cancellations" capped collection, using "departureTime" as the increasing field, with a default regeneration cursor delay of 1000ms, with persistent tail tracking turned on, and persisting under the "cancellationsTracker" id on the "flights.camelTailTracking", storing the last processed value under the "lastTrackingValue" field (`camelTailTracking` and `lastTrackingValue` are defaults).

-   Java
    
-   XML
    
-   YAML
    

```java
from("mongodb:myDb?database=flights&collection=cancellations&tailTrackIncreasingField=departureTime&persistentTailTracking=true" +
     "&persistentId=cancellationsTracker")
    .id("tailableCursorConsumer2")
    .autoStartup(false)
    .to("mock:test");
```

```xml
<route id="tailableCursorConsumer2" autoStartup="false">
  <from uri="mongodb:myDb?database=flights&amp;collection=cancellations&amp;tailTrackIncreasingField=departureTime&amp;persistentTailTracking=true&amp;persistentId=cancellationsTracker"/>
  <to uri="mock:test"/>
</route>
```

```yaml
- route:
    id: tailableCursorConsumer2
    autoStartup: false
    from:
      uri: mongodb:myDb
      parameters:
        database: flights
        collection: cancellations
        tailTrackIncreasingField: departureTime
        persistentTailTracking: true
        persistentId: cancellationsTracker
      steps:
        - to:
            uri: mock:test
```

Below is another example identical to the one above, but where the persistent tail tracking runtime information will be stored under the "trackers.camelTrackers" collection, in the "lastProcessedDepartureTime" field:

-   Java
    
-   XML
    
-   YAML
    

```java
from("mongodb:myDb?database=flights&collection=cancellations&tailTrackIncreasingField=departureTime&persistentTailTracking=true" +
     "&persistentId=cancellationsTracker&tailTrackDb=trackers&tailTrackCollection=camelTrackers" +
     "&tailTrackField=lastProcessedDepartureTime")
    .id("tailableCursorConsumer3")
    .autoStartup(false)
    .to("mock:test");
```

```xml
<route id="tailableCursorConsumer3" autoStartup="false">
  <from uri="mongodb:myDb?database=flights&amp;collection=cancellations&amp;tailTrackIncreasingField=departureTime&amp;persistentTailTracking=true&amp;persistentId=cancellationsTracker&amp;tailTrackDb=trackers&amp;tailTrackCollection=camelTrackers&amp;tailTrackField=lastProcessedDepartureTime"/>
  <to uri="mock:test"/>
</route>
```

```yaml
- route:
    id: tailableCursorConsumer3
    autoStartup: false
    from:
      uri: mongodb:myDb
      parameters:
        database: flights
        collection: cancellations
        tailTrackIncreasingField: departureTime
        persistentTailTracking: true
        persistentId: cancellationsTracker
        tailTrackDb: trackers
        tailTrackCollection: camelTrackers
        tailTrackField: lastProcessedDepartureTime
      steps:
        - to:
            uri: mock:test
```

#### Change Streams Consumer

Change Streams allow applications to access real-time data changes without the complexity and risk of tailing the MongoDB oplog. Applications can use change streams to subscribe to all data changes on a collection and immediately react to them. Because change streams use the aggregation framework, applications can also filter for specific changes or transform the notifications at will. The exchange body will contain the full document of any change.

To configure Change Streams Consumer you need to specify `consumerType`, `database`, `collection` and optional JSON property `streamFilter` to filter events. That JSON property is standard MongoDB `$match` aggregation. It could be easily specified using the DSL configuration:

-   Java
    
-   XML
    
-   YAML
    

```java
from("mongodb:myDb?consumerType=changeStreams&database=flights&collection=tickets&streamFilter={ '$match':{'$or':[{'fullDocument.stringValue': 'specificValue'}]} }")
    .to("mock:test");
```

```xml
<route id="filterConsumer">
  <from uri="mongodb:myDb?consumerType=changeStreams&amp;database=flights&amp;collection=tickets&amp;streamFilter={ '$match':{'$or':[{'fullDocument.stringValue': 'specificValue'}]} }"/>
  <to uri="mock:test"/>
</route>
```

```yaml
- route:
    id: filterConsumer
    from:
      uri: mongodb:myDb
      parameters:
        consumerType: changeStreams
        database: flights
        collection: tickets
        streamFilter: "{ '$match':{'$or':[{'fullDocument.stringValue': 'specificValue'}]} }"
      steps:
        - to:
            uri: mock:test
```

> **Tip**
> You can externalize the streamFilter value into a property placeholder which allows the endpoint URI parameters to be _cleaner_ and easier to read.

### Type conversions

The `MongoDbBasicConverters` type converter included with the camel-mongodb component provides the following conversions:

   
| Name | From type | To type | How? |
| --- | --- | --- | --- |
| fromMapToDocument | `Map` | `Document` | constructs a new `Document` via the `new Document(Map m)` constructor. |
| fromDocumentToMap | `Document` | `Map` | `Document` already implements `Map`. |
| fromStringToDocument | `String` | `Document` | uses `com.mongodb.Document.parse(String s)`. |
| fromStringToObjectId | `String` | `ObjectId` | constructs a new `ObjectId` via the `new ObjectId(s)` |
| fromFileToDocument | `File` | `Document` | uses `fromInputStreamToDocument` under the hood |
| fromInputStreamToDocument | `InputStream` | `Document` | converts the inputstream bytes to a `Document` |
| fromStringToList | `String` | `List<Bson>` | uses `org.bson.codecs.configuration.CodecRegistries` to convert to BsonArray then to List<Bson>. |

This type converter is auto-discovered, so you don’t need to configure anything manually.

## Examples

### Example route

The following route defined in Spring XML executes the operation [getDbStats](#_getdbstats) on a collection.

**Get DB stats for specified collection**

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("mongodb:mongoBean?database=${mongodb.database}&collection=${mongodb.collection}&operation=getDbStats")
    .to("direct:result");
```

```xml
<route>
  <from uri="direct:start" />
  <!-- using bean 'mongoBean' defined above -->
  <to uri="mongodb:mongoBean?database=${mongodb.database}&amp;collection=${mongodb.collection}&amp;operation=getDbStats" />
  <to uri="direct:result" />
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: mongodb:mongoBean
            parameters:
              database: "${mongodb.database}"
              collection: "${mongodb.collection}"
              operation: getDbStats
        - to:
            uri: direct:result
```