# Apache camel 2.19.4 Release

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
      <version>2.19.4</version>
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
      <version>2.19.4</version>
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
| [apache-camel-2.19.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.19.4/apache-camel-2.19.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.19.4/apache-camel-2.19.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.19.4/apache-camel-2.19.4-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.19.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.19.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (31)

[CAMEL-11967](https://issues.apache.org/jira/browse/CAMEL-11967)

Restlet binding should not create jaxb marshaller when binding mode is set to json

[CAMEL-11962](https://issues.apache.org/jira/browse/CAMEL-11962)

AdviceWith weaveAddFirst using onCompletion issue

[CAMEL-11961](https://issues.apache.org/jira/browse/CAMEL-11961)

ClassCastException in HttpMessage

[CAMEL-11951](https://issues.apache.org/jira/browse/CAMEL-11951)

Uri matching does not match request type

[CAMEL-11926](https://issues.apache.org/jira/browse/CAMEL-11926)

close JMXConnector on shutdown of JMXConsumer in camel-jmx

[CAMEL-11922](https://issues.apache.org/jira/browse/CAMEL-11922)

Persistent tail tracking picks random tail tracker from mongoDB collection

[CAMEL-11920](https://issues.apache.org/jira/browse/CAMEL-11920)

camel-hdfs2 not working in osgi using documented HdfsOsgiHelper

[CAMEL-11898](https://issues.apache.org/jira/browse/CAMEL-11898)

camel-spring-ws - Attachments are lost

[CAMEL-11896](https://issues.apache.org/jira/browse/CAMEL-11896)

camel-spring-boot - set CamelLogDebugBodyMaxChars when 0 or negative

[CAMEL-11894](https://issues.apache.org/jira/browse/CAMEL-11894)

camel-karaf-commands deployment failed on karaf 4.0

[CAMEL-11892](https://issues.apache.org/jira/browse/CAMEL-11892)

SpringWebserviceConsumer and class cast exception

[CAMEL-11881](https://issues.apache.org/jira/browse/CAMEL-11881)

Queue/Exchange parameters need to be numeric when declaring in RabbitMQ

[CAMEL-11866](https://issues.apache.org/jira/browse/CAMEL-11866)

Simple Expression Language bean doesn't throw exception when bean not found

[CAMEL-11848](https://issues.apache.org/jira/browse/CAMEL-11848)

Using MongoDB Tailable Cursor Consumer on non-capped collection results in NullPointerException (instead of proper error message)

[CAMEL-11844](https://issues.apache.org/jira/browse/CAMEL-11844)

camel-azure - Should work with Camel file component OOTB

[CAMEL-11843](https://issues.apache.org/jira/browse/CAMEL-11843)

Unable to configure some URI options on DockerEndpoint

[CAMEL-11838](https://issues.apache.org/jira/browse/CAMEL-11838)

camel-websocket - Static resource returns empty body

[CAMEL-11811](https://issues.apache.org/jira/browse/CAMEL-11811)

Camel FTP fails to create intermediate directory

[CAMEL-11798](https://issues.apache.org/jira/browse/CAMEL-11798)

Connector API assumes flat classpath

[CAMEL-11797](https://issues.apache.org/jira/browse/CAMEL-11797)

CamelMessageHistoryOutputFormat global option ignored for message history

[CAMEL-11791](https://issues.apache.org/jira/browse/CAMEL-11791)

RabbitMQ Producer/Consumer does not recover if exchange/queue is deleted manually

[CAMEL-11785](https://issues.apache.org/jira/browse/CAMEL-11785)

CompositeApiClient cannot handle null ResponseStream

[CAMEL-11772](https://issues.apache.org/jira/browse/CAMEL-11772)

Sjms with Artemis causes NullPointerException due to a ClassCastException

[CAMEL-11698](https://issues.apache.org/jira/browse/CAMEL-11698)

S3 Consumer does not close S3 Object Input Streams and this causes HTTP connection leaks

[CAMEL-11681](https://issues.apache.org/jira/browse/CAMEL-11681)

camel-cxf - getting TypeConversionException when schema-validation-enabled=true for unwrapped response

[CAMEL-11632](https://issues.apache.org/jira/browse/CAMEL-11632)

QuartzScheduledPollConsumerScheduler causes trigger misfires on each application start

[CAMEL-11624](https://issues.apache.org/jira/browse/CAMEL-11624)

REST DSL/component method Uppercase

[CAMEL-11482](https://issues.apache.org/jira/browse/CAMEL-11482)

SSLContextParameters settings are not properly copied to SslContextFactory

[CAMEL-11387](https://issues.apache.org/jira/browse/CAMEL-11387)

SFTP is delivered into incorrect location, without exception (file in subfolder + temp file is created + Camel running on Window & SFTP server running on LINUX)

[CAMEL-11286](https://issues.apache.org/jira/browse/CAMEL-11286)

Imported Xquery modules will not resolve using classpath - Regression

[CAMEL-11045](https://issues.apache.org/jira/browse/CAMEL-11045)

onCompletion does not trigger on failure if split is in route

### Improvement (6)

[CAMEL-11929](https://issues.apache.org/jira/browse/CAMEL-11929)

camel-castor - Add more configuration

[CAMEL-11895](https://issues.apache.org/jira/browse/CAMEL-11895)

camel-hystrix - Expose state of circuit breaker on JMX / processor

[CAMEL-11891](https://issues.apache.org/jira/browse/CAMEL-11891)

XML2JSON Data Format and empty requests

[CAMEL-11862](https://issues.apache.org/jira/browse/CAMEL-11862)

Convert to requested type values retrieved from the repository

[CAMEL-11788](https://issues.apache.org/jira/browse/CAMEL-11788)

Chunk may not find templates in modular class loading environments

[CAMEL-11308](https://issues.apache.org/jira/browse/CAMEL-11308)

MongoDB: No (auto) conversion for BigDecimal

### New Feature (1)

[CAMEL-11923](https://issues.apache.org/jira/browse/CAMEL-11923)

Camel-Hessian: Add Whitelisting feature

### Task (1)

[CAMEL-11775](https://issues.apache.org/jira/browse/CAMEL-11775)

Upgrade to Spring Boot 1.5.7 or better

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).