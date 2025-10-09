# Apache camel 3.11.2 Release

## New and Noteworthy

This release is the new Camel 3.11.2 LTS patch release.

## Supported Java version

This version supports Java 8 and 11.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.11.2</version>
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
      <version>3.11.2</version>
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
| [apache-camel-3.11.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.11.2/apache-camel-3.11.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.11.2/apache-camel-3.11.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.11.2/apache-camel-3.11.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.11.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.11.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (19)

[CAMEL-16923](https://issues.apache.org/jira/browse/CAMEL-16923)

Specifying OpenAPI license & contact info causes a NullPointerException

[CAMEL-16922](https://issues.apache.org/jira/browse/CAMEL-16922)

StringHelper.removeLeadingAndEndingQuotes() may cause IndexOutOfBoundsException

[CAMEL-16921](https://issues.apache.org/jira/browse/CAMEL-16921)

KafkaSpanDecorator sometimes sets the wrong message\_bus.destination tag value

[CAMEL-16920](https://issues.apache.org/jira/browse/CAMEL-16920)

Dump routes does not show uri with endpointdsl

[CAMEL-16918](https://issues.apache.org/jira/browse/CAMEL-16918)

Datasonnet expression fails on first runs in a route called in multicast

[CAMEL-16917](https://issues.apache.org/jira/browse/CAMEL-16917)

more general way to determine if a Spring ApplicationContext is self management ApplicationContext

[CAMEL-16904](https://issues.apache.org/jira/browse/CAMEL-16904)

Camel Swagger API response message headers of type string generate an empty enum even when allowableValues are not specified.

[CAMEL-16902](https://issues.apache.org/jira/browse/CAMEL-16902)

camel-core - WireTap should preserve OUT message when copying

[CAMEL-16893](https://issues.apache.org/jira/browse/CAMEL-16893)

Potential NPE in GrpcStreamingExchangeForwarder

[CAMEL-16878](https://issues.apache.org/jira/browse/CAMEL-16878)

using breadcrumbs can cause ClassCastException in MailBinding

[CAMEL-16874](https://issues.apache.org/jira/browse/CAMEL-16874)

PollEnrich with file and option sendEmptyMessageWhenIdle keeps sending empty messages

[CAMEL-16865](https://issues.apache.org/jira/browse/CAMEL-16865)

Xtokenize does not track a level up again once it detects a non matching namespace

[CAMEL-16857](https://issues.apache.org/jira/browse/CAMEL-16857)

breakOnFirstError causes thread and memory leaks in camel-kafka

[CAMEL-16853](https://issues.apache.org/jira/browse/CAMEL-16853)

camel-xslt: setting resultHandlerFactory via URI is broken

[CAMEL-16850](https://issues.apache.org/jira/browse/CAMEL-16850)

camel-main - Unable to reference properties after bootstrap

[CAMEL-16843](https://issues.apache.org/jira/browse/CAMEL-16843)

camel-kubernetes: NULL watcher is causing a NPE when stopping the sub-component consumers

[CAMEL-16841](https://issues.apache.org/jira/browse/CAMEL-16841)

camel-kubernetes: NULL watcher is causing a NPE when stopping the configmaps component

[CAMEL-16832](https://issues.apache.org/jira/browse/CAMEL-16832)

camel-kafka - file descriptor leak

[CAMEL-16793](https://issues.apache.org/jira/browse/CAMEL-16793)

apiHost option in REST DSL is ignored

### Dependency upgrade (4)

[CAMEL-16919](https://issues.apache.org/jira/browse/CAMEL-16919)

Upgrade to spring boot 2.5.4

[CAMEL-16910](https://issues.apache.org/jira/browse/CAMEL-16910)

Update Commons Compress to 1.21

[CAMEL-16872](https://issues.apache.org/jira/browse/CAMEL-16872)

Upgrade xchange to 5.0.11

[CAMEL-16856](https://issues.apache.org/jira/browse/CAMEL-16856)

camel-karaf - Add azure-blob-changefeed bundle to the camel-azure-blob-storage feature

### Improvement (1)

[CAMEL-16873](https://issues.apache.org/jira/browse/CAMEL-16873)

Route template parameter are not replaced when dumpRoutesAsXML

### Task (2)

[CAMEL-16935](https://issues.apache.org/jira/browse/CAMEL-16935)

camel-main and camel-base-engine both exports org.apache.camel.main package

[CAMEL-16838](https://issues.apache.org/jira/browse/CAMEL-16838)

camel-kubernetes: configmap documentation refers to invalid query parameters

### Test (2)

[CAMEL-16939](https://issues.apache.org/jira/browse/CAMEL-16939)

XPathTransformTest only check JDK ea version when it's 16-ea

[CAMEL-16886](https://issues.apache.org/jira/browse/CAMEL-16886)

NewCommentsConsumerTest#singleIssueCommentsTest fails intermitently

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).