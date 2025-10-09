# CSimple jOOR

**Since Camel 3.7**

The csimple (compiled simple) expression language can either be source code generated and compiled together with your application using the regular Java compiler. Or compiled at runtime using jOOR during bootstrap.

This module includes the jOOR compiler for the csimple language for runtime compilation.

To use this, just include `camel-csimple-joor` in the classpath.

> **Note**
> Java 8 is not supported. Java 11 or newer is required.

## Limitations

The supported runtime is intended for Java standalone, Spring Boot, Camel Quarkus and other microservices runtimes. It is not supported in OSGi, Camel Karaf or any kind of Java Application Server runtime.

jOOR does not support runtime compilation with Spring Boot using _fat jar_ packaging ([https://github.com/jOOQ/jOOR/issues/69](https://github.com/jOOQ/jOOR/issues/69)), it works with exploded classpath.

## Dependencies

To use scripting languages in your camel routes you need to add a dependency on **camel-csimple-joor**.

If you use Maven you could just add the following to your `pom.xml`, substituting the version number for the latest and greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-csimple-joor</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using csimple-joor with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-csimple-joor-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component has no Spring Boot auto configuration options.