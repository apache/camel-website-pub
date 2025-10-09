# Apache camel 3.0.0 Release

## New and Noteworthy

This release is the new Camel 3.0.0 major release.

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
      <version>3.0.0</version>
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
      <version>3.0.0</version>
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
| [apache-camel-3.0.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.0.0/apache-camel-3.0.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.0.0/apache-camel-3.0.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.0.0/apache-camel-3.0.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.0.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.0.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (16)

[CAMEL-13942](https://issues.apache.org/jira/browse/CAMEL-13942)

camel-undertow - UnitOfWork should be done after send back response

[CAMEL-13941](https://issues.apache.org/jira/browse/CAMEL-13941)

NullPointerException when Conduit is null

[CAMEL-13931](https://issues.apache.org/jira/browse/CAMEL-13931)

camel-file - tempFileName directory is not auto-created if it is relative before the endpoint path

[CAMEL-13924](https://issues.apache.org/jira/browse/CAMEL-13924)

Camel-DirectVM: failIfNoConsumers option not taken into account when block is enabled

[CAMEL-13795](https://issues.apache.org/jira/browse/CAMEL-13795)

TokenXMLExpressionIterator with inheritNamespaceToken creates duplicate default namespace definition

[CAMEL-13776](https://issues.apache.org/jira/browse/CAMEL-13776)

\[MongoDB\] autoclosable cursor

[CAMEL-13770](https://issues.apache.org/jira/browse/CAMEL-13770)

Properties of class Map does not work with Spring Boot 2.x

[CAMEL-13750](https://issues.apache.org/jira/browse/CAMEL-13750)

Incoming JMSCorrelationID is passed along when useMessageIDAsCorrelationID

[CAMEL-13724](https://issues.apache.org/jira/browse/CAMEL-13724)

camel route customized id isn't correct if there are more than one Rest DSL route availble

[CAMEL-13718](https://issues.apache.org/jira/browse/CAMEL-13718)

Fix syntax for pulsar component

[CAMEL-13687](https://issues.apache.org/jira/browse/CAMEL-13687)

NotifyBuilder not working as expected

[CAMEL-13667](https://issues.apache.org/jira/browse/CAMEL-13667)

Windows network UNC paths not treated correctly (File2/tempPrefix)

[CAMEL-13642](https://issues.apache.org/jira/browse/CAMEL-13642)

Testing for an expected Header in a MockEndpoint doesnt happen if there is no Exchange received

[CAMEL-13466](https://issues.apache.org/jira/browse/CAMEL-13466)

DefaultCamelContext not stopping all routes on doStop()

[CAMEL-13424](https://issues.apache.org/jira/browse/CAMEL-13424)

Rest Component custom routeId is not accessible in processor

[CAMEL-12471](https://issues.apache.org/jira/browse/CAMEL-12471)

Dots in RabbitMQ-component headers do not work

### Improvement (3)

[CAMEL-13951](https://issues.apache.org/jira/browse/CAMEL-13951)

JdbcAggregationRepository doesn't work with PostgreSQL

[CAMEL-13697](https://issues.apache.org/jira/browse/CAMEL-13697)

URISupport - Mask accessToken and clientSecret in uri logging

[CAMEL-13696](https://issues.apache.org/jira/browse/CAMEL-13696)

Upgrade to slf4j ver 1.7.26

### New Feature (1)

[CAMEL-13898](https://issues.apache.org/jira/browse/CAMEL-13898)

ensure camel-cxf consumer can propagate protocol headers from camel exchange headers when throwing a soap fault

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).