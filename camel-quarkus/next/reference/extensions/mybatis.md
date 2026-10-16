# MyBatis

JVM since1.1.0 Native since2.8.0

Performs a query, poll, insert, update or delete in a relational database using MyBatis.

## What’s inside

-   [MyBatis component](../../../../components/next/mybatis-component.md), URI syntax: `mybatis:statement`
    
-   [MyBatis Bean component](../../../../components/next/mybatis-bean-component.md), URI syntax: `mybatis-bean:beanName:methodName`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-mybatis)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-mybatis</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

Please refer to [Quarkus MyBatis](https://quarkiverse.github.io/quarkiverse-docs/quarkus-mybatis/dev/index.md) for configuration. It must enable the following options

```properties
quarkus.mybatis.xmlconfig.enable=true
quarkus.mybatis.xmlconfig.path=SqlMapConfig.xml
```

> **Tip**
> `quarkus.mybatis.xmlconfig.path` must be the same with `configurationUri` param in the mybatis endpoint.