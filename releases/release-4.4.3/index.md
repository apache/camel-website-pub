# Apache camel 4.4.3 Release

## New and Noteworthy

This release is the new Camel 4.4.3 LTS patch release.

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
      <version>4.4.3</version>
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
      <version>4.4.3</version>
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
| [apache-camel-4.4.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.4.3/apache-camel-4.4.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.3/apache-camel-4.4.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.3/apache-camel-4.4.3-src.zip.sha512) |
| [apache-camel-4.4.3-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.4.3/apache-camel-4.4.3-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.3/apache-camel-4.4.3-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.3/apache-camel-4.4.3-sbom.xml.sha512) |
| [apache-camel-4.4.3-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.4.3/apache-camel-4.4.3-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.3/apache-camel-4.4.3-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.3/apache-camel-4.4.3-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.4.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.4.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (26)

[CAMEL-20873](https://issues.apache.org/jira/browse/CAMEL-20873)

camel-platform-http-vertx: Responses may not complete if exceptions are thrown in VertxPlatformHttpSupport.writeResponse

[CAMEL-20864](https://issues.apache.org/jira/browse/CAMEL-20864)

camel-kafka - With confluent schema registry does not work properly.

[CAMEL-20850](https://issues.apache.org/jira/browse/CAMEL-20850)

LRUCache evicts entries unexpectedly

[CAMEL-20841](https://issues.apache.org/jira/browse/CAMEL-20841)

DataSonnet expressions are removed under memory load

[CAMEL-20835](https://issues.apache.org/jira/browse/CAMEL-20835)

OOM using RecipientList

[CAMEL-20834](https://issues.apache.org/jira/browse/CAMEL-20834)

camel-salesforce - A NullPointException in SubscriptionHelper.subscribe() interrupts platform-event subscription

[CAMEL-20823](https://issues.apache.org/jira/browse/CAMEL-20823)

camel-smb component polling doesn't account for directories

[CAMEL-20820](https://issues.apache.org/jira/browse/CAMEL-20820)

camel-core - Duplicate JMX MBean operation for resource endpoints

[CAMEL-20819](https://issues.apache.org/jira/browse/CAMEL-20819)

camel-jbang - Reload mode with supervising route controller does not reload routes

[CAMEL-20812](https://issues.apache.org/jira/browse/CAMEL-20812)

camel-netty-http: hostnameVerification option not used

[CAMEL-20790](https://issues.apache.org/jira/browse/CAMEL-20790)

kafka batching consumer polls randomly failing with NPE under load

[CAMEL-20778](https://issues.apache.org/jira/browse/CAMEL-20778)

Intercept created using AdviceWithRouteBuilder causes issues with error handling (regression)

[CAMEL-20771](https://issues.apache.org/jira/browse/CAMEL-20771)

camel-jbang - Does not hot-reload java source changes

[CAMEL-20763](https://issues.apache.org/jira/browse/CAMEL-20763)

Rest template with underscore fails after Camel 4.2.0

[CAMEL-20752](https://issues.apache.org/jira/browse/CAMEL-20752)

camel-saga - NPE in compesating

[CAMEL-20750](https://issues.apache.org/jira/browse/CAMEL-20750)

camel-yaml-dsl - Rest DSL with enableCORS does not work

[CAMEL-20746](https://issues.apache.org/jira/browse/CAMEL-20746)

Bean deserialisation from YAML displays message displays wrong nodeType

[CAMEL-20738](https://issues.apache.org/jira/browse/CAMEL-20738)

camel-jasypt-starter - PropertiesParser cannot be redefined

[CAMEL-20732](https://issues.apache.org/jira/browse/CAMEL-20732)

RestDefinition does not properly handle array of primitives for\` in/out types

[CAMEL-20731](https://issues.apache.org/jira/browse/CAMEL-20731)

Route coverage fails on routes with multiple doCatch blocks

[CAMEL-20724](https://issues.apache.org/jira/browse/CAMEL-20724)

camel-saxon: xquery fluent API does not work with namespaces (regression)

[CAMEL-20715](https://issues.apache.org/jira/browse/CAMEL-20715)

camel-olingo2 and 4 - ApiName DEFAULT should be accepted

[CAMEL-20700](https://issues.apache.org/jira/browse/CAMEL-20700)

camel-core: ReflectionHelper.setField may fail for numeric type fields

[CAMEL-20699](https://issues.apache.org/jira/browse/CAMEL-20699)

camel-azure-servicebus: Broker properties not propagated to Camel Exchange

[CAMEL-20692](https://issues.apache.org/jira/browse/CAMEL-20692)

camel-cxf - No Payload is logged when the logging feature is enabled

[CAMEL-20691](https://issues.apache.org/jira/browse/CAMEL-20691)

camel-azure-servicebus: Broker properties should not be propagated into application properties

### Dependency upgrade (3)

[CAMEL-20882](https://issues.apache.org/jira/browse/CAMEL-20882)

camel-spring-boot - Upgrade to 3.2.7

[CAMEL-20780](https://issues.apache.org/jira/browse/CAMEL-20780)

camel-spring-boot - Upgrade to SB 3.2.6

[CAMEL-20753](https://issues.apache.org/jira/browse/CAMEL-20753)

camel-kafka - Upgrade to 3.6.2

### Improvement (2)

[CAMEL-20851](https://issues.apache.org/jira/browse/CAMEL-20851)

camel-elasticsearch-rest-client: Sniffer should be closed on producer stop

[CAMEL-20727](https://issues.apache.org/jira/browse/CAMEL-20727)

camel-azure - Data lake upload should not read content into memory

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).