# Apache camel 2.23.1 Release

## New and Noteworthy

This release is a minor update of the 2.23.x branch.

## Supported Java version

This version supports Java 8.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>2.23.1</version>
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
      <version>2.23.1</version>
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
| [apache-camel-2.23.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.23.1/apache-camel-2.23.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.23.1/apache-camel-2.23.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.23.1/apache-camel-2.23.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.23.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.23.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (22)

[CAMEL-13049](https://issues.apache.org/jira/browse/CAMEL-13049)

Karaf commands that start/resume contexts and routes should use proper TCCL

[CAMEL-13045](https://issues.apache.org/jira/browse/CAMEL-13045)

Camel-Slack: The verifier must be able to validate webhook and token at the same time

[CAMEL-13044](https://issues.apache.org/jira/browse/CAMEL-13044)

Camel-AWS MQ: it is not possible to set Broker "Public accessibility" parameter using createBroker command

[CAMEL-13028](https://issues.apache.org/jira/browse/CAMEL-13028)

camel-undertow - When using SSL with rest-dsl and api-doc then you can get a port already bound exception

[CAMEL-13022](https://issues.apache.org/jira/browse/CAMEL-13022)

camel-restlet - sending PATCH operation should include body

[CAMEL-13017](https://issues.apache.org/jira/browse/CAMEL-13017)

root-Path handling for SFTP on windows bug

[CAMEL-13016](https://issues.apache.org/jira/browse/CAMEL-13016)

camel-jetty - If multiple bundles uses the same context-path (pathspec) then Jetty should fail

[CAMEL-13014](https://issues.apache.org/jira/browse/CAMEL-13014)

camel mqtt crash using high volume traffic

[CAMEL-13012](https://issues.apache.org/jira/browse/CAMEL-13012)

camel-olingo4 - AbstractFutureCallback generates NPE when response is a 401

[CAMEL-13009](https://issues.apache.org/jira/browse/CAMEL-13009)

Error in generated XAdES 1.1.1 signature

[CAMEL-13008](https://issues.apache.org/jira/browse/CAMEL-13008)

Odata-connector assumes '/' at end of URI

[CAMEL-13006](https://issues.apache.org/jira/browse/CAMEL-13006)

Missing properties on Olingo4 consumer initialisation

[CAMEL-13005](https://issues.apache.org/jira/browse/CAMEL-13005)

olingo4 component serviceUri not set

[CAMEL-12994](https://issues.apache.org/jira/browse/CAMEL-12994)

xquery syntax problem in SpringDSL with spring-boot

[CAMEL-12991](https://issues.apache.org/jira/browse/CAMEL-12991)

SftpEndpoint does not allow to use custom process strategy

[CAMEL-12987](https://issues.apache.org/jira/browse/CAMEL-12987)

camel-core-osgi: OsgiServiceRegistry.onContextStop never gets called.

[CAMEL-12985](https://issues.apache.org/jira/browse/CAMEL-12985)

TransactionErrorHandler fails if UnitOfWork is null -- This seems to happen sometimes with intercepted routes

[CAMEL-12980](https://issues.apache.org/jira/browse/CAMEL-12980)

Bundle in 'Active' State but Camel Context not initialized

[CAMEL-12974](https://issues.apache.org/jira/browse/CAMEL-12974)

Route coverage: When and otherwise are not marked as covered

[CAMEL-12973](https://issues.apache.org/jira/browse/CAMEL-12973)

AbstractCamelWorkItemHandler init fails when WIH is loaded before CamelContext is created.

[CAMEL-12969](https://issues.apache.org/jira/browse/CAMEL-12969)

camel-core-osgi: Slow Memory Leak in OsgiServiceRegistry

[CAMEL-12958](https://issues.apache.org/jira/browse/CAMEL-12958)

Wrong camel context bound in service registry of jbpm/Kie Server

### Improvement (6)

[CAMEL-13042](https://issues.apache.org/jira/browse/CAMEL-13042)

camel-core - File producer should by default not allow writing files to directories outside its starting directory

[CAMEL-13035](https://issues.apache.org/jira/browse/CAMEL-13035)

Camel telegram - Update made to channel not received by camel application

[CAMEL-13029](https://issues.apache.org/jira/browse/CAMEL-13029)

camel-swagger-java - Should default use scheme from rest-dsl configuration in swagger doc

[CAMEL-13025](https://issues.apache.org/jira/browse/CAMEL-13025)

camel-core - File read lock changed - If file gets deleted then break out loop

[CAMEL-12979](https://issues.apache.org/jira/browse/CAMEL-12979)

Service beans with custom lifecycle on CxfRsEndpoint

[CAMEL-12935](https://issues.apache.org/jira/browse/CAMEL-12935)

Camel Context restarts in Blueprint Test if isCreateCamelContextPerClass is set to true

### New Feature (2)

[CAMEL-13015](https://issues.apache.org/jira/browse/CAMEL-13015)

camel-spring-boot - load multiple route xml files

[CAMEL-12964](https://issues.apache.org/jira/browse/CAMEL-12964)

Create new CamelWIH to integrate with recently added Camel support in jBPM/KIE-Server

### Task (2)

[CAMEL-13041](https://issues.apache.org/jira/browse/CAMEL-13041)

Camel-AWS MQ: Create Broker operation is not working

[CAMEL-12984](https://issues.apache.org/jira/browse/CAMEL-12984)

Backport camel-jbpm changes to 2.23

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).