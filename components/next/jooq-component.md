# JOOQ

**Since Camel 3.0**

**Both producer and consumer are supported**

The JOOQ component enables you to store and retrieve Java objects from persistent storage using JOOQ library.

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

The JOOQ component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | Component configuration (database connection, database entity type, etc.). |  | JooqConfiguration |
| **databaseConfiguration** (common) | To use a specific database configuration. |  | Configuration |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumeDelete** (consumer) | Delete entity after it is consumed. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
Type of operation to execute on query.

Enum values:

-   NONE
    
-   EXECUTE
    
-   FETCH
    
-   CONSUME
    





 | NONE | JooqOperation |
| **query** (producer) | To execute plain SQL query. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The JOOQ endpoint is configured using URI syntax:

jooq:entityType

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **entityType** (common) | JOOQ entity class. |  | Class |

### Query Parameters (24 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **databaseConfiguration** (common) | To use a specific database configuration. |  | Configuration |
| **consumeDelete** (consumer) | Delete entity after it is consumed. | true | boolean |
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
| **operation** (producer) | 

Type of operation to execute on query.

Enum values:

-   NONE
    
-   EXECUTE
    
-   FETCH
    
-   CONSUME
    





 | NONE | JooqOperation |
| **query** (producer) | To execute plain SQL query. |  | String |
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

## Usage

JOOQ provides DSL to create queries. There are two types of queries:

1.  `org.jooq.Query`: can be executed
    
2.  `org.jooq.ResultQuery`: can return results
    

For example:

_Java-only: JOOQ DSL API for creating Query and ResultQuery objects_

```java
// Create a Query object and execute it:
Query query = create.query("DELETE FROM BOOK");
query.execute();

// Create a ResultQuery object and execute it, fetching results:
ResultQuery<Record> resultQuery = create.resultQuery("SELECT * FROM BOOK");
Result<Record> result = resultQuery.fetch();
```

### Plain SQL

SQL could be executed using JOOQ’s objects "Query" or "ResultQuery". Also, the SQL query could be specified inside URI:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord?query=select * from book_store x where x.name = 'test'")
    .to("bean:myBusinessLogic");
```

```xml
<route>
    <from uri="jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord?query=select * from book_store x where x.name = 'test'"/>
    <to uri="bean:myBusinessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord
      parameters:
        query: "select * from book_store x where x.name = 'test'"
    steps:
      - to:
          uri: bean:myBusinessLogic
```

See the examples below.

### Consuming from endpoint

Consuming messages from a JOOQ consumer endpoint removes (or updates) entity beans in the database. This allows you to use a database table as a logical queue: consumers take messages from the queue and then delete/update them to logically remove them from the queue. If you do not wish to delete the entity bean when it has been processed, you can specify consumeDelete=false on the URI.

### Operations

When using jooq as a producer you can use any of the following `JooqOperation` operations:

 
| Operation | Description |
| --- | --- |
| none | Execute a query (default) |
| execute | Execute a query with no expected results |
| fetch | Execute a query and the result of the query is stored as the new message body |

## Example

JOOQ configuration:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:property-placeholder location="classpath:config.properties"
                                  xmlns:context="http://www.springframework.org/schema/context"/>

    <bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close">
        <property name="url" value="${db.url}"/>
        <property name="driverClassName" value="${db.driver}"/>
        <property name="username" value="${db.username}"/>
        <property name="password" value="${db.password}"/>
    </bean>

    <bean id="transactionAwareDataSource"
          class="org.springframework.jdbc.datasource.TransactionAwareDataSourceProxy">
        <constructor-arg ref="dataSource"/>
    </bean>

    <bean class="org.jooq.impl.DataSourceConnectionProvider" name="connectionProvider">
        <constructor-arg ref="transactionAwareDataSource"/>
    </bean>

    <bean id="dsl" class="org.jooq.impl.DefaultDSLContext">
        <constructor-arg ref="config"/>
    </bean>

    <bean id="jooqConfig" class="org.jooq.impl.DefaultConfiguration" name="config">
        <property name="SQLDialect">
            <value type="org.jooq.SQLDialect">${jooq.sql.dialect}</value>
        </property>
        <property name="connectionProvider" ref="connectionProvider"/>
    </bean>

</beans>
```

