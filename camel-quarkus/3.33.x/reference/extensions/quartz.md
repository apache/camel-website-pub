# Quartz

JVM since1.0.0 Native since1.0.0

Schedule sending of messages using the Quartz 2.x scheduler.

## What’s inside

-   [Quartz component](../../../../components/4.18.x/quartz-component.md), URI syntax: `quartz:groupName/triggerName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-quartz)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-quartz</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Clustering

Support for Quartz clustering is provided by the Quarkus Quartz extension. The following steps outline how to configure Quarkus Quartz for use with Camel.

1.  Enable Quartz clustered mode and configure a `DataSource` as a persistence Quartz job store. An example configuration is as follows.
    
    ```properties
    # Quartz configuration
    quarkus.quartz.clustered=true
    quarkus.quartz.store-type=jdbc-cmt
    quarkus.scheduler.start-mode=forced
    
    # Datasource configuration
    quarkus.datasource.db-kind=postgresql
    quarkus.datasource.username=quarkus_test
    quarkus.datasource.password=quarkus_test
    quarkus.datasource.jdbc.url=jdbc:postgresql://localhost/quarkus_test
    
    # Optional automatic creation of Quartz tables
    quarkus.flyway.connect-retries=10
    quarkus.flyway.table=flyway_quarkus_history
    quarkus.flyway.migrate-at-start=true
    quarkus.flyway.baseline-on-migrate=true
    quarkus.flyway.baseline-version=1.0
    quarkus.flyway.baseline-description=Quartz
    ```
    
2.  Add the correct JDBC driver extension to your application that corresponds to the value of `quarkus.datasource.db-kind`. In the above example `postgresql` is used, therefore the following JDBC dependency would be required. Adjust as necessary for your needs. Agroal is also required for `DataSource` support.
    
    ```xml
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-jdbc-postgresql</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-agroal</artifactId>
    </dependency>
    ```
    
3.  [Quarkus Flyway](https://quarkus.io/guides/flyway) can automatically create the necessary Quartz database tables for you. Add `quarkus-flyway` to your application (optional).
    
    ```xml
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-flyway</artifactId>
    </dependency>
    ```
    
    Also add a Quartz database creation script for your chosen database kind. The Quartz project provides ready-made scripts that can be copied from [here](https://github.com/quartz-scheduler/quartz/tree/master/quartz-core/src/main/resources/org/quartz/impl/jdbcjobstore). Add the SQL script to `src/main/resources/db/migration/V1.0.0__QuarkusQuartz.sql`. Quarkus Flyway will detect it on startup and will proceed to create the Quartz database tables.
    
4.  Configure the Camel Quartz component to use the Quarkus Quartz scheduler.
    
    ```java
    @Produces
    @Singleton
    @Named("quartz")
    public QuartzComponent quartzComponent(Scheduler scheduler) {
        QuartzComponent component = new QuartzComponent();
        component.setScheduler(scheduler);
        return component;
    }
    ```
    

Further customization of the Quartz scheduler can be done via various configuration properties. Refer to the [Quarkus Quartz Configuration](https://quarkus.io/guides/quartz#quartz-configuration-reference) guide for more information.