# Apache camel 3.0.1 Release

## New and Noteworthy

This release is a minor update of the 3.0.x branch.

## Supported Java version

This version supports Java 8 and 11.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.0.1</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-core</artifactId>
  </dependency>
  <dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-COMPONENT</artifactId>
  </dependency>
</dependencies>
```

To use this release in a Spring Boot application, use Spring Boot `spring-boot-dependencies` and Camel `camel-spring-boot-bom` Bill of Materials (BOM):

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-dependencies</artifactId>
      <version> SPRING BOOT VERSION HERE </version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
    <dependency>
      <groupId>org.apache.camel.springboot</groupId>
      <artifactId>camel-spring-boot-bom</artifactId>
      <version>3.0.1</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-COMPONENT-starter</artifactId>
  </dependency>
</dependencies>
```

## Apache Camel

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-3.0.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.0.1/apache-camel-3.0.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.0.1/apache-camel-3.0.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.0.1/apache-camel-3.0.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.0.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.0.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (23)

[CAMEL-14363](https://issues.apache.org/jira/browse/CAMEL-14363)

Camel netty requestTimeout doesn't work as expected

[CAMEL-14350](https://issues.apache.org/jira/browse/CAMEL-14350)

camel-main: xml routes discovery does not work outside the classpath

[CAMEL-14332](https://issues.apache.org/jira/browse/CAMEL-14332)

camel-blueprint - Camel route does not consider the value of ShutdownStrategy timeout.

[CAMEL-14327](https://issues.apache.org/jira/browse/CAMEL-14327)

Jt400PgmProducer doStop() method called on actively used instance

[CAMEL-14323](https://issues.apache.org/jira/browse/CAMEL-14323)

XMPP room with password disconnect after bootup

[CAMEL-14318](https://issues.apache.org/jira/browse/CAMEL-14318)

camel-blueprint - <proxy> in XSD is anyType

[CAMEL-14306](https://issues.apache.org/jira/browse/CAMEL-14306)

Endpoint DSL - ToD sets hash parameter when using complex objects as parameters

[CAMEL-14303](https://issues.apache.org/jira/browse/CAMEL-14303)

Setting matchOnUriPrefix on netty-http Rest Component causes api route to fail

[CAMEL-14302](https://issues.apache.org/jira/browse/CAMEL-14302)

Camel-spring: No longer possible to invoke static method of non-spring bean

[CAMEL-14277](https://issues.apache.org/jira/browse/CAMEL-14277)

NPE when NATS server not configured

[CAMEL-14272](https://issues.apache.org/jira/browse/CAMEL-14272)

Configuring endpoint with bean reference should fail if no such bean found

[CAMEL-14271](https://issues.apache.org/jira/browse/CAMEL-14271)

camel di does not work for routes discovered from the registry

[CAMEL-14268](https://issues.apache.org/jira/browse/CAMEL-14268)

Component auto configuration fails in Java 11

[CAMEL-14267](https://issues.apache.org/jira/browse/CAMEL-14267)

Conversion fails with NullPointerException when the body is null at the end of a route and an outputType is set

[CAMEL-14265](https://issues.apache.org/jira/browse/CAMEL-14265)

camel-cdi - Standalone CDI with Camel Main discovers routes twice

[CAMEL-14257](https://issues.apache.org/jira/browse/CAMEL-14257)

allowUseOriginalMessage not configurable

[CAMEL-14242](https://issues.apache.org/jira/browse/CAMEL-14242)

camel-rabbitmq - Binding parameters with x- is not possible when using endpointdsl

[CAMEL-14234](https://issues.apache.org/jira/browse/CAMEL-14234)

Project generated with camel-archetype-spring-boot cannot be built

[CAMEL-14224](https://issues.apache.org/jira/browse/CAMEL-14224)

Camel-Websocket: The sendToAll method in the Producer is really slow

[CAMEL-14223](https://issues.apache.org/jira/browse/CAMEL-14223)

EndpointBuilderFactory is not updated whenever \`:camel-package:generate-endpoint-dsl\` is executed

[CAMEL-14220](https://issues.apache.org/jira/browse/CAMEL-14220)

camel-activemq - Setting brokerURL via camel-main issue

[CAMEL-14219](https://issues.apache.org/jira/browse/CAMEL-14219)

ReactiveStreams subscriber does not enforce type conversion

[CAMEL-14213](https://issues.apache.org/jira/browse/CAMEL-14213)

camel-jms - Using XA and having 2 or more connection factories issue

### Improvement (13)

[CAMEL-14384](https://issues.apache.org/jira/browse/CAMEL-14384)

camel-jsonpath: Do not use reflection on the annotation proxy in DefaultAnnotationExpressionFactory

[CAMEL-14375](https://issues.apache.org/jira/browse/CAMEL-14375)

camel-kafka - The saslJaasConfig option may contain sensitive information that can be logged

[CAMEL-14361](https://issues.apache.org/jira/browse/CAMEL-14361)

camel-http - Avoid reflection in creating http method

[CAMEL-14355](https://issues.apache.org/jira/browse/CAMEL-14355)

PDF producer should close PDF documents

[CAMEL-14307](https://issues.apache.org/jira/browse/CAMEL-14307)

camel-rabbitmq - unable to set empty routing key when declaring DLX

[CAMEL-14292](https://issues.apache.org/jira/browse/CAMEL-14292)

Remove unwanted dependency to google-http-client library

[CAMEL-14288](https://issues.apache.org/jira/browse/CAMEL-14288)

Endpoint configurer should deal better with list types

[CAMEL-14287](https://issues.apache.org/jira/browse/CAMEL-14287)

getComponent on CamelContext should initialize component

[CAMEL-14273](https://issues.apache.org/jira/browse/CAMEL-14273)

Configuring endpoint which fails in setter should repot this as property binding exception

[CAMEL-14263](https://issues.apache.org/jira/browse/CAMEL-14263)

Generate configurers for types annotated with @UriParams

[CAMEL-14245](https://issues.apache.org/jira/browse/CAMEL-14245)

\[camel-main\] allow to enable/disable auto confioguiration per component/language/data-format

[CAMEL-14230](https://issues.apache.org/jira/browse/CAMEL-14230)

Disable RC4 and MD5 TLS ciphersuites by default

[CAMEL-14228](https://issues.apache.org/jira/browse/CAMEL-14228)

camel-netty - Let netty calculate the default worker count

### New Feature (1)

[CAMEL-14221](https://issues.apache.org/jira/browse/CAMEL-14221)

Stomp Component has no option to set version

### Task (3)

[CAMEL-14365](https://issues.apache.org/jira/browse/CAMEL-14365)

Create OpenTracing SpanDecorator for platform-http component

[CAMEL-14259](https://issues.apache.org/jira/browse/CAMEL-14259)

camel-spring-boot - When using main-run-controller then CamelContext is initialized twice

[CAMEL-14239](https://issues.apache.org/jira/browse/CAMEL-14239)

XSD schema for Camel 3 release for OSGi blueprint put online

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).