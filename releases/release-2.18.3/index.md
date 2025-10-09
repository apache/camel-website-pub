# Apache camel 2.18.3 Release

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
      <version>2.18.3</version>
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
      <version>2.18.3</version>
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
| [apache-camel-2.18.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.18.3/apache-camel-2.18.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.18.3/apache-camel-2.18.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.18.3/apache-camel-2.18.3-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.18.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.18.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (24)

[CAMEL-10951](https://issues.apache.org/jira/browse/CAMEL-10951)

Invalid default field values in Spring Boot ComponentConfiguration classes

[CAMEL-10914](https://issues.apache.org/jira/browse/CAMEL-10914)

CxfConsumer doesn't clean up the CXF endpoint MBean upon stop

[CAMEL-10893](https://issues.apache.org/jira/browse/CAMEL-10893)

PDU is lost when SnmpMessage is copied

[CAMEL-10888](https://issues.apache.org/jira/browse/CAMEL-10888)

camel-spring-ws - Has problem with returning proper response due invalid IN vs OUT code

[CAMEL-10874](https://issues.apache.org/jira/browse/CAMEL-10874)

JettyHttpComponent sets selector threads to 0 when running on 1 CPU

[CAMEL-10873](https://issues.apache.org/jira/browse/CAMEL-10873)

camel-sjms transacted routes dead-lock when exceptions are thrown by asynchronous processors

[CAMEL-10856](https://issues.apache.org/jira/browse/CAMEL-10856)

ZipkinTracer does not trigger doStart() when used in XML DSL

[CAMEL-10855](https://issues.apache.org/jira/browse/CAMEL-10855)

Camel adviceWith behaves differently when changing the order of weave statements

[CAMEL-10841](https://issues.apache.org/jira/browse/CAMEL-10841)

Move operation will create a warning log message

[CAMEL-10822](https://issues.apache.org/jira/browse/CAMEL-10822)

Camel Jasypt component throws NPE

[CAMEL-10817](https://issues.apache.org/jira/browse/CAMEL-10817)

dumpModelAsXml can return invalid XML namespace xmlns:xmlns

[CAMEL-10802](https://issues.apache.org/jira/browse/CAMEL-10802)

java.lang.ClassCastException when using FlexibleAggregationStrategy with Spring Boot

[CAMEL-10789](https://issues.apache.org/jira/browse/CAMEL-10789)

Indexing with simple expression broken in Apache Camel 2.18

[CAMEL-10788](https://issues.apache.org/jira/browse/CAMEL-10788)

Multiple handlers with multiple endpoints on same port causes a handler loop

[CAMEL-10783](https://issues.apache.org/jira/browse/CAMEL-10783)

XSLT transform cannot use default DTM

[CAMEL-10782](https://issues.apache.org/jira/browse/CAMEL-10782)

SFTP: cannot get files from users home with readlock changed

[CAMEL-10767](https://issues.apache.org/jira/browse/CAMEL-10767)

Versions of swagger-models and swagger-parser in conflict

[CAMEL-10756](https://issues.apache.org/jira/browse/CAMEL-10756)

Mina2 Producer "hang" until timeout if the response message could not be decoded

[CAMEL-10747](https://issues.apache.org/jira/browse/CAMEL-10747)

CamelContext is not been set in VMConsumer when used with POJO @Consume

[CAMEL-10741](https://issues.apache.org/jira/browse/CAMEL-10741)

LogEndpoint error constructing LogProducer

[CAMEL-10738](https://issues.apache.org/jira/browse/CAMEL-10738)

direct-vm component behavior broken in 2.18.1 vs 2.17.4

[CAMEL-10736](https://issues.apache.org/jira/browse/CAMEL-10736)

Box component configuration problem

[CAMEL-10537](https://issues.apache.org/jira/browse/CAMEL-10537)

Unable to remove/add restful path to an existing endpoint

[CAMEL-9502](https://issues.apache.org/jira/browse/CAMEL-9502)

karaf - Re-installing bundle using camel-cxf throws javax.management.InstanceAlreadyExistsException

### Improvement (11)

[CAMEL-10894](https://issues.apache.org/jira/browse/CAMEL-10894)

XML Validator: Improve DTD handling

[CAMEL-10870](https://issues.apache.org/jira/browse/CAMEL-10870)

camel-sql stored procedures don't support negative vendor-specific JDBC types

[CAMEL-10869](https://issues.apache.org/jira/browse/CAMEL-10869)

TRACE on ftp component reveals password

[CAMEL-10853](https://issues.apache.org/jira/browse/CAMEL-10853)

CsvDataFormat should be completed with 'CSVFormat.withTrim'

[CAMEL-10851](https://issues.apache.org/jira/browse/CAMEL-10851)

getBody(Class<T> type) on originalMessage returns null

[CAMEL-10840](https://issues.apache.org/jira/browse/CAMEL-10840)

CsvDataFormat.setRecordConverterRef not usable

[CAMEL-10813](https://issues.apache.org/jira/browse/CAMEL-10813)

Host address ignored when creating a Restlet Server

[CAMEL-10745](https://issues.apache.org/jira/browse/CAMEL-10745)

POJO @Produce @Consume does not work with multiple arguments anymore.

[CAMEL-10737](https://issues.apache.org/jira/browse/CAMEL-10737)

file component should support parent folder in tempFileName

[CAMEL-10714](https://issues.apache.org/jira/browse/CAMEL-10714)

Replace ByteArrayOutputStream in JettyContentExchange9 with OutputStreamBuilder

[CAMEL-10611](https://issues.apache.org/jira/browse/CAMEL-10611)

Align Aries namespace handlers to blueprint-core 1.7.x

### New Feature (1)

[CAMEL-5271](https://issues.apache.org/jira/browse/CAMEL-5271)

camel-snmp should provide a Producer for sending TRAPS/INFORMS

### Task (2)

[CAMEL-10824](https://issues.apache.org/jira/browse/CAMEL-10824)

Improve DefaultRuntimeProvider abstraction

[CAMEL-10758](https://issues.apache.org/jira/browse/CAMEL-10758)

camel-ahc - Upgrade to newer version

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).