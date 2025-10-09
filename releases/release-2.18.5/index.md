# Apache camel 2.18.5 Release

## New and Noteworthy

This release is a minor update of the 2.18.x branch.

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
      <version>2.18.5</version>
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
      <version>2.18.5</version>
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
| [apache-camel-2.18.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.18.5/apache-camel-2.18.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.18.5/apache-camel-2.18.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.18.5/apache-camel-2.18.5-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.18.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.18.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (38)

[CAMEL-11772](https://issues.apache.org/jira/browse/CAMEL-11772)

Sjms with Artemis causes NullPointerException due to a ClassCastException

[CAMEL-11765](https://issues.apache.org/jira/browse/CAMEL-11765)

camel-undertow - Consumer adds duplicate headers

[CAMEL-11750](https://issues.apache.org/jira/browse/CAMEL-11750)

Camel route with multicast (parallel) generate huge CPU load

[CAMEL-11748](https://issues.apache.org/jira/browse/CAMEL-11748)

Camel-Undertow: transferException option doesn't work

[CAMEL-11724](https://issues.apache.org/jira/browse/CAMEL-11724)

Camel-Hdfs2: No need for initialDelay and delay as configuration properties since they are already parameters of ScheduledPollConsumer

[CAMEL-11723](https://issues.apache.org/jira/browse/CAMEL-11723)

ManagedCamelContext.dumpRestsAsXml can fail if default charset is not utf-8

[CAMEL-11716](https://issues.apache.org/jira/browse/CAMEL-11716)

error in handling return parameters in db functions

[CAMEL-11698](https://issues.apache.org/jira/browse/CAMEL-11698)

S3 Consumer does not close S3 Object Input Streams and this causes HTTP connection leaks

[CAMEL-11690](https://issues.apache.org/jira/browse/CAMEL-11690)

Done() called two times in RoutingSlip processor

[CAMEL-11688](https://issues.apache.org/jira/browse/CAMEL-11688)

ensure transport endpoint configuration will be take into account when create JettyRestHttpBinding from REST DSL

[CAMEL-11681](https://issues.apache.org/jira/browse/CAMEL-11681)

camel-cxf - getting TypeConversionException when schema-validation-enabled=true for unwrapped response

[CAMEL-11632](https://issues.apache.org/jira/browse/CAMEL-11632)

QuartzScheduledPollConsumerScheduler causes trigger misfires on each application start

[CAMEL-11630](https://issues.apache.org/jira/browse/CAMEL-11630)

JPAMessageIdRepository Not Releasing Connections

[CAMEL-11623](https://issues.apache.org/jira/browse/CAMEL-11623)

LevelDB Java implementation wont be tried on Errors

[CAMEL-11620](https://issues.apache.org/jira/browse/CAMEL-11620)

Requiredement for date string to be longer than pattern is invalid.

[CAMEL-11608](https://issues.apache.org/jira/browse/CAMEL-11608)

Camel-AWS: Camel-Kinesis needs Jackson Dataformat CBOR to work in OSGi

[CAMEL-11607](https://issues.apache.org/jira/browse/CAMEL-11607)

NPE in MBeanInfoAssembler when debug is enabled

[CAMEL-11572](https://issues.apache.org/jira/browse/CAMEL-11572)

camel-lumberjack component doesn't restart

[CAMEL-11564](https://issues.apache.org/jira/browse/CAMEL-11564)

avoid ClassCastException when the gzip is enabled for the cxf endpoint with camel destination

[CAMEL-11540](https://issues.apache.org/jira/browse/CAMEL-11540)

Unable to disable ProducerCache by setting cacheSize="-1"

[CAMEL-11533](https://issues.apache.org/jira/browse/CAMEL-11533)

Simple language - comparison againist negative value fails with unknown token

[CAMEL-11524](https://issues.apache.org/jira/browse/CAMEL-11524)

Camel File Consumer fails when doneFileName contains '$'

[CAMEL-11523](https://issues.apache.org/jira/browse/CAMEL-11523)

JasyptPropertiesParser fails on properties references with default value

[CAMEL-11520](https://issues.apache.org/jira/browse/CAMEL-11520)

camel-hipchat: Unable to send to room name containing spaces

[CAMEL-11510](https://issues.apache.org/jira/browse/CAMEL-11510)

The consumer endpoint for Twitter component timeline/user doesn't poll the tweets even if the type is set to polling and delay attribute doesn't work

[CAMEL-11477](https://issues.apache.org/jira/browse/CAMEL-11477)

Can not override isUseAdviceWith in CamelBlueprintTestSupport

[CAMEL-11472](https://issues.apache.org/jira/browse/CAMEL-11472)

\[camel-box\] missing Karaf feature dependency

[CAMEL-11469](https://issues.apache.org/jira/browse/CAMEL-11469)

Camel-Hipchat - Configure via xml is broken

[CAMEL-11441](https://issues.apache.org/jira/browse/CAMEL-11441)

Main - setPropertyPlaceholderLocations should be public

[CAMEL-11427](https://issues.apache.org/jira/browse/CAMEL-11427)

camel-leveldb does not work on Solaris -- no native code library and no Java fallback

[CAMEL-11424](https://issues.apache.org/jira/browse/CAMEL-11424)

Endless wait when unhandled exception occurs in camel-olingo

[CAMEL-11423](https://issues.apache.org/jira/browse/CAMEL-11423)

Accept header is not compliant with IETF RFC-7231

[CAMEL-11417](https://issues.apache.org/jira/browse/CAMEL-11417)

route-reset-stats completion issue

[CAMEL-11414](https://issues.apache.org/jira/browse/CAMEL-11414)

camel-restlet - Rest DSL issue with empty path variables

[CAMEL-11394](https://issues.apache.org/jira/browse/CAMEL-11394)

Undertow endpoint option REUSE\_ADDRESS is configured using the value for TCP\_NO\_DELAY

[CAMEL-11392](https://issues.apache.org/jira/browse/CAMEL-11392)

String to ByteBuffer conversion causes overflow due to multibyte chars

[CAMEL-11317](https://issues.apache.org/jira/browse/CAMEL-11317)

\[OSGi, camel-jpa\] Problems with mapping idempotent.jpa.MessageProcessed with Aries + Hibernate

[CAMEL-11298](https://issues.apache.org/jira/browse/CAMEL-11298)

Using chmodDirectory with full paths makes file producer to created directories relative to source

### Improvement (12)

[CAMEL-12251](https://issues.apache.org/jira/browse/CAMEL-12251)

Do not hide (so much) blueprint.container.ComponentDefinitionException

[CAMEL-11755](https://issues.apache.org/jira/browse/CAMEL-11755)

toD should ignore when dynamic uri is empty

[CAMEL-11728](https://issues.apache.org/jira/browse/CAMEL-11728)

Camel-AWS S3: Avoid warn log message about content length

[CAMEL-11720](https://issues.apache.org/jira/browse/CAMEL-11720)

GoogleDriveProducer should be able to honor the http.proxyPort and http.proxyHost properties from the CamelContext

[CAMEL-11719](https://issues.apache.org/jira/browse/CAMEL-11719)

add a string to ChildReference converter for camel-google-drive

[CAMEL-11706](https://issues.apache.org/jira/browse/CAMEL-11706)

Remove duplicate type converter methods from HBaseModelConverter

[CAMEL-11552](https://issues.apache.org/jira/browse/CAMEL-11552)

Provide FailureEvent interface as a general means of retrieving the cause

[CAMEL-11551](https://issues.apache.org/jira/browse/CAMEL-11551)

Use abstract base class for all context and route events

[CAMEL-11463](https://issues.apache.org/jira/browse/CAMEL-11463)

back port CAMEL-11319 to 2.18

[CAMEL-11355](https://issues.apache.org/jira/browse/CAMEL-11355)

Consumer - ErrorHandler should ignore rejected exception due to shutdown

[CAMEL-11323](https://issues.apache.org/jira/browse/CAMEL-11323)

Query Params are not mapped to camel headers with SparkJava

[CAMEL-11313](https://issues.apache.org/jira/browse/CAMEL-11313)

set defaultValue for FixedLength and other factories

### Task (2)

[CAMEL-11326](https://issues.apache.org/jira/browse/CAMEL-11326)

Exclude org.json from camel-spark

[CAMEL-11301](https://issues.apache.org/jira/browse/CAMEL-11301)

Camel-weather and camel-geocoder: freegeoip.io/json has been moved permanently

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).