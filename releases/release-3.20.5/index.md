# Apache camel 3.20.5 Release

## New and Noteworthy

This release is the new Camel 3.20.5 LTS patch release.

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
      <version>3.20.5</version>
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
      <version>3.20.5</version>
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
| [apache-camel-3.20.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.20.5/apache-camel-3.20.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.5/apache-camel-3.20.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.5/apache-camel-3.20.5-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.20.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.20.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (11)

[CAMEL-19371](https://issues.apache.org/jira/browse/CAMEL-19371)

RedeliveryErrorHandler's suppressed exceptions cause memory leak and logging issue

[CAMEL-19345](https://issues.apache.org/jira/browse/CAMEL-19345)

KameletDiscoveryTest fails to find routeTemplate

[CAMEL-19342](https://issues.apache.org/jira/browse/CAMEL-19342)

Rest Inline Routes mixed with direct routes.

[CAMEL-19339](https://issues.apache.org/jira/browse/CAMEL-19339)

karaf - ConnectionFactory not found when use camel-activemq

[CAMEL-19314](https://issues.apache.org/jira/browse/CAMEL-19314)

camel-aws - Connection pool shutdown when aws health checks are used

[CAMEL-19298](https://issues.apache.org/jira/browse/CAMEL-19298)

Snmp: version 3 is not supported for several actions for the component

[CAMEL-19296](https://issues.apache.org/jira/browse/CAMEL-19296)

Unable to init camel file with JBang for multi dot file name suffix - eg 'foo.camel.xml'

[CAMEL-19293](https://issues.apache.org/jira/browse/CAMEL-19293)

camel-spring-ldap - base is set twice when using SB AutoConfiguration

[CAMEL-19281](https://issues.apache.org/jira/browse/CAMEL-19281)

Aws2- healthchecks not closing resources for awsClient

[CAMEL-19095](https://issues.apache.org/jira/browse/CAMEL-19095)

Camel Karaf using buggy Saxon bundle with wrong imports

[CAMEL-18985](https://issues.apache.org/jira/browse/CAMEL-18985)

camel-kafka: messages are getting lost with "breakOnFirstError"

### Dependency upgrade (3)

[CAMEL-19372](https://issues.apache.org/jira/browse/CAMEL-19372)

camel-spring-boot - Upgrade to 2.7.12

[CAMEL-19351](https://issues.apache.org/jira/browse/CAMEL-19351)

camel-jackson - Upgrade to 2.14.3

[CAMEL-19301](https://issues.apache.org/jira/browse/CAMEL-19301)

camel-jbang - Upgrade to hawtio 2.17.2

### Improvement (14)

[CAMEL-19370](https://issues.apache.org/jira/browse/CAMEL-19370)

camel-jbang - Make it possible to show full url for very long endpoints

[CAMEL-19366](https://issues.apache.org/jira/browse/CAMEL-19366)

camel-core - Trigger reload via dev console make it async

[CAMEL-19361](https://issues.apache.org/jira/browse/CAMEL-19361)

camel-jbang - Parse trait.camel.apache.org/camel.properties from KameletBinding

[CAMEL-19360](https://issues.apache.org/jira/browse/CAMEL-19360)

camel-jbang - Export a set of files

[CAMEL-19357](https://issues.apache.org/jira/browse/CAMEL-19357)

camel-jbang - Use a vertx task for tasks to avoid blocking io thread

[CAMEL-19352](https://issues.apache.org/jira/browse/CAMEL-19352)

Improve camel-mybatis documentation

[CAMEL-19333](https://issues.apache.org/jira/browse/CAMEL-19333)

ensure cxf springboot autoconfiguration works OOTB in camel-cxf springboot starters

[CAMEL-19326](https://issues.apache.org/jira/browse/CAMEL-19326)

camel-jbang - Register reload services eager

[CAMEL-19324](https://issues.apache.org/jira/browse/CAMEL-19324)

Be able to convert all elements from CXF MessageContentsList.class to String.class if not in "CXF Context"

[CAMEL-19322](https://issues.apache.org/jira/browse/CAMEL-19322)

camel-jbang - Source Dir to support application.properties

[CAMEL-19313](https://issues.apache.org/jira/browse/CAMEL-19313)

camel-jbang - Provide a way to append Maven repository provided from command-line to the one provided in configuration

[CAMEL-19306](https://issues.apache.org/jira/browse/CAMEL-19306)

camel-jbang - Allow to load yaml files with beans only

[CAMEL-19302](https://issues.apache.org/jira/browse/CAMEL-19302)

Use filename to generate id of route when creating Camel file in XML DSL with Camel JBang

[CAMEL-17652](https://issues.apache.org/jira/browse/CAMEL-17652)

camel-minio - Auto create bucket should not be done in endpoint

### New Feature (5)

[CAMEL-19344](https://issues.apache.org/jira/browse/CAMEL-19344)

camel-jbang - Reload to source dir via http

[CAMEL-19320](https://issues.apache.org/jira/browse/CAMEL-19320)

camel-jbang - Add command to reload

[CAMEL-19309](https://issues.apache.org/jira/browse/CAMEL-19309)

camel-jbang - Run with empty folder

[CAMEL-19299](https://issues.apache.org/jira/browse/CAMEL-19299)

camel-console - Add dev console for bean registry

[CAMEL-19099](https://issues.apache.org/jira/browse/CAMEL-19099)

Camel-Jbang Export: Add a flag to include secret refresh properties in application.properties

### Task (2)

[CAMEL-19328](https://issues.apache.org/jira/browse/CAMEL-19328)

CamelAwsSesTo and CamelAwsSesReplyToAddresses update documentation with String instead of List

[CAMEL-19294](https://issues.apache.org/jira/browse/CAMEL-19294)

camel-test-infra-zookeeper: unable to use a custom Zookeeper container

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).