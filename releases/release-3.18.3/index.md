# Apache camel 3.18.3 Release

## New and Noteworthy

This release is the new Camel 3.18.3 LTS patch release.

## Supported Java version

This version supports Java 11 and 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.18.3</version>
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
      <version>3.18.3</version>
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
| [apache-camel-3.18.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.18.3/apache-camel-3.18.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.18.3/apache-camel-3.18.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.18.3/apache-camel-3.18.3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.18.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.18.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (25)

[CAMEL-18627](https://issues.apache.org/jira/browse/CAMEL-18627)

camel-kafka: Kafka resume throws null pointer exception if no partition offset exists

[CAMEL-18624](https://issues.apache.org/jira/browse/CAMEL-18624)

camel-jbang - Should load custom type converters when adding new JARs

[CAMEL-18612](https://issues.apache.org/jira/browse/CAMEL-18612)

Inconsistency in JsonPath component causes problems with databinding

[CAMEL-18603](https://issues.apache.org/jira/browse/CAMEL-18603)

Camel-Jbang: When using aws-ddb-sink Kamelet dependency are not resolved

[CAMEL-18589](https://issues.apache.org/jira/browse/CAMEL-18589)

Bug in org.apache.camel.http.common.DefaultHttpBinding.java

[CAMEL-18588](https://issues.apache.org/jira/browse/CAMEL-18588)

Kafka consumer on any exception should repoll records after the committed offset

[CAMEL-18587](https://issues.apache.org/jira/browse/CAMEL-18587)

Kafka Consumer closes on any exception if breakOnFirstError is set to TRUE

[CAMEL-18586](https://issues.apache.org/jira/browse/CAMEL-18586)

Spinning JVM through interception using interceptFrom interceptSendToEndpoint

[CAMEL-18585](https://issues.apache.org/jira/browse/CAMEL-18585)

Validator: investigate strange validator behavior

[CAMEL-18583](https://issues.apache.org/jira/browse/CAMEL-18583)

\[camel-minio\] deleteObjects operation does not delete multiple objects

[CAMEL-18579](https://issues.apache.org/jira/browse/CAMEL-18579)

Missing osgi import for CxfUtils in camel-cxf-rest

[CAMEL-18563](https://issues.apache.org/jira/browse/CAMEL-18563)

camel-karaf - ClassNotDefFoundError when an exception thrown from a cxfrs route

[CAMEL-18544](https://issues.apache.org/jira/browse/CAMEL-18544)

camel-http - ToD optimized context-path with spaces problem

[CAMEL-18530](https://issues.apache.org/jira/browse/CAMEL-18530)

Camel box cannot authorize

[CAMEL-18514](https://issues.apache.org/jira/browse/CAMEL-18514)

camel-health - health check for not automatically started routes should always be up

[CAMEL-18510](https://issues.apache.org/jira/browse/CAMEL-18510)

camel-jbang - camel bind may not work with --local-kamelet-dir

[CAMEL-18490](https://issues.apache.org/jira/browse/CAMEL-18490)

camel-jbang - Reset statistics can cause JMX inflight counter to be negative

[CAMEL-18489](https://issues.apache.org/jira/browse/CAMEL-18489)

camel-file - Exclusive rename should handle windows locking the file

[CAMEL-18483](https://issues.apache.org/jira/browse/CAMEL-18483)

camel-microprofile-health: Routes and consumers health checks are not registered if routes are supervised

[CAMEL-18477](https://issues.apache.org/jira/browse/CAMEL-18477)

knative producer with ProducerTemplate is missing the fromRouteId

[CAMEL-18476](https://issues.apache.org/jira/browse/CAMEL-18476)

when artemis streaming enabled then Camel-jms component is not closing inputstream for Bytes message, blocking deletion of file after its archived in windows

[CAMEL-18473](https://issues.apache.org/jira/browse/CAMEL-18473)

Knative component : CloudEvents have wrong time format

[CAMEL-18427](https://issues.apache.org/jira/browse/CAMEL-18427)

Camel Debezium with Postgres on Spring Boot doesn't work

[CAMEL-18350](https://issues.apache.org/jira/browse/CAMEL-18350)

camel-kafka: enabling "breakOnFirstError" causes camel to reconsume all records on error

[CAMEL-17859](https://issues.apache.org/jira/browse/CAMEL-17859)

camel-smpp: Consumer sometimes tries to reconnect only once

### Dependency upgrade (4)

[CAMEL-18631](https://issues.apache.org/jira/browse/CAMEL-18631)

spring boot - upgrade to 2.7.5

[CAMEL-18573](https://issues.apache.org/jira/browse/CAMEL-18573)

upgrade to spring boot 2.7.4

[CAMEL-18535](https://issues.apache.org/jira/browse/CAMEL-18535)

camel-hbase: Upgrade to 2.5.0

[CAMEL-18464](https://issues.apache.org/jira/browse/CAMEL-18464)

camel-jbang - upgrade to kamelets 0.9.0

### Improvement (9)

[CAMEL-18626](https://issues.apache.org/jira/browse/CAMEL-18626)

Set the ExchangePattern with a routeTemplate

[CAMEL-18622](https://issues.apache.org/jira/browse/CAMEL-18622)

camel-yaml-dsl - Add support for xxx.camel.yaml extension

[CAMEL-18613](https://issues.apache.org/jira/browse/CAMEL-18613)

camel-cxf - Add option on endpoint to configure schema validation

[CAMEL-18565](https://issues.apache.org/jira/browse/CAMEL-18565)

Camel fails to start routes without failure message when routes-include-pattern has an invalid entry

[CAMEL-18549](https://issues.apache.org/jira/browse/CAMEL-18549)

Dynamic router component should add filters to a map (by filter id) instead of a list to prevent multiple additions of the same filter.

[CAMEL-18533](https://issues.apache.org/jira/browse/CAMEL-18533)

camel-netty - TimeoutCorrelationManagerSupport should stop created thread-pools

[CAMEL-18528](https://issues.apache.org/jira/browse/CAMEL-18528)

ensure CXF SpringBus honor camel graceful shutdown

[CAMEL-18507](https://issues.apache.org/jira/browse/CAMEL-18507)

camel-resilience4j - Add option to throw exception if CB rejected due to half-open/open state

[CAMEL-18461](https://issues.apache.org/jira/browse/CAMEL-18461)

camel-core - Add api\_key as a known secret parameter

### New Feature (5)

[CAMEL-18593](https://issues.apache.org/jira/browse/CAMEL-18593)

Platform-http : add reverse proxy feature

[CAMEL-18527](https://issues.apache.org/jira/browse/CAMEL-18527)

Camel Kafka Component: batch producer with individual headers

[CAMEL-18503](https://issues.apache.org/jira/browse/CAMEL-18503)

Configure max ack extension period parameter in PubSub subscriber

[CAMEL-18494](https://issues.apache.org/jira/browse/CAMEL-18494)

camel-mllp - Allow the ability to set MIN\_BUFFER\_SIZE for SocketBuffer

[CAMEL-18451](https://issues.apache.org/jira/browse/CAMEL-18451)

camel-azure-eventhubs: Add support for Azure-AD authentication

### Task (9)

[CAMEL-18467](https://issues.apache.org/jira/browse/CAMEL-18467)

\[DOCS\] Velocity component - missing java code sample

[CAMEL-18346](https://issues.apache.org/jira/browse/CAMEL-18346)

Remove use of Xalan

[CAMEL-18327](https://issues.apache.org/jira/browse/CAMEL-18327)

camel-kafka: Kafka consumer closes when it is paused

[CAMEL-18296](https://issues.apache.org/jira/browse/CAMEL-18296)

camel-example tag is using snapshot camel version

[CAMEL-18244](https://issues.apache.org/jira/browse/CAMEL-18244)

\[DOCS\] AWS SQS component - code samples needs to be updated

[CAMEL-18243](https://issues.apache.org/jira/browse/CAMEL-18243)

\[DOCS\] Kafka component - multiple options need updates

[CAMEL-18241](https://issues.apache.org/jira/browse/CAMEL-18241)

\[DOCS\] HTTP component - missing sample

[CAMEL-18240](https://issues.apache.org/jira/browse/CAMEL-18240)

\[DOCS\] FHIR component - documentation issues

[CAMEL-18239](https://issues.apache.org/jira/browse/CAMEL-18239)

\[DOCS\] Bean components - missing examples

### Test (1)

[CAMEL-18509](https://issues.apache.org/jira/browse/CAMEL-18509)

use servlet transport for camel-cxf spring boot test

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).