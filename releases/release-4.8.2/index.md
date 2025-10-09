# Apache camel 4.8.2 Release

## New and Noteworthy

This release is the new Camel 4.8.2 release.

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
      <version>4.8.2</version>
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
      <version>4.8.2</version>
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
| [apache-camel-4.8.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.2/apache-camel-4.8.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.2/apache-camel-4.8.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.2/apache-camel-4.8.2-src.zip.sha512) |
| [apache-camel-4.8.2-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.2/apache-camel-4.8.2-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.2/apache-camel-4.8.2-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.2/apache-camel-4.8.2-sbom.xml.sha512) |
| [apache-camel-4.8.2-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.2/apache-camel-4.8.2-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.2/apache-camel-4.8.2-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.2/apache-camel-4.8.2-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (30)

[CAMEL-22417](https://issues.apache.org/jira/browse/CAMEL-22417)

ErrorHandlerReifier fails with Unsupported definition: null

[CAMEL-21493](https://issues.apache.org/jira/browse/CAMEL-21493)

camel-ref: should use CamelContext.hasEndpoint but not CamelContext.getEndpoint to check existence of an endpoint

[CAMEL-21488](https://issues.apache.org/jira/browse/CAMEL-21488)

camel-jbang - Export with multiple customer kamelets

[CAMEL-21487](https://issues.apache.org/jira/browse/CAMEL-21487)

camel-jbang - Should be able to load route template files

[CAMEL-21471](https://issues.apache.org/jira/browse/CAMEL-21471)

camel-quartz ignores ignoreExpiredNextFireTime when endAt is expired

[CAMEL-21467](https://issues.apache.org/jira/browse/CAMEL-21467)

Simple expressions execute forever. Thread is RUNNABLE for ever. Issue appears with bean expressions inside simple expressions on SimpleLRUCache

[CAMEL-21446](https://issues.apache.org/jira/browse/CAMEL-21446)

configmap/secret - default takes precedence

[CAMEL-21444](https://issues.apache.org/jira/browse/CAMEL-21444)

camel-jbang - catalog using since-after can do NPE if version is single digit

[CAMEL-21436](https://issues.apache.org/jira/browse/CAMEL-21436)

camel-jbang - Export beans with secret function should work even if k8s is not configured

[CAMEL-21432](https://issues.apache.org/jira/browse/CAMEL-21432)

multicast function executes for ever. Thread is RUNNABLE for ever. Issue appears with multicast operating on SimpleLRUCache

[CAMEL-21430](https://issues.apache.org/jira/browse/CAMEL-21430)

camel-rest-openapi - Generated produces string is missing media types

[CAMEL-21423](https://issues.apache.org/jira/browse/CAMEL-21423)

camel-crypto - It is not possible to use "inline" with "AES/GCM/NoPadding"

[CAMEL-21419](https://issues.apache.org/jira/browse/CAMEL-21419)

Camel Spring Boot v. 4.8.1: Multiple Task Executor Beans Detected

[CAMEL-21407](https://issues.apache.org/jira/browse/CAMEL-21407)

camel-dynamic-router component: unsubscribe by control message does not work

[CAMEL-21406](https://issues.apache.org/jira/browse/CAMEL-21406)

camel-sql - RowMapperFactory should be configurable to refer a bean by id

[CAMEL-21404](https://issues.apache.org/jira/browse/CAMEL-21404)

camel-jbang - Skip files without extension when using --source-dir

[CAMEL-21403](https://issues.apache.org/jira/browse/CAMEL-21403)

AS2 Component - Incorrect message length calculation when generating MIC for EDI messages with multi-byte characters

[CAMEL-21401](https://issues.apache.org/jira/browse/CAMEL-21401)

camel-core - Custom bean in DSL using factory method should avoid ClassCastException

[CAMEL-21399](https://issues.apache.org/jira/browse/CAMEL-21399)

Kubernetes plugin regression. Fails on OCP deployments

[CAMEL-21397](https://issues.apache.org/jira/browse/CAMEL-21397)

camel-file: autoCreateStepwise not working in Windows

[CAMEL-21386](https://issues.apache.org/jira/browse/CAMEL-21386)

camel k8s run --dev does not work on openshift

[CAMEL-21382](https://issues.apache.org/jira/browse/CAMEL-21382)

camel-core - Tracing with headers that are Map type can cause ClassCastException when dumping as XML

[CAMEL-21381](https://issues.apache.org/jira/browse/CAMEL-21381)

camel k8s cannot run spring-boot on openshift

[CAMEL-21379](https://issues.apache.org/jira/browse/CAMEL-21379)

camel-salesforce: introduce delay in pub/sub reconnect attempts

[CAMEL-21376](https://issues.apache.org/jira/browse/CAMEL-21376)

UseOriginalAggregationStrategy - null pointer

[CAMEL-21374](https://issues.apache.org/jira/browse/CAMEL-21374)

camel-jbang - Export pipe with local kamelets seems to fail

[CAMEL-21372](https://issues.apache.org/jira/browse/CAMEL-21372)

Camel JBang Export/Run are not working based on external camel-version setting

[CAMEL-21361](https://issues.apache.org/jira/browse/CAMEL-21361)

fabric8 kubernetes-client fails to connect to openshift

[CAMEL-21355](https://issues.apache.org/jira/browse/CAMEL-21355)

LangChain4j Tools fails with direct LLM response

[CAMEL-21302](https://issues.apache.org/jira/browse/CAMEL-21302)

camel-opentelemetry context leak with direct async producer

### Dependency upgrade (3)

[CAMEL-21469](https://issues.apache.org/jira/browse/CAMEL-21469)

camel-spring-boot - Upgrade to SB 3.3.6

[CAMEL-21455](https://issues.apache.org/jira/browse/CAMEL-21455)

camel-beanio - Upgrade to 3.2.0

[CAMEL-21366](https://issues.apache.org/jira/browse/CAMEL-21366)

camel-spring-boot - Upgrade to 3.3.5

### Improvement (8)

[CAMEL-21492](https://issues.apache.org/jira/browse/CAMEL-21492)

Doc: it would be nice to have a list of components usable for payload security

[CAMEL-21482](https://issues.apache.org/jira/browse/CAMEL-21482)

camel-jaxb - JaxbDataFormat ignoreJAXBElement is default true

[CAMEL-21475](https://issues.apache.org/jira/browse/CAMEL-21475)

camel-yaml-dsl - Using route templates with hardcoded ids problem

[CAMEL-21474](https://issues.apache.org/jira/browse/CAMEL-21474)

Camel-SMBProducer is never disconnecting

[CAMEL-21445](https://issues.apache.org/jira/browse/CAMEL-21445)

camel-core - Vault with secret refresh should be disabled as default

[CAMEL-21380](https://issues.apache.org/jira/browse/CAMEL-21380)

camel-salesforce: pub/sub: add ability to opt out of proxy

[CAMEL-21371](https://issues.apache.org/jira/browse/CAMEL-21371)

camel-core - Add converter for Reader to InputStream

[CAMEL-21369](https://issues.apache.org/jira/browse/CAMEL-21369)

camel-jbang - Kubernetes plugin - Use quarkus extensions for Route trait

### Task (1)

[CAMEL-21395](https://issues.apache.org/jira/browse/CAMEL-21395)

camel-debezium - Avoid split packages

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).