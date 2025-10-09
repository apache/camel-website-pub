# Apache camel 4.4.2 Release

## New and Noteworthy

This release is the new Camel 4.4.2 LTS patch release.

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
      <version>4.4.2</version>
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
      <version>4.4.2</version>
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
| [apache-camel-4.4.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.4.2/apache-camel-4.4.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.2/apache-camel-4.4.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.2/apache-camel-4.4.2-src.zip.sha512) |
| [apache-camel-4.4.2-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.4.2/apache-camel-4.4.2-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.2/apache-camel-4.4.2-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.2/apache-camel-4.4.2-sbom.xml.sha512) |
| [apache-camel-4.4.2-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.4.2/apache-camel-4.4.2-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.2/apache-camel-4.4.2-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.2/apache-camel-4.4.2-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.4.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.4.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (23)

[CAMEL-20677](https://issues.apache.org/jira/browse/CAMEL-20677)

camel-hazelcast: Seda nested transactions are not allowed

[CAMEL-20676](https://issues.apache.org/jira/browse/CAMEL-20676)

camel-snmp - Delay cannot be configured

[CAMEL-20669](https://issues.apache.org/jira/browse/CAMEL-20669)

Camel-jbang export does not work if camel.jbang.metrics=true

[CAMEL-20663](https://issues.apache.org/jira/browse/CAMEL-20663)

camel-main: baseMainSupport may fail to doConfigureCamelContextFromMainConfiguration

[CAMEL-20656](https://issues.apache.org/jira/browse/CAMEL-20656)

camel-vertx-websocket - Error when using consumeAsClient and upgrade to websocket because of invalid query parameters

[CAMEL-20637](https://issues.apache.org/jira/browse/CAMEL-20637)

camel-rest-dsl - Matching rest operation may not select correct

[CAMEL-20635](https://issues.apache.org/jira/browse/CAMEL-20635)

camel-jbang - Export to quarkus does not work with newer Q releases

[CAMEL-20624](https://issues.apache.org/jira/browse/CAMEL-20624)

camel-http - OAuth2 support adds duplicate Authorization header if one already exists on the Exchange

[CAMEL-20615](https://issues.apache.org/jira/browse/CAMEL-20615)

YAML DSL issue with variables

[CAMEL-20614](https://issues.apache.org/jira/browse/CAMEL-20614)

KameletConsumerNotAvailableException is thrown when two or more threads call toD

[CAMEL-20613](https://issues.apache.org/jira/browse/CAMEL-20613)

ConcurrentModificationException when a new endpoint is created with toD

[CAMEL-20597](https://issues.apache.org/jira/browse/CAMEL-20597)

camel-salesforce - NullPointerException when query header is missing

[CAMEL-20588](https://issues.apache.org/jira/browse/CAMEL-20588)

camel-salesforce: java.lang.IllegalArgumentException: Request header too large Exception

[CAMEL-20577](https://issues.apache.org/jira/browse/CAMEL-20577)

Spring Beans XML Camel context duplicates rest routes defined in java or xml-io DSL

[CAMEL-20576](https://issues.apache.org/jira/browse/CAMEL-20576)

camel-jbang-plugin-k run command kebab-case parsing invalid

[CAMEL-20563](https://issues.apache.org/jira/browse/CAMEL-20563)

camel-kafka - breakOnFirstError causes thread and memory leaks

[CAMEL-20558](https://issues.apache.org/jira/browse/CAMEL-20558)

Ability to use the old Micrometer meter names does not work on MicrometerExchangeEventNotifier

[CAMEL-20551](https://issues.apache.org/jira/browse/CAMEL-20551)

camel-core: Default registry should not ignore beans in repositories

[CAMEL-20549](https://issues.apache.org/jira/browse/CAMEL-20549)

camel-kafka - Using sslKeystoreType should work with PEM

[CAMEL-20521](https://issues.apache.org/jira/browse/CAMEL-20521)

camel-amqp - AMQP publisher application is losing messages with local JMS transaction enabled

[CAMEL-20512](https://issues.apache.org/jira/browse/CAMEL-20512)

camel-jbang - camel debug may not work on windows

[CAMEL-20388](https://issues.apache.org/jira/browse/CAMEL-20388)

Salesforce component does not handshake on the connection failure

[CAMEL-18017](https://issues.apache.org/jira/browse/CAMEL-18017)

camel-as2 - Signed content in MDN gets corrupted and is not possible to validate

### Dependency upgrade (1)

[CAMEL-20689](https://issues.apache.org/jira/browse/CAMEL-20689)

camel-spring-boot - Upgrade to SB 3.2.5

### Improvement (6)

[CAMEL-20596](https://issues.apache.org/jira/browse/CAMEL-20596)

Propagate Azure Service Bus message headers (properties) to Camel Message

[CAMEL-20590](https://issues.apache.org/jira/browse/CAMEL-20590)

Delay to execute timeout to Camel RabbitMQ (InOut)

[CAMEL-20568](https://issues.apache.org/jira/browse/CAMEL-20568)

Set errorHandler on route level in YAML DSL

[CAMEL-20567](https://issues.apache.org/jira/browse/CAMEL-20567)

Add support for restConfiguration in XML DSL IO

[CAMEL-20564](https://issues.apache.org/jira/browse/CAMEL-20564)

camel-xslt: Make variables available as xsl:param

[CAMEL-20555](https://issues.apache.org/jira/browse/CAMEL-20555)

camel-lra html response when creating a saga with invalid lra-url

### Task (2)

[CAMEL-20518](https://issues.apache.org/jira/browse/CAMEL-20518)

Camel project - doesn't build on Windows anymore

[CAMEL-20383](https://issues.apache.org/jira/browse/CAMEL-20383)

camel CI: investigate consolidating Jenkinsfiles

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).