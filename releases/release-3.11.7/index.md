# Apache camel 3.11.7 Release

## New and Noteworthy

This release is the new Camel 3.11.7 LTS patch release.

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
      <version>3.11.7</version>
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
      <version>3.11.7</version>
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
| [apache-camel-3.11.7-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.11.7/apache-camel-3.11.7-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.11.7/apache-camel-3.11.7-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.11.7/apache-camel-3.11.7-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.11.7` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.11.7

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (3)

[CAMEL-17940](https://issues.apache.org/jira/browse/CAMEL-17940)

Quartz Scheduler - unscheduleTask should check if scheduler is clustered

[CAMEL-17912](https://issues.apache.org/jira/browse/CAMEL-17912)

camel-sjms2 - preserveMessageQoS seems to not work as expected

[CAMEL-17910](https://issues.apache.org/jira/browse/CAMEL-17910)

camel-jms - InOut with reply-to-type shared - race condition

### Dependency upgrade (2)

[CAMEL-18011](https://issues.apache.org/jira/browse/CAMEL-18011)

upgrade to spring boot 2.6.7

[CAMEL-17899](https://issues.apache.org/jira/browse/CAMEL-17899)

spring4shell CVE means spring upgrades needed

### Improvement (1)

[CAMEL-17788](https://issues.apache.org/jira/browse/CAMEL-17788)

camel-fhir: Support FHIR versions DSTU2\_HL7ORG & DSTU2\_1

### Task (1)

[CAMEL-17957](https://issues.apache.org/jira/browse/CAMEL-17957)

camel-cxf - OSGi import range too restrictive

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).