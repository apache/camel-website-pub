# CSimple jOOR

> **Warning**
> **Deprecated:** This csimple-joor is deprecated and may be removed in a future release.

**Since Camel 3.7**

> **Warning**
> The CSimple (compiled simple) language and the camel-csimple-joor component are **deprecated** (since Camel 4.19) and will be removed in a future release. Use the [Simple](../languages/simple-language.md) language instead.

The CSimple (compiled simple) expression language can either be source code generated and compiled together with your application using the regular Java compiler. Or compiled at runtime using jOOR during bootstrap.

This module includes the jOOR compiler for the CSimple language for runtime compilation.

To use this, just include `camel-csimple-joor` in the classpath.

## Limitations

The supported runtime is intended for Java standalone, Spring Boot, Camel Quarkus and other microservices runtimes. It is not supported on any kind of Java Application Server runtime.

jOOR does not support runtime compilation with Spring Boot using _fat jar_ packaging ([https://github.com/jOOQ/jOOR/issues/69](https://github.com/jOOQ/jOOR/issues/69)), it works with exploded classpath.

## Dependencies

To use scripting languages in your camel routes you need to add a dependency on **camel-csimple-joor**.

If you use Maven you could add the following to your `pom.xml`, substituting the version number for the latest and greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-csimple-joor</artifactId>
  <version>x.x.x</version>
</dependency>
```