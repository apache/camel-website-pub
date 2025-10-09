# Apache camel-k 1.5.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-1.5.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-1.5.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-1.5.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-1.5.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-1.5.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-client-1.5.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-1.5.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-sources-1.5.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-sources-1.5.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.5.0/camel-k-sources-1.5.0.tar.gz.sha512) |

## Git tag checkout

Release is tagged with `v1.5.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v1.5.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#2470](https://github.com/apache/camel-k/issues/2470)

Release 1.5.0

[#2441](https://github.com/apache/camel-k/issues/2441)

Parameters in YAML DSL are not recognized

[#2357](https://github.com/apache/camel-k/issues/2357)

Maven logs are no longer shown

[#2331](https://github.com/apache/camel-k/issues/2331)

kamelets: add condition to report when an integration is stuck waiting for them

[#2330](https://github.com/apache/camel-k/issues/2330)

Property in cron trait to set \`startingDeadlineSeconds\`

[#2306](https://github.com/apache/camel-k/issues/2306)

Integration container build errors are absent from the log messages

[#2305](https://github.com/apache/camel-k/issues/2305)

Kamel delete should consider KameletBindings

[#2276](https://github.com/apache/camel-k/issues/2276)

Normalize Spectrum build logs

[#2271](https://github.com/apache/camel-k/issues/2271)

kamelets: support for kamelet local beans

[#2268](https://github.com/apache/camel-k/issues/2268)

Normalize Maven build log

[#2237](https://github.com/apache/camel-k/issues/2237)

Add a flag to enable/disable the installation of default kamelets

[#2098](https://github.com/apache/camel-k/issues/2098)

Dependency autoloading is not working correctly with YAML format

[#2080](https://github.com/apache/camel-k/issues/2080)

Kamelet file parameters

[#2003](https://github.com/apache/camel-k/issues/2003)

Revisit configuration options

[#2000](https://github.com/apache/camel-k/issues/2000)

Logging configuration does not affect integrations

[#1945](https://github.com/apache/camel-k/issues/1945)

SinkBinding produces errored pods on 0.18+ / OpenShift Serverless 1.12

[#1941](https://github.com/apache/camel-k/issues/1941)

kamelet-binding : suport for error handling

[#1838](https://github.com/apache/camel-k/issues/1838)

Document secrets for using secrets (and config maps)

[#1831](https://github.com/apache/camel-k/issues/1831)

Add a new configuration type to set build time properties

[#1534](https://github.com/apache/camel-k/issues/1534)

Support custom application.properties for Quarkus builds

[#1502](https://github.com/apache/camel-k/issues/1502)

Fix github landing page

[#1468](https://github.com/apache/camel-k/issues/1468)

Installation on a kind cluster

[#1137](https://github.com/apache/camel-k/issues/1137)

Generate CRD documentation for website

[#580](https://github.com/apache/camel-k/issues/580)

Integration logging configuration

[#185](https://github.com/apache/camel-k/issues/185)

kamel run - compile errors should be more visible

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).