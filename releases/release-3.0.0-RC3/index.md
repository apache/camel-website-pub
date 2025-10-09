# Apache camel 3.0.0-RC3 Release

## New and Noteworthy

This release the third and final release candidate towards Camel 3.0.0 release.

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
      <version>3.0.0-RC3</version>
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
      <version>3.0.0-RC3</version>
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
| [apache-camel-3.0.0-RC3-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.0.0-RC3/apache-camel-3.0.0-RC3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.0.0-RC3/apache-camel-3.0.0-RC3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.0.0-RC3/apache-camel-3.0.0-RC3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.0.0-RC3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.0.0-RC3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (15)

[CAMEL-14166](https://issues.apache.org/jira/browse/CAMEL-14166)

Netty is reporting a resource leak

[CAMEL-14087](https://issues.apache.org/jira/browse/CAMEL-14087)

camel-debezium - The maven plugin generates a new default port number each time

[CAMEL-14081](https://issues.apache.org/jira/browse/CAMEL-14081)

camel-api-component-maven-plugin fromApis throw java.lang.StringIndexOutOfBoundsException

[CAMEL-14078](https://issues.apache.org/jira/browse/CAMEL-14078)

camel-bean - Exception from message getBody may not be handled by error handler

[CAMEL-14072](https://issues.apache.org/jira/browse/CAMEL-14072)

FileInputStreamCache will not delete temporary file if file system is full

[CAMEL-14071](https://issues.apache.org/jira/browse/CAMEL-14071)

\[Camel-as2\] Integration tests are not working

[CAMEL-14054](https://issues.apache.org/jira/browse/CAMEL-14054)

Placeholder are not resolved when using GeneratedPropertyConfigurer

[CAMEL-14035](https://issues.apache.org/jira/browse/CAMEL-14035)

JDBC StreamList and outputClass does not work

[CAMEL-14033](https://issues.apache.org/jira/browse/CAMEL-14033)

multiple consumers for namedReplyTo results in a cryptic nullPointer

[CAMEL-14030](https://issues.apache.org/jira/browse/CAMEL-14030)

camel-ftp - streamDownload=true and move options dont work

[CAMEL-14027](https://issues.apache.org/jira/browse/CAMEL-14027)

Camel-Netty-Http: NettyHttpStreamTest is failing consistently

[CAMEL-14023](https://issues.apache.org/jira/browse/CAMEL-14023)

Camel-salesforce-maven-plugin generate fails on IBM jdk

[CAMEL-14010](https://issues.apache.org/jira/browse/CAMEL-14010)

Camel-Kafka ConsumerCount drops to 1 (default) from the defined value

[CAMEL-13270](https://issues.apache.org/jira/browse/CAMEL-13270)

camel-rabbitmq - x-death header gets lost because of incorrect header value validation

[CAMEL-13122](https://issues.apache.org/jira/browse/CAMEL-13122)

Potential bug in BeanExpression/HttpMessage

### Improvement (30)

[CAMEL-14083](https://issues.apache.org/jira/browse/CAMEL-14083)

camel-jms - Consumer with poison message should automatic deal with that

[CAMEL-14073](https://issues.apache.org/jira/browse/CAMEL-14073)

camel-hdfs - Cleanup HA/Cluster related classes

[CAMEL-14068](https://issues.apache.org/jira/browse/CAMEL-14068)

Retry subscribe to Salesforce event when server returns 503 Server too busy

[CAMEL-14067](https://issues.apache.org/jira/browse/CAMEL-14067)

camel-hdfs - Expose HighAvailability configuration (ConfiguredFailoverProxyProvider)

[CAMEL-14066](https://issues.apache.org/jira/browse/CAMEL-14066)

Split route parsing from the main CamelContext api

[CAMEL-14060](https://issues.apache.org/jira/browse/CAMEL-14060)

Deprecate camel-restlet as its not active maintained

[CAMEL-14057](https://issues.apache.org/jira/browse/CAMEL-14057)

Update resource path for camel context version retrieval

[CAMEL-14056](https://issues.apache.org/jira/browse/CAMEL-14056)

Camel website - Component reference page should be generated as on github

[CAMEL-14055](https://issues.apache.org/jira/browse/CAMEL-14055)

Improve support for custom SSLHandler

[CAMEL-14052](https://issues.apache.org/jira/browse/CAMEL-14052)

camel-paho - Make it possible to configure userName, password from application.properties

[CAMEL-14051](https://issues.apache.org/jira/browse/CAMEL-14051)

camel-ftp - receiveBufferSize is actually also used for producer

[CAMEL-14050](https://issues.apache.org/jira/browse/CAMEL-14050)

camel-main - Add logic for automatic RouteBuilder class detection ala camel-spring-boot has

[CAMEL-14049](https://issues.apache.org/jira/browse/CAMEL-14049)

camel-netty - Should include scheme in its endpoint url when creating endpoint

[CAMEL-14048](https://issues.apache.org/jira/browse/CAMEL-14048)

camel-core - ServicePool should wait while starting service when acquiring

[CAMEL-14047](https://issues.apache.org/jira/browse/CAMEL-14047)

camel-pulsar: Allow Pulsar to auto-select the unique producerName

[CAMEL-14046](https://issues.apache.org/jira/browse/CAMEL-14046)

Make ValidatorReifier constructor public and add a way to register custom reifiers

[CAMEL-14045](https://issues.apache.org/jira/browse/CAMEL-14045)

Protect against ByteBuffer / CharBuffer inconsistencies between jdk 8 and 9

[CAMEL-14044](https://issues.apache.org/jira/browse/CAMEL-14044)

Do not report validation error for camel uri based on property placeholder

[CAMEL-14041](https://issues.apache.org/jira/browse/CAMEL-14041)

scheduled poll consumer - Add option to limit number of polls

[CAMEL-14040](https://issues.apache.org/jira/browse/CAMEL-14040)

DefaultRegistry - findByType should return merged result incl fallback

[CAMEL-14034](https://issues.apache.org/jira/browse/CAMEL-14034)

Orderes RoutesBuilder

[CAMEL-14032](https://issues.apache.org/jira/browse/CAMEL-14032)

NotifyBuilder.from does not normalize endpoint URI

[CAMEL-14031](https://issues.apache.org/jira/browse/CAMEL-14031)

Move process control from Main to MainSupport

[CAMEL-14022](https://issues.apache.org/jira/browse/CAMEL-14022)

\[MongoDB\] add meta and verifier

[CAMEL-14017](https://issues.apache.org/jira/browse/CAMEL-14017)

camel-netty-http - support the full streaming both on inbound and outbound

[CAMEL-14009](https://issues.apache.org/jira/browse/CAMEL-14009)

Change camel-debezium configuration to be generated during compile time

[CAMEL-13955](https://issues.apache.org/jira/browse/CAMEL-13955)

SJMS-Batch does not support CompletionAware aggregators

[CAMEL-13875](https://issues.apache.org/jira/browse/CAMEL-13875)

Support for MicroProfile Health

[CAMEL-13684](https://issues.apache.org/jira/browse/CAMEL-13684)

Support More CordaOps Operations in Camel-Corda component

[CAMEL-13392](https://issues.apache.org/jira/browse/CAMEL-13392)

camel-bindy - Add allowEmptyStream option

### New Feature (3)

[CAMEL-14025](https://issues.apache.org/jira/browse/CAMEL-14025)

Http consumers - Add option to turn off dump exception in plain text as response

[CAMEL-12854](https://issues.apache.org/jira/browse/CAMEL-12854)

Provide a GraphQL component

[CAMEL-9952](https://issues.apache.org/jira/browse/CAMEL-9952)

Provide access to stream in camel-netty4-http component

### Sub-task (1)

[CAMEL-14037](https://issues.apache.org/jira/browse/CAMEL-14037)

Create a camel-testcontainers-junit5 module

### Task (2)

[CAMEL-14039](https://issues.apache.org/jira/browse/CAMEL-14039)

camel-karaf - Remove features deprecated in OSGi

[CAMEL-14024](https://issues.apache.org/jira/browse/CAMEL-14024)

camel-mqtt - Deprecate as the mqtt client is not active maintained

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).