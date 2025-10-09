# Apache camel-quarkus 3.22.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.22.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.22.0/apache-camel-quarkus-3.22.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.22.0/apache-camel-quarkus-3.22.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.22.0/apache-camel-quarkus-3.22.0-src.zip.sha512) |
| [apache-camel-quarkus-3.22.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.22.0/apache-camel-quarkus-3.22.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.22.0/apache-camel-quarkus-3.22.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.22.0/apache-camel-quarkus-3.22.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.22.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.22.0/apache-camel-quarkus-3.22.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.22.0/apache-camel-quarkus-3.22.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.22.0/apache-camel-quarkus-3.22.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.22.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.22.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#7286](https://github.com/apache/camel-quarkus/issues/7286)

Aws2-s3 tests fail on FIPS machine.

[#7280](https://github.com/apache/camel-quarkus/issues/7280)

It is worng checking when looking for the default bean

[#7275](https://github.com/apache/camel-quarkus/issues/7275)

Jasypt tests fail on FIPS machine

[#7272](https://github.com/apache/camel-quarkus/issues/7272)

Drop Camel http from Knative consumers

[#7269](https://github.com/apache/camel-quarkus/issues/7269)

Couchdb is disabled until ibm/java-sdk-core updates gson

[#7262](https://github.com/apache/camel-quarkus/issues/7262)

Quarkiverse-amazonservices bom should be removed from the test-bom and azure-core-http-client-vertx

[#7257](https://github.com/apache/camel-quarkus/issues/7257)

git integration tests fail due to java.lang.IllegalAccessError for org.eclipse.jgit.dircache.DirCache$DirCacheVersion

[#7254](https://github.com/apache/camel-quarkus/issues/7254)

Camel Quarkus JPA can not work with the named persistence unit

[#7226](https://github.com/apache/camel-quarkus/issues/7226)

Ldap: Quarkus like configuration and tests refactor

[#7219](https://github.com/apache/camel-quarkus/issues/7219)

Smooks: EDI incompatibility with Scala versions

[#7217](https://github.com/apache/camel-quarkus/issues/7217)

Ldap: use certificate-generator for the tests

[#7189](https://github.com/apache/camel-quarkus/issues/7189)

Ban com.google.auto.value:auto-value-annotations

[#7188](https://github.com/apache/camel-quarkus/issues/7188)

Camel 4.11 - Add camel-dfdl extension

[#7166](https://github.com/apache/camel-quarkus/issues/7166)

azure-files component support in quarkus

[#7119](https://github.com/apache/camel-quarkus/issues/7119)

Onboard Camel-Opentelemetry2

[#7105](https://github.com/apache/camel-quarkus/issues/7105)

Quarkus Example using yaml route only

[#7104](https://github.com/apache/camel-quarkus/issues/7104)

Camel 4.11 - Add IBM Secrets Manager Extension

[#7085](https://github.com/apache/camel-quarkus/issues/7085)

Camel Quarkus 3.19.0/Quarkus 3.19.1 ignores empty body in .when() statement

[#7068](https://github.com/apache/camel-quarkus/issues/7068)

Switch Pinecone testing from WireMock to container emulator

[#6771](https://github.com/apache/camel-quarkus/issues/6771)

DataFormat endpoints ignore camel.dataformat.\* configuration properties

[#6733](https://github.com/apache/camel-quarkus/issues/6733)

Register files under default routes inclusion locations as HotDeploymentWatchedFile

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).