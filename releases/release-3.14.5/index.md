# Apache camel 3.14.5 Release

## New and Noteworthy

This release is the new Camel 3.14.5 LTS patch release.

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
      <version>3.14.5</version>
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
      <version>3.14.5</version>
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
| [apache-camel-3.14.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.14.5/apache-camel-3.14.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.14.5/apache-camel-3.14.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.14.5/apache-camel-3.14.5-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.14.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.14.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (10)

[CAMEL-18391](https://issues.apache.org/jira/browse/CAMEL-18391)

camel-http - HttpSendDynamicAware not optimizing for url without slashes

[CAMEL-18379](https://issues.apache.org/jira/browse/CAMEL-18379)

camel-mail: attachments with empty fileName

[CAMEL-18331](https://issues.apache.org/jira/browse/CAMEL-18331)

camel-spring-xml - <endpoint> bean added via beans.xml are parsed twice

[CAMEL-18324](https://issues.apache.org/jira/browse/CAMEL-18324)

camel-core - Exception during preparing exchange task can block thread

[CAMEL-18321](https://issues.apache.org/jira/browse/CAMEL-18321)

camel-mybatis - Should support using Map message body as-is for insert/update

[CAMEL-18319](https://issues.apache.org/jira/browse/CAMEL-18319)

camel-core - Supervising route controller should not eager warmup routes

[CAMEL-18270](https://issues.apache.org/jira/browse/CAMEL-18270)

IMAP skipFailedMessage=true, but route blocked if mail is moved while download

[CAMEL-18253](https://issues.apache.org/jira/browse/CAMEL-18253)

camel-kafka: idempotent repository may report incorrect number of messages

[CAMEL-18250](https://issues.apache.org/jira/browse/CAMEL-18250)

When a Call to Salesforce timeouts then we have Exchange.HTTP\_RESPONSE\_CODE Exchange Header set as "0"

[CAMEL-16287](https://issues.apache.org/jira/browse/CAMEL-16287)

camel-aws2-sqs should use pagination for deciding which aws sqs queues it should create

### Dependency upgrade (2)

[CAMEL-18395](https://issues.apache.org/jira/browse/CAMEL-18395)

camel-spring-boot - Upgrade to 2.6.10

[CAMEL-18242](https://issues.apache.org/jira/browse/CAMEL-18242)

upgrade to spring boot 2.6.10

### Improvement (2)

[CAMEL-18318](https://issues.apache.org/jira/browse/CAMEL-18318)

camel-quartz - Context fails to start when one of the cron configuration has expired

[CAMEL-18264](https://issues.apache.org/jira/browse/CAMEL-18264)

Camel SFTP: Cannot configure JSch client to use ssh-dss key

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).