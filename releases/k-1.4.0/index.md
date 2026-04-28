# Apache camel-k 1.4.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-1.4.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-1.4.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-1.4.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-1.4.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-1.4.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-client-1.4.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-1.4.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-sources-1.4.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-sources-1.4.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.4.0/camel-k-sources-1.4.0.tar.gz.sha512) |

## Git tag checkout

Release is tagged with `v1.4.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v1.4.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#2164](https://github.com/apache/camel-k/issues/2164)

Review generated CSV

[#2158](https://github.com/apache/camel-k/issues/2158)

Normalize object references

[#2149](https://github.com/apache/camel-k/issues/2149)

Ability to provide Maven repository CA certificates

[#2134](https://github.com/apache/camel-k/issues/2134)

Release 1.4.0

[#2109](https://github.com/apache/camel-k/issues/2109)

Consuming from more than 1 knative channel is broken

[#2090](https://github.com/apache/camel-k/issues/2090)

Error when using an external kit

[#2083](https://github.com/apache/camel-k/issues/2083)

cli: add a binding sub command

[#2043](https://github.com/apache/camel-k/issues/2043)

kamelet-binding: support for processing steps

[#2009](https://github.com/apache/camel-k/issues/2009)

Can't mount secrets with binary data

[#1983](https://github.com/apache/camel-k/issues/1983)

Allow to scaffold a Kamelet via kamel init

[#1930](https://github.com/apache/camel-k/issues/1930)

Warnings on getting operator versions

[#1928](https://github.com/apache/camel-k/issues/1928)

Provide a way to use kamelet ID in binding

[#1881](https://github.com/apache/camel-k/issues/1881)

Corrupted binaries attached as resource

[#1840](https://github.com/apache/camel-k/issues/1840)

Make Knative endpoints and kameletbinding work with broker without explicit event type

[#1799](https://github.com/apache/camel-k/issues/1799)

Implementing a global build strategy

[#1738](https://github.com/apache/camel-k/issues/1738)

Add a cli subcommand to inspect dependencies required by an Integration

[#1693](https://github.com/apache/camel-k/issues/1693)

Camel K installed globally by default

[#1664](https://github.com/apache/camel-k/issues/1664)

camel-K installation failed with Helm on GKE

[#1652](https://github.com/apache/camel-k/issues/1652)

Add a warning when operating from a CLI with a different installed Operator version

[#1547](https://github.com/apache/camel-k/issues/1547)

Increase trait test coverage

[#1507](https://github.com/apache/camel-k/issues/1507)

Adding camel-jackson dependency creates issues with inner classes

[#1299](https://github.com/apache/camel-k/issues/1299)

Reference to IntegrationKit metdata in Builder CR

[#1159](https://github.com/apache/camel-k/issues/1159)

Implement kit\_create command's flags test

[#1158](https://github.com/apache/camel-k/issues/1158)

Implement install command's flags test

[#1157](https://github.com/apache/camel-k/issues/1157)

Implement delete command's flags test

[#1156](https://github.com/apache/camel-k/issues/1156)

Implement builder command's flags test

[#886](https://github.com/apache/camel-k/issues/886)

kamel --output option should not need deploy resources to cluster

[#681](https://github.com/apache/camel-k/issues/681)

Build controller service / operator

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).