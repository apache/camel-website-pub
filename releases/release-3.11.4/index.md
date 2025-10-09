# Apache camel 3.11.4 Release

## New and Noteworthy

This release is the new Camel 3.11.4 LTS patch release.

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
      <version>3.11.4</version>
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
      <version>3.11.4</version>
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
| [apache-camel-3.11.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.11.4/apache-camel-3.11.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.11.4/apache-camel-3.11.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.11.4/apache-camel-3.11.4-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.11.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.11.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (13)

[CAMEL-17181](https://issues.apache.org/jira/browse/CAMEL-17181)

camel-core - XPathBuilder never clears pool when using @XPath annotation and grows pool causing memory leak

[CAMEL-17174](https://issues.apache.org/jira/browse/CAMEL-17174)

UnitOfWorkHelper doesn't clear UoW when job is done

[CAMEL-17167](https://issues.apache.org/jira/browse/CAMEL-17167)

Camel-AWS2-SQS: Message attributes can be at most 10

[CAMEL-17159](https://issues.apache.org/jira/browse/CAMEL-17159)

rest-dsl - clientRequestValidation fails then operation produces more than just xml and/or json

[CAMEL-17135](https://issues.apache.org/jira/browse/CAMEL-17135)

camel-debezium-mongodb-starter does not pupulate values from application.properties

[CAMEL-17131](https://issues.apache.org/jira/browse/CAMEL-17131)

camel-kafka - JMX MBean InstanceAlreadyExistsException thrown

[CAMEL-17124](https://issues.apache.org/jira/browse/CAMEL-17124)

HttpRestHeaderFilterStrategy doesn't filter queryParameter headers

[CAMEL-17114](https://issues.apache.org/jira/browse/CAMEL-17114)

camel-jslt cannot load files from classpath in quarkus dev-mode

[CAMEL-17105](https://issues.apache.org/jira/browse/CAMEL-17105)

Transactions - Ignored property Exchange.markRollbackOnlyLast

[CAMEL-17095](https://issues.apache.org/jira/browse/CAMEL-17095)

camel-resilience4j - Using timeout and bulkhead together does not work

[CAMEL-17073](https://issues.apache.org/jira/browse/CAMEL-17073)

camel-core - Incorrect Simple expression behavior when cache enabled

[CAMEL-17067](https://issues.apache.org/jira/browse/CAMEL-17067)

Datasonnet header can't be used to set bodyMediaType

[CAMEL-17049](https://issues.apache.org/jira/browse/CAMEL-17049)

authUsername and authPassword parameters not passed to the underlaying endpoint

### Dependency upgrade (1)

[CAMEL-17123](https://issues.apache.org/jira/browse/CAMEL-17123)

Upgrade to Spring Boot 2.5.6

### Improvement (3)

[CAMEL-17175](https://issues.apache.org/jira/browse/CAMEL-17175)

Camel-MLLP: option 'logPhi' with value 'false' does not work for exception logging

[CAMEL-17156](https://issues.apache.org/jira/browse/CAMEL-17156)

camel-aws - Cancelling "Extending visibility window" while processing completed causes interruption exception

[CAMEL-17126](https://issues.apache.org/jira/browse/CAMEL-17126)

camel-restdsl plugin doesn't implement parameter clientRequestValidation

### Task (3)

[CAMEL-17169](https://issues.apache.org/jira/browse/CAMEL-17169)

Three copies of same-named attribute in generated spring-boot.json file

[CAMEL-17146](https://issues.apache.org/jira/browse/CAMEL-17146)

SprintBoot pprovider of Catalog declares crypto-cms as a component but definition is missing

[CAMEL-17052](https://issues.apache.org/jira/browse/CAMEL-17052)

Azure BOM import forces incorrect Netty dependency version

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).