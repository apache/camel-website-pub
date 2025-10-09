# Apache camel 2.21.1 Release

## New and Noteworthy

This release is a minor update of the 2.21.x branch.

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
      <version>2.21.1</version>
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
      <version>2.21.1</version>
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
| [apache-camel-2.21.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.21.1/apache-camel-2.21.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.21.1/apache-camel-2.21.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.21.1/apache-camel-2.21.1-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.21.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.21.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (31)

[CAMEL-15026](https://issues.apache.org/jira/browse/CAMEL-15026)

Camel throws exception on HHTP response Content-Type header with additional info

[CAMEL-12465](https://issues.apache.org/jira/browse/CAMEL-12465)

Don't carry soapAction forward if operationName is specified explicitly for the CxfProducer

[CAMEL-12457](https://issues.apache.org/jira/browse/CAMEL-12457)

file consumer - Should not use readlock by default

[CAMEL-12454](https://issues.apache.org/jira/browse/CAMEL-12454)

camel-kafka - AutoCommitEnabled=false should not auto commit

[CAMEL-12451](https://issues.apache.org/jira/browse/CAMEL-12451)

Memory leak: camel-cxf componet don't release UoW in case of using "robust" property

[CAMEL-12449](https://issues.apache.org/jira/browse/CAMEL-12449)

DefaultServiceLoadBalancer throws IndexOutOfBoundsException after applying ServiceFilter

[CAMEL-12448](https://issues.apache.org/jira/browse/CAMEL-12448)

camel-consul - service health state calculated from all services with same name

[CAMEL-12445](https://issues.apache.org/jira/browse/CAMEL-12445)

spring-boot-rest-swagger example does not compile due to missing servlet-api dependendency

[CAMEL-12441](https://issues.apache.org/jira/browse/CAMEL-12441)

MulticastProcessor doProcessParallel blocks indefinitly if exception occurs in it.next()

[CAMEL-12436](https://issues.apache.org/jira/browse/CAMEL-12436)

camel-undertow - should extract body message from PATCH request

[CAMEL-12435](https://issues.apache.org/jira/browse/CAMEL-12435)

camel-netty4 - Shared connection pool should re-create connection if its no longer valid

[CAMEL-12425](https://issues.apache.org/jira/browse/CAMEL-12425)

SqsProducer doesn't support Number attributes

[CAMEL-12424](https://issues.apache.org/jira/browse/CAMEL-12424)

HTTPHelper.setCharsetFromContentType can't properly extract the charset if it isn't the last parameter

[CAMEL-12422](https://issues.apache.org/jira/browse/CAMEL-12422)

Wrong language syntax declarations for code samples in documentation

[CAMEL-12418](https://issues.apache.org/jira/browse/CAMEL-12418)

camel-consul - High CPU load on events watching

[CAMEL-12415](https://issues.apache.org/jira/browse/CAMEL-12415)

Camel-jaxb option "encoding" with option "filterNonXmlChars" generate wrong data

[CAMEL-12412](https://issues.apache.org/jira/browse/CAMEL-12412)

camel-jclouds - Fallback type converter is wrong

[CAMEL-12407](https://issues.apache.org/jira/browse/CAMEL-12407)

camel-olingo4-api should explicitly depend on commons-io

[CAMEL-12406](https://issues.apache.org/jira/browse/CAMEL-12406)

camel-dropbox - Need to use force to check for file/folder exists

[CAMEL-12399](https://issues.apache.org/jira/browse/CAMEL-12399)

CxfRsProducer doesn't configure CxfRsEndpointConfigurer while using the Proxy API

[CAMEL-12395](https://issues.apache.org/jira/browse/CAMEL-12395)

HttpProducer cookie handling broken

[CAMEL-12384](https://issues.apache.org/jira/browse/CAMEL-12384)

camel-influxdb Query

[CAMEL-12379](https://issues.apache.org/jira/browse/CAMEL-12379)

Shutdown only AWS clients owned by the context

[CAMEL-12370](https://issues.apache.org/jira/browse/CAMEL-12370)

Camel-SFTP: errors in SSH routes after changes in read-lock

[CAMEL-12364](https://issues.apache.org/jira/browse/CAMEL-12364)

ensure a SOAP 1.2 enabled camel-cxf consumer endpoint can handle SOAP 1.1 request correctly

[CAMEL-12356](https://issues.apache.org/jira/browse/CAMEL-12356)

Claim Check EPI: ManagedManagementStrategy: Can not register service: ClaimCheck\[\*\] as Service MBean

[CAMEL-12355](https://issues.apache.org/jira/browse/CAMEL-12355)

simple - Body.ognl function should validate that OGNL starts with a dot

[CAMEL-12348](https://issues.apache.org/jira/browse/CAMEL-12348)

camel-core - Potential NPE in ExchangeHelper.isStreamCaching

[CAMEL-12345](https://issues.apache.org/jira/browse/CAMEL-12345)

LinkedIn component throws IllegalArgumentException on API requests

[CAMEL-12325](https://issues.apache.org/jira/browse/CAMEL-12325)

lastConnectionActivityTicks is not getting updated by MllpTcpClientProducer

[CAMEL-12252](https://issues.apache.org/jira/browse/CAMEL-12252)

Dynamic setting the DESTINATION\_OVERRIDE\_URL doesn't work on CXFRS producer

### Improvement (14)

[CAMEL-12458](https://issues.apache.org/jira/browse/CAMEL-12458)

camel-twitter - Should support extended mode by default

[CAMEL-12446](https://issues.apache.org/jira/browse/CAMEL-12446)

Splitter - Make it easier to turn off propgate exception

[CAMEL-12444](https://issues.apache.org/jira/browse/CAMEL-12444)

XML Validator - Improve DTD handling

[CAMEL-12439](https://issues.apache.org/jira/browse/CAMEL-12439)

FailedToCreateRouteException should mask sensitive information in uris

[CAMEL-12438](https://issues.apache.org/jira/browse/CAMEL-12438)

camel-netty4 - Add timeout support for SPI correlation manager

[CAMEL-12429](https://issues.apache.org/jira/browse/CAMEL-12429)

Avoid restlet response header warnings by using Restlet HeaderUtils

[CAMEL-12427](https://issues.apache.org/jira/browse/CAMEL-12427)

camel-netty4 - Add SPI to plugin custom correlation state for request/reply in producer

[CAMEL-12419](https://issues.apache.org/jira/browse/CAMEL-12419)

camel-elasticsearch-rest should return complete bulk response instead of just ids

[CAMEL-12394](https://issues.apache.org/jira/browse/CAMEL-12394)

Camel Bindy: marshal doesn't quote headers

[CAMEL-12393](https://issues.apache.org/jira/browse/CAMEL-12393)

Add karaf feature for camel-lra

[CAMEL-12358](https://issues.apache.org/jira/browse/CAMEL-12358)

Camel-SMPP: Use timeout when creating socket connection

[CAMEL-12357](https://issues.apache.org/jira/browse/CAMEL-12357)

Unexpected change in JSON formatting due to CAMEL-11970

[CAMEL-12352](https://issues.apache.org/jira/browse/CAMEL-12352)

simple - Lookup env var should be case-insensitive

[CAMEL-12337](https://issues.apache.org/jira/browse/CAMEL-12337)

camel-ftp - ignoreFileNotFoundOrPermissionError not work when folder not found

### Task (3)

[CAMEL-12468](https://issues.apache.org/jira/browse/CAMEL-12468)

Add dependency-management entry for camel-azure-starter

[CAMEL-12447](https://issues.apache.org/jira/browse/CAMEL-12447)

camel-jms - Exclude spring-messaging JAR

[CAMEL-12431](https://issues.apache.org/jira/browse/CAMEL-12431)

Upgrade to spring boot 1.5.12

### Wish (1)

[CAMEL-12274](https://issues.apache.org/jira/browse/CAMEL-12274)

Bindy - Unescape double quotes inside CSV field

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).