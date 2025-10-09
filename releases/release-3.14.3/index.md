# Apache camel 3.14.3 Release

## New and Noteworthy

This release is the new Camel 3.14.3 LTS patch release.

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
      <version>3.14.3</version>
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
      <version>3.14.3</version>
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
| [apache-camel-3.14.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.14.3/apache-camel-3.14.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.14.3/apache-camel-3.14.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.14.3/apache-camel-3.14.3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.14.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.14.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (16)

[CAMEL-17992](https://issues.apache.org/jira/browse/CAMEL-17992)

camel-netty-starter - camel.component.netty.ssl-context-parameters does not work

[CAMEL-17940](https://issues.apache.org/jira/browse/CAMEL-17940)

Quartz Scheduler - unscheduleTask should check if scheduler is clustered

[CAMEL-17912](https://issues.apache.org/jira/browse/CAMEL-17912)

camel-sjms2 - preserveMessageQoS seems to not work as expected

[CAMEL-17910](https://issues.apache.org/jira/browse/CAMEL-17910)

camel-jms - InOut with reply-to-type shared - race condition

[CAMEL-17901](https://issues.apache.org/jira/browse/CAMEL-17901)

camel-google-pubsub - concurrent access error on shutdown

[CAMEL-17865](https://issues.apache.org/jira/browse/CAMEL-17865)

camel-platform-http-vertx: CORS conflict in Camel REST

[CAMEL-17773](https://issues.apache.org/jira/browse/CAMEL-17773)

camel-http: HttpSendDynamicAware parse uri incroectly if there are empty path and get parametrs in uri

[CAMEL-17768](https://issues.apache.org/jira/browse/CAMEL-17768)

Camel-cm-sms: Handle changed error message correctly

[CAMEL-17767](https://issues.apache.org/jira/browse/CAMEL-17767)

camel-csv - Empty header uri parameter interpreted as fixed column ""

[CAMEL-17764](https://issues.apache.org/jira/browse/CAMEL-17764)

Camel-quartz: endpoint enriches job detail with wrong type of data (should be String)

[CAMEL-17761](https://issues.apache.org/jira/browse/CAMEL-17761)

camel-test-infra: unable to define a custom Cassandra container

[CAMEL-17751](https://issues.apache.org/jira/browse/CAMEL-17751)

camel-saga - LRASagaService does not proceed to completion or compensation routes

[CAMEL-17738](https://issues.apache.org/jira/browse/CAMEL-17738)

camel-spring-boot - Cannot load resources from nested jar inside spring boot fat jar

[CAMEL-17704](https://issues.apache.org/jira/browse/CAMEL-17704)

camel-netty-starter - Unable to set camel.component.netty.decoders

[CAMEL-17602](https://issues.apache.org/jira/browse/CAMEL-17602)

camel-aws2-sqs - Camel converts Number.Boolean messageAttribute into string "1" or "0" instead of Boolean

[CAMEL-17554](https://issues.apache.org/jira/browse/CAMEL-17554)

camel-quickfix - lazy-create-engines option is not working

### Dependency upgrade (2)

[CAMEL-18011](https://issues.apache.org/jira/browse/CAMEL-18011)

upgrade to spring boot 2.6.7

[CAMEL-17899](https://issues.apache.org/jira/browse/CAMEL-17899)

spring4shell CVE means spring upgrades needed

### Improvement (6)

[CAMEL-17990](https://issues.apache.org/jira/browse/CAMEL-17990)

FileInputStreamCache is missing some InputStream delegates

[CAMEL-17935](https://issues.apache.org/jira/browse/CAMEL-17935)

camel-cassandraql: Use ClassLoadingAwareObjectInputStream in CassandraCamelCodec

[CAMEL-17934](https://issues.apache.org/jira/browse/CAMEL-17934)

camel-cassandraql: Provide a ClassLoder to CqlSessionBuilder

[CAMEL-17789](https://issues.apache.org/jira/browse/CAMEL-17789)

camel-fhir: Update FHIR dataformat metadata for fhirVersion option

[CAMEL-17788](https://issues.apache.org/jira/browse/CAMEL-17788)

camel-fhir: Support FHIR versions DSTU2\_HL7ORG & DSTU2\_1

[CAMEL-17593](https://issues.apache.org/jira/browse/CAMEL-17593)

camel-aws2-sqs - Camel skips messageAttributes if more then 10 without any info

### Task (2)

[CAMEL-17957](https://issues.apache.org/jira/browse/CAMEL-17957)

camel-cxf - OSGi import range too restrictive

[CAMEL-17612](https://issues.apache.org/jira/browse/CAMEL-17612)

camel google functions documentation shows consumer example instead of producer

### Test (1)

[CAMEL-17797](https://issues.apache.org/jira/browse/CAMEL-17797)

camel-fhir: Test with FHIR version R4

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).