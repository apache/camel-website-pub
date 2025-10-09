# Apache camel 2.23.3 Release

## New and Noteworthy

This release is a minor update of the 2.23.x branch.

## Supported Java version

This version supports Java 8.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>2.23.3</version>
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
      <version>2.23.3</version>
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
| [apache-camel-2.23.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.23.3/apache-camel-2.23.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.23.3/apache-camel-2.23.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.23.3/apache-camel-2.23.3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.23.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.23.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (27)

[CAMEL-13625](https://issues.apache.org/jira/browse/CAMEL-13625)

Quartz2 firenow doesn't work consistently

[CAMEL-13587](https://issues.apache.org/jira/browse/CAMEL-13587)

InflightRepository, InflightEntry getElapsed is 0

[CAMEL-13576](https://issues.apache.org/jira/browse/CAMEL-13576)

avoid adding cxf message context map into camel exchange

[CAMEL-13554](https://issues.apache.org/jira/browse/CAMEL-13554)

Using "route1" as a route id produces infinite loop

[CAMEL-13541](https://issues.apache.org/jira/browse/CAMEL-13541)

Race condition in camel-hystrix when xecutionTimeoutInMilliseconds() and onFallback() are used

[CAMEL-13536](https://issues.apache.org/jira/browse/CAMEL-13536)

StackOverflow when using bean(this)

[CAMEL-13524](https://issues.apache.org/jira/browse/CAMEL-13524)

RuntimeCamelCatalog#asEndpointUri strips dash from url with toD and netty4-http

[CAMEL-13513](https://issues.apache.org/jira/browse/CAMEL-13513)

CXFRS header "CamelDestinationOverrideUrl" ignored after changing it twice

[CAMEL-13497](https://issues.apache.org/jira/browse/CAMEL-13497)

Setting a clientConfig parameter always creates new cookie store per endpoint

[CAMEL-13496](https://issues.apache.org/jira/browse/CAMEL-13496)

maven-invoker-plugin taking as much heapspace as the Maven itself

[CAMEL-13479](https://issues.apache.org/jira/browse/CAMEL-13479)

Camel Shiro has a transitive dependency to Commons-Collections

[CAMEL-13477](https://issues.apache.org/jira/browse/CAMEL-13477)

KafkaConfiguration puts truststore password into keystore password property

[CAMEL-13468](https://issues.apache.org/jira/browse/CAMEL-13468)

Exception tag is missing when Camel Java DSL is converted into XML using dumpRouteAsXml() operation

[CAMEL-13464](https://issues.apache.org/jira/browse/CAMEL-13464)

Problem with Olingo4 and authenticated metadata

[CAMEL-13438](https://issues.apache.org/jira/browse/CAMEL-13438)

Camel jBPM WorkItemHandler should allow passthrough of Exceptions

[CAMEL-13437](https://issues.apache.org/jira/browse/CAMEL-13437)

ThrowExceptionProcessor should use 'getConstructor' instead of 'getDeclaredConstructor', so it doesn't force users to implement the constructors of their exception classes.

[CAMEL-13433](https://issues.apache.org/jira/browse/CAMEL-13433)

S3: Exchange body stream is loaded into memory to calculate content length which is already set via headers

[CAMEL-13428](https://issues.apache.org/jira/browse/CAMEL-13428)

camel-undertow - Response with large data gets truncated on cloud

[CAMEL-13409](https://issues.apache.org/jira/browse/CAMEL-13409)

Fix syntax for nsq component

[CAMEL-13407](https://issues.apache.org/jira/browse/CAMEL-13407)

CouchDbChangesetTracker fails silently on network error and does not recover

[CAMEL-13400](https://issues.apache.org/jira/browse/CAMEL-13400)

Camel FTP Cannot list directory with 'File not found' prepending additional '/' in front of directory automatically

[CAMEL-13397](https://issues.apache.org/jira/browse/CAMEL-13397)

RedisStringIdempotentRepository resetting expiry on existing keys

[CAMEL-13396](https://issues.apache.org/jira/browse/CAMEL-13396)

camel-leveldb can no longer use non-native leveldb libraries

[CAMEL-13376](https://issues.apache.org/jira/browse/CAMEL-13376)

camel-cxf - failure processor for custom exception handling cannot get the original message

[CAMEL-12975](https://issues.apache.org/jira/browse/CAMEL-12975)

WARN: No CamelContext defined yet so cannot inject into bean: org.apache.camel.converter.jaxb.FallbackTypeConverter

[CAMEL-12963](https://issues.apache.org/jira/browse/CAMEL-12963)

camel-salesforce-maven-plugin generates code that does not compile

[CAMEL-12947](https://issues.apache.org/jira/browse/CAMEL-12947)

MockEndpoint.expectedHeaderReceived should fail when no exchange received

### Improvement (4)

[CAMEL-13593](https://issues.apache.org/jira/browse/CAMEL-13593)

avoid “expected resource not found” warnings when using camel-mail in OSGi

[CAMEL-13527](https://issues.apache.org/jira/browse/CAMEL-13527)

Implement missing optimisation for DelimiterBasedFrameDecoder

[CAMEL-13476](https://issues.apache.org/jira/browse/CAMEL-13476)

QuartzScheduledPollConsumerScheduler should not remove trigger when quartz is clustered

[CAMEL-12978](https://issues.apache.org/jira/browse/CAMEL-12978)

Add support to configure CamelContext created by KIE-Server extension

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).