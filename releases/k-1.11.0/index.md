# Apache camel-k 1.11.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-1.11.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-1.11.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-1.11.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-1.11.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-1.11.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-client-1.11.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-1.11.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-sources-1.11.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-sources-1.11.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/1.11.0/camel-k-sources-1.11.0.tar.gz.sha512) |

## Git tag checkout

Release is tagged with `v1.11.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v1.11.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#3840](https://github.com/apache/camel-k/issues/3840)

Remove deprecated Kubernetes API

[#3837](https://github.com/apache/camel-k/issues/3837)

Release 1.11.0

[#3790](https://github.com/apache/camel-k/issues/3790)

Deprecate overlapping Kamel CLI features in favour of Camel JBang

[#3761](https://github.com/apache/camel-k/issues/3761)

Ready condition message not always taken from Camel Health Check

[#3732](https://github.com/apache/camel-k/pull/3732)

Fixes licenses in pkg

[#3729](https://github.com/apache/camel-k/pull/3729)

Fixed licenses for addons

[#3706](https://github.com/apache/camel-k/pull/3706)

Added Support for Azure Key Vault addon

[#3697](https://github.com/apache/camel-k/pull/3697)

GCP Vault Support leveraging Camel-Google-Secret-Manager Properties Function

[#3696](https://github.com/apache/camel-k/pull/3696)

chore(api): Add validation to trait enum parameters in CRDs

[#3691](https://github.com/apache/camel-k/pull/3691)

fix: Use SIGTERM and SIGINT aware context for bootstrap operations

[#3689](https://github.com/apache/camel-k/pull/3689)

More docs AWS Secrets Manager Vault

[#3688](https://github.com/apache/camel-k/pull/3688)

chore(trait): Deprecate cached discovery option from GC trait

[#3684](https://github.com/apache/camel-k/pull/3684)

Adds the default maven repositories if extra ones are added

[#3683](https://github.com/apache/camel-k/pull/3683)

Added docs for AWS Secrets Manager Vault trait

[#3682](https://github.com/apache/camel-k/pull/3682)

fix(#3671): Fix native mode for KameletBinding

[#3679](https://github.com/apache/camel-k/pull/3679)

Added Support AWS Secrets Manager Vault from Camel

[#3674](https://github.com/apache/camel-k/pull/3674)

feat(cli): promote allow Integration update

[#3660](https://github.com/apache/camel-k/pull/3660)

fix(#3657): Use OPERATOR\_ID EnvVar consistently

[#3654](https://github.com/apache/camel-k/issues/3654)

camel k 0.11.0 helm - Error: parse error at (camel-k/templates/operator.yaml:87): "-en"

[#3640](https://github.com/apache/camel-k/pull/3640)

feat(controller/cli): improve handling of invalid components & dependencies against Camel catalog

[#3631](https://github.com/apache/camel-k/pull/3631)

feat(cli): Allow to set build publish strategy options from install cmd

[#3626](https://github.com/apache/camel-k/pull/3626)

feat(cmd/run): secret/configmap as runtime/build-time properties

[#3624](https://github.com/apache/camel-k/pull/3624)

doc: generate Resume trait doc

[#3623](https://github.com/apache/camel-k/pull/3623)

feat(cli): Add add-repo command to add a repo for custom Kamelet catalog

[#3599](https://github.com/apache/camel-k/pull/3599)

feat(cli): Add a config command to manage the default settings

[#3595](https://github.com/apache/camel-k/pull/3595)

fix: Prevent operator panic on wrong Kamelet binding

[#3594](https://github.com/apache/camel-k/pull/3594)

feat(ci): smoke test before nightly release

[#3589](https://github.com/apache/camel-k/pull/3589)

feat(cli): Add tail flag to the log command

[#3572](https://github.com/apache/camel-k/issues/3572)

Run E2E test before nightly releases

[#3571](https://github.com/apache/camel-k/pull/3571)

feat(metadata): raise error when capability/dependency not resolved in CamelCatalog

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).