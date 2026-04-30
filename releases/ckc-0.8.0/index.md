# Apache camel-kafka-connector 0.8.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 8 and 11.

## Getting the binaries from Maven Central

We maintain a handy table linking to binary packages for the latest release on the [connector list](../../camel-kafka-connector/next/reference/index.md).

For this release you can use Maven Central Repository Search to find and download the binary packages. This search will show the packages from this release: `g:org.apache.camel.kafkaconnector AND l:package AND v:0.8.0`, or you can follow this link to the [search results](https://search.maven.org/search?q=g:org.apache.camel.kafkaconnector%20AND%20l:package%20AND%20v:0.8.0).

## Source Distribution

Source distribution contains all the artifacts Apache Camel project distributes in source form

## Apache Camel Kafka Connector

| Download | Signature and checksum |
| --- | --- |
| [camel-kafka-connector-0.8.0-src.zip](https://archive.apache.org/dist/camel/camel-kafka-connector/0.8.0/camel-kafka-connector-0.8.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-kafka-connector/0.8.0/camel-kafka-connector-0.8.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-kafka-connector/0.8.0/camel-kafka-connector-0.8.0-src.zip.sha512) |
| [Connectors download list](../../camel-kafka-connector/next/reference/index.md) |

## Git tag checkout

Release is tagged with `camel-kafka-connector0.8.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-kafka-connector.git
cd camel-kafka-connector
git checkout camel-kafka-connector-0.8.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#1007](https://github.com/apache/camel-kafka-connector/pull/1007)

Fix problem when call 'context.errantRecordReporter()' will result in a NoSuchMethodException or NoClassDefFoundError when the sink connector is deployed to Connect runtimes older than Kafka 2.6

[#997](https://github.com/apache/camel-kafka-connector/issues/997)

Azure storage blob failing on camel-master

[#980](https://github.com/apache/camel-kafka-connector/issues/980)

camel.source.contentLogLevel config not honored in source connectors

[#979](https://github.com/apache/camel-kafka-connector/issues/979)

Improve description of connector

[#976](https://github.com/apache/camel-kafka-connector/issues/976)

Azure storage queue failing on Camel Master

[#975](https://github.com/apache/camel-kafka-connector/issues/975)

SJMS2 Startup test failing on Camel Master

[#973](https://github.com/apache/camel-kafka-connector/issues/973)

CamelKafkaConnectMain is showing sensitive information in summary

[#923](https://github.com/apache/camel-kafka-connector/issues/923)

Add a map Camel Headers to Kafka headers option to make the behavior configurable

[#922](https://github.com/apache/camel-kafka-connector/issues/922)

Add a map Camel Properties to Kafka headers option to make the behavior configurable

[#913](https://github.com/apache/camel-kafka-connector/issues/913)

Java 14 support

[#908](https://github.com/apache/camel-kafka-connector/issues/908)

Camel-Cron connector: We need to add at least camel-quartz as dependency

[#903](https://github.com/apache/camel-kafka-connector/issues/903)

Add removeHeaders documentation

[#902](https://github.com/apache/camel-kafka-connector/issues/902)

create a toHeader SMT

[#896](https://github.com/apache/camel-kafka-connector/issues/896)

Add a column to compatibility matrix about Kafka version

[#894](https://github.com/apache/camel-kafka-connector/issues/894)

Bump to Strimzi 0.21.1

[#889](https://github.com/apache/camel-kafka-connector/issues/889)

Bump Apicurio Registry to 1.3.2.Final

[#878](https://github.com/apache/camel-kafka-connector/issues/878)

Couchbase dependency missing?

[#876](https://github.com/apache/camel-kafka-connector/issues/876)

Bump to Strimzi 0.21.0

[#875](https://github.com/apache/camel-kafka-connector/issues/875)

Bump to Kafka 2.7.0

[#866](https://github.com/apache/camel-kafka-connector/issues/866)

AWS2-Kinesis: Add examples

[#857](https://github.com/apache/camel-kafka-connector/issues/857)

AWS2-Kinesis connector: Add a transformation to extract only the data from a source stream

[#853](https://github.com/apache/camel-kafka-connector/issues/853)

Github source connector: Add some transforms to deal with the different possible events

[#844](https://github.com/apache/camel-kafka-connector/issues/844)

Camel-Master: SJMS2 it test is failing

[#843](https://github.com/apache/camel-kafka-connector/issues/843)

\[Question\] How to process avro message in S3 connector

[#842](https://github.com/apache/camel-kafka-connector/issues/842)

Remove changelog gh action

[#823](https://github.com/apache/camel-kafka-connector/issues/823)

Add Mongodb examples

[#816](https://github.com/apache/camel-kafka-connector/issues/816)

Support camel dataformat configuration for marshaller/unmarshaller

[#700](https://github.com/apache/camel-kafka-connector/issues/700)

Add test for AWS 2 SNS

[#640](https://github.com/apache/camel-kafka-connector/issues/640)

Create a Twitter timeline example

[#166](https://github.com/apache/camel-kafka-connector/issues/166)

Add tests to camel-kafka-connector-generator-maven-plugin

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).