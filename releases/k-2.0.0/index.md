# Apache camel-k 2.0.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-2.0.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-2.0.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-2.0.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-2.0.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-2.0.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-client-2.0.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-2.0.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-sources-2.0.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-sources-2.0.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.0.0/camel-k-sources-2.0.0.tar.gz.sha512) |

## Git tag checkout

Release is tagged with `v2.0.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v2.0.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#4582](https://github.com/apache/camel-k/issues/4582)

Release 2.0.0

[#4560](https://github.com/apache/camel-k/issues/4560)

Give the possibility to add a maven profile to an Integration project

[#4525](https://github.com/apache/camel-k/issues/4525)

Builder image name missing the organization configuration

[#4476](https://github.com/apache/camel-k/issues/4476)

Can't install Camel-K 2.0 nightly on OpenShift cluster

[#4430](https://github.com/apache/camel-k/issues/4430)

SBOM for Camel K

[#4429](https://github.com/apache/camel-k/issues/4429)

Use maven distribution available in the operator image

[#4297](https://github.com/apache/camel-k/issues/4297)

Operator is not able to push builder image to the internal registry (OpenShift cluster)

[#4282](https://github.com/apache/camel-k/issues/4282)

Camel K 2.0 release process

[#4281](https://github.com/apache/camel-k/issues/4281)

Transform the Build into a Pipeline

[#4241](https://github.com/apache/camel-k/issues/4241)

Builder pod that hit timeout is not terminated

[#4198](https://github.com/apache/camel-k/issues/4198)

Cannot copy local runtime dependencies

[#4179](https://github.com/apache/camel-k/issues/4179)

Camel K 2.x upgrade 1.x strategy

[#4177](https://github.com/apache/camel-k/issues/4177)

Customize Builder resources when Quarkus Native

[#4163](https://github.com/apache/camel-k/issues/4163)

property with dollar sign and brackets replaced with emtpy value

[#4160](https://github.com/apache/camel-k/issues/4160)

Kamel cli reset/uninstall --all does not clean the camelcatalog

[#4148](https://github.com/apache/camel-k/issues/4148)

Multi architecture support - Operator and builder pods

[#4126](https://github.com/apache/camel-k/issues/4126)

Bring an option to force an image build to the kamel run command

[#4086](https://github.com/apache/camel-k/issues/4086)

Nightly release fail after 2.0

[#4080](https://github.com/apache/camel-k/issues/4080)

Secret managers parsing errors

[#4026](https://github.com/apache/camel-k/issues/4026)

Remove all deprecated code in 1.x version

[#3831](https://github.com/apache/camel-k/issues/3831)

Build refactoring (to address runtime decoupling)

[#3803](https://github.com/apache/camel-k/issues/3803)

Improve error reporting in case of knative is required but not installed

[#2931](https://github.com/apache/camel-k/issues/2931)

Release documentation: Review steps and make it a bit more complete for new release manager

[#2633](https://github.com/apache/camel-k/issues/2633)

Camel-K Tracing Trait error

[#2625](https://github.com/apache/camel-k/issues/2625)

A better name for KameletBinding

[#2622](https://github.com/apache/camel-k/issues/2622)

Kamel 1.5.1 CLI generates broken zsh completions

[#2485](https://github.com/apache/camel-k/issues/2485)

ImagePullBackOff when node failed

[#2474](https://github.com/apache/camel-k/issues/2474)

Debug seems not to work on knative pods

[#2418](https://github.com/apache/camel-k/issues/2418)

Groovy script JSON paring runs into java.util.ServiceConfigurationError: org.apache.groovy.json.FastStringServiceFactory: org.apache.groovy.json.DefaultFastStringServiceFactory not a subtype

[#1980](https://github.com/apache/camel-k/issues/1980)

Add support for multiple data types and schemas in Kamelets

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).