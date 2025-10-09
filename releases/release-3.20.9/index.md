# Apache camel 3.20.9 Release

## New and Noteworthy

This release is the new Camel 3.20.9 LTS patch release.

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
      <version>3.20.9</version>
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
      <version>3.20.9</version>
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
| [apache-camel-3.20.9-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.20.9/apache-camel-3.20.9-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.9/apache-camel-3.20.9-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.9/apache-camel-3.20.9-src.zip.sha512) |
| [apache-camel-3.20.9-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/3.20.9/apache-camel-3.20.9-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.9/apache-camel-3.20.9-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.9/apache-camel-3.20.9-sbom.xml.sha512) |
| [apache-camel-3.20.9-sbom.json](https://archive.apache.org/dist/camel/apache-camel/3.20.9/apache-camel-3.20.9-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.9/apache-camel-3.20.9-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.9/apache-camel-3.20.9-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-3.20.9` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.20.9

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (6)

[CAMEL-20152](https://issues.apache.org/jira/browse/CAMEL-20152)

camel-jetty - OutOfMemoryError with big file upload via multipart

[CAMEL-20139](https://issues.apache.org/jira/browse/CAMEL-20139)

aggregate EIP: wrong correlation key set for the first aggregate exchange

[CAMEL-20079](https://issues.apache.org/jira/browse/CAMEL-20079)

EndpointDslMojo generates wrong header names

[CAMEL-20054](https://issues.apache.org/jira/browse/CAMEL-20054)

camel-kubernetes - Configuration of Kubernetes secrets with Camel K not working as expected

[CAMEL-20053](https://issues.apache.org/jira/browse/CAMEL-20053)

camel-jira: watchUpdates consumer does not see issues created after route startup

[CAMEL-20035](https://issues.apache.org/jira/browse/CAMEL-20035)

Program terminates with OutOfMemoryError

### Dependency upgrade (2)

[CAMEL-20146](https://issues.apache.org/jira/browse/CAMEL-20146)

camel-spring-boot - Upgrade to 2.7.18

[CAMEL-20049](https://issues.apache.org/jira/browse/CAMEL-20049)

camel-activemq - Upgrade to latest releases

### Task (1)

[CAMEL-20094](https://issues.apache.org/jira/browse/CAMEL-20094)

camel-catalog: camel-spring.xsd keeps being regenerated

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).