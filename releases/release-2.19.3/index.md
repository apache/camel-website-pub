# Apache camel 2.19.3 Release

## New and Noteworthy

This release is a minor update of the 2.19.x branch.

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
      <version>2.19.3</version>
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
      <version>2.19.3</version>
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
| [apache-camel-2.19.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.19.3/apache-camel-2.19.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.19.3/apache-camel-2.19.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.19.3/apache-camel-2.19.3-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.19.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.19.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (26)

[CAMEL-11765](https://issues.apache.org/jira/browse/CAMEL-11765)

camel-undertow - Consumer adds duplicate headers

[CAMEL-11750](https://issues.apache.org/jira/browse/CAMEL-11750)

Camel route with multicast (parallel) generate huge CPU load

[CAMEL-11748](https://issues.apache.org/jira/browse/CAMEL-11748)

Camel-Undertow: transferException option doesn't work

[CAMEL-11742](https://issues.apache.org/jira/browse/CAMEL-11742)

File consumer - Delete orphan lock files on startup may not match a lock file when using include/antInclude filtering

[CAMEL-11724](https://issues.apache.org/jira/browse/CAMEL-11724)

Camel-Hdfs2: No need for initialDelay and delay as configuration properties since they are already parameters of ScheduledPollConsumer

[CAMEL-11723](https://issues.apache.org/jira/browse/CAMEL-11723)

ManagedCamelContext.dumpRestsAsXml can fail if default charset is not utf-8

[CAMEL-11716](https://issues.apache.org/jira/browse/CAMEL-11716)

error in handling return parameters in db functions

[CAMEL-11709](https://issues.apache.org/jira/browse/CAMEL-11709)

Camel-Milo component cannot write to newer server versions

[CAMEL-11690](https://issues.apache.org/jira/browse/CAMEL-11690)

Done() called two times in RoutingSlip processor

[CAMEL-11688](https://issues.apache.org/jira/browse/CAMEL-11688)

ensure transport endpoint configuration will be take into account when create JettyRestHttpBinding from REST DSL

[CAMEL-11677](https://issues.apache.org/jira/browse/CAMEL-11677)

TypeConverterLoaderException: Cannot find any type converter classes from the following packages: com.abc.storage.service.converter if application is packaged using spring-boot-maven-plugin

[CAMEL-11671](https://issues.apache.org/jira/browse/CAMEL-11671)

camel-ahc - No way to disable url encoding

[CAMEL-11649](https://issues.apache.org/jira/browse/CAMEL-11649)

Cookie Handling only works for one cookie

[CAMEL-11648](https://issues.apache.org/jira/browse/CAMEL-11648)

camel-mongodb-gridfs - Created document cannot be read by the new MongoDB GridFS API

[CAMEL-11636](https://issues.apache.org/jira/browse/CAMEL-11636)

property placeholder is not replaced in REST DSL in blueprint context

[CAMEL-11630](https://issues.apache.org/jira/browse/CAMEL-11630)

JPAMessageIdRepository Not Releasing Connections

[CAMEL-11626](https://issues.apache.org/jira/browse/CAMEL-11626)

ServiceNowException is printing "%d" (not replacing value)

[CAMEL-11623](https://issues.apache.org/jira/browse/CAMEL-11623)

LevelDB Java implementation wont be tried on Errors

[CAMEL-11620](https://issues.apache.org/jira/browse/CAMEL-11620)

Requiredement for date string to be longer than pattern is invalid.

[CAMEL-11615](https://issues.apache.org/jira/browse/CAMEL-11615)

WorkerPool is null in DefaultCamelReactiveStreamsService

[CAMEL-11608](https://issues.apache.org/jira/browse/CAMEL-11608)

Camel-AWS: Camel-Kinesis needs Jackson Dataformat CBOR to work in OSGi

[CAMEL-11607](https://issues.apache.org/jira/browse/CAMEL-11607)

NPE in MBeanInfoAssembler when debug is enabled

[CAMEL-11593](https://issues.apache.org/jira/browse/CAMEL-11593)

Global rest configuration gets overridden by default

[CAMEL-11591](https://issues.apache.org/jira/browse/CAMEL-11591)

ClassNotFound: javax.servlet.ServletOutputStream in opentracing example client

[CAMEL-11523](https://issues.apache.org/jira/browse/CAMEL-11523)

JasyptPropertiesParser fails on properties references with default value

[CAMEL-11455](https://issues.apache.org/jira/browse/CAMEL-11455)

Automatic transform String to DBObject after previous conversion error

### Improvement (12)

[CAMEL-11755](https://issues.apache.org/jira/browse/CAMEL-11755)

toD should ignore when dynamic uri is empty

[CAMEL-11743](https://issues.apache.org/jira/browse/CAMEL-11743)

camel-ldap - Make it possible to use ENV when configuring DirContext

[CAMEL-11728](https://issues.apache.org/jira/browse/CAMEL-11728)

Camel-AWS S3: Avoid warn log message about content length

[CAMEL-11726](https://issues.apache.org/jira/browse/CAMEL-11726)

Elsql producer inconsistent behavior compare to sql component producer

[CAMEL-11720](https://issues.apache.org/jira/browse/CAMEL-11720)

GoogleDriveProducer should be able to honor the http.proxyPort and http.proxyHost properties from the CamelContext

[CAMEL-11719](https://issues.apache.org/jira/browse/CAMEL-11719)

add a string to ChildReference converter for camel-google-drive

[CAMEL-11710](https://issues.apache.org/jira/browse/CAMEL-11710)

trim for fixlength only trim one direction

[CAMEL-11706](https://issues.apache.org/jira/browse/CAMEL-11706)

Remove duplicate type converter methods from HBaseModelConverter

[CAMEL-11691](https://issues.apache.org/jira/browse/CAMEL-11691)

Should resubscribe when reconnect MQTT

[CAMEL-11613](https://issues.apache.org/jira/browse/CAMEL-11613)

camel-spring-boot - Add auto configuration for FluentProducerTemplate

[CAMEL-11594](https://issues.apache.org/jira/browse/CAMEL-11594)

rest configuration in spring boot should use map instead of list

[CAMEL-11577](https://issues.apache.org/jira/browse/CAMEL-11577)

apt plugin should generate URL as URL and not U R L in displayName

### New Feature (2)

[CAMEL-10744](https://issues.apache.org/jira/browse/CAMEL-10744)

Camel Salesforce maven plugin should generate JSON schema

[CAMEL-10743](https://issues.apache.org/jira/browse/CAMEL-10743)

Add support in Salesforce component for plain JSON input and output

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).