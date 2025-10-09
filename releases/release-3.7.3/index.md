# Apache camel 3.7.3 Release

## New and Noteworthy

This release is the new Camel 3.7.3 LTS release.

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
      <version>3.7.3</version>
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
      <version>3.7.3</version>
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
| [apache-camel-3.7.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.7.3/apache-camel-3.7.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.7.3/apache-camel-3.7.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.7.3/apache-camel-3.7.3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.7.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.7.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (23)

[CAMEL-16305](https://issues.apache.org/jira/browse/CAMEL-16305)

camel-servicenow-maven-plugin generated model classes wont compile

[CAMEL-16297](https://issues.apache.org/jira/browse/CAMEL-16297)

camel-core - Splitter does not call aggregation strategy when transacted is enabled

[CAMEL-16296](https://issues.apache.org/jira/browse/CAMEL-16296)

camel-as2 - Restarting bundle on karaf causes PortNumberInUse error

[CAMEL-16291](https://issues.apache.org/jira/browse/CAMEL-16291)

camel-cxfrs producer shouldn't try to read Entity from javax.ws.rs.core.Response

[CAMEL-16284](https://issues.apache.org/jira/browse/CAMEL-16284)

camel-couchbase: Incorrect Endpoint URI breaks CKC's couchbase connector

[CAMEL-16283](https://issues.apache.org/jira/browse/CAMEL-16283)

camel-jetty - NPE in binding for query parsing

[CAMEL-16282](https://issues.apache.org/jira/browse/CAMEL-16282)

VertxBufferConverter does not handle encoding correctly

[CAMEL-16276](https://issues.apache.org/jira/browse/CAMEL-16276)

WireTap does not work with NoErrorHandler

[CAMEL-16252](https://issues.apache.org/jira/browse/CAMEL-16252)

\[camel-azure-storage-blob\] Stream caching bug due to unsupported InputStream mark operation

[CAMEL-16241](https://issues.apache.org/jira/browse/CAMEL-16241)

Endpoint DSL (http component) Properties are not correctly set for Basic Authentications

[CAMEL-16227](https://issues.apache.org/jira/browse/CAMEL-16227)

Netty with reuseChannel=true invokes wrong callback

[CAMEL-16225](https://issues.apache.org/jira/browse/CAMEL-16225)

camel-karaf - route-list command fail with NPE

[CAMEL-16210](https://issues.apache.org/jira/browse/CAMEL-16210)

camel-core - Choice EIP exception from predicate may trigger otherwise

[CAMEL-16196](https://issues.apache.org/jira/browse/CAMEL-16196)

camel-main - Configure using Java only does not configure for some types

[CAMEL-16189](https://issues.apache.org/jira/browse/CAMEL-16189)

AWS2S3Producer not setting serverside encryption values

[CAMEL-16178](https://issues.apache.org/jira/browse/CAMEL-16178)

Enrich with REST+netty hangs when connection is closed without response

[CAMEL-16177](https://issues.apache.org/jira/browse/CAMEL-16177)

File stream cache problem with multicast parallel processing and encrypted stream

[CAMEL-16176](https://issues.apache.org/jira/browse/CAMEL-16176)

camel-kafka - Bug in header filter strategy regexp pattern

[CAMEL-16161](https://issues.apache.org/jira/browse/CAMEL-16161)

camel-core - Route template does not support autoStartup

[CAMEL-16152](https://issues.apache.org/jira/browse/CAMEL-16152)

XML DSL tokenize with token in simple language and group does not set the delimiter correctly

[CAMEL-16145](https://issues.apache.org/jira/browse/CAMEL-16145)

camel-report-maven-plugin: coverageThreshold cannot be set

[CAMEL-16079](https://issues.apache.org/jira/browse/CAMEL-16079)

aws-sn2 does not recognise FIFO queue configured though arn

[CAMEL-16063](https://issues.apache.org/jira/browse/CAMEL-16063)

should consider multiple ApplicationContext instances when specifying another management.server.port

### Improvement (6)

[CAMEL-16292](https://issues.apache.org/jira/browse/CAMEL-16292)

Upgrade to spring boot 2.4.3

[CAMEL-16265](https://issues.apache.org/jira/browse/CAMEL-16265)

camel-microprofile-metrics - Mask sensitive data in endpoint URLs

[CAMEL-16203](https://issues.apache.org/jira/browse/CAMEL-16203)

camel-core - Optimize removeHeaders all

[CAMEL-16202](https://issues.apache.org/jira/browse/CAMEL-16202)

camel-core - Optimize DefaultHeaderFilterStrategy filtering

[CAMEL-16199](https://issues.apache.org/jira/browse/CAMEL-16199)

camel-http - Optimize headers added as request headers in producer

[CAMEL-16181](https://issues.apache.org/jira/browse/CAMEL-16181)

KafkaIdempotentRepository cache incorrectly flagged as ready

### Task (5)

[CAMEL-16303](https://issues.apache.org/jira/browse/CAMEL-16303)

URI generation: if a part of the component name is equal to a path parameter the URI generation will fail

[CAMEL-16268](https://issues.apache.org/jira/browse/CAMEL-16268)

camel-xstream - Test dependency of junit-vintage-engine not set to scope test

[CAMEL-16190](https://issues.apache.org/jira/browse/CAMEL-16190)

Sensitive configuration values not redacted in Auto-configuration summary

[CAMEL-16167](https://issues.apache.org/jira/browse/CAMEL-16167)

camel-cxf - Upgrade to CXF 3.4.2

[CAMEL-16166](https://issues.apache.org/jira/browse/CAMEL-16166)

camel-jetty - Upgrade to 9.4.36

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).