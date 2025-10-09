# Apache camel 4.14.2 Release

## New and Noteworthy

This release is the new Camel 4.14.2 LTS release.

## Supported Java version

This version supports Java 17 and 21.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.14.2</version>
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
      <version>4.14.2</version>
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
| [apache-camel-4.14.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.14.2/apache-camel-4.14.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.2/apache-camel-4.14.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.2/apache-camel-4.14.2-src.zip.sha512) |
| [apache-camel-4.14.2-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.14.2/apache-camel-4.14.2-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.2/apache-camel-4.14.2-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.2/apache-camel-4.14.2-sbom.xml.sha512) |
| [apache-camel-4.14.2-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.14.2/apache-camel-4.14.2-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.2/apache-camel-4.14.2-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.2/apache-camel-4.14.2-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.14.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.14.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (20)

[CAMEL-22597](https://issues.apache.org/jira/browse/CAMEL-22597)

Jira possible error when using jira url ending with /

[CAMEL-22571](https://issues.apache.org/jira/browse/CAMEL-22571)

\[camel-beanio\] No type converter for encoding

[CAMEL-22565](https://issues.apache.org/jira/browse/CAMEL-22565)

camel-sql - DefaultSqlPrepareStatementStrategy is missing exchange in tryConverter

[CAMEL-22560](https://issues.apache.org/jira/browse/CAMEL-22560)

camel-telemetry - excludePatterns incorrectly prevents execution of excluded steps

[CAMEL-22558](https://issues.apache.org/jira/browse/CAMEL-22558)

Jira - Consumer ignores delay option

[CAMEL-22535](https://issues.apache.org/jira/browse/CAMEL-22535)

camel-jbang-container: Missing version pinning breaks container images / Further improvements

[CAMEL-22534](https://issues.apache.org/jira/browse/CAMEL-22534)

JPA: fails if used with splitter (with parallelProcessing)

[CAMEL-22533](https://issues.apache.org/jira/browse/CAMEL-22533)

ConcurrentModificationException thrown in JMX-enabled application using Split EIP w/ shared UoW

[CAMEL-22526](https://issues.apache.org/jira/browse/CAMEL-22526)

camel-core - The dfdl dataformat is missing in model

[CAMEL-22494](https://issues.apache.org/jira/browse/CAMEL-22494)

camel-as2 - AS2 consumer URI remains active after route stop/removal

[CAMEL-22493](https://issues.apache.org/jira/browse/CAMEL-22493)

camel-rest-openapi: Potential NPE in OpenApiUtils.isArrayType

[CAMEL-22491](https://issues.apache.org/jira/browse/CAMEL-22491)

camel-plc4j - NPE exception when cannot connect to remote service

[CAMEL-22488](https://issues.apache.org/jira/browse/CAMEL-22488)

camlel-sql - Error when automatically creating JdbcIdempotent table

[CAMEL-22484](https://issues.apache.org/jira/browse/CAMEL-22484)

camel-jbang-kubernetes fails to deploy to openshift when using custom GAV

[CAMEL-22480](https://issues.apache.org/jira/browse/CAMEL-22480)

camel-core - Using property placeholders in endpoint URIs in the context-path containing ? sign can lead to double ? in resolved URI

[CAMEL-22476](https://issues.apache.org/jira/browse/CAMEL-22476)

camel-plc4j - Cannot load drivers when using poll mode

[CAMEL-22474](https://issues.apache.org/jira/browse/CAMEL-22474)

camel-http - HttpActivityListener null exchange when redelivery

[CAMEL-22468](https://issues.apache.org/jira/browse/CAMEL-22468)

camel-bean - Bean cache should initialize later

[CAMEL-22458](https://issues.apache.org/jira/browse/CAMEL-22458)

flatpack converter accesses invalid column names for header and trailer record value retrieval of fixed width files

[CAMEL-22414](https://issues.apache.org/jira/browse/CAMEL-22414)

In 4.14.0, after calling CXF HTTP, the response stream is not cached

### Dependency upgrade (5)

[CAMEL-22595](https://issues.apache.org/jira/browse/CAMEL-22595)

camel-spring-boot - Upgrade to 3.5.7

[CAMEL-22563](https://issues.apache.org/jira/browse/CAMEL-22563)

camel-spring - Upgrade to spring 6.2.12

[CAMEL-22531](https://issues.apache.org/jira/browse/CAMEL-22531)

camel-pulsar - Upgrade to 4.0.7

[CAMEL-22490](https://issues.apache.org/jira/browse/CAMEL-22490)

camel-minio - Upgrade to 8.6.x

[CAMEL-22469](https://issues.apache.org/jira/browse/CAMEL-22469)

grpc-netty-shaded - Upgrade to 1.75

### Improvement (12)

[CAMEL-22611](https://issues.apache.org/jira/browse/CAMEL-22611)

SmbComponent: file move error if the user does not have "Full Control" permissions

[CAMEL-22603](https://issues.apache.org/jira/browse/CAMEL-22603)

camel-jbang - Add CSB/CEQ imports to known dependencies

[CAMEL-22566](https://issues.apache.org/jira/browse/CAMEL-22566)

camel-core - Backlog tracer should drain with higher capacity

[CAMEL-22521](https://issues.apache.org/jira/browse/CAMEL-22521)

camel-jbang: Allow overriding quarkus gav using system properties

[CAMEL-22516](https://issues.apache.org/jira/browse/CAMEL-22516)

camel-core - RAW() should mask the value when printing

[CAMEL-22511](https://issues.apache.org/jira/browse/CAMEL-22511)

camel-kamelet - Secret options may not be auto RAW() substituted

[CAMEL-22507](https://issues.apache.org/jira/browse/CAMEL-22507)

camel-jbang - When using toD with dynamic parameters but static kamelet name then include kamelet spec file

[CAMEL-22485](https://issues.apache.org/jira/browse/CAMEL-22485)

camel-core: ContextServicePlugin should support unload operations

[CAMEL-22471](https://issues.apache.org/jira/browse/CAMEL-22471)

camel-jbang - Send command with file location should use absolute path

[CAMEL-22456](https://issues.apache.org/jira/browse/CAMEL-22456)

Use route.openshift.io to detect the openshift cluster

[CAMEL-22455](https://issues.apache.org/jira/browse/CAMEL-22455)

Use mirror.gcr.io for base image

[CAMEL-17348](https://issues.apache.org/jira/browse/CAMEL-17348)

camel-jira component newIssue does not work across multiple projects

### Task (3)

[CAMEL-22541](https://issues.apache.org/jira/browse/CAMEL-22541)

\[camel-core\] Flaky FileLockClusteredRoutePolicyTest unit test

[CAMEL-22499](https://issues.apache.org/jira/browse/CAMEL-22499)

Add missing spring-boot-name in components documentation

[CAMEL-22489](https://issues.apache.org/jira/browse/CAMEL-22489)

\[camel-core\]: enable cloud location .properties file

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).