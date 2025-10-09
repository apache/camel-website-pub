# Apache camel-quarkus 3.0.0-M2 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.0.0-M2-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.0.0-M2/apache-camel-quarkus-3.0.0-M2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.0.0-M2/apache-camel-quarkus-3.0.0-M2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.0.0-M2/apache-camel-quarkus-3.0.0-M2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `3.0.0-M2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.0.0-M2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#4885](https://github.com/apache/camel-quarkus/issues/4885)

Remove the local upgrade of maven-resolver used by mvnw once we upgrade to mvnw 3.9.2

[#4881](https://github.com/apache/camel-quarkus/issues/4881)

Snmp: cover snmp v3 for POLL operation

[#4860](https://github.com/apache/camel-quarkus/issues/4860)

simple("${exchange.getMessage().getBody()}") causes a MethodNotFoundException in native mode

[#4855](https://github.com/apache/camel-quarkus/issues/4855)

Stop managing woodstox directly, rather rely on quarkus-cxf-bom

[#4850](https://github.com/apache/camel-quarkus/issues/4850)

Snmp: Extend coverage of some smaller features

[#4843](https://github.com/apache/camel-quarkus/issues/4843)

Snmp: Extend coverage for supported versions

[#4842](https://github.com/apache/camel-quarkus/issues/4842)

CI build fails to download Maven artifacts due to: \` java.net.ConnectException: Connection timed out\`

[#4839](https://github.com/apache/camel-quarkus/issues/4839)

Remove org.apache.cxf:cxf-codegen plugin (cxf-sopak extension is used instead)

[#4832](https://github.com/apache/camel-quarkus/issues/4832)

Cannot find eclipse-formatter-config.xml when an example is copied out of examples source tree.

[#4823](https://github.com/apache/camel-quarkus/issues/4823)

Camel quartz job silently removed if io.quarkus.scheduler.Scheduled is in use

[#4821](https://github.com/apache/camel-quarkus/issues/4821)

Add tests and usage guide for LDAP extension

[#4811](https://github.com/apache/camel-quarkus/issues/4811)

FHIR integration test native image build fails

[#4799](https://github.com/apache/camel-quarkus/issues/4799)

\[camel-main\] Add \`quarkus-jackson-jq-extra\` to jq extension runtime module dependencies

[#4797](https://github.com/apache/camel-quarkus/issues/4797)

Smnp: Extend test coverage

[#4789](https://github.com/apache/camel-quarkus/issues/4789)

Test OpenTelemetry extension integration with \`opentelemetry-jdbc\`

[#4781](https://github.com/apache/camel-quarkus/issues/4781)

Intermittent failure of MyBatisConsumerTest

[#4773](https://github.com/apache/camel-quarkus/issues/4773)

\[camel-main\] ObservabilityTest.metrics in examples fails

[#4752](https://github.com/apache/camel-quarkus/issues/4752)

CamelJdbcTest leaks a statement

[#4749](https://github.com/apache/camel-quarkus/issues/4749)

java-joor-dsl - Add templated route support to native mode

[#4746](https://github.com/apache/camel-quarkus/issues/4746)

CXF generates different WSDL files with JVM/Native modes

[#4745](https://github.com/apache/camel-quarkus/issues/4745)

\[camel-main\] Csimple: Cannot find compiled csimple language for expression: Hello ${body}

[#4741](https://github.com/apache/camel-quarkus/issues/4741)

Missing \`@Component\` annotation for \`QuarkusVertxWebsocketComponent\`

[#4735](https://github.com/apache/camel-quarkus/issues/4735)

\[camel-main\] Foundation: BeanTest.parameterTypes fails with the current Camel main

[#4731](https://github.com/apache/camel-quarkus/issues/4731)

java-joor-dsl - Add support of inner classes

[#4727](https://github.com/apache/camel-quarkus/issues/4727)

\[Quarkus 3.0.0.CR2\] Performance regression introduced in Camel Quarkus 3.0.0-M1

[#4723](https://github.com/apache/camel-quarkus/issues/4723)

Intermittent failure in Jdbc native tests

[#4717](https://github.com/apache/camel-quarkus/issues/4717)

Expand came-quarkus-mybatis test coverage

[#4716](https://github.com/apache/camel-quarkus/issues/4716)

java-joor-dsl - Add RegisterForReflection annotation support

[#4712](https://github.com/apache/camel-quarkus/issues/4712)

\[camel-main\] Groovy support causes CI failure

[#4711](https://github.com/apache/camel-quarkus/issues/4711)

Add Build-Date in MANIFEST.MF in Camel Quarkus release JARs

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).