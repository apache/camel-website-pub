# Apache camel-k 2.10.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-2.10.0-linux-amd64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.10.0/camel-k-client-2.10.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-2.10.0-linux-arm64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.10.0/camel-k-client-2.10.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-2.10.0-darwin-amd64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.10.0/camel-k-client-2.10.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-2.10.0-darwin-arm64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.10.0/camel-k-client-2.10.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-2.10.0-windows-amd64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.10.0/camel-k-client-2.10.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-client-2.10.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-2.10.0.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.10.0/camel-k-sources-2.10.0.tar.gz) (Sources) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-sources-2.10.0.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.10.0/camel-k-sources-2.10.0.tar.gz.sha512) |
| [sbom.json](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.10.0/sbom.json) (SBOM) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.10.0/sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.10.0/sbom.json.sha512) |

## Git tag checkout

Release is tagged with `v2.10.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v2.10.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6552](https://github.com/apache/camel-k/issues/6552)

Release 2.10.0

[#6546](https://github.com/apache/camel-k/issues/6546)

Event logging may be broken after switch to newer dependency

[#6541](https://github.com/apache/camel-k/issues/6541)

Review actions used by the CI and include in the Apache allow list

[#6537](https://github.com/apache/camel-k/issues/6537)

Commonly used dependencies should be set on integration plaftorm and/or profile

[#6536](https://github.com/apache/camel-k/issues/6536)

'kamel version' command should only report to be deprecated when operator version is requested.

[#6534](https://github.com/apache/camel-k/issues/6534)

ECR Create-on-Push with EKS Pod Identity

[#6533](https://github.com/apache/camel-k/issues/6533)

\[Helm\] Camel-K Operator sharding via Helm is broken.

[#6530](https://github.com/apache/camel-k/issues/6530)

Deprecate Synthetic Integration

[#6529](https://github.com/apache/camel-k/issues/6529)

Upgrade maven to 3.9 or 4.x

[#6515](https://github.com/apache/camel-k/issues/6515)

GitOps triggered when moving from "Build Complete" to Deploying

[#6512](https://github.com/apache/camel-k/issues/6512)

GitOps kustomization all profile new line

[#6498](https://github.com/apache/camel-k/issues/6498)

Plain Quarkus 3.31.x not working

[#6494](https://github.com/apache/camel-k/issues/6494)

Upgrade to ctrl.runtime 0.23.1

[#6450](https://github.com/apache/camel-k/issues/6450)

Add an E2E blog explaining the details of the 2.9 gitops feature

[#6447](https://github.com/apache/camel-k/issues/6447)

Build from Maven project contained in monorepo

[#6440](https://github.com/apache/camel-k/issues/6440)

GPG sign \`kamel\` CLI

[#6434](https://github.com/apache/camel-k/issues/6434)

Please claim ArtifactHub ownership for this charts repo

[#6432](https://github.com/apache/camel-k/issues/6432)

Trait jvm should accept more than one certificate in caCert

[#6421](https://github.com/apache/camel-k/issues/6421)

Enable GitOps Pipe

[#6420](https://github.com/apache/camel-k/issues/6420)

Make gitops work with dry-build

[#6345](https://github.com/apache/camel-k/issues/6345)

Use a fixed tag instad of main starting from apache kamelets 4.15.0 release

[#6284](https://github.com/apache/camel-k/issues/6284)

Create integration from non maven git repo, i.e. only dsl

[#5986](https://github.com/apache/camel-k/issues/5986)

Use base image SHA instead of tag

[#5072](https://github.com/apache/camel-k/issues/5072)

Support kubernetes Gateway API

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).