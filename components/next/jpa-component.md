# JPA

**Since Camel 1.0**

**Both producer and consumer are supported**

The JPA component enables you to store and retrieve Java objects from persistent storage using EJB 3’s Java Persistence Architecture (JPA). JPA is a standard interface layer that wraps Object/Relational Mapping (ORM) products such as OpenJPA, Hibernate, TopLink, and so on.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jpa</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

jpa:entityClassName\[?options\]

For sending to the endpoint, the _entityClassName_ is optional. If specified, it helps the [Type Converter](http://camel.apache.org/type-converter.md) to ensure the body is of the correct type.

For consuming, the _entityClassName_ is mandatory.

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

The JPA component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **aliases** (common) | Maps an alias to a JPA entity class. The alias can then be used in the endpoint URI (instead of the fully qualified class name). |  | Map |
| **entityManagerFactory** (common) | **Autowired** To use the EntityManagerFactory. This is strongly recommended to configure. |  | EntityManagerFactory |
| **joinTransaction** (common) | The camel-jpa component will join transaction by default. You can use this option to turn this off, for example if you use LOCAL\_RESOURCE and join transaction doesn’t work with your JPA provider. This option can also be set globally on the JpaComponent, instead of having to set it on all endpoints. | true | boolean |
| **sharedEntityManager** (common) | Whether to use Spring’s SharedEntityManager for the consumer/producer. Note in most cases joinTransaction should be set to false as this is not an EXTENDED EntityManager. | false | boolean |
| **transactionStrategy** (common) | To use the TransactionStrategy for running the operations in a transaction. |  | TransactionStrategy |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The JPA endpoint is configured using URI syntax:

jpa:entityType

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **entityType** (common) | **Required** Entity class name. |  | Class |

### Query Parameters (48 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **entityManagerFactory** (common) | The EntityManagerFactory to use. |  | EntityManagerFactory |
| **joinTransaction** (common) | The camel-jpa component will join transaction by default. You can use this option to turn this off, for example, if you use LOCAL\_RESOURCE and join transaction doesn’t work with your JPA provider. This option can also be set globally on the JpaComponent, instead of having to set it on all endpoints. | true | boolean |
| **maximumResults** (common) | Set the maximum number of results to retrieve on the Query. | \-1 | int |
| **namedQuery** (common) | To use a named query. |  | String |
| **nativeQuery** (common) | To use a custom native query. You may want to use the option resultClass also when using native queries. |  | String |
| **persistenceUnit** (common) | **Required** The JPA persistence unit used by default. | camel | String |
| **query** (common) | To use a custom query. |  | String |
| **resultClass** (common) | Defines the type of the returned payload (we will call entityManager.createNativeQuery(nativeQuery, resultClass) instead of entityManager.createNativeQuery(nativeQuery)). Without this option, we will return an object array. Only has an effect when using in conjunction with a native query when consuming data. |  | Class |
| **consumeDelete** (consumer) | If true, the entity is deleted after it is consumed; if false, the entity is not deleted. | true | boolean |
| **consumeLockEntity** (consumer) | Specifies whether to set an exclusive lock on each entity bean while processing the results from polling. | true | boolean |
| **deleteHandler** (consumer) | To use a custom DeleteHandler to delete the row after the consumer is done processing the exchange. |  | DeleteHandler |
| **lockModeType** (consumer) | 
To configure the lock mode on the consumer.

Enum values:

-   READ
    
-   WRITE
    
-   OPTIMISTIC
    
-   OPTIMISTIC\_FORCE\_INCREMENT
    
-   PESSIMISTIC\_READ
    
-   PESSIMISTIC\_WRITE
    
-   PESSIMISTIC\_FORCE\_INCREMENT
    
-   NONE
    





 | PESSIMISTIC\_WRITE | LockModeType |
| **maxMessagesPerPoll** (consumer) | An integer value to define the maximum number of messages to gather per poll. By default, no maximum is set. It can be used to avoid polling many thousands of messages when starting up the server. Set a value of 0 or negative to disable. |  | int |
| **preDeleteHandler** (consumer) | To use a custom Pre-DeleteHandler to delete the row after the consumer has read the entity. |  | DeleteHandler |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **skipLockedEntity** (consumer) | To configure whether to use NOWAIT on lock and silently skip the entity. | false | boolean |
| **transacted** (consumer) | Whether to run the consumer in transacted mode, by which all messages will either commit or rollback, when the entire batch has been processed. The default behavior (false) is to commit all the previously successfully processed messages, and only roll back the last failed message. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **parameters** (consumer (advanced)) | This key/value mapping is used for building the query parameters. It is expected to be of the generic type java.util.Map where the keys are the named parameters of a given JPA query and the values are their corresponding effective values you want to select for. When it’s used for producer, Simple expression can be used as a parameter value. It allows you to retrieve parameter values from the message body, header and etc. . This is a multi-value option with prefix: parameters. |  | Map |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **findEntity** (producer) | If enabled, then the producer will find a single entity by using the message body as a key and entityType as the class type. This can be used instead of a query to find a single entity. | false | boolean |
| **firstResult** (producer) | Set the position of the first result to retrieve. | \-1 | int |
| **flushOnSend** (producer) | Flushes the EntityManager after the entity bean has been persisted. | true | boolean |
| **outputTarget** (producer) | To put the query (or find) result in a header or property instead of the body. If the value starts with the prefix property:, put the result into the so named property, otherwise into the header. |  | String |
| **remove** (producer) | Indicates to use entityManager.remove(entity). | false | boolean |
| **singleResult** (producer) | If enabled, a query or a find which would return no results or more than one result, will throw an exception instead. | false | boolean |
| **useExecuteUpdate** (producer) | To configure whether to use executeUpdate() when producer executes a query. When you use INSERT, UPDATE or a DELETE statement as a named query, you need to specify this option to 'true'. | false | Boolean |
| **usePersist** (producer) | Indicates to use entityManager.persist(entity) instead of entityManager.merge(entity). Note: entityManager.persist(entity) doesn’t work for detached entities (where the EntityManager has to execute an UPDATE instead of an INSERT query)!. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **usePassedInEntityManager** (producer (advanced)) | If set to true, then Camel will use the EntityManager from the header JpaConstants.ENTITY\_MANAGER instead of the configured entity manager on the component/endpoint. This allows end users to control which entity manager will be in use. | false | boolean |
| **entityManagerProperties** (advanced) | Additional properties for the entity manager to use. This is a multi-value option with prefix: emf. |  | Map |
| **sharedEntityManager** (advanced) | Whether to use Spring’s SharedEntityManager for the consumer/producer. Note in most cases, joinTransaction should be set to false as this is not an EXTENDED EntityManager. | false | boolean |
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

The JPA component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelEntityManager** (common) Constant: [`ENTITY_MANAGER`](https://javadoc.io/doc/org.apache.camel/camel-jpa/latest/org/apache/camel/component/jpa/JpaConstants.html#ENTITY_MANAGER) | The JPA EntityManager object. |  | EntityManager |
| **CamelJpaParameters** (producer) Constant: [`JPA_PARAMETERS_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-jpa/latest/org/apache/camel/component/jpa/JpaConstants.html#JPA_PARAMETERS_HEADER) | Alternative way for passing query parameters as an Exchange header. |  | Map |
| **CamelJpaMaximumResults** (producer) Constant: [`JPA_MAXIMUM_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-jpa/latest/org/apache/camel/component/jpa/JpaConstants.html#JPA_MAXIMUM_RESULTS) | Defines the maximum number of results to retrieve on the query; takes precedence over the value set on the endpoint, if any. |  |  |
| **CamelJpaFirstResult** (producer) Constant: [`JPA_FIRST_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-jpa/latest/org/apache/camel/component/jpa/JpaConstants.html#JPA_FIRST_RESULT) | Defines the position of the first result to retrieve; takes precedence over the value set on the endpoint, if any. |  |  |

## Usage

### Sending to the endpoint

You can store a Java entity bean in a database by sending it to a JPA producer endpoint. The body of the _In_ message is assumed to be an entity bean (that is a POJO with an [@Entity](https://jakarta.ee/specifications/persistence/2.2/apidocs/javax/persistence/entity) annotation on it) or a collection or array of entity beans.

If the body is a List of entities, make sure to use **entityType=java.util.List** as a configuration passed to the producer endpoint.

If the body does not contain one of the previous listed types, put a Message Translator in front of the endpoint to perform the necessary conversion first.

You can use `query`, `namedQuery` or `nativeQuery` for the producer as well. Also in the value of the `parameters`, you can use Simple expression which allows you to retrieve parameter values from Message body, header, etc. Those query can be used for retrieving a set of data with using `SELECT` JPQL/SQL statement as well as executing bulk update/delete with using `UPDATE`/`DELETE` JPQL/SQL statement. Please note that you need to specify `useExecuteUpdate` to `true` if you execute `UPDATE`/`DELETE` with `namedQuery` as Camel doesn’t look into the named query unlike `query` and `nativeQuery`.

### Consuming from the endpoint

Consuming messages from a JPA consumer endpoint removes (or updates) entity beans in the database. This allows you to use a database table as a logical queue: consumers take messages from the queue and then delete/update them to logically remove them from the queue.

If you do not wish to delete the entity bean when it has been processed (and when routing is done), you can specify `consumeDelete=false` on the URI. This will result in the entity being processed in each poll.

If you would rather perform some update on the entity to mark it as processed (such as to exclude it from a future query), then you can annotate a method with `@Consumed` (org.apache.camel.component.jpa.Consumed). It will be invoked on your entity bean when the entity bean has been processed (and when routing is done).

You can use `@PreConsumed` (org.apache.camel.component.jpa.PreConsumed) which will be invoked on your entity bean before it has been processed (before routing).

If you are consuming a lot of rows (100K+) and experience `OutOfMemory` problems, you should set the `maximumResults` to a sensible value.

### Configuring EntityManagerFactory

It’s strongly advised to configure the JPA component to use a specific `EntityManagerFactory` instance. If failed to do so each `JpaEndpoint` will auto create their own instance of `EntityManagerFactory` which most often is not what you want.

For example, you can instantiate a JPA component that references the `myEMFactory` entity manager factory, as follows:

```xml
<bean id="jpa" class="org.apache.camel.component.jpa.JpaComponent">
   <property name="entityManagerFactory" ref="myEMFactory"/>
</bean>
```

The `JpaComponent` looks up automatically the `EntityManagerFactory` from the Registry which means you do not need to configure this on the `JpaComponent` as shown above. You only need to do so if there is ambiguity, in which case Camel will log a WARN.

### Configuring TransactionStrategy

The `TransactionStrategy` is a vendor neutral abstraction that allows `camel-jpa` to easily plug in and work with Spring `TransactionManager` or Quarkus Transaction API.

The `JpaComponent` looks up automatically the `TransactionStrategy` from the Registry. If Camel cannot find any `TransactionStrategy` instance registered, it will also look up for the `TransactionTemplate` and try to extract `TransactionStrategy` from it.

If none `TransactionTemplate` is available in the registry, `JpaEndpoint` will auto create a default instance (`org.apache.camel.component.jpa.DefaultTransactionStrategy`) of `TransactionStrategy` which most often is not what you want.

If more than single instance of the `TransactionStrategy` is found, Camel will log a WARN. In such cases you might want to instantiate and explicitly configure a JPA component that references the `myTransactionManager` transaction manager, as follows:

```xml
<bean id="jpa" class="org.apache.camel.component.jpa.JpaComponent">
   <property name="entityManagerFactory" ref="myEMFactory"/>
   <property name="transactionStrategy" ref="myTransactionStrategy"/>
</bean>
```

### Using a consumer with a named query

For consuming only selected entities, you can use the `namedQuery` URI query option. First, you have to define the named query in the JPA Entity class:

_Java-only: JPA entity class definition with @NamedQuery annotation_

```java
@Entity
@NamedQuery(name = "step1", query = "select x from MultiSteps x where x.step = 1")
public class MultiSteps {
   ...
}
```

After that, you can define a consumer uri like this one:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jpa://org.apache.camel.examples.MultiSteps?namedQuery=step1")
    .to("bean:myBusinessLogic");
```

```xml
<route>
  <from uri="jpa://org.apache.camel.examples.MultiSteps?namedQuery=step1"/>
  <to uri="bean:myBusinessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: jpa://org.apache.camel.examples.MultiSteps
      parameters:
        namedQuery: step1
      steps:
        - to:
            uri: bean:myBusinessLogic
```

### Using a consumer with a query

For consuming only selected entities, you can use the `query` URI query option. You only have to define the query option:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jpa://org.apache.camel.examples.MultiSteps?query=select o from org.apache.camel.examples.MultiSteps o where o.step = 1")
    .to("bean:myBusinessLogic");
```

```xml
<route>
    <from uri="jpa://org.apache.camel.examples.MultiSteps?query=select o from org.apache.camel.examples.MultiSteps o where o.step = 1"/>
    <to uri="bean:myBusinessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: jpa://org.apache.camel.examples.MultiSteps
      parameters:
        query: "select o from org.apache.camel.examples.MultiSteps o where o.step = 1"
    steps:
      - to:
          uri: bean:myBusinessLogic
```

### Using a consumer with a native query

For consuming only selected entities, you can use the `nativeQuery` URI query option. You only have to define the native query option:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jpa://org.apache.camel.examples.MultiSteps?nativeQuery=select * from MultiSteps where step = 1")
    .to("bean:myBusinessLogic");
```

```xml
<route>
    <from uri="jpa://org.apache.camel.examples.MultiSteps?nativeQuery=select * from MultiSteps where step = 1"/>
    <to uri="bean:myBusinessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: jpa://org.apache.camel.examples.MultiSteps
      parameters:
        nativeQuery: "select * from MultiSteps where step = 1"
    steps:
      - to:
          uri: bean:myBusinessLogic
```

If you use the native query option, you will receive an object array in the message body.

### Using a producer with a named query

For retrieving selected entities or execute bulk update/delete, you can use the `namedQuery` URI query option. First, you have to define the named query in the JPA Entity class:

_Java-only: JPA entity class definition with @NamedQuery annotation_

```java
@Entity
@NamedQuery(name = "step1", query = "select x from MultiSteps x where x.step = 1")
public class MultiSteps {
   ...
}
```

After that, you can define a producer uri like this one:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:namedQuery")
    .to("jpa://org.apache.camel.examples.MultiSteps?namedQuery=step1");
```

```xml
<route>
  <from uri="direct:namedQuery"/>
  <to uri="jpa://org.apache.camel.examples.MultiSteps?namedQuery=step1"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:namedQuery
      steps:
        - to:
            uri: jpa://org.apache.camel.examples.MultiSteps
            parameters:
              namedQuery: step1
```

Note that you need to specify `useExecuteUpdate` option to `true` to execute `UPDATE`/`DELETE` statement as a named query.

### Using a producer with a query

For retrieving selected entities or execute bulk update/delete, you can use the `query` URI query option. You only have to define the query option:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:query")
    .to("jpa://org.apache.camel.examples.MultiSteps?query=select o from org.apache.camel.examples.MultiSteps o where o.step = 1");
```

```xml
<route>
    <from uri="direct:query"/>
    <to uri="jpa://org.apache.camel.examples.MultiSteps?query=select o from org.apache.camel.examples.MultiSteps o where o.step = 1"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:query
    steps:
      - to:
          uri: jpa://org.apache.camel.examples.MultiSteps
          parameters:
            query: "select o from org.apache.camel.examples.MultiSteps o where o.step = 1"
```

### Using a producer with a native query

For retrieving selected entities or execute bulk update/delete, you can use the `nativeQuery` URI query option. You only have to define the native query option:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:nativeQuery")
    .to("jpa://org.apache.camel.examples.MultiSteps?resultClass=org.apache.camel.examples.MultiSteps&nativeQuery=select * from MultiSteps where step = 1");
```

```xml
<route>
    <from uri="direct:nativeQuery"/>
    <to uri="jpa://org.apache.camel.examples.MultiSteps?resultClass=org.apache.camel.examples.MultiSteps&amp;nativeQuery=select * from MultiSteps where step = 1"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:nativeQuery
    steps:
      - to:
          uri: jpa://org.apache.camel.examples.MultiSteps
          parameters:
            resultClass: org.apache.camel.examples.MultiSteps
            nativeQuery: "select * from MultiSteps where step = 1"
```

If you use the native query option without specifying `resultClass`, you will receive an object array in the message body.

### Using the JPA-Based Idempotent Repository

The Idempotent Consumer from the [EIP patterns](http://camel.apache.org/enterprise-integration-patterns.md) is used to filter out duplicate messages. A JPA-based idempotent repository is provided.

To use the JPA based idempotent repository.

Procedure

1.  Set up a `persistence-unit` in the persistence.xml file:
    
2.  Set up a `org.springframework.orm.jpa.JpaTemplate` which is used by the `org.apache.camel.processor.idempotent.jpa.JpaMessageIdRepository`:
    
3.  Configure the error formatting macro: snippet: java.lang.IndexOutOfBoundsException: Index: 20, Size: 20
    
4.  Configure the idempotent repository: `org.apache.camel.processor.idempotent.jpa.JpaMessageIdRepository`:
    
5.  Create the JPA idempotent repository in the Spring XML file:
    

```xml
<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route id="JpaMessageIdRepositoryTest">
        <from uri="direct:start" />
        <idempotentConsumer idempotentRepository="jpaStore">
            <header>messageId</header>
            <to uri="mock:result" />
        </idempotentConsumer>
    </route>
</camelContext>
```

## Important Development Notes

If you run the [tests of this component](https://github.com/apache/camel/tree/main/components/camel-jpa/src/test) directly inside your IDE, and not through Maven, then you could see exceptions like these:

org.springframework.transaction.CannotCreateTransactionException: Could not open JPA EntityManager for transaction; nested exception is
<openjpa-2.2.1-r422266:1396819 nonfatal user error> org.apache.openjpa.persistence.ArgumentException: This configuration disallows runtime optimization,
but the following listed types were not enhanced at build time or at class load time with a javaagent: "org.apache.camel.examples.SendEmail".
    at org.springframework.orm.jpa.JpaTransactionManager.doBegin(JpaTransactionManager.java:427)
    at org.springframework.transaction.support.AbstractPlatformTransactionManager.getTransaction(AbstractPlatformTransactionManager.java:371)
    at org.springframework.transaction.support.TransactionTemplate.execute(TransactionTemplate.java:127)
    at org.apache.camel.processor.jpa.JpaRouteTest.cleanupRepository(JpaRouteTest.java:96)
    at org.apache.camel.processor.jpa.JpaRouteTest.createCamelContext(JpaRouteTest.java:67)
    at org.apache.camel.test.junit6.CamelTestSupport.doSetUp(CamelTestSupport.java:238)
    at org.apache.camel.test.junit6.CamelTestSupport.setUp(CamelTestSupport.java:208)

The problem here is that the source has been compiled or recompiled through your IDE and not through Maven, which would [enhance the byte-code at build time](https://github.com/apache/camel/blob/main/components/camel-jpa/pom.xml). To overcome this, you need to enable [dynamic byte-code enhancement of OpenJPA](http://openjpa.apache.org/entity-enhancement.html#dynamic-enhancement). For example, assuming the current OpenJPA version being used in Camel is 2.2.1, to run the tests inside your IDE, you would need to pass the following argument to the JVM:

\-javaagent:<path\_to\_your\_local\_m2\_cache>/org/apache/openjpa/openjpa/2.2.1/openjpa-2.2.1.jar

## Spring Boot Auto-Configuration

When using jpa with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jpa-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jpa.aliases** | Maps an alias to a JPA entity class. The alias can then be used in the endpoint URI (instead of the fully qualified class name). |  | Map |
| **camel.component.jpa.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jpa.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.jpa.enabled** | Whether to enable auto configuration of the jpa component. This is enabled by default. |  | Boolean |
| **camel.component.jpa.entity-manager-factory** | To use the EntityManagerFactory. This is strongly recommended to configure. The option is a jakarta.persistence.EntityManagerFactory type. |  | EntityManagerFactory |
| **camel.component.jpa.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.jpa.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.jpa.join-transaction** | The camel-jpa component will join transaction by default. You can use this option to turn this off, for example if you use LOCAL\_RESOURCE and join transaction doesn’t work with your JPA provider. This option can also be set globally on the JpaComponent, instead of having to set it on all endpoints. | true | Boolean |
| **camel.component.jpa.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.jpa.shared-entity-manager** | Whether to use Spring’s SharedEntityManager for the consumer/producer. Note in most cases joinTransaction should be set to false as this is not an EXTENDED EntityManager. | false | Boolean |
| **camel.component.jpa.transaction-strategy** | To use the TransactionStrategy for running the operations in a transaction. The option is a org.apache.camel.component.jpa.TransactionStrategy type. |  | TransactionStrategy |