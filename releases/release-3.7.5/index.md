# Apache camel 3.7.5 Release

## New and Noteworthy

This release is the new Camel 3.7.5 LTS release.

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
      <version>3.7.5</version>
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
      <version>3.7.5</version>
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
| [apache-camel-3.7.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.7.5/apache-camel-3.7.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.7.5/apache-camel-3.7.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.7.5/apache-camel-3.7.5-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.7.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.7.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (14)

[CAMEL-16718](https://issues.apache.org/jira/browse/CAMEL-16718)

Conflict with Netty TCP + Resilience4J circuit breaker

[CAMEL-16707](https://issues.apache.org/jira/browse/CAMEL-16707)

camel-rabbitmq connection leak on error during 'declare'

[CAMEL-16699](https://issues.apache.org/jira/browse/CAMEL-16699)

HttpProducer skip request headers for query params on bridge endpoint broken for common types

[CAMEL-16681](https://issues.apache.org/jira/browse/CAMEL-16681)

LazyStartProducer can result in NullPointerException in a multithreaded context

[CAMEL-16659](https://issues.apache.org/jira/browse/CAMEL-16659)

camel-core - Simple language parses minus sign (-) as a numeric value instead of a string value

[CAMEL-16658](https://issues.apache.org/jira/browse/CAMEL-16658)

AmbiguousMethodCallException when using Mockito mock as bean for camel-bean component.

[CAMEL-16629](https://issues.apache.org/jira/browse/CAMEL-16629)

camel-core - InterceptSendToEndpoint - AfterUri should only trigger if when was true

[CAMEL-16622](https://issues.apache.org/jira/browse/CAMEL-16622)

Validator component fails with java.lang.IllegalArgumentException: protocol = https host = null

[CAMEL-16587](https://issues.apache.org/jira/browse/CAMEL-16587)

camel-openstack - Cannot create ObjectStore V3 Client

[CAMEL-16586](https://issues.apache.org/jira/browse/CAMEL-16586)

camel-aws2-sns: messages for different endpoints are published to the same topic

[CAMEL-16582](https://issues.apache.org/jira/browse/CAMEL-16582)

camel-mail - Error Marshal mimeMultipart() with attachments

[CAMEL-16574](https://issues.apache.org/jira/browse/CAMEL-16574)

camel-salesforce - NPE On Response Callback - DefaultCompositeApiClient

[CAMEL-16566](https://issues.apache.org/jira/browse/CAMEL-16566)

camel-core - Nested enrich with shareUnitOfWork=true result in ConcurrentModificationException

[CAMEL-16509](https://issues.apache.org/jira/browse/CAMEL-16509)

Incorrect span timing information reported by camel-zipkin when using parallel processing with multicast/recipientList

### Dependency upgrade (1)

[CAMEL-16785](https://issues.apache.org/jira/browse/CAMEL-16785)

camel 3.7.x - Dependency upgrades

### Improvement (1)

[CAMEL-16619](https://issues.apache.org/jira/browse/CAMEL-16619)

camel-rabbitmq - Producer destroys rabbit channels when returns it back to the pool

### Task (1)

[CAMEL-16686](https://issues.apache.org/jira/browse/CAMEL-16686)

camel-website - Asciidoc ERROR/WARN during build

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).