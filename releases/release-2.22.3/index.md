# Apache camel 2.22.3 Release

## New and Noteworthy

This release is a minor update of the 2.22.x branch.

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
      <version>2.22.3</version>
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
      <version>2.22.3</version>
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
| [apache-camel-2.22.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.22.3/apache-camel-2.22.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.22.3/apache-camel-2.22.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.22.3/apache-camel-2.22.3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.22.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.22.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (37)

[CAMEL-13125](https://issues.apache.org/jira/browse/CAMEL-13125)

Camel-MongoDB: Endpoint shutdown closes mongo connection, killing the connection for everyone

[CAMEL-13123](https://issues.apache.org/jira/browse/CAMEL-13123)

Endpoint shutdown closes mongo connection, killing the connection for everyone

[CAMEL-13098](https://issues.apache.org/jira/browse/CAMEL-13098)

Camel-google-mail: Stream component doesn't work in OSGi

[CAMEL-13093](https://issues.apache.org/jira/browse/CAMEL-13093)

Output of route-profile is empty if there are same route-id for multiple camel-contexts.

[CAMEL-13077](https://issues.apache.org/jira/browse/CAMEL-13077)

Olingo4 Consumer appears to not work with backoffIdleThreshold

[CAMEL-13063](https://issues.apache.org/jira/browse/CAMEL-13063)

Olingo2Endpoint swallowing consumer. options

[CAMEL-13062](https://issues.apache.org/jira/browse/CAMEL-13062)

olingo2 component serviceUri not set

[CAMEL-13061](https://issues.apache.org/jira/browse/CAMEL-13061)

Missing properties on Olingo2 consumer initialisation

[CAMEL-13059](https://issues.apache.org/jira/browse/CAMEL-13059)

camel-olingo2 assumes '/' at end of URI

[CAMEL-13058](https://issues.apache.org/jira/browse/CAMEL-13058)

AbstractFutureCallback generates NPE when response is a 401

[CAMEL-13054](https://issues.apache.org/jira/browse/CAMEL-13054)

Olingo4Endpoint swallowing consumer. options

[CAMEL-13049](https://issues.apache.org/jira/browse/CAMEL-13049)

Karaf commands that start/resume contexts and routes should use proper TCCL

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

[CAMEL-13008](https://issues.apache.org/jira/browse/CAMEL-13008)

Odata-connector assumes '/' at end of URI

[CAMEL-13006](https://issues.apache.org/jira/browse/CAMEL-13006)

Missing properties on Olingo4 consumer initialisation

[CAMEL-13005](https://issues.apache.org/jira/browse/CAMEL-13005)

olingo4 component serviceUri not set

[CAMEL-12994](https://issues.apache.org/jira/browse/CAMEL-12994)

xquery syntax problem in SpringDSL with spring-boot

[CAMEL-12987](https://issues.apache.org/jira/browse/CAMEL-12987)

camel-core-osgi: OsgiServiceRegistry.onContextStop never gets called.

[CAMEL-12985](https://issues.apache.org/jira/browse/CAMEL-12985)

TransactionErrorHandler fails if UnitOfWork is null -- This seems to happen sometimes with intercepted routes

[CAMEL-12980](https://issues.apache.org/jira/browse/CAMEL-12980)

Bundle in 'Active' State but Camel Context not initialized

[CAMEL-12974](https://issues.apache.org/jira/browse/CAMEL-12974)

Route coverage: When and otherwise are not marked as covered

[CAMEL-12969](https://issues.apache.org/jira/browse/CAMEL-12969)

camel-core-osgi: Slow Memory Leak in OsgiServiceRegistry

[CAMEL-12942](https://issues.apache.org/jira/browse/CAMEL-12942)

camel-dropbox: upload file does not work

[CAMEL-12940](https://issues.apache.org/jira/browse/CAMEL-12940)

Dynamic doneFileName is not working with filename containing 2 dots

[CAMEL-12933](https://issues.apache.org/jira/browse/CAMEL-12933)

Camel FTP regression: RemoteFile does not override populateHeaders method

[CAMEL-12932](https://issues.apache.org/jira/browse/CAMEL-12932)

Camel-AHC-WS: Consumer parameters are not set

[CAMEL-12916](https://issues.apache.org/jira/browse/CAMEL-12916)

camel-http4 - The sslContextParameters option should be documented on endpoint as well

[CAMEL-12911](https://issues.apache.org/jira/browse/CAMEL-12911)

gzip Content-Encoding problems after upgrading to Jetty 9.4.12

[CAMEL-12899](https://issues.apache.org/jira/browse/CAMEL-12899)

Handle LinkedIn Captcha redirects gracefully

[CAMEL-12835](https://issues.apache.org/jira/browse/CAMEL-12835)

camel-json-validator - Potential issue with reading from streams

[CAMEL-12774](https://issues.apache.org/jira/browse/CAMEL-12774)

Error during type conversion from type: java.lang.String to the required type: org.elasticsearch.action.update.UpdateRequest

### Improvement (9)

[CAMEL-13114](https://issues.apache.org/jira/browse/CAMEL-13114)

Provide single Cookie header for multiple cookies

[CAMEL-13072](https://issues.apache.org/jira/browse/CAMEL-13072)

In DefaultUnitOfWork:popRouteContext() avoid exception thrown

[CAMEL-13066](https://issues.apache.org/jira/browse/CAMEL-13066)

camel-hystrix - Do not fallback on HystrixBadRequestException

[CAMEL-13042](https://issues.apache.org/jira/browse/CAMEL-13042)

camel-core - File producer should by default not allow writing files to directories outside its starting directory

[CAMEL-13035](https://issues.apache.org/jira/browse/CAMEL-13035)

Camel telegram - Update made to channel not received by camel application

[CAMEL-13029](https://issues.apache.org/jira/browse/CAMEL-13029)

camel-swagger-java - Should default use scheme from rest-dsl configuration in swagger doc

[CAMEL-13025](https://issues.apache.org/jira/browse/CAMEL-13025)

camel-core - File read lock changed - If file gets deleted then break out loop

[CAMEL-12935](https://issues.apache.org/jira/browse/CAMEL-12935)

Camel Context restarts in Blueprint Test if isCreateCamelContextPerClass is set to true

[CAMEL-12631](https://issues.apache.org/jira/browse/CAMEL-12631)

SFTP: Socket timeout overwrites Server Alive Interval

### New Feature (1)

[CAMEL-13015](https://issues.apache.org/jira/browse/CAMEL-13015)

camel-spring-boot - load multiple route xml files

### Task (1)

[CAMEL-13041](https://issues.apache.org/jira/browse/CAMEL-13041)

Camel-AWS MQ: Create Broker operation is not working

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).