# Apache camel-quarkus 2.12.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-2.12.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/2.12.0/apache-camel-quarkus-2.12.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/2.12.0/apache-camel-quarkus-2.12.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/2.12.0/apache-camel-quarkus-2.12.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `2.12.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 2.12.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#4028](https://github.com/apache/camel-quarkus/issues/4028)

AWS SQS test sqsAutoCreateDelayedQueue fails

[#4027](https://github.com/apache/camel-quarkus/issues/4027)

Debezium test DebeziumSqlserverTest fails

[#4021](https://github.com/apache/camel-quarkus/issues/4021)

Dropbox integration test authentication failure

[#4016](https://github.com/apache/camel-quarkus/issues/4016)

perf-regression: JDK 17 support

[#4015](https://github.com/apache/camel-quarkus/issues/4015)

perf-regression: disable itests when -D quickly is passed

[#4014](https://github.com/apache/camel-quarkus/issues/4014)

perf-regression: java.lang.NumberFormatException: For input string: "782,36"

[#4004](https://github.com/apache/camel-quarkus/issues/4004)

perf-regression: avoid using fixed port

[#4001](https://github.com/apache/camel-quarkus/issues/4001)

perf-regression: complete unit test coverage

[#3995](https://github.com/apache/camel-quarkus/issues/3995)

CEQ 2.11 - rest component .route() method not available but present in docs

[#3993](https://github.com/apache/camel-quarkus/issues/3993)

\`quarkus.camel.routes-discovery.exclude-patterns\` does not work when the \`RouteBuilder\` is a CDI bean

[#3982](https://github.com/apache/camel-quarkus/issues/3982)

perf-regression: add integration-tests

[#3979](https://github.com/apache/camel-quarkus/issues/3979)

\`perf-regression\` module should not import \`io.quarkus.platform:quarkus-bom\`

[#3978](https://github.com/apache/camel-quarkus/issues/3978)

Duplicate BOM dependency declaration \`org.apache.santuario:xmlsec\`

[#3974](https://github.com/apache/camel-quarkus/issues/3974)

perf-regression: Use pure Camel transformation

[#3971](https://github.com/apache/camel-quarkus/issues/3971)

Register \`HttpOperationFailedException\` for reflection

[#3967](https://github.com/apache/camel-quarkus/issues/3967)

perf-regression: introduce the performance regression in the release process

[#3966](https://github.com/apache/camel-quarkus/issues/3966)

CxfSoapClientIT.wsSecurityClient fails in native mode: wsse:Nonce not present in the request

[#3964](https://github.com/apache/camel-quarkus/issues/3964)

\[Quarkus 2.12.0\] Azure Storage Blob native integration test failure

[#3961](https://github.com/apache/camel-quarkus/issues/3961)

\[Quarkus 2.12.0\] Figure out how to test \`js-dsl\` in native mode

[#3960](https://github.com/apache/camel-quarkus/issues/3960)

perf-regression: Align to the root mvnw

[#3957](https://github.com/apache/camel-quarkus/issues/3957)

Google-pubsub remove @TestMethodOrder from the tests and investigate closing error

[#3947](https://github.com/apache/camel-quarkus/issues/3947)

\[Quarkus 2.12.0\] Secure gRPC consumer tests are failing

[#3946](https://github.com/apache/camel-quarkus/issues/3946)

camel-quarkus-servicenow - 2.11.0 release - java.lang.ClassNotFoundException: javax.ws.rs.client.ClientRequestFilter

[#3942](https://github.com/apache/camel-quarkus/issues/3942)

\[Camel 3.19.0\] Dependency covergence check failure in HDFS extension

[#3923](https://github.com/apache/camel-quarkus/issues/3923)

Add camel-quarkus-master example

[#3910](https://github.com/apache/camel-quarkus/issues/3910)

Improve google-pubsub test coverage

[#3905](https://github.com/apache/camel-quarkus/issues/3905)

Merge the performance regression prototype in camel-quarkus main

[#3822](https://github.com/apache/camel-quarkus/issues/3822)

Test Azure Storage Blob with \`credentialType\` \`AZURE\_IDENTITY\`

[#3529](https://github.com/apache/camel-quarkus/issues/3529)

\`CamelMainRoutesIncludePatternWithAbsoluteFilePrefixDevModeTest\` fails on Windows

[#3511](https://github.com/apache/camel-quarkus/issues/3511)

CamelTestSupport style of testing

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).