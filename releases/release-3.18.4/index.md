# Apache camel 3.18.4 Release

## New and Noteworthy

This release is the new Camel 3.18.4 LTS patch release.

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
      <version>3.18.4</version>
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
      <version>3.18.4</version>
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
| [apache-camel-3.18.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.18.4/apache-camel-3.18.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.18.4/apache-camel-3.18.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.18.4/apache-camel-3.18.4-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.18.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.18.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (15)

[CAMEL-18755](https://issues.apache.org/jira/browse/CAMEL-18755)

camel-yaml-dsl - Intercept is not added in the route definition.

[CAMEL-18753](https://issues.apache.org/jira/browse/CAMEL-18753)

camel-yaml-dsl - OnCompletion is not added in the route definition.

[CAMEL-18736](https://issues.apache.org/jira/browse/CAMEL-18736)

Duplicate schema/cxfEndpoint.xsd resource in camel-cxf-spring-rest and camel-cxf-spring-soap jars

[CAMEL-18730](https://issues.apache.org/jira/browse/CAMEL-18730)

camel-report-maven-plugin - Class missing when generating the route coverage report

[CAMEL-18722](https://issues.apache.org/jira/browse/CAMEL-18722)

Camel AWS2 S3 doesn't handle metadata correctly

[CAMEL-18717](https://issues.apache.org/jira/browse/CAMEL-18717)

camel-kafka: investigate offset not increasing

[CAMEL-18711](https://issues.apache.org/jira/browse/CAMEL-18711)

OpenAPI Schema references not generating correctly

[CAMEL-18690](https://issues.apache.org/jira/browse/CAMEL-18690)

camel-jbang generates package name with special symbols

[CAMEL-18676](https://issues.apache.org/jira/browse/CAMEL-18676)

Camel-Jbang does not add camel-openapi-java component when required

[CAMEL-18657](https://issues.apache.org/jira/browse/CAMEL-18657)

camel-jbang - Loading dynamic JARs should load EndpointUriFactory

[CAMEL-18656](https://issues.apache.org/jira/browse/CAMEL-18656)

Camel-git always merge at master branch

[CAMEL-18642](https://issues.apache.org/jira/browse/CAMEL-18642)

camel-jbang change class packag when export

[CAMEL-18614](https://issues.apache.org/jira/browse/CAMEL-18614)

Getting Route for a RouteConfiguration is null when doing manual route loading

[CAMEL-18447](https://issues.apache.org/jira/browse/CAMEL-18447)

Camel-pubsub: com.google.api.gax.rpc.AsyncTaskException: Asynchronous task failed with real account

[CAMEL-18255](https://issues.apache.org/jira/browse/CAMEL-18255)

Memory Leak with MDCUnitOfWork

### Dependency upgrade (2)

[CAMEL-18758](https://issues.apache.org/jira/browse/CAMEL-18758)

camel-spring-boot - Upgrade to 2.7.6

[CAMEL-18644](https://issues.apache.org/jira/browse/CAMEL-18644)

Camel - Upgrade hsqldb 2.7.1

### Improvement (5)

[CAMEL-18761](https://issues.apache.org/jira/browse/CAMEL-18761)

camel-open-api - Warning log when using boolean type.

[CAMEL-18702](https://issues.apache.org/jira/browse/CAMEL-18702)

camel-mail-microsoft-oauth: Add a Spring Boot starter

[CAMEL-18696](https://issues.apache.org/jira/browse/CAMEL-18696)

camel-ldap - Make filter a bit easier to use

[CAMEL-18684](https://issues.apache.org/jira/browse/CAMEL-18684)

Add Microsoft Exchange Online OAuth2 Mail Authenticator

[CAMEL-18669](https://issues.apache.org/jira/browse/CAMEL-18669)

camel-jbang - Using resilience4j as CB should include include dependency

### Task (4)

[CAMEL-18746](https://issues.apache.org/jira/browse/CAMEL-18746)

camel-spring-boot 3.18.3 release missing debezium-db2-starter / debezium-oracle-starter

[CAMEL-18672](https://issues.apache.org/jira/browse/CAMEL-18672)

\[DOCS\] Dataset component - incorrect link

[CAMEL-18671](https://issues.apache.org/jira/browse/CAMEL-18671)

\[DOCS\] Dataset component - unclear parameter description

[CAMEL-18670](https://issues.apache.org/jira/browse/CAMEL-18670)

\[DOCS\] Dataset component - unclear parameter name

### Test (1)

[CAMEL-18729](https://issues.apache.org/jira/browse/CAMEL-18729)

add more tests for camel-cxf-soap-starter

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).