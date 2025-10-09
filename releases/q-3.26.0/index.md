# Apache camel-quarkus 3.26.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.26.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.26.0/apache-camel-quarkus-3.26.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.26.0/apache-camel-quarkus-3.26.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.26.0/apache-camel-quarkus-3.26.0-src.zip.sha512) |
| [apache-camel-quarkus-3.26.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.26.0/apache-camel-quarkus-3.26.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.26.0/apache-camel-quarkus-3.26.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.26.0/apache-camel-quarkus-3.26.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.26.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.26.0/apache-camel-quarkus-3.26.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.26.0/apache-camel-quarkus-3.26.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.26.0/apache-camel-quarkus-3.26.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.26.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.26.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#7640](https://github.com/apache/camel-quarkus/issues/7640)

Move CamelContext RUNTIME\_INIT customizations to CamelContextCustomizer

[#7638](https://github.com/apache/camel-quarkus/issues/7638)

Debezium: oracle native test fails if is executed as a part of debezium-grouped

[#7632](https://github.com/apache/camel-quarkus/issues/7632)

Jasypt not finding password in application.properties

[#7607](https://github.com/apache/camel-quarkus/issues/7607)

Add netty example

[#7601](https://github.com/apache/camel-quarkus/issues/7601)

Add spring-redis example

[#7593](https://github.com/apache/camel-quarkus/issues/7593)

Add Aws2-s3 example

[#7588](https://github.com/apache/camel-quarkus/issues/7588)

Add AMQP example

[#7586](https://github.com/apache/camel-quarkus/issues/7586)

Deprecate camel-quarkus-langchain4j extension

[#7585](https://github.com/apache/camel-quarkus/issues/7585)

Use WireMock for Olingo4 tests

[#7572](https://github.com/apache/camel-quarkus/issues/7572)

Enable disabled InfinispanTest#query test

[#7565](https://github.com/apache/camel-quarkus/issues/7565)

\[3.25.0\] Cannot invoke "org.apache.camel.spi.ManagementNameStrategy.getName()" because the return value of "org.apache.camel.CamelContext.getManagementNameStrategy()" is null

[#7558](https://github.com/apache/camel-quarkus/issues/7558)

Integration of beans annotated with @Identifier only partially works

[#7555](https://github.com/apache/camel-quarkus/issues/7555)

Mail-microsoft-oauth: test should delete the sent email in case the route fails to do it

[#7547](https://github.com/apache/camel-quarkus/issues/7547)

Route option in camel-mail searchTerm.subject doesn't work in Native

[#7534](https://github.com/apache/camel-quarkus/issues/7534)

Quarkus Jackson JQ extension uses legacy config classes

[#7532](https://github.com/apache/camel-quarkus/issues/7532)

Cassandra Quarkus extension uses legacy config classes

[#7530](https://github.com/apache/camel-quarkus/issues/7530)

Add iso8583 extension

[#7304](https://github.com/apache/camel-quarkus/issues/7304)

Remove io.quarkiverse.amazonservices:quarkus-amazon-services-bom

[#7054](https://github.com/apache/camel-quarkus/issues/7054)

ManagedCamelContext dump stats methods do not work in native mode

[#6978](https://github.com/apache/camel-quarkus/issues/6978)

Review extension config phase values

[#6593](https://github.com/apache/camel-quarkus/issues/6593)

Remove Swagger ModelResolverSubstitutions

[#5679](https://github.com/apache/camel-quarkus/issues/5679)

Intermittent failure of EipTest.throttle

[#5675](https://github.com/apache/camel-quarkus/issues/5675)

Intermittent failure of JasyptSecureExtensionConfigTest.secureDirectComponentTimeout

[#5244](https://github.com/apache/camel-quarkus/issues/5244)

Fop native failures due to pdfbox 3 upgrade

[#4089](https://github.com/apache/camel-quarkus/issues/4089)

ftps tests are failing on camel-main

[#4069](https://github.com/apache/camel-quarkus/issues/4069)

Test Framework :: Junit5 :: Extension Tests: live reload causes problems in \`camel-main\` night builds

[#3230](https://github.com/apache/camel-quarkus/issues/3230)

"exit code 137" in Tika native test on GH actions

[#2810](https://github.com/apache/camel-quarkus/issues/2810)

FtpsIT fails intermittently on the CI

[#2407](https://github.com/apache/camel-quarkus/issues/2407)

bindy: data format locales may not be applied in native mode

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).