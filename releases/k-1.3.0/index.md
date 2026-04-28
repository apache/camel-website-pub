# Apache camel-k 1.3.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-1.3.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-1.3.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-1.3.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-1.3.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-1.3.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-client-1.3.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-1.3.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-sources-1.3.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-sources-1.3.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.3.0/camel-k-sources-1.3.0.tar.gz.sha512) |

## Git tag checkout

Release is tagged with `v1.3.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v1.3.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#1867](https://github.com/apache/camel-k/issues/1867)

Release 1.3.0

[#1842](https://github.com/apache/camel-k/issues/1842)

Groovy example is broken

[#1813](https://github.com/apache/camel-k/issues/1813)

Telegram Kamlet sets CloudEvent source attribute to Knative sink

[#1803](https://github.com/apache/camel-k/issues/1803)

Remove main runtime from operator codebase

[#1771](https://github.com/apache/camel-k/issues/1771)

Use registry secrets for both pulling and pushing

[#1761](https://github.com/apache/camel-k/issues/1761)

Move released images to a hub without rate limits

[#1760](https://github.com/apache/camel-k/issues/1760)

Ability to configure PodDisruptionBudget for integrations

[#1740](https://github.com/apache/camel-k/issues/1740)

Add suport for gists

[#1675](https://github.com/apache/camel-k/issues/1675)

Define default global Kamelets

[#1654](https://github.com/apache/camel-k/issues/1654)

Enable SinkBinding automatically

[#1562](https://github.com/apache/camel-k/issues/1562)

Remove support for Main runtime for integrations

[#1549](https://github.com/apache/camel-k/issues/1549)

Auto-detect json in yaml syntax

[#1537](https://github.com/apache/camel-k/issues/1537)

Provide yaml schema of design definition

[#1321](https://github.com/apache/camel-k/issues/1321)

Add a nodeport option to the service trait

[#1308](https://github.com/apache/camel-k/issues/1308)

Misleading error message in knative trait: cannot find event default

[#1267](https://github.com/apache/camel-k/issues/1267)

Expose operator related metrics

[#1186](https://github.com/apache/camel-k/issues/1186)

Add time it takes to build a kit in the builder pod log

[#1185](https://github.com/apache/camel-k/issues/1185)

Document the --config option in the kamel CLI

[#1135](https://github.com/apache/camel-k/issues/1135)

Basic module structure for Camel K projects

[#751](https://github.com/apache/camel-k/issues/751)

Make sure global and local operators can cohexist

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).