# Apache camel 3.14.4 Release

## New and Noteworthy

This release is the new Camel 3.14.4 LTS patch release.

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
      <version>3.14.4</version>
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
      <version>3.14.4</version>
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
| [apache-camel-3.14.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.14.4/apache-camel-3.14.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.14.4/apache-camel-3.14.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.14.4/apache-camel-3.14.4-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.14.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.14.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (15)

[CAMEL-18218](https://issues.apache.org/jira/browse/CAMEL-18218)

camel-jira: components field is not updated

[CAMEL-18210](https://issues.apache.org/jira/browse/CAMEL-18210)

camel-core - Pooled exchanges in batch consumer may use an exchange concurrently

[CAMEL-18202](https://issues.apache.org/jira/browse/CAMEL-18202)

camel-mongodb-gridfs - initial delay is not configured correctly

[CAMEL-18187](https://issues.apache.org/jira/browse/CAMEL-18187)

slack: inconsistent message payload when batch ends

[CAMEL-18185](https://issues.apache.org/jira/browse/CAMEL-18185)

slack: npe when processing batch messages

[CAMEL-18159](https://issues.apache.org/jira/browse/CAMEL-18159)

camel-jms SendDynamicAware incorrectly parses destination if it starts with "jms|activemq|etc://" and doesn't have queue: or topic: prefix

[CAMEL-18157](https://issues.apache.org/jira/browse/CAMEL-18157)

camel-jdbc - The settings provided by the query parameter "parameters" are ignored when useHeadersAsParameters

[CAMEL-18123](https://issues.apache.org/jira/browse/CAMEL-18123)

Aws2-sqs: Operations PurgeQueue and DeleteQueue requires unnecessary header

[CAMEL-18119](https://issues.apache.org/jira/browse/CAMEL-18119)

Regression in 3.4 in date formatting of Simple expression

[CAMEL-18110](https://issues.apache.org/jira/browse/CAMEL-18110)

camel-smpp - DeliverSM handle message payload optional parameter

[CAMEL-18101](https://issues.apache.org/jira/browse/CAMEL-18101)

camel-core - Pooled exchanges with netty-http/jetty/servlet can cause reference leaks

[CAMEL-18027](https://issues.apache.org/jira/browse/CAMEL-18027)

camel-netty (producer) wrongly closes client channels

[CAMEL-17999](https://issues.apache.org/jira/browse/CAMEL-17999)

Simple Language: Invoke clone() method

[CAMEL-17949](https://issues.apache.org/jira/browse/CAMEL-17949)

camel-netty-http - Infinite loop when setting retries

[CAMEL-17911](https://issues.apache.org/jira/browse/CAMEL-17911)

camel-olingo2 : I/O Dispatcher threads leak

### Dependency upgrade (3)

[CAMEL-18213](https://issues.apache.org/jira/browse/CAMEL-18213)

camel-spring-boot - Upgrade to 2.6.8

[CAMEL-18183](https://issues.apache.org/jira/browse/CAMEL-18183)

camel-karaf - Wrong definition in the camel-azure-storage-datalake feature

[CAMEL-18047](https://issues.apache.org/jira/browse/CAMEL-18047)

Upgrade jakarta.mail to 1.6.7

### Improvement (4)

[CAMEL-18113](https://issues.apache.org/jira/browse/CAMEL-18113)

camel-ftp - Root cause exceptions "accidently" supressed in operations classes

[CAMEL-18051](https://issues.apache.org/jira/browse/CAMEL-18051)

Backport CAMEL-17835 to 3.14.x

[CAMEL-17941](https://issues.apache.org/jira/browse/CAMEL-17941)

Dropbox: long-lived access tokens are retired, must use refresh token

[CAMEL-17100](https://issues.apache.org/jira/browse/CAMEL-17100)

Minio Consumer is really slow on listing initially if you have a lot of files

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).