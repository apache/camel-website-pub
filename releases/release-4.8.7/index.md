# Apache camel 4.8.7 Release

## New and Noteworthy

This release is the new Camel 4.8.7 release.

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
      <version>4.8.7</version>
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
      <version>4.8.7</version>
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
| [apache-camel-4.8.7-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.7/apache-camel-4.8.7-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.7/apache-camel-4.8.7-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.7/apache-camel-4.8.7-src.zip.sha512) |
| [apache-camel-4.8.7-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.7/apache-camel-4.8.7-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.7/apache-camel-4.8.7-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.7/apache-camel-4.8.7-sbom.xml.sha512) |
| [apache-camel-4.8.7-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.7/apache-camel-4.8.7-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.7/apache-camel-4.8.7-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.7/apache-camel-4.8.7-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.7` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.7

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (15)

[CAMEL-22038](https://issues.apache.org/jira/browse/CAMEL-22038)

aws-ddb: float/doubles are being set as ddb attribute type=S while using transformer - Ddb2JsonDataTypeTransformer

[CAMEL-22026](https://issues.apache.org/jira/browse/CAMEL-22026)

Camel SJMS & SJMS2 component cause thread leak when the route is stopped.

[CAMEL-22020](https://issues.apache.org/jira/browse/CAMEL-22020)

platform-http - Error in clientRequestValidation consumes & produces when plus sign in content-type

[CAMEL-22004](https://issues.apache.org/jira/browse/CAMEL-22004)

Kafka component shutdown may get stuck when rebalancing occurs

[CAMEL-21964](https://issues.apache.org/jira/browse/CAMEL-21964)

camel-salesforce: bulk api 2.0 error responses fail to deserialize

[CAMEL-21957](https://issues.apache.org/jira/browse/CAMEL-21957)

camel-core - Error handler should store failure route id eager so onRedelivery/onExceptionOccurred processors have access

[CAMEL-21954](https://issues.apache.org/jira/browse/CAMEL-21954)

camel-core - Route templates with onException does not work

[CAMEL-21953](https://issues.apache.org/jira/browse/CAMEL-21953)

camel-groovy: GroovyLanguage.stop may throw UnsupportedOperationException

[CAMEL-21947](https://issues.apache.org/jira/browse/CAMEL-21947)

GenericFileConsumer with eager idempotence and read lock stop processing file

[CAMEL-21940](https://issues.apache.org/jira/browse/CAMEL-21940)

camel-kafka - KafkaProducerCallBack can execute the continuation twice

[CAMEL-21938](https://issues.apache.org/jira/browse/CAMEL-21938)

camel-jolt - inputType & outputType can't be set for http uris

[CAMEL-21912](https://issues.apache.org/jira/browse/CAMEL-21912)

camel-cxf - Caching of ToStringTypeConverter breaks CXF RS Rest service

[CAMEL-21901](https://issues.apache.org/jira/browse/CAMEL-21901)

Salesforce consumer endpoint query parameter fallBackReplayId not working

[CAMEL-21892](https://issues.apache.org/jira/browse/CAMEL-21892)

Stopped producer in DefaultProducerCache.lastUsedProducer

[CAMEL-21877](https://issues.apache.org/jira/browse/CAMEL-21877)

ServiceNow incident update fails due to model/body type mismatch

### Dependency upgrade (1)

[CAMEL-22009](https://issues.apache.org/jira/browse/CAMEL-22009)

camel-spring-boot - Upgrade to SB 3.3.11

### Improvement (1)

[CAMEL-22029](https://issues.apache.org/jira/browse/CAMEL-22029)

aws dynamodb scan and query not implemented with attributes-to-get

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).