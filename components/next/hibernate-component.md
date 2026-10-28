# Hibernate

**Since Camel 4.24**

**Both producer and consumer are supported**

The Hibernate component provides integration with relational databases using **Hibernate ORM 8**.

The component uses Hibernate’s native `SessionFactory`, `Session`, `StatelessSession`, `SelectionQuery`, and `MutationQuery` APIs.

It supports HQL selection and mutation queries, natural-id lookups, Hibernate filters, read-only queries, streaming query results, stateless insert and upsert operations, multi-tenancy, and competing consumers using `SKIP_LOCKED`.

The component can either reuse an existing Hibernate `SessionFactory` or bootstrap one using a configured `DataSource` and explicit entity classes.

The component does not use Jakarta Persistence (JPA), `camel-jpa`, or Spring `PlatformTransactionManager`.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-hibernate</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

> **Warning**
> When using Spring Boot, the component does not work with the Hibernate ORM and Jakarta Persistence versions managed by Spring Boot. See [Using with Spring Boot](#hibernate-spring-boot).

## URI format

### hibernate:entityClassName

Where `entityClassName` is the fully qualified name of the target entity class.

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

The Hibernate component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataSource** (common) | The DataSource to use for bootstrapping the SessionFactory (bean reference or registry name). |  | Object |
| **hibernateProperties** (common) | Arbitrary Hibernate configuration properties passthrough map. |  | Map |
| **schemaAction** (common) | 
Schema generation action: none, validate, update, create, create-drop, create-only, drop.

Enum values:

-   none
    
-   validate
    
-   update
    
-   create
    
-   create-drop
    
-   create-only
    
-   drop
    





 | none | String |
| **sessionFactory** (common) | The Hibernate SessionFactory to use. |  | SessionFactory |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Hibernate endpoint is configured using URI syntax:

hibernate:entityClassName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **entityClassName** (common) | **Required** Target entity class name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **filters** (common) | Hibernate filters and their parameter values. This is a multi-value option with prefix: filter. |  | Map |
| **readOnly** (common) | Whether the Hibernate session and selection query should be read-only. | false | boolean |
| **selectionQuery** (common) | The HQL selection query to execute. |  | String |
| **tenantIdentifier** (common) | The tenant identifier used to create the Hibernate session. |  | String |
| **consumeDelete** (consumer) | Whether to delete consumed entities after successful processing. | true | boolean |
| **maximumResults** (consumer) | The maximum number of entities to retrieve in a single poll. |  | int |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **skipLocked** (consumer) | Whether the consumer should skip rows that are already locked by another consumer. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **mutationQuery** (producer) | The HQL mutation query to execute. |  | String |
| **naturalIdParameters** (producer) | The natural-id property values used for lookup. String values can use Simple expressions from the message. This is a multi-value option with prefix: naturalId. |  | Map |
| **statelessOperation** (producer) | 

Stateless operation to perform: insert or upsert.

Enum values:

-   INSERT
    
-   UPSERT
    





 |  | StatelessOperation |
| **streaming** (producer) | Whether selection query results should be returned as a stream. | false | boolean |
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

The Hibernate component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHibernateParameters** (producer) Constant: [`HIBERNATE_PARAMETERS`](https://javadoc.io/doc/org.apache.camel/camel-hibernate/latest/org/apache/camel/component/hibernate/HibernateConstants.html#HIBERNATE_PARAMETERS) | Map of named parameters to bind to the Hibernate query, or to override natural-id lookup values. |  | Map |

## Message Body

The message body at each side of the Hibernate component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `pojo` | The configured selection query emits one entity per message.
With `entityClassName` set: an object of the class it names, or null.

 |
| **Producer input** | `any` | 

Stateless insert/upsert consumes the entity in the message body. For selection and mutation queries, the body is not used; named parameters come from the CamelHibernateParameters header. Natural-id values can be configured on the endpoint or supplied in that header.

-   With `statelessOperation` set: `pojo`
    





 |
| **Producer output** | `pojo`, `list`, `value`, `null` or `unchanged` | 

The result depends on the operation: a selection query returns a list, or a java.util.stream.Stream when streaming=true; a mutation query returns the affected-row count; a natural-id lookup returns the entity or null; stateless operations leave the body unchanged.

-   With `streaming=true`: `iterator`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### SessionFactory configuration

The component can use an existing Hibernate `SessionFactory` or create one during startup.

#### Using an existing SessionFactory

An existing `SessionFactory` can be configured directly on the component:

```java
HibernateComponent component = new HibernateComponent();
component.setSessionFactory(sessionFactory);

context.addComponent("hibernate", component);
```

The component does not own an externally supplied `SessionFactory` and therefore does not close it when the component stops.

If no `SessionFactory` is explicitly configured, the component attempts to reuse a `SessionFactory` available in the Camel registry.

#### Bootstrapping a SessionFactory

The component can bootstrap a `SessionFactory` using a `DataSource` and explicit entity classes:

```java
HibernateComponent component = new HibernateComponent();
component.setDataSource(dataSource);
component.setEntityClasses(new Class[] {
    MyEntity.class
});
component.setSchemaAction("update");

context.addComponent("hibernate", component);
```

The `DataSource` can be supplied directly or as a Camel registry name.

Supported values for `schemaAction` are:

-   `none`
    
-   `validate`
    
-   `update`
    
-   `create`
    
-   `create-drop`
    
-   `create-only`
    
-   `drop`
    

When the component creates the `SessionFactory`, it owns the resulting `SessionFactory` and closes it when the component stops.

Hibernate determines the database dialect automatically; the component does not require an explicit dialect configuration.

> **Note**
> Entity package scanning is not currently provided. Use `entityClasses` to explicitly register the entity classes used by the `SessionFactory`. `entityClasses` is currently a Java/Spring component configuration property, not a URI option; YAML routes should use a `SessionFactory` that has already been configured with its entity classes unless the component is configured separately.

#### Hibernate properties

Additional Hibernate configuration properties can be supplied through `hibernateProperties`.

```java
component.setHibernateProperties(Map.of(
    "hibernate.show_sql", true,
    "hibernate.format_sql", true
));
```

The supplied properties are passed directly to Hibernate during `SessionFactory` bootstrap.

### Producer operations

When acting as a producer, the endpoint performs exactly one configured operation.

The supported operations are:

-   `selectionQuery`
    
-   `mutationQuery`
    
-   `naturalIdParameters`
    
-   `statelessOperation`
    

The endpoint validates this configuration during startup.

#### Selection query

Use `selectionQuery` to execute an HQL selection query using Hibernate’s `SelectionQuery` API.

```java
from("direct:findEntities")
    .to("hibernate:com.example.MyEntity?selectionQuery=from MyEntity where status = :status");
```

Query parameters are supplied through the `CamelHibernateParameters` message header:

```java
exchange.getMessage().setHeader(
    HibernateConstants.HIBERNATE_PARAMETERS,
    Map.of("status", "ACTIVE"));
```

The query result is placed in the message body.

#### Mutation query

Use `mutationQuery` to execute an HQL mutation query using Hibernate’s `MutationQuery` API.

```java
from("direct:updateEntities")
    .to("hibernate:com.example.MyEntity?mutationQuery=update MyEntity set status = :status where status = :oldStatus");
```

Parameters are supplied through the `CamelHibernateParameters` header:

```java
exchange.getMessage().setHeader(
    HibernateConstants.HIBERNATE_PARAMETERS,
    Map.of(
        "status", "INACTIVE",
        "oldStatus", "EXPIRED"));
```

The mutation update count is placed in the message body.

#### Natural-id lookup

Hibernate entities that define a natural identifier can be looked up using `naturalId.` URI parameters (`naturalIdParameters` in Java).

String values are evaluated with Simple, so the natural-id can come from the message. Values can also be passed or overridden with the `CamelHibernateParameters` header.

> **Note**
> Values configured through the `naturalId.` URI prefix are Strings. For non-String natural-id types, such as `Long`, configure the `naturalIdParameters` map using Java or a Camel registry bean so the appropriate Java type is preserved. Individual values in the `naturalId.` URI prefix do not resolve `#bean` references.

```java
from("direct:findByEmail")
    .to("hibernate:com.example.User?naturalId.email=${header.email}");
```

The lookup uses Hibernate’s native natural-id functionality rather than constructing an HQL query.

#### Read-only queries

Set `readOnly=true` for a selection query when the returned entities are not intended to be modified.

```java
from("direct:readEntities")
    .to("hibernate:com.example.MyEntity?selectionQuery=from MyEntity&readOnly=true");
```

The component configures both the Hibernate `Session` and the `SelectionQuery` as read-only.

#### Hibernate filters

Hibernate filters can be configured through the `filters` endpoint option.

The configuration contains the filter name and its parameter values. The component enables the configured filters on the Hibernate `Session` before executing the operation.

URI parameters use the `filter.` prefix:

```text
hibernate:com.example.MyEntity?selectionQuery=from MyEntity&filter.tenantFilter.tenantId=tenant-a
```

Java and `#bean` configuration is also supported:

```java
Map<String, Map<String, Object>> filters = Map.of(
    "tenantFilter", Map.of("tenantId", "tenant-a"));

endpoint.setFilters(filters);
```

> **Note**
> Values configured through the `filter.` URI prefix are Strings. For non-String filter parameter types, such as `Long`, configure the values using Java or `#bean` configuration so the appropriate Java type is preserved.

When a producer reuses a `Session` supplied by a Hibernate consumer, its filter configuration must match the filters associated with that `Session`. If the producer’s filters differ, the shared `Session` is not reused and the producer opens a separate `Session` so that its filters can be applied without changing the consumer’s session state.

When the producer’s filters differ from the consumer’s session, the producer opens a separate `Session`. If the consumer holds a pessimistic lock, such as when `skipLocked=true`, the producer’s separate session may block waiting for a lock held by the consumer. Configure compatible filters when the producer needs to operate on rows locked by the consumer so that the consumer session can be reused.

#### Multi-tenancy

A tenant identifier can be supplied through `tenantIdentifier`.

```java
from("direct:tenantEntities")
    .to("hibernate:com.example.MyEntity?selectionQuery=from MyEntity&tenantIdentifier=tenant-a");
```

The tenant identifier is used when creating the Hibernate `Session`.

The tenant is configured by the route rather than being taken from an untrusted message header.

#### Stateless insert

Use `statelessOperation=insert` to insert the entity contained in the message body using Hibernate’s native `StatelessSession`.

```java
from("direct:insertEntity")
    .to("hibernate:com.example.MyEntity?statelessOperation=insert");
```

#### Stateless upsert

Use `statelessOperation=upsert` to perform a stateless upsert using Hibernate’s native `StatelessSession`.

```java
from("direct:upsertEntity")
    .to("hibernate:com.example.MyEntity?statelessOperation=upsert");
```

The supported stateless operations are `insert` and `upsert`.

### Consumer operations

When acting as a consumer, the endpoint periodically executes its configured `selectionQuery`.

Each selected entity is delivered to the route as the message body.

By default, successfully processed entities are deleted from the database (`consumeDelete=true`). Set `consumeDelete=false` to leave consumed entities in the database.

When a Hibernate consumer invokes a Hibernate producer in the same route processing thread, the producer reuses the consumer’s Hibernate `Session` and transaction when the producer’s session requirements are compatible with the consumer session. This allows the producer to operate on entities and locks held by the consumer without opening a second session.

Session sharing has limits. A copied exchange does not carry the live Hibernate `Session`, so processing a copied exchange can open a separate session. Stateless operations always use their own `StatelessSession`.

If an operation on the shared session marks the Hibernate transaction rollback-only, the consumer rolls back the whole poll even if the route handles the operation’s exception. The batch may be delivered again on a subsequent poll.

If processing an entity fails, the consumer rolls back the active poll transaction and stops processing the current batch. This prevents changes made earlier in the same poll from being committed after a later entity fails. Entities processed before the failure may therefore be delivered again on a subsequent poll. A consistently failing entity can prevent later rows from being processed until the failure is resolved.

For example:

```java
from("hibernate:com.example.MyEntity?selectionQuery=from MyEntity&maximumResults=100&initialDelay=1000&delay=5000")
    .to("direct:processEntity");
```

#### Maximum results

Use `maximumResults` to limit the number of entities retrieved during a poll.

```java
from("hibernate:com.example.MyEntity?selectionQuery=from MyEntity&maximumResults=100")
    .to("direct:processEntity");
```

#### Competing consumers with SKIP LOCKED

Set `skipLocked=true` to configure the selection query with a pessimistic write lock and Hibernate’s `SKIP_LOCKED` timeout.

```java
from("hibernate:com.example.MyEntity?selectionQuery=from MyEntity&skipLocked=true&maximumResults=100")
    .to("direct:processEntity");
```

This allows multiple consumer instances to compete for database rows while skipping rows already locked by another consumer.

The database and Hibernate dialect must support the required locking behavior.

When processing uses a copied exchange that cannot reuse the consumer’s `Session`, the processing may use a separate session and therefore does not share the consumer’s live transaction or session-level locks.

### Streaming query results

Set `streaming=true` on a selection query to return the results as a Java `Stream`.

```java
from("direct:streamEntities")
    .to("hibernate:com.example.MyEntity?selectionQuery=from MyEntity&streaming=true")
    .process(exchange -> {
        Stream<?> stream = exchange.getMessage().getBody(Stream.class);
        try (stream) {
            stream.forEach(entity -> {
                // process entity
            });
        }
    });
```

The returned stream is backed by a live Hibernate session. Consume and close it within the same route exchange, before the exchange completes; the component closes an owned session when the exchange completes.

The Hibernate `Session` and transaction remain open while the stream is being consumed.

The returned stream must be closed after consumption so that the Hibernate session and transaction can be closed.

Streaming is not supported inside a transacted Camel exchange because the stream can outlive the route transaction while the Hibernate `Session` and transaction remain open.

## Query parameters

Query parameters are supplied through the `CamelHibernateParameters` message header.

For example:

```java
Map<String, Object> parameters = Map.of(
    "status", "ACTIVE",
    "country", "US");

exchange.getMessage().setHeader(
    HibernateConstants.HIBERNATE_PARAMETERS,
    parameters);
```

The parameters are bound to the configured Hibernate query.

The component does not support replacing the configured query through a message header. Query text remains part of the route configuration.

## Transactions

The component uses native Hibernate transactions through `Session` and `StatelessSession`.

Regular producer and consumer operations create a Hibernate `Session` and transaction. Each operation commits its own transaction unless the configured `SessionFactory` is backed by JTA.

Stateless operations use a Hibernate `StatelessSession` and transaction. Stateless operations do not participate in consumer session reuse.

Entities may become detached when the Hibernate `Session` is closed. Lazy associations should therefore be initialized while the session is active. This is particularly important when consumer results are sent to asynchronous endpoints such as `seda:` or `wireTap:`, where processing can outlive the consumer’s poll session.

The component does not provide its own JTA or Spring transaction-manager integration. A transacted Camel exchange requires a JTA-backed `SessionFactory`; using a resource-local `SessionFactory` in a transacted exchange fails fast.

Streaming is not supported inside a transacted Camel exchange because the returned stream can outlive the route transaction while the Hibernate `Session` and transaction remain open.

The component does not use `camel-jpa`, Jakarta Persistence, Spring `PlatformTransactionManager`, or a JPA transaction strategy.

## Examples

### Selection query

Java

```java
from("direct:findEntities")
    .to("hibernate:com.example.MyEntity?selectionQuery=from MyEntity where status = :status");
```

XML

```xml
<route>
    <from uri="direct:findEntities"/>
    <to uri="hibernate:com.example.MyEntity?selectionQuery=from MyEntity where status = :status"/>
</route>
```

YAML

```yaml
- route:
    from:
      uri: direct:findEntities
      steps:
        - to:
            uri: hibernate:com.example.MyEntity
            parameters:
              selectionQuery: "from MyEntity where status = :status"
```

### Mutation query

Java

```java
from("direct:updateEntities")
    .to("hibernate:com.example.MyEntity?mutationQuery=update MyEntity set status = :status where id = :id");
```

XML

```xml
<route>
    <from uri="direct:updateEntities"/>
    <to uri="hibernate:com.example.MyEntity?mutationQuery=update MyEntity set status = :status where id = :id"/>
</route>
```

YAML

```yaml
- route:
    from:
      uri: direct:updateEntities
      steps:
        - to:
            uri: hibernate:com.example.MyEntity
            parameters:
              mutationQuery: "update MyEntity set status = :status where id = :id"
```

### Stateless insert

Java

```java
from("direct:insertEntity")
    .to("hibernate:com.example.MyEntity?statelessOperation=insert");
```

XML

```xml
<route>
    <from uri="direct:insertEntity"/>
    <to uri="hibernate:com.example.MyEntity?statelessOperation=insert"/>
</route>
```

YAML

```yaml
- route:
    from:
      uri: direct:insertEntity
      steps:
        - to:
            uri: hibernate:com.example.MyEntity
            parameters:
              statelessOperation: insert
```

### Stateless upsert

Java

```java
from("direct:upsertEntity")
    .to("hibernate:com.example.MyEntity?statelessOperation=upsert");
```

XML

```xml
<route>
    <from uri="direct:upsertEntity"/>
    <to uri="hibernate:com.example.MyEntity?statelessOperation=upsert"/>
</route>
```

YAML

```yaml
- route:
    from:
      uri: direct:upsertEntity
      steps:
        - to:
            uri: hibernate:com.example.MyEntity
            parameters:
              statelessOperation: upsert
```

### Polling consumer

Java

```java
from("hibernate:com.example.MyEntity?selectionQuery=from MyEntity&maximumResults=100&initialDelay=1000&delay=5000")
    .to("direct:processEntity");
```

XML

```xml
<route>
    <from uri="hibernate:com.example.MyEntity?selectionQuery=from MyEntity&amp;maximumResults=100&amp;initialDelay=1000&amp;delay=5000"/>
    <to uri="direct:processEntity"/>
</route>
```

YAML

```yaml
- route:
    from:
      uri: hibernate:com.example.MyEntity
      parameters:
        selectionQuery: "from MyEntity"
        maximumResults: 100
        initialDelay: 1000
        delay: 5000
      steps:
        - to:
            uri: direct:processEntity
```

### Competing consumers with SKIP LOCKED

Java

```java
from("hibernate:com.example.MyEntity?selectionQuery=from MyEntity&skipLocked=true&maximumResults=100")
    .to("direct:processEntity");
```

XML

```xml
<route>
    <from uri="hibernate:com.example.MyEntity?selectionQuery=from MyEntity&amp;skipLocked=true&amp;maximumResults=100"/>
    <to uri="direct:processEntity"/>
</route>
```

YAML

```yaml
- route:
    from:
      uri: hibernate:com.example.MyEntity
      parameters:
        selectionQuery: "from MyEntity"
        skipLocked: true
        maximumResults: 100
      steps:
        - to:
            uri: direct:processEntity
```

### Streaming

Java

```java
from("direct:streamEntities")
    .to("hibernate:com.example.MyEntity?selectionQuery=from MyEntity&streaming=true")
    .process(exchange -> {
        Stream<?> stream = exchange.getMessage().getBody(Stream.class);
        try (stream) {
            stream.forEach(entity -> {
                // process entity
            });
        }
    });
```

XML

```xml
<route>
    <from uri="direct:streamEntities"/>
    <to uri="hibernate:com.example.MyEntity?selectionQuery=from MyEntity&amp;streaming=true"/>
</route>
```

YAML

```yaml
- route:
    from:
      uri: direct:streamEntities
      steps:
        - to:
            uri: hibernate:com.example.MyEntity
            parameters:
              selectionQuery: "from MyEntity"
              streaming: true
```

### Native Hibernate SessionFactory configuration

Java

```java
HibernateComponent component = new HibernateComponent();
component.setSessionFactory(sessionFactory);
context.addComponent("hibernate", component);

from("direct:findEntities")
    .to("hibernate:com.example.MyEntity?selectionQuery=from MyEntity");
```

XML

```xml
<bean id="hibernate" class="org.apache.camel.component.hibernate.HibernateComponent">
    <property name="sessionFactory" ref="sessionFactory"/>
</bean>
```

YAML

```yaml
- route:
    from:
      uri: direct:findEntities
      steps:
        - to:
            uri: hibernate:com.example.MyEntity
            parameters:
              selectionQuery: "from MyEntity"
```

### Bootstrapping a SessionFactory

Java

```java
HibernateComponent component = new HibernateComponent();
component.setDataSource(dataSource);
component.setEntityClasses(new Class[] {
    MyEntity.class
});
component.setSchemaAction("update");
context.addComponent("hibernate", component);
```

XML

```xml
<bean id="hibernate" class="org.apache.camel.component.hibernate.HibernateComponent">
    <property name="dataSource" ref="dataSource"/>
    <property name="entityClasses">
        <array>
            <value>com.example.MyEntity</value>
        </array>
    </property>
    <property name="schemaAction" value="update"/>
</bean>
```

YAML

```yaml
- route:
    from:
      uri: direct:findEntities
      steps:
        - to:
            uri: hibernate:com.example.MyEntity
            parameters:
              selectionQuery: "from MyEntity"
```

## Using with Spring Boot

> **Warning**
> This component requires Hibernate ORM 8 and Jakarta Persistence 4.0. The Spring Boot dependency management provides Hibernate ORM 7.x and Jakarta Persistence 3.2, which are not compatible with this component: the application starts, but some operations, such as mutation queries and `skipLocked` consumers, fail at runtime with `NoSuchMethodError`.
>
> To use `camel-hibernate-starter`:
>
> -   Override the Hibernate ORM and Jakarta Persistence versions with the ones used by this Camel release (see the `camel-hibernate` dependencies).
>     
> -   Do not combine it with Spring Data JPA or with the Spring Boot JPA and Hibernate auto-configuration (for example `spring-boot-starter-data-jpa`). They do not support Hibernate ORM 8 and Jakarta Persistence 4.0 yet.
>     
>
> An application can contain only one Hibernate ORM and one Jakarta Persistence version, so the override applies to the whole application, including any other library that uses Jakarta Persistence, such as `camel-jpa`.

When the application uses `spring-boot-starter-parent`, set the version properties in the `pom.xml`:

```xml
<properties>
    <hibernate.version>8.0.0.Beta3</hibernate.version>
    <jakarta-persistence.version>4.0.0-M7</jakarta-persistence.version>
</properties>
```

When the application imports the `spring-boot-dependencies` BOM instead, declare `org.hibernate.orm:hibernate-core` and `jakarta.persistence:jakarta.persistence-api` with these versions in `dependencyManagement`, before the Spring Boot BOM.

Without the Spring Boot JPA and Hibernate auto-configuration, no `SessionFactory` is created by Spring Boot. Configure the component to bootstrap one from a `DataSource` and entity classes, or provide your own Hibernate ORM 8 `SessionFactory` bean, as described in the SessionFactory configuration section above.

## Limitations and deferred features

The following features are intentionally not part of the current implementation:

-   **Package entity scanning:** `packagesToScan` is not currently implemented. Entity classes are registered explicitly through `entityClasses`.
    
-   **Dynamic-map entities:** Legacy Hibernate `EntityMode.MAP` / dynamic-map support is not used because the legacy public API is not suitable for Hibernate ORM 8. The component uses typed entity classes.
    
-   **Message query replacement:** The component does not allow a message header to replace the query configured on the endpoint. Query text remains route configuration and message data is supplied through bound parameters.
    
-   **Transaction-manager integration:** The component uses native Hibernate transactions and does not use `camel-jpa`, Spring `PlatformTransactionManager`, or Jakarta Persistence.
    
-   **JTA transaction integration:** The component does not configure or provide JTA transaction coordination itself. When a Camel exchange is already transacted, the configured SessionFactory must provide JTA-backed transaction coordination. Resource-local SessionFactory operations are rejected in that case.
    
-   **Streaming in transacted exchanges:** `streaming=true` cannot be used inside a transacted Camel exchange because the Hibernate stream and session may outlive the route transaction.