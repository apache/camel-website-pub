# Apache camel 4.4.1 Release

## New and Noteworthy

This release is the new Camel 4.4.1 LTS patch release.

## Supported Java version

This version supports Java 17 and 21.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.4.1</version>
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
      <version>4.4.1</version>
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
| [apache-camel-4.4.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.4.1/apache-camel-4.4.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.1/apache-camel-4.4.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.1/apache-camel-4.4.1-src.zip.sha512) |
| [apache-camel-4.4.1-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.4.1/apache-camel-4.4.1-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.1/apache-camel-4.4.1-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.1/apache-camel-4.4.1-sbom.xml.sha512) |
| [apache-camel-4.4.1-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.4.1/apache-camel-4.4.1-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.1/apache-camel-4.4.1-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.1/apache-camel-4.4.1-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.4.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.4.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (17)

[CAMEL-20542](https://issues.apache.org/jira/browse/CAMEL-20542)

camel-spring-boot - Using Duration as option may fail

[CAMEL-20530](https://issues.apache.org/jira/browse/CAMEL-20530)

camel-mongodb: unable to convert InputStream to org.bson.conversions.Bson

[CAMEL-20523](https://issues.apache.org/jira/browse/CAMEL-20523)

camel-xpath - The resultQName converter is wrong causing CSB not to work with xpath in language endpoint

[CAMEL-20498](https://issues.apache.org/jira/browse/CAMEL-20498)

camel-http OAuth2 support is not adding the text "Bearer " to the Authorization header

[CAMEL-20483](https://issues.apache.org/jira/browse/CAMEL-20483)

camel-core - Rest DSL with api-context-path may append null in host name

[CAMEL-20481](https://issues.apache.org/jira/browse/CAMEL-20481)

camel-core - Rest DSL should resolve placeholder for context-path and others

[CAMEL-20475](https://issues.apache.org/jira/browse/CAMEL-20475)

camel-bindy - Handle values with quotes better

[CAMEL-20470](https://issues.apache.org/jira/browse/CAMEL-20470)

camel-jbang - Rest dsl with /api context path should auto detect platform-http as consumer

[CAMEL-20457](https://issues.apache.org/jira/browse/CAMEL-20457)

camel-core - NullPointerException for Split parallel and timeout without AggregationStrategy

[CAMEL-20444](https://issues.apache.org/jira/browse/CAMEL-20444)

Camel-Azure-Servicebus: Support setting of CorrelationId on producer

[CAMEL-20440](https://issues.apache.org/jira/browse/CAMEL-20440)

Camel JBang 4.4 - Windows 11 errors with every command

[CAMEL-20438](https://issues.apache.org/jira/browse/CAMEL-20438)

camel-xslt - XPath evaluation fails in Java DSL routes

[CAMEL-20435](https://issues.apache.org/jira/browse/CAMEL-20435)

camel-core - Resequencer EIP cannot be started again after being stopped

[CAMEL-20434](https://issues.apache.org/jira/browse/CAMEL-20434)

camel-http - Use NullEntity when request body is null

[CAMEL-20433](https://issues.apache.org/jira/browse/CAMEL-20433)

camel-jbang - Log command - java.lang.IllegalArgumentException: Comparison method violates its general contract!

[CAMEL-20431](https://issues.apache.org/jira/browse/CAMEL-20431)

camel-jbang - Run and debug route with 'org.apache.camel.debugger.suspend=true' property is not working for different jbang cli and --camel-version versions

[CAMEL-20420](https://issues.apache.org/jira/browse/CAMEL-20420)

CSimple: use of builder throws UnsupportedOperationException

### Dependency upgrade (1)

[CAMEL-20448](https://issues.apache.org/jira/browse/CAMEL-20448)

camel-spring-boot - Upgrade to 3.2.3

### Improvement (12)

[CAMEL-20538](https://issues.apache.org/jira/browse/CAMEL-20538)

camel-jbang - The jbang DEPS with ${ } should be supported

[CAMEL-20534](https://issues.apache.org/jira/browse/CAMEL-20534)

camel-grpc: Port validation should check if a port was specified

[CAMEL-20529](https://issues.apache.org/jira/browse/CAMEL-20529)

Misleading summary on components page

[CAMEL-20495](https://issues.apache.org/jira/browse/CAMEL-20495)

camel-jsonpath - ResultType List should store single element into a List so it can be used afterwards with Split EIP

[CAMEL-20482](https://issues.apache.org/jira/browse/CAMEL-20482)

camel-file - Can ant filter be optimized when using min/max depth with orphan marker file check

[CAMEL-20471](https://issues.apache.org/jira/browse/CAMEL-20471)

camel-jbang - trace command should have show-exchange-variables option

[CAMEL-20459](https://issues.apache.org/jira/browse/CAMEL-20459)

EIP Documentation: grammar, typos and other fixes

[CAMEL-20446](https://issues.apache.org/jira/browse/CAMEL-20446)

camel-jbang - Add support for reloading open-api file in dev mode

[CAMEL-20445](https://issues.apache.org/jira/browse/CAMEL-20445)

JMX - Support update of variables through MBean for JMX debugger

[CAMEL-20442](https://issues.apache.org/jira/browse/CAMEL-20442)

Camel JBang with --open-api flag, stop watching the route

[CAMEL-20418](https://issues.apache.org/jira/browse/CAMEL-20418)

camel-core - Log EIP should only use source line:name if enabled

[CAMEL-20410](https://issues.apache.org/jira/browse/CAMEL-20410)

Documentation: grammar, typos and other fixes

### Task (2)

[CAMEL-20519](https://issues.apache.org/jira/browse/CAMEL-20519)

camel-servlet: Tidy and improve documentation

[CAMEL-20462](https://issues.apache.org/jira/browse/CAMEL-20462)

Beans component typo

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).