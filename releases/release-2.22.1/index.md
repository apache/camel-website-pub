# Apache camel 2.22.1 Release

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
      <version>2.22.1</version>
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
      <version>2.22.1</version>
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
| [apache-camel-2.22.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.22.1/apache-camel-2.22.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.22.1/apache-camel-2.22.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.22.1/apache-camel-2.22.1-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.22.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.22.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (33)

[CAMEL-12762](https://issues.apache.org/jira/browse/CAMEL-12762)

camel-sjms - MessageProducer is not closed when using shared session

[CAMEL-12746](https://issues.apache.org/jira/browse/CAMEL-12746)

Temporary reply queues being created with main endpoint autoAck setting

[CAMEL-12740](https://issues.apache.org/jira/browse/CAMEL-12740)

Olingo4Component creates and ignores HttpAsyncClientBuilder

[CAMEL-12732](https://issues.apache.org/jira/browse/CAMEL-12732)

Kafka manual commit to file repository doesn't work properly (using Spring boot)

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

[CAMEL-12705](https://issues.apache.org/jira/browse/CAMEL-12705)

Optimising toD via SendDynamicAware component removes the 3rd octet from IP address

[CAMEL-12701](https://issues.apache.org/jira/browse/CAMEL-12701)

servicenow: meta data serivce ignores tables without parent when retrieving table list

[CAMEL-12685](https://issues.apache.org/jira/browse/CAMEL-12685)

relative references for nested xslt inclusions don't get resolved

[CAMEL-12681](https://issues.apache.org/jira/browse/CAMEL-12681)

BreadcrumbId not required for aws-sqs aws-sns endpoints

[CAMEL-12680](https://issues.apache.org/jira/browse/CAMEL-12680)

Fix syntax for micrometer endpoint

[CAMEL-12659](https://issues.apache.org/jira/browse/CAMEL-12659)

MllpTcpServerConsumer logging failure to set HL7 headers even when setting HL7 headers is disabled

[CAMEL-12656](https://issues.apache.org/jira/browse/CAMEL-12656)

camel-zipkin - Root Span Id is not reported if the route calls multiple route

[CAMEL-12654](https://issues.apache.org/jira/browse/CAMEL-12654)

RabbitMQ Headers - Headers with null value are skipped.

[CAMEL-12647](https://issues.apache.org/jira/browse/CAMEL-12647)

Problem in setting region for camel AWS-SQS endpoint

[CAMEL-12638](https://issues.apache.org/jira/browse/CAMEL-12638)

DefaultFluentProducerTemplate is not thread safe

[CAMEL-12637](https://issues.apache.org/jira/browse/CAMEL-12637)

XmlConverter can't transform StAXSource when external xalan lib available

[CAMEL-12635](https://issues.apache.org/jira/browse/CAMEL-12635)

Potential NPE in CamelEndpointDetails.hashCode method

[CAMEL-12630](https://issues.apache.org/jira/browse/CAMEL-12630)

Better attachment handling in camel-mail component

[CAMEL-12624](https://issues.apache.org/jira/browse/CAMEL-12624)

ActiveMQ Artemis AMQP integration issue with topic prefix hardcode

[CAMEL-12621](https://issues.apache.org/jira/browse/CAMEL-12621)

Rest DSL with Jetty9|netty4-http components returns 404 instead of 405, when http method is not supported

[CAMEL-12613](https://issues.apache.org/jira/browse/CAMEL-12613)

Camel file endpoint loses modification date and length information when preMove is used

[CAMEL-12607](https://issues.apache.org/jira/browse/CAMEL-12607)

When using Tokenizer skipFirst - java.util.NoSuchElementException if only one element

[CAMEL-12603](https://issues.apache.org/jira/browse/CAMEL-12603)

Thread stuck in re-delivery loop after interrupting it

[CAMEL-12594](https://issues.apache.org/jira/browse/CAMEL-12594)

Rest Producer - Query Parameters : Wrong query parameter name is used when header substitution is performed

[CAMEL-12589](https://issues.apache.org/jira/browse/CAMEL-12589)

Surviving Header AGGREGATION\_COMPLETE\_ALL\_GROUPS\_INCLUSIVE affects following aggregations

[CAMEL-12575](https://issues.apache.org/jira/browse/CAMEL-12575)

camel-cxfrs: NPE on GET request with Content-Type header

[CAMEL-12565](https://issues.apache.org/jira/browse/CAMEL-12565)

outputTypeWithValidate (or inputTypeWithValidate) + validator()... doesn't work as expected

[CAMEL-12525](https://issues.apache.org/jira/browse/CAMEL-12525)

camel-kafka component commits the offset as soon as it is retrieved

[CAMEL-12410](https://issues.apache.org/jira/browse/CAMEL-12410)

No type converter from java.lang.String to java.math.BigInteger required for firstIndex

### Improvement (8)

[CAMEL-12735](https://issues.apache.org/jira/browse/CAMEL-12735)

XmlRouteParser does not handle usage of xml namespace prefix for camel

[CAMEL-12707](https://issues.apache.org/jira/browse/CAMEL-12707)

Docker integration test profiles should respect the skipTests property

[CAMEL-12697](https://issues.apache.org/jira/browse/CAMEL-12697)

Add hapi-structures-v21 to camel-parent

[CAMEL-12692](https://issues.apache.org/jira/browse/CAMEL-12692)

Add camel-as2 to camel-parent POM

[CAMEL-12691](https://issues.apache.org/jira/browse/CAMEL-12691)

Allow configuration of org.xml.sax.ErrorHandler on DocumentBuilders used in Camel

[CAMEL-12653](https://issues.apache.org/jira/browse/CAMEL-12653)

JaxbDataFormat.unmarshal should use passed Exchange when converting given InputStream into XMLStreamReader

[CAMEL-12639](https://issues.apache.org/jira/browse/CAMEL-12639)

tooling - Provide line numbers for CamelEndpointDetails for java dsl

[CAMEL-12587](https://issues.apache.org/jira/browse/CAMEL-12587)

camel-zipkin-starter fails mapping service names

### New Feature (1)

[CAMEL-12651](https://issues.apache.org/jira/browse/CAMEL-12651)

Allow to override serializing and deserializing default mechanism for kafka headers

### Task (4)

[CAMEL-12754](https://issues.apache.org/jira/browse/CAMEL-12754)

Upgrade Apache Ignite

[CAMEL-12658](https://issues.apache.org/jira/browse/CAMEL-12658)

camel-weather: Freegeoip service is no longer avaiable, we need to switch to apilayer IPstack

[CAMEL-12632](https://issues.apache.org/jira/browse/CAMEL-12632)

Pass CXF service class to EndpointInfo

[CAMEL-12586](https://issues.apache.org/jira/browse/CAMEL-12586)

Use consistant Surefire and JAXB version

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).