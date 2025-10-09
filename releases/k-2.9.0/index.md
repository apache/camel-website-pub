# Apache camel-k 2.9.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-2.9.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-2.9.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-2.9.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-2.9.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-2.9.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-client-2.9.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-2.9.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-sources-2.9.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-sources-2.9.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.9.0/camel-k-sources-2.9.0.tar.gz.sha512) |
| [sbom.json](https://archive.apache.org/dist/camel/camel-k/2.9.0/sbom.json) (SBOM) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.9.0/sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.9.0/sbom.json.sha512) |

## Git tag checkout

Release is tagged with `v2.9.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v2.9.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6425](https://github.com/apache/camel-k/issues/6425)

Change caCert params from secrets to files

[#6415](https://github.com/apache/camel-k/issues/6415)

Release 2.9.0

[#6388](https://github.com/apache/camel-k/issues/6388)

Deprecate master trait

[#6364](https://github.com/apache/camel-k/issues/6364)

Plain Quarkus \`--dev\` mode failing

[#6358](https://github.com/apache/camel-k/issues/6358)

Unable to mount configs & resources from the same configmap/secret even with key filtering

[#6353](https://github.com/apache/camel-k/issues/6353)

How to debug Integrations

[#6351](https://github.com/apache/camel-k/issues/6351)

Review TestRunConfigConfigmaps test in \`plain-quarkus\`

[#6342](https://github.com/apache/camel-k/issues/6342)

Remove unsupported code in CLI

[#6341](https://github.com/apache/camel-k/issues/6341)

Dry build - first readiness info

[#6340](https://github.com/apache/camel-k/issues/6340)

Dry build - support Pipe

[#6338](https://github.com/apache/camel-k/issues/6338)

Error when trying to use compression option with "plain-quarkus" provider

[#6336](https://github.com/apache/camel-k/issues/6336)

Camel YAML DSL could not detect beanio

[#6327](https://github.com/apache/camel-k/issues/6327)

\`kamel bind\` to use \`.spec.traits\` instead of annotations

[#6315](https://github.com/apache/camel-k/issues/6315)

Review traits, mark deprecated, not used and internals

[#6314](https://github.com/apache/camel-k/issues/6314)

Deprecate telemetry trait

[#6313](https://github.com/apache/camel-k/issues/6313)

Deprecate logging trait

[#6312](https://github.com/apache/camel-k/issues/6312)

Keda automatic mapping

[#6309](https://github.com/apache/camel-k/issues/6309)

Add Pipe traits

[#6308](https://github.com/apache/camel-k/issues/6308)

Nightly releases failing due to some not authorized action

[#6303](https://github.com/apache/camel-k/issues/6303)

Remove Pipe crossname reference restriction

[#6300](https://github.com/apache/camel-k/issues/6300)

Move off knative types from api package

[#6299](https://github.com/apache/camel-k/issues/6299)

Safer \`kamel reset\`

[#6298](https://github.com/apache/camel-k/issues/6298)

Deprecate CLI commands

[#6288](https://github.com/apache/camel-k/issues/6288)

New KEDA trait

[#6287](https://github.com/apache/camel-k/issues/6287)

Bump nightly-install-olm workflow

[#6137](https://github.com/apache/camel-k/issues/6137)

Integration git, create a PR with integration yaml result after build

[#5846](https://github.com/apache/camel-k/issues/5846)

Use Kamelet catalog coming from Camel distribution dependency

[#5588](https://github.com/apache/camel-k/issues/5588)

Give the operator the possibility to build an Integration without running

[#3877](https://github.com/apache/camel-k/issues/3877)

Health Trait : probe with HTTPS scheme not working

[#2820](https://github.com/apache/camel-k/issues/2820)

JVM trait option to add a trusted root cert on startup

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).