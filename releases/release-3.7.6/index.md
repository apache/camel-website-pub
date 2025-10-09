# Apache camel 3.7.6 Release

## New and Noteworthy

This release is the new Camel 3.7.6 LTS release.

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
      <version>3.7.6</version>
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
      <version>3.7.6</version>
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
| [apache-camel-3.7.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.7.6/apache-camel-3.7.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.7.6/apache-camel-3.7.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.7.6/apache-camel-3.7.6-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.7.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.7.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (14)

[CAMEL-17011](https://issues.apache.org/jira/browse/CAMEL-17011)

camel-ssh - The producer should not be singleton

[CAMEL-17004](https://issues.apache.org/jira/browse/CAMEL-17004)

camel-servlet - Should not close HttpServletInputStream when reading body into stream caching

[CAMEL-16957](https://issues.apache.org/jira/browse/CAMEL-16957)

NettyHttpHelper appends slash to an URI in case of empty CamelHttpPath

[CAMEL-16936](https://issues.apache.org/jira/browse/CAMEL-16936)

camel-aws2-s3: Not setting CONTENT-MD5 header which breaks putObject with object locks

[CAMEL-16927](https://issues.apache.org/jira/browse/CAMEL-16927)

camel-spring - Using Spring XML can create multiple SpringCamelContext instances causing a deadlock when multiple camel proxies involved

[CAMEL-16922](https://issues.apache.org/jira/browse/CAMEL-16922)

StringHelper.removeLeadingAndEndingQuotes() may cause IndexOutOfBoundsException

[CAMEL-16916](https://issues.apache.org/jira/browse/CAMEL-16916)

camel split with parallel processing true consumes lots of heap space when using camel-ftp

[CAMEL-16877](https://issues.apache.org/jira/browse/CAMEL-16877)

camel-salesforce: any salesforce operation inside transaction times out

[CAMEL-16874](https://issues.apache.org/jira/browse/CAMEL-16874)

PollEnrich with file and option sendEmptyMessageWhenIdle keeps sending empty messages

[CAMEL-16865](https://issues.apache.org/jira/browse/CAMEL-16865)

Xtokenize does not track a level up again once it detects a non matching namespace

[CAMEL-16853](https://issues.apache.org/jira/browse/CAMEL-16853)

camel-xslt: setting resultHandlerFactory via URI is broken

[CAMEL-16807](https://issues.apache.org/jira/browse/CAMEL-16807)

camel-kafka - problem using two kafka connections in the same application

[CAMEL-16802](https://issues.apache.org/jira/browse/CAMEL-16802)

camel-core - Split / Aggregate with parallelprocessing aggregates in random order

[CAMEL-14823](https://issues.apache.org/jira/browse/CAMEL-14823)

Support to disable the stream caching in camel-servlet from the camel context - once more

### Dependency upgrade (1)

[CAMEL-16910](https://issues.apache.org/jira/browse/CAMEL-16910)

Update Commons Compress to 1.21

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).