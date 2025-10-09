# Apache camel 4.8.3 Release

## New and Noteworthy

This release is the new Camel 4.8.3 release.

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
      <version>4.8.3</version>
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
      <version>4.8.3</version>
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
| [apache-camel-4.8.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.3/apache-camel-4.8.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.3/apache-camel-4.8.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.3/apache-camel-4.8.3-src.zip.sha512) |
| [apache-camel-4.8.3-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.3/apache-camel-4.8.3-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.3/apache-camel-4.8.3-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.3/apache-camel-4.8.3-sbom.xml.sha512) |
| [apache-camel-4.8.3-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.3/apache-camel-4.8.3-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.3/apache-camel-4.8.3-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.3/apache-camel-4.8.3-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (21)

[CAMEL-21595](https://issues.apache.org/jira/browse/CAMEL-21595)

camel-langchain4j-tools: code may thrown an NPE if no tools are called

[CAMEL-21572](https://issues.apache.org/jira/browse/CAMEL-21572)

Camel JBang with --runtime=spring-boot throw NullPointerException

[CAMEL-21567](https://issues.apache.org/jira/browse/CAMEL-21567)

camel-jbang - Debug command should accept options from run

[CAMEL-21562](https://issues.apache.org/jira/browse/CAMEL-21562)

If HeadBucket call is not allowed, AWS2S3Endpoint fails to start

[CAMEL-21552](https://issues.apache.org/jira/browse/CAMEL-21552)

camel-yaml-dsl - "param" property from YAML DSL is not present in Camel model

[CAMEL-21550](https://issues.apache.org/jira/browse/CAMEL-21550)

camel-aws-sqs - message is getting expired before extender changes the visibility

[CAMEL-21545](https://issues.apache.org/jira/browse/CAMEL-21545)

camel-jsonpath - Should not use XmlMapper

[CAMEL-21543](https://issues.apache.org/jira/browse/CAMEL-21543)

camel-main - MainListenerClasses loaded from application.properties is not activated

[CAMEL-21536](https://issues.apache.org/jira/browse/CAMEL-21536)

camel-platform-http-starter throws "No ThreadPoolTaskExecutor configured" if virtual threads are enabled

[CAMEL-21532](https://issues.apache.org/jira/browse/CAMEL-21532)

Camel JBang --logging-category is not respected on Windows

[CAMEL-21531](https://issues.apache.org/jira/browse/CAMEL-21531)

RestOpenApiReaderTest is broken for some locations

[CAMEL-21528](https://issues.apache.org/jira/browse/CAMEL-21528)

camel-vertx-http: Response handling may block the Vert.x event loop

[CAMEL-21526](https://issues.apache.org/jira/browse/CAMEL-21526)

camel-aws - Unable to set Timestamp in query parameters to initialize iterator of AT\_TIMESTAMP type for AWS Kinesis component

[CAMEL-21525](https://issues.apache.org/jira/browse/CAMEL-21525)

Issue camel-debezium-postgres-starter Auto-Configured Bean

[CAMEL-21516](https://issues.apache.org/jira/browse/CAMEL-21516)

camel-jbang - Transform route from xml to yaml with uri-as-parameters for context-path

[CAMEL-21512](https://issues.apache.org/jira/browse/CAMEL-21512)

camel-jbang - camel transform route with multiple <rest> only include last

[CAMEL-21506](https://issues.apache.org/jira/browse/CAMEL-21506)

camel-pdf: type converter doesn't work with the file component

[CAMEL-21504](https://issues.apache.org/jira/browse/CAMEL-21504)

camel-spring-boot - MicrometerTagsAutoConfiguration class puts http method in uri tag

[CAMEL-21495](https://issues.apache.org/jira/browse/CAMEL-21495)

camel-quarkus: REST route inlining works incorrectly when testing

[CAMEL-21486](https://issues.apache.org/jira/browse/CAMEL-21486)

camel k8s ... cannot push to image-registry.openshift-image-registry.svc:5000

[CAMEL-21418](https://issues.apache.org/jira/browse/CAMEL-21418)

camel-rest - Client request validation and multiple values in Accept header

### Dependency upgrade (5)

[CAMEL-21590](https://issues.apache.org/jira/browse/CAMEL-21590)

camel-pulsar - Upgrade to 3.3.3

[CAMEL-21571](https://issues.apache.org/jira/browse/CAMEL-21571)

camel-mina - Upgrade to 2.2.4

[CAMEL-21566](https://issues.apache.org/jira/browse/CAMEL-21566)

camel-cxf - Upgrade to 4.0.6

[CAMEL-21565](https://issues.apache.org/jira/browse/CAMEL-21565)

camel-spring-boot - Upgrade to SB 3.3.7

[CAMEL-21561](https://issues.apache.org/jira/browse/CAMEL-21561)

camel-kafka - Upgrade to kafka 3.8.1

### Improvement (8)

[CAMEL-21568](https://issues.apache.org/jira/browse/CAMEL-21568)

camel-jbang - Debug should support step into/over

[CAMEL-21563](https://issues.apache.org/jira/browse/CAMEL-21563)

Camel-Jbang ps output in JSON

[CAMEL-21559](https://issues.apache.org/jira/browse/CAMEL-21559)

camel-mongodb - Improve save performance

[CAMEL-21519](https://issues.apache.org/jira/browse/CAMEL-21519)

camel-jbang - camel transform route - Expression should be quoted

[CAMEL-21511](https://issues.apache.org/jira/browse/CAMEL-21511)

camel-jbang - camel transform route with rest-dsl should not inline routes

[CAMEL-21510](https://issues.apache.org/jira/browse/CAMEL-21510)

camel-jbang - Kubernetes plugin support for parameter name

[CAMEL-21507](https://issues.apache.org/jira/browse/CAMEL-21507)

Camel-Jbang Kubernetes Plugin: Use new Trait model

[CAMEL-21223](https://issues.apache.org/jira/browse/CAMEL-21223)

camel-jbang - Debug may not go inside Split EIP

### New Feature (1)

[CAMEL-21529](https://issues.apache.org/jira/browse/CAMEL-21529)

camel-catalog - Consider adding another version discovery step

### Task (5)

[CAMEL-21585](https://issues.apache.org/jira/browse/CAMEL-21585)

camel-test-infra: select platform-specific containers dynamically

[CAMEL-21576](https://issues.apache.org/jira/browse/CAMEL-21576)

camel-test-infra: container pulling adjustments

[CAMEL-21533](https://issues.apache.org/jira/browse/CAMEL-21533)

Backport Knative test coverage to 4.8.x

[CAMEL-21530](https://issues.apache.org/jira/browse/CAMEL-21530)

camel-jbang - Remove deps on runtime and cluster-type where no longer needed

[CAMEL-21502](https://issues.apache.org/jira/browse/CAMEL-21502)

camel-langchain4j-tools: fix incorrect documentation

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).