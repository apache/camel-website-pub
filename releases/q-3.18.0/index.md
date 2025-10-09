# Apache camel-quarkus 3.18.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.18.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.18.0/apache-camel-quarkus-3.18.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.18.0/apache-camel-quarkus-3.18.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.18.0/apache-camel-quarkus-3.18.0-src.zip.sha512) |
| [apache-camel-quarkus-3.18.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.18.0/apache-camel-quarkus-3.18.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.18.0/apache-camel-quarkus-3.18.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.18.0/apache-camel-quarkus-3.18.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.18.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.18.0/apache-camel-quarkus-3.18.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.18.0/apache-camel-quarkus-3.18.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.18.0/apache-camel-quarkus-3.18.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.18.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.18.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6927](https://github.com/apache/camel-quarkus/issues/6927)

Smooks support

[#6922](https://github.com/apache/camel-quarkus/issues/6922)

Add a JMS Component customizer if Artemis JMS RA is availiable

[#6909](https://github.com/apache/camel-quarkus/issues/6909)

Ssh: extend test coverage

[#6905](https://github.com/apache/camel-quarkus/issues/6905)

Add an integration test for using artemis jms jca connector

[#6896](https://github.com/apache/camel-quarkus/issues/6896)

HTTP producer throws StackOverflowError in native mode when extracting the response body as stream

[#6888](https://github.com/apache/camel-quarkus/issues/6888)

Replace @SessionScoped with @ApplicationScoped in Camel CXF

[#6880](https://github.com/apache/camel-quarkus/issues/6880)

cxf-soap example - Why use \`@SessionScoped\` for the CXF endpoints?

[#6866](https://github.com/apache/camel-quarkus/issues/6866)

\[Quarkus LangChain4j 0.23.x\] AI services should be resolvable by name

[#6831](https://github.com/apache/camel-quarkus/issues/6831)

Build time Kamelet processing may result in \`StackOverflowError \`

[#6720](https://github.com/apache/camel-quarkus/issues/6720)

Camel 4.9 - camel-fury extension

[#6492](https://github.com/apache/camel-quarkus/issues/6492)

Junit5-extension-test DoubleRoutesPerClassTest is disabled (possibly would be removed)

[#5230](https://github.com/apache/camel-quarkus/issues/5230)

Kamelet extension unable to serialize objects of type class org.apache.camel.impl.engine.DefaultResourceResolvers$ClasspathResolver$1 to bytecode

[#3773](https://github.com/apache/camel-quarkus/issues/3773)

Debezium bom messes with cassandraQL driver unit tests since Debezium 1.19.2.Final

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).