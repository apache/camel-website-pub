# Apache camel-k 1.10.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-1.10.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-1.10.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-1.10.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-1.10.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-1.10.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-client-1.10.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-1.10.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-sources-1.10.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-sources-1.10.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.10.0/camel-k-sources-1.10.0.tar.gz.sha512) |

## Git tag checkout

Release is tagged with `v1.10.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v1.10.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#3588](https://github.com/apache/camel-k/pull/3588)

Update the staging repository for camel-k-runtime 1.14.0

[#3564](https://github.com/apache/camel-k/pull/3564)

Camel k runtime 1.14.0 as Default

[#3560](https://github.com/apache/camel-k/issues/3560)

1.10.0 Release

[#3557](https://github.com/apache/camel-k/pull/3557)

chore: add pod tolerations options to operator

[#3556](https://github.com/apache/camel-k/pull/3556)

feat(cli): Force arguments for the rebuild command

[#3554](https://github.com/apache/camel-k/pull/3554)

migrate and improve languages example

[#3552](https://github.com/apache/camel-k/pull/3552)

chore: Upgrade k8s and Knative dependencies

[#3546](https://github.com/apache/camel-k/pull/3546)

Feat(trait): Knative service visibility support

[#3544](https://github.com/apache/camel-k/pull/3544)

fix(trait): force a volume path when key is set

[#3499](https://github.com/apache/camel-k/pull/3499)

fix(cli): more user-friendly error messages for kamel local subcommands

[#3471](https://github.com/apache/camel-k/pull/3471)

fix(trait): nil pointer dereference when applying traits during kit building

[#3445](https://github.com/apache/camel-k/issues/3445)

\`kamel rebuild\` default should not rebuild all Integrations

[#3441](https://github.com/apache/camel-k/issues/3441)

CPU Spikes on Openshift with unusual operator behaviour

[#3381](https://github.com/apache/camel-k/issues/3381)

Update to Knative v1.5.0

[#3325](https://github.com/apache/camel-k/pull/3325)

feat(cli): environment promotion

[#3317](https://github.com/apache/camel-k/pull/3317)

chore(build): let bom managed by camel k runtime

[#2213](https://github.com/apache/camel-k/issues/2213)

\`kamel local build\` doesn't support same dependency notation

[#1614](https://github.com/apache/camel-k/issues/1614)

Traits configuration schema

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).