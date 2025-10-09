# Apache camel 2.22.2 Release

## New and Noteworthy

This release is a minor update of the 2.22.x branch.

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
      <version>2.22.2</version>
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
      <version>2.22.2</version>
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
| [apache-camel-2.22.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.22.2/apache-camel-2.22.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.22.2/apache-camel-2.22.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.22.2/apache-camel-2.22.2-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.22.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.22.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (36)

[CAMEL-12882](https://issues.apache.org/jira/browse/CAMEL-12882)

Camel Jms headers missing if producer endpoint has transferExchange=true

[CAMEL-12880](https://issues.apache.org/jira/browse/CAMEL-12880)

Atom consumer stops polling

[CAMEL-12870](https://issues.apache.org/jira/browse/CAMEL-12870)

make cxf consumer endpoints suspendable

[CAMEL-12852](https://issues.apache.org/jira/browse/CAMEL-12852)

Fix unstable test PubNubPresenceTest

[CAMEL-12850](https://issues.apache.org/jira/browse/CAMEL-12850)

camel-ftp tries reconnects twice as much as maximumReconnectAttempts

[CAMEL-12844](https://issues.apache.org/jira/browse/CAMEL-12844)

splitter with grouping looses encoding property

[CAMEL-12843](https://issues.apache.org/jira/browse/CAMEL-12843)

CamelContext Start command shouldn't start a Suspended context

[CAMEL-12838](https://issues.apache.org/jira/browse/CAMEL-12838)

Camel Twitter Send Direct Message Endpoint not working

[CAMEL-12829](https://issues.apache.org/jira/browse/CAMEL-12829)

An autocreated CXF Bus not shut down in CxfSpringEndpoint

[CAMEL-12821](https://issues.apache.org/jira/browse/CAMEL-12821)

Fix MQTT URI param typo

[CAMEL-12805](https://issues.apache.org/jira/browse/CAMEL-12805)

camel-restdsl-swagger-plugin doesn't convert integer default value to string

[CAMEL-12787](https://issues.apache.org/jira/browse/CAMEL-12787)

Accept header is not respected anymore in CXFRS consumer when POST

[CAMEL-12786](https://issues.apache.org/jira/browse/CAMEL-12786)

Option readLockLoggingLevel not working for SFTP changed read lock strategy

[CAMEL-12785](https://issues.apache.org/jira/browse/CAMEL-12785)

ServletComponent ignores httpBinding option

[CAMEL-12779](https://issues.apache.org/jira/browse/CAMEL-12779)

camel-spring-redis - When stopping consumer it should stop the message listener

[CAMEL-12775](https://issues.apache.org/jira/browse/CAMEL-12775)

Using StubComponent can block routes depending on MEP

[CAMEL-12769](https://issues.apache.org/jira/browse/CAMEL-12769)

Combination of File consumer with charset and Split DSL with XPath doesn't parse XML correctly

[CAMEL-12762](https://issues.apache.org/jira/browse/CAMEL-12762)

camel-sjms - MessageProducer is not closed when using shared session

[CAMEL-12758](https://issues.apache.org/jira/browse/CAMEL-12758)

SOAP request causing null namespace URI in SimpleNsStreamWriter camel-cxf/woodstox

[CAMEL-12746](https://issues.apache.org/jira/browse/CAMEL-12746)

Temporary reply queues being created with main endpoint autoAck setting

[CAMEL-12740](https://issues.apache.org/jira/browse/CAMEL-12740)

Olingo4Component creates and ignores HttpAsyncClientBuilder

[CAMEL-12725](https://issues.apache.org/jira/browse/CAMEL-12725)

\[ERROR\] /sobject-pojo-optional.vm: Encountered "(" at line 64, column 8.

[CAMEL-12724](https://issues.apache.org/jira/browse/CAMEL-12724)

Simple SFTP-to-File integration with charset options fails

[CAMEL-12720](https://issues.apache.org/jira/browse/CAMEL-12720)

Krati implementation does not work properly persistence after put operation.

[CAMEL-12713](https://issues.apache.org/jira/browse/CAMEL-12713)

relative paths can remove scheme from xslt URI

[CAMEL-12709](https://issues.apache.org/jira/browse/CAMEL-12709)

UseOriginalAggregationStrategy in outer loops

[CAMEL-12685](https://issues.apache.org/jira/browse/CAMEL-12685)

relative references for nested xslt inclusions don't get resolved

[CAMEL-12681](https://issues.apache.org/jira/browse/CAMEL-12681)

BreadcrumbId not required for aws-sqs aws-sns endpoints

[CAMEL-12656](https://issues.apache.org/jira/browse/CAMEL-12656)

camel-zipkin - Root Span Id is not reported if the route calls multiple route

[CAMEL-12654](https://issues.apache.org/jira/browse/CAMEL-12654)

RabbitMQ Headers - Headers with null value are skipped.

[CAMEL-12638](https://issues.apache.org/jira/browse/CAMEL-12638)

DefaultFluentProducerTemplate is not thread safe

[CAMEL-12575](https://issues.apache.org/jira/browse/CAMEL-12575)

camel-cxfrs: NPE on GET request with Content-Type header

[CAMEL-12565](https://issues.apache.org/jira/browse/CAMEL-12565)

outputTypeWithValidate (or inputTypeWithValidate) + validator()... doesn't work as expected

[CAMEL-12484](https://issues.apache.org/jira/browse/CAMEL-12484)

Camel-salesforce component does not try to reconnect on specific error

[CAMEL-12410](https://issues.apache.org/jira/browse/CAMEL-12410)

No type converter from java.lang.String to java.math.BigInteger required for firstIndex

[CAMEL-12087](https://issues.apache.org/jira/browse/CAMEL-12087)

camel-core: WARN No CamelContext defined yet so cannot inject into bean

### Improvement (2)

[CAMEL-12691](https://issues.apache.org/jira/browse/CAMEL-12691)

Allow configuration of org.xml.sax.ErrorHandler on DocumentBuilders used in Camel

[CAMEL-12653](https://issues.apache.org/jira/browse/CAMEL-12653)

JaxbDataFormat.unmarshal should use passed Exchange when converting given InputStream into XMLStreamReader

### New Feature (1)

[CAMEL-12651](https://issues.apache.org/jira/browse/CAMEL-12651)

Allow to override serializing and deserializing default mechanism for kafka headers

### Task (2)

[CAMEL-12754](https://issues.apache.org/jira/browse/CAMEL-12754)

Upgrade Apache Ignite

[CAMEL-12658](https://issues.apache.org/jira/browse/CAMEL-12658)

camel-weather: Freegeoip service is no longer avaiable, we need to switch to apilayer IPstack

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).