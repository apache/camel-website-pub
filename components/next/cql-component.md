# Cassandra CQL

**Since Camel 2.15**

**Both producer and consumer are supported**

[Apache Cassandra](http://cassandra.apache.org) is an open source NoSQL database designed to handle large amounts on commodity hardware. Like Amazon’s DynamoDB, Cassandra has a peer-to-peer and master-less architecture to avoid a single point of failure and guaranty high availability. Like Google’s BigTable, Cassandra data is structured using column families which can be accessed through the Thrift RPC API or an SQL-like API called CQL.

> **Note**
> This component aims at integrating Cassandra 2.0+ using the CQL3 API instead of the Thrift API. It’s based on [Cassandra Java Driver](https://github.com/datastax/java-driver) provided by DataStax.

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

The Cassandra CQL component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Cassandra CQL endpoint is configured using URI syntax:

cql:beanRef:hosts:port/keyspace

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **beanRef** (common) | beanRef is defined using bean:id. |  | String |
| **hosts** (common) | Hostname(s) Cassandra server(s). Multiple hosts can be separated by comma. |  | String |
| **port** (common) | Port number of Cassandra server(s). |  | Integer |
| **keyspace** (common) | Keyspace to use. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clusterName** (common) | Cluster name. |  | String |
| **cql** (common) | CQL query to perform. Can be overridden with the message header with key CamelCqlQuery. |  | String |
| **datacenter** (common) | Datacenter to use. | datacenter1 | String |
| **prepareStatements** (common) | Whether to use PreparedStatements or regular Statements. | true | boolean |
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
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **extraTypeCodecs** (advanced) | To use a specific comma separated list of Extra Type codecs. Possible values are: BLOB\_TO\_ARRAY, BOOLEAN\_LIST\_TO\_ARRAY, BYTE\_LIST\_TO\_ARRAY, SHORT\_LIST\_TO\_ARRAY, INT\_LIST\_TO\_ARRAY, LONG\_LIST\_TO\_ARRAY, FLOAT\_LIST\_TO\_ARRAY, DOUBLE\_LIST\_TO\_ARRAY, TIMESTAMP\_UTC, TIMESTAMP\_MILLIS\_SYSTEM, TIMESTAMP\_MILLIS\_UTC, ZONED\_TIMESTAMP\_SYSTEM, ZONED\_TIMESTAMP\_UTC, ZONED\_TIMESTAMP\_PERSISTED, LOCAL\_TIMESTAMP\_SYSTEM and LOCAL\_TIMESTAMP\_UTC. |  | String |
| **loadBalancingPolicyClass** (advanced) | To use a specific LoadBalancingPolicyClass. |  | String |
| **resultSetConversionStrategy** (advanced) | To use a custom class that implements logic for converting ResultSet into message body ALL, ONE, LIMIT\_10, LIMIT\_100…​ |  | ResultSetConversionStrategy |
| **session** (advanced) | To use the Session instance (you would normally not use this option). |  | CqlSession |
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
| **password** (security) | Password for session authentication. |  | String |
| **username** (security) | Username for session authentication. |  | String |

## Message Headers

The Cassandra CQL component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelCqlQuery** (producer) Constant: [`CQL_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-cassandraql/latest/org/apache/camel/component/cassandra/CassandraConstants.html#CQL_QUERY) | The CQL query to execute. |  | String |
| **CamelCqlResumeAction** (consumer) Constant: [`CASSANDRA_RESUME_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-cassandraql/latest/org/apache/camel/component/cassandra/CassandraConstants.html#CASSANDRA_RESUME_ACTION) | The resume action to execute when resuming. |  | String |

## Usage

### Endpoint Connection Syntax

The endpoint can initiate the Cassandra connection or use an existing one.

 
| URI | Description |
| --- | --- |
| `cql:localhost/keyspace` | Single host, default port, usual for testing |
| `cql:host1,host2/keyspace` | Multi host, default port |
| `cql:host1,host2:9042/keyspace` | Multi host, custom port |
| `cql:host1,host2` | Default port and keyspace |
| `cql:bean:sessionRef` | Provided Session reference |

To fine-tune the Cassandra connection (SSL options, pooling options, load balancing policy, retry policy, reconnection policy…​), create your own Cluster instance and give it to the Camel endpoint.

### Messages

#### Incoming Message

The Camel Cassandra endpoint expects a bunch of simple objects (`Object` or `Object[]` or `Collection<Object>`) which will be bound to the CQL statement as query parameters. If the message body is null or empty, then CQL query will be executed without binding parameters.

Headers:

-   `CamelCqlQuery` (optional, `String` or `RegularStatement`): CQL query either as a plain String or built using the `QueryBuilder`.
    

#### Outgoing Message

The Camel Cassandra endpoint produces one or many a Cassandra Row objects depending on the `resultSetConversionStrategy`:

-   `List<Row>` if `resultSetConversionStrategy` is `ALL` or `LIMIT_[0-9]+`
    
-   Single\` Row\` if `resultSetConversionStrategy` is `ONE`
    
-   Anything else, if `resultSetConversionStrategy` is a custom implementation of the `ResultSetConversionStrategy`
    

### Repositories

Cassandra can be used to store message keys or messages for the idempotent and aggregation EIP.

Cassandra might not be the best tool for queuing use cases yet, read [Cassandra anti-patterns queues and queue like datasets](http://www.datastax.com/dev/blog/cassandra-anti-patterns-queues-and-queue-like-datasets). It’s advised to use LeveledCompaction and a small GC grace setting for these tables to allow tombstoned rows to be removed quickly.

#### Idempotent repository

The `NamedCassandraIdempotentRepository` stores messages keys in a Cassandra table like this:

**CAMEL\_IDEMPOTENT.cql**

```sql
CREATE TABLE CAMEL_IDEMPOTENT (
  NAME varchar,   -- Repository name
  KEY varchar,    -- Message key
  PRIMARY KEY (NAME, KEY)
) WITH compaction = {'class':'LeveledCompactionStrategy'}
  AND gc_grace_seconds = 86400;
```

This repository implementation uses lightweight transactions, (also known as Compare and Set) and requires Cassandra 2.0.7+.

Alternatively, the `CassandraIdempotentRepository` does not have a `NAME` column and can be extended to use a different data model.

  
| Option | Default | Description |
| --- | --- | --- |
| `table` | `CAMEL_IDEMPOTENT` | Table name |
| `pkColumns` | `NAME`,\` KEY\` | Primary key columns |
| `name` |  | Repository name, value used for `NAME` column |
| `ttl` |  | Key time to live |
| `writeConsistencyLevel` |  | Consistency level used to insert/delete key: `ANY`, `ONE`, `TWO`, `QUORUM`, `LOCAL_QUORUM`… |
| `readConsistencyLevel` |  | Consistency level used to read/check key: `ONE`, `TWO`, `QUORUM`, `LOCAL_QUORUM`… |

#### Aggregation repository

The `NamedCassandraAggregationRepository` stores exchanges by correlation key in a Cassandra table like this:

**CAMEL\_AGGREGATION.cql**

```sql
CREATE TABLE CAMEL_AGGREGATION (
  NAME varchar,        -- Repository name
  KEY varchar,         -- Correlation id
  EXCHANGE_ID varchar, -- Exchange id
  EXCHANGE blob,       -- Serialized exchange
  PRIMARY KEY (NAME, KEY)
) WITH compaction = {'class':'LeveledCompactionStrategy'}
  AND gc_grace_seconds = 86400;
```

Alternatively, the `CassandraAggregationRepository` does not have a `NAME` column and can be extended to use a different data model.

  
| Option | Default | Description |
| --- | --- | --- |
| `table` | `CAMEL_AGGREGATION` | Table name |
| `pkColumns` | `NAME`,`KEY` | Primary key columns |
| `exchangeIdColumn` | `EXCHANGE_ID` | Exchange Id column |
| `exchangeColumn` | `EXCHANGE` | Exchange content column |
| `name` |  | Repository name, value used for `NAME` column |
| `ttl` |  | Exchange time to live |
| `writeConsistencyLevel` |  | Consistency level used to insert/delete exchange: `ANY`, `ONE`, `TWO`, `QUORUM`, `LOCAL_QUORUM`… |
| `readConsistencyLevel` |  | Consistency level used to read/check exchange: `ONE`, `TWO`, `QUORUM`, `LOCAL_QUORUM`… |

While deserializing, it’s important to notice that the `unmarshallExchange` method will allow only all java packages and subpackages and org.apache.camel packages and subpackages. The remaining classes will be blacklisted. So you’ll need to change the filter in case of need. This could be accomplished by changing the deserializationFilter field in the repository.

## Examples

To insert something on a table, you can use the following code:

_Java-only: route with CQL query string concatenation_

```java
String CQL = "insert into camel_user(login, first_name, last_name) values (?, ?, ?)";
from("direct:input")
    .to("cql://localhost/camel_ks?cql=" + CQL);
```

At this point, you should be able to insert data by using a list as body

_Java-only: creating a parameter list for CQL binding_

```java
Arrays.asList("davsclaus", "Claus", "Ibsen");
```

The same approach can be used for updating or querying the table.