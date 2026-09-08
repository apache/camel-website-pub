# Apache camel-k 2.11.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-2.11.0-linux-amd64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.11.0/camel-k-client-2.11.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-2.11.0-linux-arm64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.11.0/camel-k-client-2.11.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-2.11.0-darwin-amd64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.11.0/camel-k-client-2.11.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-2.11.0-darwin-arm64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.11.0/camel-k-client-2.11.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-2.11.0-windows-amd64.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.11.0/camel-k-client-2.11.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-client-2.11.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-2.11.0.tar.gz](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.11.0/camel-k-sources-2.11.0.tar.gz) (Sources) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-sources-2.11.0.tar.gz.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.11.0/camel-k-sources-2.11.0.tar.gz.sha512) |
| [sbom.json](https://www.apache.org/dyn/closer.lua/camel/camel-k/2.11.0/sbom.json) (SBOM) | [PGP Signature](https://downloads.apache.org/camel/camel-k/2.11.0/sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-k/2.11.0/sbom.json.sha512) |

## Git tag checkout

Release is tagged with `v2.11.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v2.11.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6764](https://github.com/apache/camel-k/issues/6764)

Drop support for deprecated Jolokia trait

[#6753](https://github.com/apache/camel-k/issues/6753)

OLM installation note

[#6741](https://github.com/apache/camel-k/issues/6741)

Release 2.11.0

[#6738](https://github.com/apache/camel-k/issues/6738)

keda trait cannot set trigger-level metricType — CPU/memory scalers broken on KEDA v2.18+

[#6737](https://github.com/apache/camel-k/issues/6737)

Reduce the deprecation scope for Pod template

[#6733](https://github.com/apache/camel-k/issues/6733)

Don't create IntegrationKit outside own or operator namespace

[#6730](https://github.com/apache/camel-k/issues/6730)

CONTAINER\_IMAGE is empty unless the Kustomize replacements step runs (Helm / raw-manifest installs)

[#6724](https://github.com/apache/camel-k/issues/6724)

Support for setting enableServiceLinks on the pod spec template

[#6705](https://github.com/apache/camel-k/issues/6705)

Feature parity between IntegrationProfile and IntegrationPlatform

[#6698](https://github.com/apache/camel-k/issues/6698)

Don't use pull secret from environment

[#6691](https://github.com/apache/camel-k/issues/6691)

Camel-k Operator sharding broken again due to hardcoded name for registry-reader in ClusterRoleBinding

[#6648](https://github.com/apache/camel-k/issues/6648)

Deprecate Knative (eventing) trait

[#6644](https://github.com/apache/camel-k/issues/6644)

Cannot use custom components easily

[#6623](https://github.com/apache/camel-k/issues/6623)

Deprecate old camel k runtime

[#6616](https://github.com/apache/camel-k/issues/6616)

Operator tenancy model

[#6615](https://github.com/apache/camel-k/issues/6615)

Integration with missing operator metadata not working

[#6580](https://github.com/apache/camel-k/issues/6580)

Remove MavenSpec.Extension

[#6579](https://github.com/apache/camel-k/issues/6579)

Remove MavenBuildSpec.Servers (was used by registry trait only)

[#6578](https://github.com/apache/camel-k/issues/6578)

IntegrationProfile controller watch

[#6577](https://github.com/apache/camel-k/issues/6577)

Deprecate profile concept

[#6576](https://github.com/apache/camel-k/issues/6576)

Deprecate image puller delegation

[#6516](https://github.com/apache/camel-k/issues/6516)

Promote the usage of Camel Monitor operator as monitoring tool

[#6508](https://github.com/apache/camel-k/issues/6508)

Allow specifying CPU/Memory resources for Init and Sidecar Containers

[#6497](https://github.com/apache/camel-k/issues/6497)

Owner trait: add all labels and annotations

[#6489](https://github.com/apache/camel-k/issues/6489)

Change trait documentation to reflect yaml spec vs CLI spec

[#5462](https://github.com/apache/camel-k/issues/5462)

Build container images to run as non root

[#5024](https://github.com/apache/camel-k/issues/5024)

Make healt trait as default

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).