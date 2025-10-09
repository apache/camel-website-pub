# Apache camel 3.7.2 Release

## New and Noteworthy

This release is the new Camel 3.7.2 LTS release.

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
      <version>3.7.2</version>
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
      <version>3.7.2</version>
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
| [apache-camel-3.7.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.7.2/apache-camel-3.7.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.7.2/apache-camel-3.7.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.7.2/apache-camel-3.7.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.7.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.7.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (15)

[CAMEL-16135](https://issues.apache.org/jira/browse/CAMEL-16135)

Exception on routeinitialization when using split in onException-Block

[CAMEL-16114](https://issues.apache.org/jira/browse/CAMEL-16114)

DataFormat UnmarshalType defined as an Array Class Fails in Java DSL

[CAMEL-16112](https://issues.apache.org/jira/browse/CAMEL-16112)

Camel REST deserializes response to wrong type

[CAMEL-16111](https://issues.apache.org/jira/browse/CAMEL-16111)

camel-spring-boot - Bean reference by name in properties not working when there are custom property converters

[CAMEL-16110](https://issues.apache.org/jira/browse/CAMEL-16110)

camel-cxfrs - CxfRsProducer leaks Header when Exchange.HTTP\_QUERY is set

[CAMEL-16109](https://issues.apache.org/jira/browse/CAMEL-16109)

camel-hystrix-starter auto-config fails with multiple "servletRegistrationBean"

[CAMEL-16104](https://issues.apache.org/jira/browse/CAMEL-16104)

ProducerCache does not close producers when cacheSize is 1 (potential memory leak)

[CAMEL-16103](https://issues.apache.org/jira/browse/CAMEL-16103)

Stack size increases in split with transacted

[CAMEL-16091](https://issues.apache.org/jira/browse/CAMEL-16091)

Using netty-http with enricher causes buffer leak

[CAMEL-16083](https://issues.apache.org/jira/browse/CAMEL-16083)

OnCompletion with After Consumer mode does not fire if defined in routeScope

[CAMEL-16082](https://issues.apache.org/jira/browse/CAMEL-16082)

Single choice() without otherwise() always executed

[CAMEL-16068](https://issues.apache.org/jira/browse/CAMEL-16068)

Camel-AWS2-S3: Fix condition for throwing exception in case bucket does not exist

[CAMEL-16035](https://issues.apache.org/jira/browse/CAMEL-16035)

HazelcastQueueConsumer : when using mode POLL, the consumer sends NULL

[CAMEL-16034](https://issues.apache.org/jira/browse/CAMEL-16034)

MDC Logging causing OutOfMemory with large split

[CAMEL-16018](https://issues.apache.org/jira/browse/CAMEL-16018)

HazelcastReplicatedConsumer not receiving events

### Improvement (1)

[CAMEL-16129](https://issues.apache.org/jira/browse/CAMEL-16129)

Avoid property binding via reflection in NettyConfiguration

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).