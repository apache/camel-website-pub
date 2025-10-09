# Apache camel 3.11.6 Release

## New and Noteworthy

This release is the new Camel 3.11.6 LTS patch release.

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
      <version>3.11.6</version>
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
      <version>3.11.6</version>
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
| [apache-camel-3.11.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.11.6/apache-camel-3.11.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.11.6/apache-camel-3.11.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.11.6/apache-camel-3.11.6-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.11.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.11.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (12)

[CAMEL-17702](https://issues.apache.org/jira/browse/CAMEL-17702)

\[camel-google-storage\] Payload type File causes NPE on consumer

[CAMEL-17618](https://issues.apache.org/jira/browse/CAMEL-17618)

camel-ref: only add the endpoint into camelContext when not exist

[CAMEL-17592](https://issues.apache.org/jira/browse/CAMEL-17592)

concurrentConsumers URI parameter not working with aws2-sqs endpoint

[CAMEL-17565](https://issues.apache.org/jira/browse/CAMEL-17565)

camel-jms - JmsBinding not closing the InputStream

[CAMEL-17521](https://issues.apache.org/jira/browse/CAMEL-17521)

camel-http - httpClient parameters are not filtered out

[CAMEL-17503](https://issues.apache.org/jira/browse/CAMEL-17503)

camel-ahc-ws - Unable to reconnect to Server after server reboot

[CAMEL-17501](https://issues.apache.org/jira/browse/CAMEL-17501)

camel-core - FailedToCreateRouteException issue if route is very long and complex uris that cannot be sanitized

[CAMEL-17486](https://issues.apache.org/jira/browse/CAMEL-17486)

camel-core - ThrottlePermit compareTo cast to int causes issues

[CAMEL-17485](https://issues.apache.org/jira/browse/CAMEL-17485)

Camel-JSLT: Currently it could only load resources from classpath

[CAMEL-17471](https://issues.apache.org/jira/browse/CAMEL-17471)

Snakeyaml: Use safe constructor where the default one has been used

[CAMEL-17358](https://issues.apache.org/jira/browse/CAMEL-17358)

AWS SDK2 Producer does not set the Content Type at all

[CAMEL-17137](https://issues.apache.org/jira/browse/CAMEL-17137)

camel-karaf - Error while adding camel-cxf

### Dependency upgrade (3)

[CAMEL-17715](https://issues.apache.org/jira/browse/CAMEL-17715)

upgrade to spring boot 2.6.4 and 2.5.10

[CAMEL-17522](https://issues.apache.org/jira/browse/CAMEL-17522)

camel-spring-boot - Upgrade to spring boot 2.5.9

[CAMEL-17395](https://issues.apache.org/jira/browse/CAMEL-17395)

upgrade to log4j 2.17.1

### Improvement (6)

[CAMEL-17713](https://issues.apache.org/jira/browse/CAMEL-17713)

CAMEL-AWS2-S3 doesn't support uploading files with custom metadata headers

[CAMEL-17694](https://issues.apache.org/jira/browse/CAMEL-17694)

camel-vertx-websocket: Improve handling of SEND\_TO\_ALL header

[CAMEL-17650](https://issues.apache.org/jira/browse/CAMEL-17650)

camel-vertx-websocket: sendToAll operation should consider the path WebSocket clients are connected to

[CAMEL-17646](https://issues.apache.org/jira/browse/CAMEL-17646)

camel-vertx-websocket - Server exception handler should check for cause ConnectionBase.CLOSED\_EXCEPTION

[CAMEL-17616](https://issues.apache.org/jira/browse/CAMEL-17616)

JdbcAggregationRepository will not start if it contains too many exchanges

[CAMEL-17519](https://issues.apache.org/jira/browse/CAMEL-17519)

Make Camel MainSupport internalBeforeStart method protected

### Test (1)

[CAMEL-17453](https://issues.apache.org/jira/browse/CAMEL-17453)

MTOM/XOP tests in camel-cxf are broken

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).