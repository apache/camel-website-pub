# Apache camel 3.18.1 Release

## New and Noteworthy

This release is the new Camel 3.18.1 LTS patch release.

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
      <version>3.18.1</version>
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
      <version>3.18.1</version>
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
| [apache-camel-3.18.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.18.1/apache-camel-3.18.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.18.1/apache-camel-3.18.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.18.1/apache-camel-3.18.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.18.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.18.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (22)

[CAMEL-18434](https://issues.apache.org/jira/browse/CAMEL-18434)

JMSMessages being dropped after a EOFException/bad packet received

[CAMEL-18378](https://issues.apache.org/jira/browse/CAMEL-18378)

SFTP serverHostKeys-parameter is unknown

[CAMEL-18338](https://issues.apache.org/jira/browse/CAMEL-18338)

IMAP MailConsumer NullPointerException due CAMEL-16180

[CAMEL-18336](https://issues.apache.org/jira/browse/CAMEL-18336)

camel-jbang: YAML DSL cannot find classes for local beans

[CAMEL-18331](https://issues.apache.org/jira/browse/CAMEL-18331)

camel-spring-xml - <endpoint> bean added via beans.xml are parsed twice

[CAMEL-18329](https://issues.apache.org/jira/browse/CAMEL-18329)

RouteTemplate: templateParameter doesn't get resolved

[CAMEL-18324](https://issues.apache.org/jira/browse/CAMEL-18324)

camel-core - Exception during preparing exchange task can block thread

[CAMEL-18322](https://issues.apache.org/jira/browse/CAMEL-18322)

Camel-Jbang export copy properties erroneously

[CAMEL-18321](https://issues.apache.org/jira/browse/CAMEL-18321)

camel-mybatis - Should support using Map message body as-is for insert/update

[CAMEL-18319](https://issues.apache.org/jira/browse/CAMEL-18319)

camel-core - Supervising route controller should not eager warmup routes

[CAMEL-18310](https://issues.apache.org/jira/browse/CAMEL-18310)

Global SSL Context Params Force SSL for All HTTP Connections

[CAMEL-18300](https://issues.apache.org/jira/browse/CAMEL-18300)

Google storage component does not set metadata appropriately

[CAMEL-18289](https://issues.apache.org/jira/browse/CAMEL-18289)

camel-xslt-saxon: XsltAggregationStrategyTest fails with removing the log definition

[CAMEL-18288](https://issues.apache.org/jira/browse/CAMEL-18288)

YAML DSL DoTry does not work

[CAMEL-18286](https://issues.apache.org/jira/browse/CAMEL-18286)

\[Camel Spring Boot\] camel-lra-starter needs camel-servlet-starter to work

[CAMEL-18279](https://issues.apache.org/jira/browse/CAMEL-18279)

When run 3.18.0 with Spring Boot, received java.io.FileNotFoundException: class path resource \[.class\] cannot be opened because it does not exist

[CAMEL-18278](https://issues.apache.org/jira/browse/CAMEL-18278)

AdviceWith fails with Spring XML and several route cross cutting concerns

[CAMEL-18274](https://issues.apache.org/jira/browse/CAMEL-18274)

OSGi - camel-file: ClassNotFoundException because of Private-Package

[CAMEL-18270](https://issues.apache.org/jira/browse/CAMEL-18270)

IMAP skipFailedMessage=true, but route blocked if mail is moved while download

[CAMEL-18266](https://issues.apache.org/jira/browse/CAMEL-18266)

Can not use bean uri in xslt component

[CAMEL-18262](https://issues.apache.org/jira/browse/CAMEL-18262)

Templated route exception handling not working

[CAMEL-16287](https://issues.apache.org/jira/browse/CAMEL-16287)

camel-aws2-sqs should use pagination for deciding which aws sqs queues it should create

### Dependency upgrade (2)

[CAMEL-18294](https://issues.apache.org/jira/browse/CAMEL-18294)

upgrade to spring boot 2.7.2

[CAMEL-18246](https://issues.apache.org/jira/browse/CAMEL-18246)

CVE-2022-26612: Upgrade hadoop-common >= 3.3.3

### Improvement (16)

[CAMEL-18345](https://issues.apache.org/jira/browse/CAMEL-18345)

EMPTY\_ELEMENT\_AS\_NULL disabled by default in jackson-dataformat-xml

[CAMEL-18343](https://issues.apache.org/jira/browse/CAMEL-18343)

camel-yaml-dsl - Add route-policy

[CAMEL-18339](https://issues.apache.org/jira/browse/CAMEL-18339)

camel-joor - Java DSL - Allow compiled classes to be loadable from anywhere in Camel

[CAMEL-18333](https://issues.apache.org/jira/browse/CAMEL-18333)

camel-kafka: better error messages in the health check

[CAMEL-18323](https://issues.apache.org/jira/browse/CAMEL-18323)

camel-jpa: introduce a transaction strategy

[CAMEL-18318](https://issues.apache.org/jira/browse/CAMEL-18318)

camel-quartz - Context fails to start when one of the cron configuration has expired

[CAMEL-18311](https://issues.apache.org/jira/browse/CAMEL-18311)

camel-jbang - Running files should detect duplicated names

[CAMEL-18307](https://issues.apache.org/jira/browse/CAMEL-18307)

camel-stub - Should accept lenient configuration

[CAMEL-18306](https://issues.apache.org/jira/browse/CAMEL-18306)

camel-jbang - Allow to specify open-api in application.properties

[CAMEL-18299](https://issues.apache.org/jira/browse/CAMEL-18299)

camel-core - ResumeAdapter should use FactoryFinder to lookup implementations

[CAMEL-18297](https://issues.apache.org/jira/browse/CAMEL-18297)

camel-core - Languages with namespace support should be exposed in model

[CAMEL-18293](https://issues.apache.org/jira/browse/CAMEL-18293)

camel-cxf - Move CXFTestSupport to test-jar

[CAMEL-18292](https://issues.apache.org/jira/browse/CAMEL-18292)

Datasonnet expression should not fail if body is empty

[CAMEL-18285](https://issues.apache.org/jira/browse/CAMEL-18285)

camel-file - Lazy-loading for file length and last modified attributes for faster performance

[CAMEL-18264](https://issues.apache.org/jira/browse/CAMEL-18264)

Camel SFTP: Cannot configure JSch client to use ssh-dss key

[CAMEL-18260](https://issues.apache.org/jira/browse/CAMEL-18260)

debugger - Reflect exchange changes on BacklogTracerEventMessage

### New Feature (1)

[CAMEL-18291](https://issues.apache.org/jira/browse/CAMEL-18291)

SSLContextParameters parsePropertyValue support for certAlias property

### Task (1)

[CAMEL-17947](https://issues.apache.org/jira/browse/CAMEL-17947)

camel-kafka: fix concurrent access in camel-health

### Test (1)

[CAMEL-18349](https://issues.apache.org/jira/browse/CAMEL-18349)

Core - XPathRouteConcurrentBigTest - newly added limit of "operators an XPath expression can contain." fails the test

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).