# Apache camel 4.0.3 Release

## New and Noteworthy

This release is the new Camel 4.0.3 LTS patch release.

## Supported Java version

This version supports Java 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.0.3</version>
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
      <version>4.0.3</version>
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
| [apache-camel-4.0.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.3/apache-camel-4.0.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.3/apache-camel-4.0.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.3/apache-camel-4.0.3-src.zip.sha512) |
| [apache-camel-4.0.3-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.0.3/apache-camel-4.0.3-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.3/apache-camel-4.0.3-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.3/apache-camel-4.0.3-sbom.xml.sha512) |
| [apache-camel-4.0.3-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.0.3/apache-camel-4.0.3-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.3/apache-camel-4.0.3-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.3/apache-camel-4.0.3-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (14)

[CAMEL-20109](https://issues.apache.org/jira/browse/CAMEL-20109)

Endpoints with special characters (especially '#' like in spring-redis when specifying a redisTemplate)) can't be removed anymore with context.removeEndpoint

[CAMEL-20103](https://issues.apache.org/jira/browse/CAMEL-20103)

DefaultProducerCache returns wrong ProducerTemplate under high concurrency load

[CAMEL-20100](https://issues.apache.org/jira/browse/CAMEL-20100)

Camel-jsonpath can't fetch missing field in some cases when body is returned from a http/https call

[CAMEL-20099](https://issues.apache.org/jira/browse/CAMEL-20099)

Camel-http is creating invalid Content-Encoding header based on charset from Content-Type header

[CAMEL-20092](https://issues.apache.org/jira/browse/CAMEL-20092)

camel-core - ScheduledPollConsumer should reset error count when greedy

[CAMEL-20086](https://issues.apache.org/jira/browse/CAMEL-20086)

Camel JBang loosing kamelets-version setting when using camel-version

[CAMEL-20079](https://issues.apache.org/jira/browse/CAMEL-20079)

EndpointDslMojo generates wrong header names

[CAMEL-20054](https://issues.apache.org/jira/browse/CAMEL-20054)

camel-kubernetes - Configuration of Kubernetes secrets with Camel K not working as expected

[CAMEL-20053](https://issues.apache.org/jira/browse/CAMEL-20053)

camel-jira: watchUpdates consumer does not see issues created after route startup

[CAMEL-20037](https://issues.apache.org/jira/browse/CAMEL-20037)

camel-http builds StringEntity with wrong contentEncoding

[CAMEL-20035](https://issues.apache.org/jira/browse/CAMEL-20035)

Program terminates with OutOfMemoryError

[CAMEL-20032](https://issues.apache.org/jira/browse/CAMEL-20032)

camel-yaml-dsl - Choice should not have steps in schema

[CAMEL-20031](https://issues.apache.org/jira/browse/CAMEL-20031)

camel-yaml-dsl: Description property have incorrect title and description

[CAMEL-20028](https://issues.apache.org/jira/browse/CAMEL-20028)

camel-mail - Missing attachments if disposition not set

### Dependency upgrade (1)

[CAMEL-20049](https://issues.apache.org/jira/browse/CAMEL-20049)

camel-activemq - Upgrade to latest releases

### Improvement (3)

[CAMEL-20039](https://issues.apache.org/jira/browse/CAMEL-20039)

camel-core - SimpleLRUCache add support for soft cache

[CAMEL-20038](https://issues.apache.org/jira/browse/CAMEL-20038)

camel-core - Deprecate LRUWeakCache

[CAMEL-19999](https://issues.apache.org/jira/browse/CAMEL-19999)

camel-bean - Allow to configure bean introspection cache on component

### Task (5)

[CAMEL-20094](https://issues.apache.org/jira/browse/CAMEL-20094)

camel-catalog: camel-spring.xsd keeps being regenerated

[CAMEL-20066](https://issues.apache.org/jira/browse/CAMEL-20066)

camel-language - Missing examples in docs

[CAMEL-20030](https://issues.apache.org/jira/browse/CAMEL-20030)

camel-xslt-saxon - Non-working link in docs

[CAMEL-20029](https://issues.apache.org/jira/browse/CAMEL-20029)

camel-language - Missing examples in docs

[CAMEL-20022](https://issues.apache.org/jira/browse/CAMEL-20022)

camel-yaml-dsl: Add WARN log if kebab-case is detected

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).