Camel context configuration:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">

    <import resource="classpath:jooq-spring.xml"/>

    <!-- Configure component -->
    <bean id="jooq" class="org.apache.camel.component.jooq.JooqComponent">
        <property name="configuration">
            <bean id="jooqConfiguration" class="org.apache.camel.component.jooq.JooqConfiguration">
                <property name="databaseConfiguration" ref="jooqConfig"/>
            </bean>
        </property>
    </bean>

    <camelContext xmlns="http://camel.apache.org/schema/spring">
        <!-- Create and store entity -->
        <route id="insert-route">
            <from uri="direct:insert"/>
            <transform>
                <method ref="org.apache.camel.component.jooq.beans.BookStoreRecordBean" method="generate"/>
            </transform>
            <!-- Send entity to endpoint -->
            <to uri="jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord"/>
        </route>

        <!-- Create JOOQ ResultQuery and fetch -->
        <route id="execute-route">
            <from uri="direct:fetch"/>
            <transform>
                <method ref="org.apache.camel.component.jooq.beans.BookStoreRecordBean" method="select"/>
            </transform>
            <to uri="jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord/fetch"/>
            <log message="Fetched ${body}"/>
        </route>

        <!-- Create JOOQ Query end execute -->
        <route id="query-route">
            <from uri="direct:execute"/>
            <transform>
                <method ref="org.apache.camel.component.jooq.beans.BookStoreRecordBean" method="delete"/>
            </transform>
            <to uri="jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord/execute"/>
            <log message="Executed ${body}"/>
        </route>

        <!-- Consume entity -->
        <route id="queue-route">
            <from uri="jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord?consumeDelete=false"/>
            <log message="Consumed ${body}"/>
        </route>

        <!-- SQL: select -->
        <route id="sql-select">
            <from uri="direct:sql-select"/>
            <to uri="jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord/fetch?query=select * from book_store x where x.name = 'test'"/>
            <log message="Fetched ${body}"/>
        </route>

        <!-- SQL: delete -->
        <route id="sql-delete">
            <from uri="direct:sql-delete"/>
            <to uri="jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord/execute?query=delete from book_store x where x.name = 'test'"/>
            <log message="Fetched ${body}"/>
        </route>

        <!-- SQL: consume -->
        <route id="sql-consume">
            <from uri="jooq://org.apache.camel.component.jooq.db.tables.records.BookStoreRecord?query=select * from book_store x where x.name = 'test'"/>
            <log message="Fetched ${body}"/>
        </route>
    </camelContext>
</beans>
```

_Java-only: JOOQ bean with Query and ResultQuery factory methods_

```java
@Component
public class BookStoreRecordBean {
    private String name = "test";

    public BookStoreRecord generate() {
        return new BookStoreRecord(name);
    }

    public ResultQuery select() {
        return DSL.selectFrom(BOOK_STORE).where(BOOK_STORE.NAME.eq(name));
    }

    public Query delete() {
        return DSL.delete(BOOK_STORE).where(BOOK_STORE.NAME.eq(name));
    }
}
```

## Spring Boot Auto-Configuration

When using jooq with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jooq-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jooq.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jooq.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.jooq.configuration** | Component configuration (database connection, database entity type, etc.). The option is a org.apache.camel.component.jooq.JooqConfiguration type. |  | JooqConfiguration |
| **camel.component.jooq.consume-delete** | Delete entity after it is consumed. | true | Boolean |
| **camel.component.jooq.database-configuration** | To use a specific database configuration. The option is a org.jooq.Configuration type. |  | Configuration |
| **camel.component.jooq.enabled** | Whether to enable auto configuration of the jooq component. This is enabled by default. |  | Boolean |
| **camel.component.jooq.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.jooq.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.jooq.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.jooq.operation** | Type of operation to execute on query. | none | JooqOperation |
| **camel.component.jooq.query** | To execute plain SQL query. |  | String |