# Apache camel 2.19.1 Release

## New and Noteworthy

This release is a minor update of the 2.19.x branch.

## Supported Java version

This version supports Java 8.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>2.19.1</version>
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
      <version>2.19.1</version>
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
| [apache-camel-2.19.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.19.1/apache-camel-2.19.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.19.1/apache-camel-2.19.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.19.1/apache-camel-2.19.1-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.19.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.19.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (33)

[CAMEL-11440](https://issues.apache.org/jira/browse/CAMEL-11440)

Some attributes in spring camel xml can't be replaced by property placeholder when used in spring boot

[CAMEL-11394](https://issues.apache.org/jira/browse/CAMEL-11394)

Undertow endpoint option REUSE\_ADDRESS is configured using the value for TCP\_NO\_DELAY

[CAMEL-11392](https://issues.apache.org/jira/browse/CAMEL-11392)

String to ByteBuffer conversion causes overflow due to multibyte chars

[CAMEL-11390](https://issues.apache.org/jira/browse/CAMEL-11390)

camel maven plugin (2.19.0) downloading catalog when configuration disabled it

[CAMEL-11386](https://issues.apache.org/jira/browse/CAMEL-11386)

Potential NullPointerException if HTTP client not started and stop was performed

[CAMEL-11382](https://issues.apache.org/jira/browse/CAMEL-11382)

Creating IgniteComponent from Ignite Instance throws IllegalStateException

[CAMEL-11352](https://issues.apache.org/jira/browse/CAMEL-11352)

duplicated/missing logs when camel-paxlogging work with pax-logging-log4j2

[CAMEL-11317](https://issues.apache.org/jira/browse/CAMEL-11317)

\[OSGi, camel-jpa\] Problems with mapping idempotent.jpa.MessageProcessed with Aries + Hibernate

[CAMEL-11305](https://issues.apache.org/jira/browse/CAMEL-11305)

camel-test - Using dump route coverage with custom processor may cause NPE

[CAMEL-11299](https://issues.apache.org/jira/browse/CAMEL-11299)

Camel Rest DSL Does Not Creating OPTIONS routes for defined routes

[CAMEL-11298](https://issues.apache.org/jira/browse/CAMEL-11298)

Using chmodDirectory with full paths makes file producer to created directories relative to source

[CAMEL-11293](https://issues.apache.org/jira/browse/CAMEL-11293)

Rest DSL Producer HTTP ignores http verb from uri

[CAMEL-11288](https://issues.apache.org/jira/browse/CAMEL-11288)

camel-grpc producer incorrectly called async services

[CAMEL-11287](https://issues.apache.org/jira/browse/CAMEL-11287)

MDC routeId value is lost after calling a direct route from a transacted route

[CAMEL-11283](https://issues.apache.org/jira/browse/CAMEL-11283)

camel-hystrix-starter - The circuitBreakerForceClose option is default true which should be false

[CAMEL-11281](https://issues.apache.org/jira/browse/CAMEL-11281)

camel-spring is not usable in an osgi-context

[CAMEL-11280](https://issues.apache.org/jira/browse/CAMEL-11280)

camel-twitter : hard-coded component scheme

[CAMEL-11279](https://issues.apache.org/jira/browse/CAMEL-11279)

Camel hystrix does not handle exceptions properly

[CAMEL-11273](https://issues.apache.org/jira/browse/CAMEL-11273)

ReloadStrategySupport does take changed routeContext files into account

[CAMEL-11272](https://issues.apache.org/jira/browse/CAMEL-11272)

ReloadStrategySupport wrongly logs "Routes with no id's detected"

[CAMEL-11269](https://issues.apache.org/jira/browse/CAMEL-11269)

URISupport sanitizeUri partial support for RAW()

[CAMEL-11264](https://issues.apache.org/jira/browse/CAMEL-11264)

Potential NPE in DefaultUndertowHttpBinding

[CAMEL-11255](https://issues.apache.org/jira/browse/CAMEL-11255)

Error handler may be called twice if routing from onException to direct with global scoped error handler

[CAMEL-11240](https://issues.apache.org/jira/browse/CAMEL-11240)

Simple Language: MethodNotFoundException when calling interface method implemented by super class

[CAMEL-11235](https://issues.apache.org/jira/browse/CAMEL-11235)

Simple Language: AmbiguousMethodCallException when calling method implemented by super class when method is defined by interface and abstract class

[CAMEL-11234](https://issues.apache.org/jira/browse/CAMEL-11234)

NullPointerException while trying to get the Route Status on startup

[CAMEL-11229](https://issues.apache.org/jira/browse/CAMEL-11229)

Infinite recursion if exception happens inside exception handler

[CAMEL-11227](https://issues.apache.org/jira/browse/CAMEL-11227)

Simple expression colon in sql-stored component

[CAMEL-11225](https://issues.apache.org/jira/browse/CAMEL-11225)

Deadlock in component creation

[CAMEL-11221](https://issues.apache.org/jira/browse/CAMEL-11221)

camel-netty4-http cannot have a URL larger than 409 bytes by default, rather than the assumed 4096 byte limit

[CAMEL-11215](https://issues.apache.org/jira/browse/CAMEL-11215)

Camel Kafka component commits offsets in case of exceptions

[CAMEL-10728](https://issues.apache.org/jira/browse/CAMEL-10728)

Camel MongoDB Multiple Insert issue

[CAMEL-9935](https://issues.apache.org/jira/browse/CAMEL-9935)

Rest DSL passes blank query parameters as null

### Improvement (18)

[CAMEL-11381](https://issues.apache.org/jira/browse/CAMEL-11381)

Upgrade camel-opentracing to use OpenTracing-Java 0.30.0 with active span management

[CAMEL-11365](https://issues.apache.org/jira/browse/CAMEL-11365)

camel-spring-boot - allowUseOriginalMessage should have same default as camel-core

[CAMEL-11355](https://issues.apache.org/jira/browse/CAMEL-11355)

Consumer - ErrorHandler should ignore rejected exception due to shutdown

[CAMEL-11345](https://issues.apache.org/jira/browse/CAMEL-11345)

Remove dependency on spring-core from gRPC component

[CAMEL-11343](https://issues.apache.org/jira/browse/CAMEL-11343)

gRPC component cannot load service class

[CAMEL-11329](https://issues.apache.org/jira/browse/CAMEL-11329)

swagger-dsl-generator artifact changed names to camel-swagger-dsl-generator, need to fix poms

[CAMEL-11323](https://issues.apache.org/jira/browse/CAMEL-11323)

Query Params are not mapped to camel headers with SparkJava

[CAMEL-11319](https://issues.apache.org/jira/browse/CAMEL-11319)

sql-stored - Add support for function

[CAMEL-11313](https://issues.apache.org/jira/browse/CAMEL-11313)

set defaultValue for FixedLength and other factories

[CAMEL-11310](https://issues.apache.org/jira/browse/CAMEL-11310)

"code too large" when generating Salesforce DTOs

[CAMEL-11309](https://issues.apache.org/jira/browse/CAMEL-11309)

Components missing from parent POM dependency management

[CAMEL-11289](https://issues.apache.org/jira/browse/CAMEL-11289)

camel-ehcache: allow to configure cache manager on component

[CAMEL-11278](https://issues.apache.org/jira/browse/CAMEL-11278)

camel-opentracing - Should deal with curly brackets may be encoded

[CAMEL-11267](https://issues.apache.org/jira/browse/CAMEL-11267)

Add SpanDecorator for 'rest' component

[CAMEL-11263](https://issues.apache.org/jira/browse/CAMEL-11263)

set HeaderFilterStrategy before setting properties

[CAMEL-11258](https://issues.apache.org/jira/browse/CAMEL-11258)

Use TracerResolver to obtain Tracer

[CAMEL-11253](https://issues.apache.org/jira/browse/CAMEL-11253)

camel-http4 - Add missing doc to component option

[CAMEL-11216](https://issues.apache.org/jira/browse/CAMEL-11216)

REST-DSL - Producer fails with NPE or other exceptions if you have not set a hostname

### Sub-task (1)

[CAMEL-7933](https://issues.apache.org/jira/browse/CAMEL-7933)

Camel-apns should create https connections using SSLContextParameters

### Task (5)

[CAMEL-11326](https://issues.apache.org/jira/browse/CAMEL-11326)

Exclude org.json from camel-spark

[CAMEL-11320](https://issues.apache.org/jira/browse/CAMEL-11320)

sql-stored - Should not extend polling endpoint as its not for consumer

[CAMEL-11301](https://issues.apache.org/jira/browse/CAMEL-11301)

Camel-weather and camel-geocoder: freegeoip.io/json has been moved permanently

[CAMEL-11265](https://issues.apache.org/jira/browse/CAMEL-11265)

Fix maven warning about fork option

[CAMEL-11239](https://issues.apache.org/jira/browse/CAMEL-11239)

camel-catalog-maven - Remove sl4j logger

### Test (1)

[CAMEL-11314](https://issues.apache.org/jira/browse/CAMEL-11314)

Fix failing tests in camel-swagger-java

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).