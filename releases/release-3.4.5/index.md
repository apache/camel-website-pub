# Apache camel 3.4.5 Release

## New and Noteworthy

This release is the new Camel 3.4.5 patch release.

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
      <version>3.4.5</version>
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
      <version>3.4.5</version>
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
| [apache-camel-3.4.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.4.5/apache-camel-3.4.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.4.5/apache-camel-3.4.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.4.5/apache-camel-3.4.5-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.4.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.4.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (19)

[CAMEL-15937](https://issues.apache.org/jira/browse/CAMEL-15937)

camel-netty - WARN logging with disconnect=true

[CAMEL-15840](https://issues.apache.org/jira/browse/CAMEL-15840)

camel-aws2-sns: duplicate copies of configuration objects lead to undefined behavior

[CAMEL-15834](https://issues.apache.org/jira/browse/CAMEL-15834)

NATS consumer throws NullPointerException on connection failure

[CAMEL-15803](https://issues.apache.org/jira/browse/CAMEL-15803)

missing jar libraries in download zip

[CAMEL-15793](https://issues.apache.org/jira/browse/CAMEL-15793)

MethodNotFoundException when calling method on OSGi service reference in Blueprint

[CAMEL-15788](https://issues.apache.org/jira/browse/CAMEL-15788)

Apache Camel Yammer component does not work in 3.x (from 3.1)

[CAMEL-15760](https://issues.apache.org/jira/browse/CAMEL-15760)

org.osgi.service.blueprint.container.NoSuchComponentException: No component with id 'blueprintBundle' could be found

[CAMEL-15748](https://issues.apache.org/jira/browse/CAMEL-15748)

Paho consumer never connects if the broker is not reachable at startup

[CAMEL-15710](https://issues.apache.org/jira/browse/CAMEL-15710)

OpenTracingTracer does not activate created span

[CAMEL-15682](https://issues.apache.org/jira/browse/CAMEL-15682)

Aggregate route recovery fails to start up

[CAMEL-15678](https://issues.apache.org/jira/browse/CAMEL-15678)

camel-aws2-s3 multipart upload multiplies file by number of parts

[CAMEL-15669](https://issues.apache.org/jira/browse/CAMEL-15669)

When the registry does not have any nodes, ServiceCallDefinition will be blocked

[CAMEL-15644](https://issues.apache.org/jira/browse/CAMEL-15644)

camel-salesforce - NullPointerException on route startup

[CAMEL-15623](https://issues.apache.org/jira/browse/CAMEL-15623)

osgi - Reference methods not found in blueprint context

[CAMEL-15602](https://issues.apache.org/jira/browse/CAMEL-15602)

camel-main - Add support for property placeholders in #class factory method parameters

[CAMEL-15581](https://issues.apache.org/jira/browse/CAMEL-15581)

Unable to load XML REST definitions with camel-main xmlRests config property

[CAMEL-15580](https://issues.apache.org/jira/browse/CAMEL-15580)

SJMS Batch Consumer startup race condition

[CAMEL-15558](https://issues.apache.org/jira/browse/CAMEL-15558)

pollEnrich timeout issue

[CAMEL-15526](https://issues.apache.org/jira/browse/CAMEL-15526)

Camel-AWS2-S3: Consume Gzip file from S3 not working.

### Improvement (3)

[CAMEL-15917](https://issues.apache.org/jira/browse/CAMEL-15917)

Resilience4j Property Component doesn't work for configurationRef

[CAMEL-15600](https://issues.apache.org/jira/browse/CAMEL-15600)

platoform http vertx: thread blocked calling knative REST

[CAMEL-15591](https://issues.apache.org/jira/browse/CAMEL-15591)

Put a configurable limit on the size of unzipped data using camel-zipfile + camel-tarfile

### Task (3)

[CAMEL-15702](https://issues.apache.org/jira/browse/CAMEL-15702)

Camel-Karaf and camel-spring-boot: Generated documentation for 3.4.x LTS, should point to correct components/dataformat/languages documentation

[CAMEL-15594](https://issues.apache.org/jira/browse/CAMEL-15594)

incorrect bundle.symbolicName in camel-example-servlet-rest-karaf-jaas

[CAMEL-15571](https://issues.apache.org/jira/browse/CAMEL-15571)

The order of loading settings is changed in the method AbstractLocationPropertiesSource::loadProperties(Predicate)

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).