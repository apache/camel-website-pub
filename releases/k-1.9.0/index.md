# Apache camel-k 1.9.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-1.9.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-1.9.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-1.9.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-1.9.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-1.9.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-client-1.9.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-1.9.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-sources-1.9.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-sources-1.9.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.9.0/camel-k-sources-1.9.0.tar.gz.sha512) |

## Git tag checkout

Release is tagged with `v1.9.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v1.9.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#3138](https://github.com/apache/camel-k/issues/3138)

Prepare for releasing Camel-K with Camel 3.16.0

[#2891](https://github.com/apache/camel-k/issues/2891)

Makefile Release staging: Pass the remote repository name as argument with origin as default

[#2890](https://github.com/apache/camel-k/issues/2890)

Release note script: Check if the GITHUB\_TOKEN var has been set before running the command

[#2436](https://github.com/apache/camel-k/issues/2436)

kamelet binding annotation should be propagated to the integration

[#2375](https://github.com/apache/camel-k/issues/2375)

languages: support kamelet eip

[#2370](https://github.com/apache/camel-k/issues/2370)

kamelet binding: use the Kamelet EIP for steps

[#2238](https://github.com/apache/camel-k/issues/2238)

Camel K CLI asks for an OpenAPI v2 when also v3 is supported

[#2232](https://github.com/apache/camel-k/issues/2232)

Traits to configure the container image and location fo the sources

[#1843](https://github.com/apache/camel-k/issues/1843)

Lower priority of modeline options

[#1802](https://github.com/apache/camel-k/issues/1802)

Use local registry config from cluster

[#1706](https://github.com/apache/camel-k/issues/1706)

Istio sidecar injection is enabled for builder pod

[#1691](https://github.com/apache/camel-k/issues/1691)

Integration controller issue

[#1476](https://github.com/apache/camel-k/issues/1476)

Kamel run fails to pull in camel-k-builder after installing with helm

[#1227](https://github.com/apache/camel-k/issues/1227)

Let dependencies be defined using file URLs

[#1155](https://github.com/apache/camel-k/issues/1155)

Write doc about file based configuration for kamel CLI

[#1028](https://github.com/apache/camel-k/issues/1028)

Deployment not found while replacing CamelSource

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).