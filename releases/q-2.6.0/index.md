# Apache camel-quarkus 2.6.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-2.6.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/2.6.0/apache-camel-quarkus-2.6.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/2.6.0/apache-camel-quarkus-2.6.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/2.6.0/apache-camel-quarkus-2.6.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `2.6.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 2.6.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#3382](https://github.com/apache/camel-quarkus/issues/3382)

protobuf: Missing method "getName" when using contentTypeFormat=json in native mode

[#3381](https://github.com/apache/camel-quarkus/issues/3381)

Use the Quarkiverse Artemis BOM and upgrade to 1.0.2

[#3377](https://github.com/apache/camel-quarkus/issues/3377)

Ban log4j-core and log4j-slf4j-impl

[#3375](https://github.com/apache/camel-quarkus/issues/3375)

Remove com.amazonaws:aws-java-sdk-swf-libraries from the BOM

[#3374](https://github.com/apache/camel-quarkus/issues/3374)

XSLT integration-test fails on Windows 10

[#3372](https://github.com/apache/camel-quarkus/issues/3372)

Exclude maven-artifact from camel-quarkus-debezium-mongodb

[#3364](https://github.com/apache/camel-quarkus/issues/3364)

Ban javax.enterprise:cdi-api in favor of jakarta.enterprise:jakarta.enterprise.cdi-api

[#3363](https://github.com/apache/camel-quarkus/issues/3363)

Ban geronimo-jms\_\*\_spec

[#3361](https://github.com/apache/camel-quarkus/issues/3361)

Ban com.sun.activation:javax.activation

[#3358](https://github.com/apache/camel-quarkus/issues/3358)

\`vertx-kafka\` extension incompatible with \`kafka-clients\` 3.0.0

[#3356](https://github.com/apache/camel-quarkus/issues/3356)

aws-lambda: itest failing when run against the real AWS API

[#3348](https://github.com/apache/camel-quarkus/issues/3348)

Bindy extension should avoid hard coding the resource path for \`NativeImageResourceDirectoryBuildItem\`

[#3340](https://github.com/apache/camel-quarkus/issues/3340)

\[JDK17\]kudu:integration test failed in native mode

[#3336](https://github.com/apache/camel-quarkus/pull/3336)

:white\_check\_mark: Kafka Oauth Integration test with Strimzi and Keyc…

[#3335](https://github.com/apache/camel-quarkus/issues/3335)

Ban com.google.code.findbugs:jsr305 unconditionally

[#3329](https://github.com/apache/camel-quarkus/issues/3329)

Camel Quarkus Kafka extension dev services support should check for the availability of \`kafka.bootstrap.servers\`

[#3321](https://github.com/apache/camel-quarkus/issues/3321)

camel-quarkus-support-\* source JARs should have manifests

[#3318](https://github.com/apache/camel-quarkus/issues/3318)

Document that \`vertx-websocket\` consumers run on the Quarkus Vert.x web server

[#3280](https://github.com/apache/camel-quarkus/issues/3280)

FOP integration test failed in native mode

[#3243](https://github.com/apache/camel-quarkus/issues/3243)

Consider removing \`camel-quarkus-support-common\`

[#3179](https://github.com/apache/camel-quarkus/issues/3179)

\`quarkus.camel.main.shutdown.timeout\` doesn't work as intended

[#2978](https://github.com/apache/camel-quarkus/issues/2978)

\[Camel 3.12\] New feature: route configurations

[#2872](https://github.com/apache/camel-quarkus/issues/2872)

\[Quarkus 2.5\] Example with kafka + Oauth2 needs the stimzi Oauth client

[#2606](https://github.com/apache/camel-quarkus/issues/2606)

Test AWS2 SQS in isolation

[#2151](https://github.com/apache/camel-quarkus/issues/2151)

JFR Native support

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).