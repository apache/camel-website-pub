# Camel Spring Boot Documentation Index

Index of Camel Spring Boot documentation pages.

# Apache Camel Spring Boot starters

Camel support for Spring Boot provides auto-configuration of the Camel and starters for many Camel [components](../../components/4.22.x/index.md). Our opinionated auto-configuration of the Camel context auto-detects Camel routes available in the Spring context and registers the key Camel utilities (like producer template, consumer template and the type converter) as beans.

Get started by adding the Camel and Spring Boot BOMs to your Maven `pom.xml` file.

```xml
<dependencyManagement>
    <dependencies>
        <!-- Camel BOM -->
        <dependency>
            <groupId>org.apache.camel.springboot</groupId>
            <artifactId>camel-spring-boot-bom</artifactId>
            <version>${camel-version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
        <!-- Spring Boot BOM -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>${spring-boot-version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

The `camel-spring-boot-bom` is a basic BOM that only holds the list of Camel Spring Boot starter JARs.

> **Note**
> It is recommended to import Camel Spring Boot BOM before Spring Boot BOM to ensure Camel dependencies are using supported JARs from the release. However, you can flip the order, and let Spring Boot BOM be first. However, you may encounter some dependency misalignments in some rare situations.

Next, add the [Camel Spring Boot starter](spring-boot.md) to start up the [Camel Context](../../manual/camelcontext.md).

```xml
    <dependencies>
        <!-- Camel Starter -->
        <dependency>
            <groupId>org.apache.camel.springboot</groupId>
            <artifactId>camel-spring-boot-starter</artifactId>
        </dependency>
        <!-- ... other dependencies ... -->
    </dependencies>
```

Also add any [component starters](list.md) your Spring Boot application requires. For example this adds the auto-configuration starter for the [JMS component](../../components/4.22.x/jms-component.md).

```xml
    <dependencies>
        <!-- ... other dependencies ... -->
        <dependency>
            <groupId>org.apache.camel.springboot</groupId>
            <artifactId>camel-jms-starter</artifactId>
        </dependency>
    </dependencies>
```

## Camel Spring Boot BOM vs Camel Spring Boot Dependencies BOM

There is a curated `camel-spring-boot-dependencies` which is a generated BOM that has adjusted the JARs that both Spring Boot and Apache Camel may use to use single shared version that will not conflict. This BOM is what is used to test camel-spring-boot itself. However Spring Boot users may want to use _pure_ Camel dependencies and hence why you can use `camel-spring-boot-bom` that only has the Camel starter JARs as managed dependencies. This may lead to a classpath conflict if a 3rd party JAR from Spring Boot is not compatible with a Camel component.

## Making sure Camel context is running in standalone Spring Boot

To ensure the Spring Boot application keeps running until being stopped or the JVM terminated, typically only need when running Spring Boot standalone, i.e. not with `spring-boot-starter-web` when the web container keeps the JVM running, set the `camel.main.run-controller=true` property in your configuration. For example in `application.properties`.

```none
# to keep the JVM running
camel.main.run-controller = true
```

## Spring Boot configuration support

Each [starter](list.md) lists configuration parameters you can configure in the standard `application.properties` or `application.yml` files. These parameters have the form of `camel.component.[component-name].[parameter]`. For example to configure the URL of the MQTT5 broker you can set:

```none
camel.component.paho-mqtt5.broker-url=tcp://localhost:61616
```

## Adding Camel routes

Camel [routes](../../manual/routes.md) are detected in the Spring application context, for example a route annotated with `org.springframework.stereotype.Component` will be loaded, added to the Camel context and run.

```java
import org.apache.camel.builder.RouteBuilder;
import org.springframework.stereotype.Component;

@Component
public class MyRoute extends RouteBuilder {

    @Override
    public void configure() throws Exception {
        from("...")
            .to("...");
    }

}
```