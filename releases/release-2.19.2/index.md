# Apache camel 2.19.2 Release

## New and Noteworthy

This release is a minor update of the 2.19.x branch.

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
      <version>2.19.2</version>
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
      <version>2.19.2</version>
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
| [apache-camel-2.19.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.19.2/apache-camel-2.19.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.19.2/apache-camel-2.19.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.19.2/apache-camel-2.19.2-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.19.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.19.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (30)

[CAMEL-11610](https://issues.apache.org/jira/browse/CAMEL-11610)

UnsatisfiedDependencyException: Error creating bean with name 'openTracingEventNotifier'

[CAMEL-11576](https://issues.apache.org/jira/browse/CAMEL-11576)

camel-catalog is not generating camel-stream URI properly

[CAMEL-11575](https://issues.apache.org/jira/browse/CAMEL-11575)

Component name mismatch: https4 or http4s

[CAMEL-11572](https://issues.apache.org/jira/browse/CAMEL-11572)

camel-lumberjack component doesn't restart

[CAMEL-11564](https://issues.apache.org/jira/browse/CAMEL-11564)

avoid ClassCastException when the gzip is enabled for the cxf endpoint with camel destination

[CAMEL-11559](https://issues.apache.org/jira/browse/CAMEL-11559)

NPE when not setting a sampling interval on client subscriptions

[CAMEL-11540](https://issues.apache.org/jira/browse/CAMEL-11540)

Unable to disable ProducerCache by setting cacheSize="-1"

[CAMEL-11537](https://issues.apache.org/jira/browse/CAMEL-11537)

undertown consumer : consumer silently fails to start if manually started after a failure

[CAMEL-11533](https://issues.apache.org/jira/browse/CAMEL-11533)

Simple language - comparison againist negative value fails with unknown token

[CAMEL-11529](https://issues.apache.org/jira/browse/CAMEL-11529)

Wrong syntax definitions in camel catalog

[CAMEL-11524](https://issues.apache.org/jira/browse/CAMEL-11524)

Camel File Consumer fails when doneFileName contains '$'

[CAMEL-11520](https://issues.apache.org/jira/browse/CAMEL-11520)

camel-hipchat: Unable to send to room name containing spaces

[CAMEL-11510](https://issues.apache.org/jira/browse/CAMEL-11510)

The consumer endpoint for Twitter component timeline/user doesn't poll the tweets even if the type is set to polling and delay attribute doesn't work

[CAMEL-11509](https://issues.apache.org/jira/browse/CAMEL-11509)

Cannot set content type with parameters without specifying charset

[CAMEL-11489](https://issues.apache.org/jira/browse/CAMEL-11489)

Declaring AWS endpoint with accessKey and secretKey, and without amazonS3Client should be possible.

[CAMEL-11486](https://issues.apache.org/jira/browse/CAMEL-11486)

NullPointerException for invalid payload with session handling enabled

[CAMEL-11477](https://issues.apache.org/jira/browse/CAMEL-11477)

Can not override isUseAdviceWith in CamelBlueprintTestSupport

[CAMEL-11469](https://issues.apache.org/jira/browse/CAMEL-11469)

Camel-Hipchat - Configure via xml is broken

[CAMEL-11454](https://issues.apache.org/jira/browse/CAMEL-11454)

camel-zipfile dataformat cannot remove successfully processed files

[CAMEL-11453](https://issues.apache.org/jira/browse/CAMEL-11453)

Fix camel-box feature

[CAMEL-11441](https://issues.apache.org/jira/browse/CAMEL-11441)

Main - setPropertyPlaceholderLocations should be public

[CAMEL-11437](https://issues.apache.org/jira/browse/CAMEL-11437)

Bug using file endpoint probeContentType and preMove attributes together causes Exchange.FILE\_CONTENT\_TYPE to get dropped. (2.19.0)

[CAMEL-11433](https://issues.apache.org/jira/browse/CAMEL-11433)

Unable to use camel-box in OSGI environment

[CAMEL-11429](https://issues.apache.org/jira/browse/CAMEL-11429)

camel-box is not assigning default configuration values

[CAMEL-11427](https://issues.apache.org/jira/browse/CAMEL-11427)

camel-leveldb does not work on Solaris -- no native code library and no Java fallback

[CAMEL-11424](https://issues.apache.org/jira/browse/CAMEL-11424)

Endless wait when unhandled exception occurs in camel-olingo

[CAMEL-11423](https://issues.apache.org/jira/browse/CAMEL-11423)

Accept header is not compliant with IETF RFC-7231

[CAMEL-11414](https://issues.apache.org/jira/browse/CAMEL-11414)

camel-restlet - Rest DSL issue with empty path variables

[CAMEL-11413](https://issues.apache.org/jira/browse/CAMEL-11413)

camel-olingo - Potential NPE in getting content-type header

[CAMEL-11388](https://issues.apache.org/jira/browse/CAMEL-11388)

camel-infinispan - InfinispanRoutePolicy issue with locking from remote server

### Improvement (11)

[CAMEL-11552](https://issues.apache.org/jira/browse/CAMEL-11552)

Provide FailureEvent interface as a general means of retrieving the cause

[CAMEL-11551](https://issues.apache.org/jira/browse/CAMEL-11551)

Use abstract base class for all context and route events

[CAMEL-11531](https://issues.apache.org/jira/browse/CAMEL-11531)

camel-http-common; dependency servlet-api should be set to provided

[CAMEL-11507](https://issues.apache.org/jira/browse/CAMEL-11507)

camel-servicenow : add an header to indicate the answer data type

[CAMEL-11506](https://issues.apache.org/jira/browse/CAMEL-11506)

MavenVersionManager blocks on unavailable URL

[CAMEL-11490](https://issues.apache.org/jira/browse/CAMEL-11490)

camel-spring-boot - Make it easy to filter Java RoutesBuilder from properties

[CAMEL-11466](https://issues.apache.org/jira/browse/CAMEL-11466)

camel-tarfile dataformat cannot remove successfully processed files

[CAMEL-11461](https://issues.apache.org/jira/browse/CAMEL-11461)

SEDA - resolve references for concurrentConsumers, limitConcurrentConsumers

[CAMEL-11422](https://issues.apache.org/jira/browse/CAMEL-11422)

Mark plugin as threadsafe

[CAMEL-11398](https://issues.apache.org/jira/browse/CAMEL-11398)

camel-google-calendar should throw more friendly exception when the required credentials lack

[CAMEL-11396](https://issues.apache.org/jira/browse/CAMEL-11396)

Upgrade wsdl4j to 1.6.3

### Sub-task (1)

[CAMEL-11491](https://issues.apache.org/jira/browse/CAMEL-11491)

Apply non-mandatory nature of amazon client to AWS components being able to specify accessKey and secretKey

### Test (1)

[CAMEL-11516](https://issues.apache.org/jira/browse/CAMEL-11516)

FtpConsumerFileSplitTest fails on windows due to platform line.seperator

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).