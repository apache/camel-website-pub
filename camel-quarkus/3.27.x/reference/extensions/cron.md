# Cron

JVM since1.0.0 Native since1.0.0

A generic interface for triggering events at times specified through the Unix cron syntax.

## What’s inside

-   [Cron component](../../../../components/4.14.x/cron-component.md), URI syntax: `cron:name`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-cron)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-cron</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

The cron component is a generic interface component, as such Camel Quarkus users will need to use the cron extension together with another extension offering an implementation. For instance, one can use the [Quartz Extension](quartz.md) and cron extension together in its project.