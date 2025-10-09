# Apache camel 4.10.4 Release

## New and Noteworthy

This release is the new Camel 4.10.4 release.

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
      <version>4.10.4</version>
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
      <version>4.10.4</version>
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
| [apache-camel-4.10.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.10.4/apache-camel-4.10.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.4/apache-camel-4.10.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.4/apache-camel-4.10.4-src.zip.sha512) |
| [apache-camel-4.10.4-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.10.4/apache-camel-4.10.4-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.4/apache-camel-4.10.4-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.4/apache-camel-4.10.4-sbom.xml.sha512) |
| [apache-camel-4.10.4-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.10.4/apache-camel-4.10.4-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.4/apache-camel-4.10.4-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.4/apache-camel-4.10.4-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.10.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.10.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (29)

[CAMEL-22015](https://issues.apache.org/jira/browse/CAMEL-22015)

camel-jbang - Export with language component should resolve dependency

[CAMEL-22014](https://issues.apache.org/jira/browse/CAMEL-22014)

camel-jbang - Should be able to include groovy files on classpath

[CAMEL-22004](https://issues.apache.org/jira/browse/CAMEL-22004)

Kafka component shutdown may get stuck when rebalancing occurs

[CAMEL-21990](https://issues.apache.org/jira/browse/CAMEL-21990)

camel-jbang - Stop integration by name may not work

[CAMEL-21988](https://issues.apache.org/jira/browse/CAMEL-21988)

Missing @UriParam with entityManagerFactory in JpaEndpoint

[CAMEL-21987](https://issues.apache.org/jira/browse/CAMEL-21987)

camel-jbang - Run with --source-dir may not load content for static HTTP server

[CAMEL-21983](https://issues.apache.org/jira/browse/CAMEL-21983)

camel-jbang - Export to quarkus produces an incorrect application.properties file when referring kamelet files

[CAMEL-21967](https://issues.apache.org/jira/browse/CAMEL-21967)

camel-jbang - Transform route to yaml with CBR cannot load into Karavan

[CAMEL-21964](https://issues.apache.org/jira/browse/CAMEL-21964)

camel-salesforce: bulk api 2.0 error responses fail to deserialize

[CAMEL-21958](https://issues.apache.org/jira/browse/CAMEL-21958)

camel-core - Java DSL wrong "otherwise" is triggered when having nested choice

[CAMEL-21957](https://issues.apache.org/jira/browse/CAMEL-21957)

camel-core - Error handler should store failure route id eager so onRedelivery/onExceptionOccurred processors have access

[CAMEL-21954](https://issues.apache.org/jira/browse/CAMEL-21954)

camel-core - Route templates with onException does not work

[CAMEL-21953](https://issues.apache.org/jira/browse/CAMEL-21953)

camel-groovy: GroovyLanguage.stop may throw UnsupportedOperationException

[CAMEL-21947](https://issues.apache.org/jira/browse/CAMEL-21947)

GenericFileConsumer with eager idempotence and read lock stop processing file

[CAMEL-21942](https://issues.apache.org/jira/browse/CAMEL-21942)

camel-jbang - Export kamelet with custom bean should not create bean when being used as part of stubbing

[CAMEL-21940](https://issues.apache.org/jira/browse/CAMEL-21940)

camel-kafka - KafkaProducerCallBack can execute the continuation twice

[CAMEL-21938](https://issues.apache.org/jira/browse/CAMEL-21938)

camel-jolt - inputType & outputType can't be set for http uris

[CAMEL-21926](https://issues.apache.org/jira/browse/CAMEL-21926)

camel-attachment: inconsistent behaviour

[CAMEL-21923](https://issues.apache.org/jira/browse/CAMEL-21923)

camel-langchain4j-tools: LLM call should include all tools at the end of the flow

[CAMEL-21912](https://issues.apache.org/jira/browse/CAMEL-21912)

camel-cxf - Caching of ToStringTypeConverter breaks CXF RS Rest service

[CAMEL-21908](https://issues.apache.org/jira/browse/CAMEL-21908)

camel-jms - Property 'idleReceivesPerTaskLimit' is not populated to spring-jms

[CAMEL-21901](https://issues.apache.org/jira/browse/CAMEL-21901)

Salesforce consumer endpoint query parameter fallBackReplayId not working

[CAMEL-21892](https://issues.apache.org/jira/browse/CAMEL-21892)

Stopped producer in DefaultProducerCache.lastUsedProducer

[CAMEL-21891](https://issues.apache.org/jira/browse/CAMEL-21891)

camel-ftp - Consumer and antInclude regression

[CAMEL-21877](https://issues.apache.org/jira/browse/CAMEL-21877)

ServiceNow incident update fails due to model/body type mismatch

[CAMEL-21816](https://issues.apache.org/jira/browse/CAMEL-21816)

camel-ai - Missing tool information when returning function call response

[CAMEL-21794](https://issues.apache.org/jira/browse/CAMEL-21794)

camel-jbang - Export bean with lazy-bean should not initialize the bean if not needed

[CAMEL-21662](https://issues.apache.org/jira/browse/CAMEL-21662)

Camel JBang - run with Spring boot / Quarkus fails on Windows

[CAMEL-21490](https://issues.apache.org/jira/browse/CAMEL-21490)

camel-jbang - Transform route to yaml with choice

### Dependency upgrade (2)

[CAMEL-22003](https://issues.apache.org/jira/browse/CAMEL-22003)

camel-spring-boot - Upgrade to 3.4.5

[CAMEL-21980](https://issues.apache.org/jira/browse/CAMEL-21980)

camel-jbang - Transform route dump YAML in tooling friendly format

### Improvement (12)

[CAMEL-22019](https://issues.apache.org/jira/browse/CAMEL-22019)

camel-smb - Add header for UNCPath for backwards compatability

[CAMEL-22018](https://issues.apache.org/jira/browse/CAMEL-22018)

camel-core - Exchange.getVariables should include message headers

[CAMEL-22007](https://issues.apache.org/jira/browse/CAMEL-22007)

camel-micrometer - Configuring tags is not tooling friendly

[CAMEL-22006](https://issues.apache.org/jira/browse/CAMEL-22006)

camel-jbang - Detect rest-openapi need rest producer component to function

[CAMEL-22001](https://issues.apache.org/jira/browse/CAMEL-22001)

camel-core - Kamelet and EIPs should propagate exchange variables

[CAMEL-21991](https://issues.apache.org/jira/browse/CAMEL-21991)

camel-jpa - Make entityManagerFactory as an autowired option

[CAMEL-21939](https://issues.apache.org/jira/browse/CAMEL-21939)

camel-jbang - Export to have --verbose option

[CAMEL-21934](https://issues.apache.org/jira/browse/CAMEL-21934)

Additional Information Needed in ContextHealthCheck message

[CAMEL-21907](https://issues.apache.org/jira/browse/CAMEL-21907)

camel-http - Add oauth2 scope to request body

[CAMEL-21884](https://issues.apache.org/jira/browse/CAMEL-21884)

Introduce the useBodyHandler option in camel-platform-http

[CAMEL-21845](https://issues.apache.org/jira/browse/CAMEL-21845)

camel-sql - Improve performance of batch inserts

[CAMEL-21710](https://issues.apache.org/jira/browse/CAMEL-21710)

Set automatic parameter when running camel-jbang kubernetes run

### Task (1)

[CAMEL-21984](https://issues.apache.org/jira/browse/CAMEL-21984)

camel-smb File type is wrong in documentation

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).