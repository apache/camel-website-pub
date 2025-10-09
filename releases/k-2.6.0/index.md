# Apache camel-k 2.6.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-2.6.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-2.6.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-2.6.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-2.6.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-2.6.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-client-2.6.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-2.6.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-sources-2.6.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-sources-2.6.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.6.0/camel-k-sources-2.6.0.tar.gz.sha512) |
| [sbom.json](https://archive.apache.org/dist/camel/camel-k/2.6.0/sbom.json) (SBOM) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.6.0/sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.6.0/sbom.json.sha512) |

## Git tag checkout

Release is tagged with `v2.6.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v2.6.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6062](https://github.com/apache/camel-k/issues/6062)

Release 2.6.0

[#6049](https://github.com/apache/camel-k/issues/6049)

Test arm-64 github actions runners

[#6030](https://github.com/apache/camel-k/issues/6030)

Can't install Camel-K operator using a local maven repository.

[#6021](https://github.com/apache/camel-k/issues/6021)

Quarkus native is not yet using native source mode

[#6014](https://github.com/apache/camel-k/issues/6014)

Prometheus PodMonitor for Knative is incorrectly generated

[#6002](https://github.com/apache/camel-k/issues/6002)

Telemetry addon configuration not working

[#5999](https://github.com/apache/camel-k/issues/5999)

Camel Quarkus (plain) runtime usage

[#5998](https://github.com/apache/camel-k/issues/5998)

\`kamel promote\` GitOps

[#5987](https://github.com/apache/camel-k/issues/5987)

Quarkus runtime deprecated configuration

[#5981](https://github.com/apache/camel-k/issues/5981)

Ingress Trait to support an array on the path

[#5958](https://github.com/apache/camel-k/issues/5958)

Change Kamelet Distribution - provide your own catalog method

[#5951](https://github.com/apache/camel-k/issues/5951)

Installation page should report the version

[#5950](https://github.com/apache/camel-k/issues/5950)

Add installation instructions in github release page

[#5933](https://github.com/apache/camel-k/issues/5933)

Do not fail if sources are exclusively passed via configuration file.

[#5928](https://github.com/apache/camel-k/issues/5928)

Kustomize common labels deprecated

[#5923](https://github.com/apache/camel-k/issues/5923)

Add a note to clarify about deprecation policy

[#5920](https://github.com/apache/camel-k/issues/5920)

Flaky Docker build process

[#5917](https://github.com/apache/camel-k/issues/5917)

Support File Based Catalog

[#5910](https://github.com/apache/camel-k/issues/5910)

Drop Camel K CRDs dependency?

[#5903](https://github.com/apache/camel-k/issues/5903)

Custom resource generation should always use a fixed tooling version

[#5894](https://github.com/apache/camel-k/issues/5894)

How to troubleshoot Maven configuration

[#5890](https://github.com/apache/camel-k/issues/5890)

Fix doc failure on compatibility matrix

[#5877](https://github.com/apache/camel-k/issues/5877)

Bump Golang version to 1.23

[#5858](https://github.com/apache/camel-k/issues/5858)

Remove github.com/mitchellh/mapstructure dependency

[#5811](https://github.com/apache/camel-k/issues/5811)

Set default resource for builder Pods

[#5810](https://github.com/apache/camel-k/issues/5810)

Report missing Maven Proxy in IntegrationPlatform conditions

[#5809](https://github.com/apache/camel-k/issues/5809)

Report usage of insecure registry in IntegrationPlatform conditions

[#5805](https://github.com/apache/camel-k/issues/5805)

Every component (like the builder) should use Java 21 as it is the current LTS version

[#5787](https://github.com/apache/camel-k/issues/5787)

Move addons into trait

[#5771](https://github.com/apache/camel-k/issues/5771)

Deprecate Openshift specific features

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).