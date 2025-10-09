# Apache camel 2.20.4 Release

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
      <version>2.20.4</version>
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
      <version>2.20.4</version>
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
| [apache-camel-2.20.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.20.4/apache-camel-2.20.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.20.4/apache-camel-2.20.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.20.4/apache-camel-2.20.4-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.20.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.20.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (22)

[CAMEL-12659](https://issues.apache.org/jira/browse/CAMEL-12659)

MllpTcpServerConsumer logging failure to set HL7 headers even when setting HL7 headers is disabled

[CAMEL-12630](https://issues.apache.org/jira/browse/CAMEL-12630)

Better attachment handling in camel-mail component

[CAMEL-12606](https://issues.apache.org/jira/browse/CAMEL-12606)

regression in camel test blueprint behaviour

[CAMEL-12573](https://issues.apache.org/jira/browse/CAMEL-12573)

ClassCastException thrown KafkaSpanDecorator

[CAMEL-12550](https://issues.apache.org/jira/browse/CAMEL-12550)

Camel-Twilio: Karaf feature is not working

[CAMEL-12541](https://issues.apache.org/jira/browse/CAMEL-12541)

camel-cxfrs - rsClient does not work programmatically, only with XML

[CAMEL-12536](https://issues.apache.org/jira/browse/CAMEL-12536)

camel-google-mail: adding the camel component to a spring boot project leads to java.lang.NoSuchMethodError: javax.servlet.ServletContext.getClassLoader()Ljava/lang/ClassLoader;

[CAMEL-12532](https://issues.apache.org/jira/browse/CAMEL-12532)

Content Based Router in Java DSL may not resolve property placeholders in when predicates

[CAMEL-12506](https://issues.apache.org/jira/browse/CAMEL-12506)

SqsProducer doesn't support Boolean attributes

[CAMEL-12487](https://issues.apache.org/jira/browse/CAMEL-12487)

S3Producer must close the streams it opens

[CAMEL-12480](https://issues.apache.org/jira/browse/CAMEL-12480)

HttpOperationFailedException exposes password when using basic auth with user:password@host notation

[CAMEL-12475](https://issues.apache.org/jira/browse/CAMEL-12475)

Undertow consumer with http4 producer results in Undertow throwing NullPointerException

[CAMEL-12454](https://issues.apache.org/jira/browse/CAMEL-12454)

camel-kafka - AutoCommitEnabled=false should not auto commit

[CAMEL-12451](https://issues.apache.org/jira/browse/CAMEL-12451)

Memory leak: camel-cxf componet don't release UoW in case of using "robust" property

[CAMEL-12449](https://issues.apache.org/jira/browse/CAMEL-12449)

DefaultServiceLoadBalancer throws IndexOutOfBoundsException after applying ServiceFilter

[CAMEL-12441](https://issues.apache.org/jira/browse/CAMEL-12441)

MulticastProcessor doProcessParallel blocks indefinitly if exception occurs in it.next()

[CAMEL-12436](https://issues.apache.org/jira/browse/CAMEL-12436)

camel-undertow - should extract body message from PATCH request

[CAMEL-12425](https://issues.apache.org/jira/browse/CAMEL-12425)

SqsProducer doesn't support Number attributes

[CAMEL-12424](https://issues.apache.org/jira/browse/CAMEL-12424)

HTTPHelper.setCharsetFromContentType can't properly extract the charset if it isn't the last parameter

[CAMEL-12412](https://issues.apache.org/jira/browse/CAMEL-12412)

camel-jclouds - Fallback type converter is wrong

[CAMEL-12406](https://issues.apache.org/jira/browse/CAMEL-12406)

camel-dropbox - Need to use force to check for file/folder exists

[CAMEL-12395](https://issues.apache.org/jira/browse/CAMEL-12395)

HttpProducer cookie handling broken

### Improvement (5)

[CAMEL-12588](https://issues.apache.org/jira/browse/CAMEL-12588)

AggregateProcessor does not stop AggregateTimeoutChecker threads on stop call

[CAMEL-12507](https://issues.apache.org/jira/browse/CAMEL-12507)

SqsProducer support for Number custom data types

[CAMEL-12444](https://issues.apache.org/jira/browse/CAMEL-12444)

XML Validator - Improve DTD handling

[CAMEL-12439](https://issues.apache.org/jira/browse/CAMEL-12439)

FailedToCreateRouteException should mask sensitive information in uris

[CAMEL-12404](https://issues.apache.org/jira/browse/CAMEL-12404)

Upgrade jackson-databind minor version in Camel 2.20.x and 2.21.x

### New Feature (1)

[CAMEL-12360](https://issues.apache.org/jira/browse/CAMEL-12360)

Add logRetryAttemptedInterval to RedeliveryPolicy

### Task (1)

[CAMEL-12579](https://issues.apache.org/jira/browse/CAMEL-12579)

Disable Google Analytics phone home

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).