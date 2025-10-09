# JPA

JVM since1.0.0 Native since1.0.0

Store and retrieve Java objects from databases using Java Persistence API (JPA).

## What’s inside

-   [JPA component](../../../../components/4.14.x/jpa-component.md), URI syntax: `jpa:entityType`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jpa)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jpa</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

The extension leverages [Quarkus Hibernate ORM](https://quarkus.io/guides/hibernate-orm) to provide the JPA implementation via Hibernate.

Refer to the [Quarkus Hibernate ORM](https://quarkus.io/guides/hibernate-orm) documentation to see how to configure Hibernate and your datasource.

Also, it leverages [Quarkus TX API](https://quarkus.io/guides/transaction#programmatic-approach) to provide `TransactionStrategy` implementation.

When a single persistence unit is used, the Camel Quarkus JPA extension will automatically configure the JPA component with a `EntityManagerFactory` and `TransactionStrategy`.

### Configuring JpaMessageIdRepository

It needs to use `EntityManagerFactory` and `TransactionStrategy` from the CDI container to configure the `JpaMessageIdRepository`:

```java
@Inject
EntityManagerFactory entityManagerFactory;

@Inject
TransactionStrategy transactionStrategy;

from("direct:idempotent")
    .idempotentConsumer(
        header("messageId"),
        new JpaMessageIdRepository(entityManagerFactory, transactionStrategy, "idempotentProcessor"));
```

> **Note**
> Since it excludes the `spring-orm` dependency, some options such as `sharedEntityManager`, `transactionManager` are not supported.