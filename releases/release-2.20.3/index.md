# Apache camel 2.20.3 Release

## New and Noteworthy

This release is a minor update of the 2.20.x branch.

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
      <version>2.20.3</version>
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
      <version>2.20.3</version>
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
| [apache-camel-2.20.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.20.3/apache-camel-2.20.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.20.3/apache-camel-2.20.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.20.3/apache-camel-2.20.3-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.20.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.20.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (25)

[CAMEL-12364](https://issues.apache.org/jira/browse/CAMEL-12364)

ensure a SOAP 1.2 enabled camel-cxf consumer endpoint can handle SOAP 1.1 request correctly

[CAMEL-12359](https://issues.apache.org/jira/browse/CAMEL-12359)

withAdvice() + weaveById() failing for global onException() route definitions

[CAMEL-12355](https://issues.apache.org/jira/browse/CAMEL-12355)

simple - Body.ognl function should validate that OGNL starts with a dot

[CAMEL-12348](https://issues.apache.org/jira/browse/CAMEL-12348)

camel-core - Potential NPE in ExchangeHelper.isStreamCaching

[CAMEL-12342](https://issues.apache.org/jira/browse/CAMEL-12342)

Camel-weather: freegeoip.io has been moved to freegeoip.net

[CAMEL-12335](https://issues.apache.org/jira/browse/CAMEL-12335)

camel-sjms - Potential NPE in consumer

[CAMEL-12328](https://issues.apache.org/jira/browse/CAMEL-12328)

Headers getting lost after calling kubernetes-services API

[CAMEL-12292](https://issues.apache.org/jira/browse/CAMEL-12292)

SnsProducer/SqsProducer setting MessageAttributes with empty values which causes errors

[CAMEL-12291](https://issues.apache.org/jira/browse/CAMEL-12291)

Blueprint error: "name is already instanciated as null and cannot be removed"

[CAMEL-12289](https://issues.apache.org/jira/browse/CAMEL-12289)

URISyntaxException in AbstractSpanDecorator

[CAMEL-12284](https://issues.apache.org/jira/browse/CAMEL-12284)

camel-beanio - Set encoding option does not work

[CAMEL-12278](https://issues.apache.org/jira/browse/CAMEL-12278)

camel-jsonpath - Should allow to load jackson adapter in OSGi

[CAMEL-12256](https://issues.apache.org/jira/browse/CAMEL-12256)

AWS S3 Consumer does not return custom headers in S3 Headers

[CAMEL-12255](https://issues.apache.org/jira/browse/CAMEL-12255)

camel-swagger-java - Body parameter fails to output type

[CAMEL-12252](https://issues.apache.org/jira/browse/CAMEL-12252)

Dynamic setting the DESTINATION\_OVERRIDE\_URL doesn't work on CXFRS producer

[CAMEL-12232](https://issues.apache.org/jira/browse/CAMEL-12232)

aws-s3: Client is immutable when created with the builder

[CAMEL-12228](https://issues.apache.org/jira/browse/CAMEL-12228)

Print command fails in case of multiple copies

[CAMEL-12222](https://issues.apache.org/jira/browse/CAMEL-12222)

ResrSwaggerServlet removes last part of context root

[CAMEL-12196](https://issues.apache.org/jira/browse/CAMEL-12196)

Mock endpoint - message().body().matches().simple - Does not work

[CAMEL-12193](https://issues.apache.org/jira/browse/CAMEL-12193)

ThrowException DSL should support no-arg constructors

[CAMEL-12184](https://issues.apache.org/jira/browse/CAMEL-12184)

EventNotifierSupport does not receive ExchangeSentEvents anymore

[CAMEL-12181](https://issues.apache.org/jira/browse/CAMEL-12181)

XML Signature: '#' missing in ObjectReference attribute of XADES element DataObjectFormat

[CAMEL-12176](https://issues.apache.org/jira/browse/CAMEL-12176)

Camel-Dropbox /search and /get are not working

[CAMEL-11996](https://issues.apache.org/jira/browse/CAMEL-11996)

RabbitConsumer could hang when RabbitMQ connection is lost and autoAck=false.

[CAMEL-11977](https://issues.apache.org/jira/browse/CAMEL-11977)

MongoDB Tailable cursor consumer fails to stop on shutdown

### Improvement (8)

[CAMEL-12394](https://issues.apache.org/jira/browse/CAMEL-12394)

Camel Bindy: marshal doesn't quote headers

[CAMEL-12358](https://issues.apache.org/jira/browse/CAMEL-12358)

Camel-SMPP: Use timeout when creating socket connection

[CAMEL-12352](https://issues.apache.org/jira/browse/CAMEL-12352)

simple - Lookup env var should be case-insensitive

[CAMEL-12337](https://issues.apache.org/jira/browse/CAMEL-12337)

camel-ftp - ignoreFileNotFoundOrPermissionError not work when folder not found

[CAMEL-12305](https://issues.apache.org/jira/browse/CAMEL-12305)

IntrospectionSupport - Reduce DEBUG logging level

[CAMEL-12293](https://issues.apache.org/jira/browse/CAMEL-12293)

Avoid KeyAlreadyExistsException in ManagedTypeConverterRegistry.listTypeConverters()

[CAMEL-12251](https://issues.apache.org/jira/browse/CAMEL-12251)

Do not hide (so much) blueprint.container.ComponentDefinitionException

[CAMEL-12034](https://issues.apache.org/jira/browse/CAMEL-12034)

camel-elasticsearch5 - Search Operation: If Map or String is used in Message Body, "size" and "from" parameters are always ignored

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).