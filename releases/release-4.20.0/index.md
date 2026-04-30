# Apache camel 4.20.0 Release

## New and Noteworthy

This release is the new Camel 4.20.0 release.

## Supported Java version

This version supports Java 17, 21 and 25.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.20.0</version>
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
      <version>4.20.0</version>
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
| [apache-camel-4.20.0-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.20.0/apache-camel-4.20.0-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.20.0/apache-camel-4.20.0-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.20.0/apache-camel-4.20.0-src.zip.sha512) |
| [apache-camel-4.20.0-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.20.0/apache-camel-4.20.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.20.0/apache-camel-4.20.0-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.20.0/apache-camel-4.20.0-sbom.xml.sha512) |
| [apache-camel-4.20.0-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.20.0/apache-camel-4.20.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.20.0/apache-camel-4.20.0-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.20.0/apache-camel-4.20.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.20.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.20.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (3)

[CAMEL-23334](https://issues.apache.org/jira/browse/CAMEL-23334)

JBang plugin resolution checks remote repositories on every CLI invocation even when artifacts are cached locally

[CAMEL-23283](https://issues.apache.org/jira/browse/CAMEL-23283)

OpenTelemetry/Micrometer traces are not correctly structured for JMS-initiated routes

[CAMEL-23192](https://issues.apache.org/jira/browse/CAMEL-23192)

jbang export to quarkus generates wrong dockerfiles

### Dependency upgrade (1)

[CAMEL-23350](https://issues.apache.org/jira/browse/CAMEL-23350)

ci jobs - Upgrade to Maven Daemon 1.0.5

### Improvement (12)

[CAMEL-23351](https://issues.apache.org/jira/browse/CAMEL-23351)

camel-oaipmh: Add custom HTTP Headers

[CAMEL-23349](https://issues.apache.org/jira/browse/CAMEL-23349)

Camel OpenTelemetry2 programmatic baggage management

[CAMEL-23348](https://issues.apache.org/jira/browse/CAMEL-23348)

camel-jbang - Custom plugins cannot use JDK ServiceLoader

[CAMEL-23325](https://issues.apache.org/jira/browse/CAMEL-23325)

camel-jbang - Only accept xxx.camel.yaml and xxx.yaml as valid YAML DSL files

[CAMEL-23322](https://issues.apache.org/jira/browse/CAMEL-23322)

camel-infinispan: align remote aggregation repository options with sibling repos

[CAMEL-23321](https://issues.apache.org/jira/browse/CAMEL-23321)

camel-jms, camel-sjms, camel-amqp - Add deserialization filtering for ObjectMessage handling

[CAMEL-23320](https://issues.apache.org/jira/browse/CAMEL-23320)

camel-platform-http-starter - Fix binary data corruption due to Spring Boot's default UTF-8 charset

[CAMEL-23319](https://issues.apache.org/jira/browse/CAMEL-23319)

Improve error handling and add input validation in camel-mina converters

[CAMEL-23315](https://issues.apache.org/jira/browse/CAMEL-23315)

camel-exec - Optimize custom header

[CAMEL-23314](https://issues.apache.org/jira/browse/CAMEL-23314)

camel-opensearch: Add SSLContextParameters support for TLS configuration

[CAMEL-23313](https://issues.apache.org/jira/browse/CAMEL-23313)

HeaderFilter Strategies: add lowerCase where it's not present - JMS, SJMS, CoAP, Google PubSub

[CAMEL-22497](https://issues.apache.org/jira/browse/CAMEL-22497)

camel-jbang - Can we make using HTTPS easier for camel.server

### New Feature (1)

[CAMEL-23331](https://issues.apache.org/jira/browse/CAMEL-23331)

camel-azure-storage-blob - Add support for blob snapshot creation and retrieval

### Task (5)

[CAMEL-23333](https://issues.apache.org/jira/browse/CAMEL-23333)

camel-core - Add documentation for sslContextParameters added to XML and YAML DSL

[CAMEL-23290](https://issues.apache.org/jira/browse/CAMEL-23290)

Update shibboleth Maven repository

[CAMEL-23164](https://issues.apache.org/jira/browse/CAMEL-23164)

camel-ftp-common - Move shared code into a common module

[CAMEL-22948](https://issues.apache.org/jira/browse/CAMEL-22948)

\[build\] ArgLine warning

[CAMEL-22555](https://issues.apache.org/jira/browse/CAMEL-22555)

\[build\] non-varargs call of varargs method with inexact argument type for last parameter

### Test (4)

[CAMEL-23366](https://issues.apache.org/jira/browse/CAMEL-23366)

VertxPlatformHttpProxyTest.testProxy test is failing

[CAMEL-23323](https://issues.apache.org/jira/browse/CAMEL-23323)

Some failing Infinispan IT tests blocked Ci during 2 hours and half

[CAMEL-23196](https://issues.apache.org/jira/browse/CAMEL-23196)

Tests fo rimpacted modules on github PRs are no more launched automatically

[CAMEL-22989](https://issues.apache.org/jira/browse/CAMEL-22989)

Fix issue related to failing test RunCommandITCase.runWithProperties

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).