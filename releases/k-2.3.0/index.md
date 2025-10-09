# Apache camel-k 2.3.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-2.3.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-2.3.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-2.3.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-2.3.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-2.3.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-client-2.3.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-2.3.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-sources-2.3.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-sources-2.3.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.3.0/camel-k-sources-2.3.0.tar.gz.sha512) |
| [sbom.json](https://archive.apache.org/dist/camel/camel-k/2.3.0/sbom.json) (SBOM) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.3.0/sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.3.0/sbom.json.sha512) |

## Git tag checkout

Release is tagged with `v2.3.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v2.3.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#5277](https://github.com/apache/camel-k/issues/5277)

Release 2.3.0

[#5244](https://github.com/apache/camel-k/pull/5244)

Azure Key Vault Trait: Support Azure Identity as authentication method

[#5242](https://github.com/apache/camel-k/issues/5242)

Pipe error handler not working with Camel 4.4.0

[#5238](https://github.com/apache/camel-k/issues/5238)

Integration builds fail with arm64 base image

[#5231](https://github.com/apache/camel-k/issues/5231)

Update buil/Dokerfile to use go 1.21

[#5195](https://github.com/apache/camel-k/issues/5195)

Builder property failure when using non xml tag characters

[#5156](https://github.com/apache/camel-k/issues/5156)

Kamel delete KameletBinding only removes integration resource

[#5143](https://github.com/apache/camel-k/issues/5143)

Performance regression due to configmap/secrets whole cluster watch

[#5120](https://github.com/apache/camel-k/issues/5120)

Monitor Camel Integrations in K8s Deployments

[#5112](https://github.com/apache/camel-k/issues/5112)

Externally built Integrations are deployed without a command in Camel-K 2.2.0

[#5108](https://github.com/apache/camel-k/issues/5108)

Coverage report wrong percentage

[#5084](https://github.com/apache/camel-k/issues/5084)

Operator is stuck in a "deploying" phase loop when internal deployment fails indefinitely

[#5060](https://github.com/apache/camel-k/issues/5060)

Operator 2.2.0 does not spawn builder pod with strategy: pod

[#5054](https://github.com/apache/camel-k/issues/5054)

Run a different set of checks for java dependencies

[#5037](https://github.com/apache/camel-k/issues/5037)

Provide a page linking to Camel DSLs

[#5033](https://github.com/apache/camel-k/issues/5033)

Nightly SBOM procedure should not run if there are no changes

[#5028](https://github.com/apache/camel-k/issues/5028)

Mac github actions failing

[#5027](https://github.com/apache/camel-k/issues/5027)

Polish trait conditions

[#5023](https://github.com/apache/camel-k/issues/5023)

Nightly release soft failure

[#5017](https://github.com/apache/camel-k/issues/5017)

Unable to authenticate with Docker Hub API v2

[#5014](https://github.com/apache/camel-k/issues/5014)

Data type Kamelet hardcoded

[#4991](https://github.com/apache/camel-k/issues/4991)

Release 2.2.0

[#4983](https://github.com/apache/camel-k/issues/4983)

Azure Key Vault Trait: Support Azure Identity as authentication method

[#4977](https://github.com/apache/camel-k/issues/4977)

Improve pipe status when the pod is full of exceptions

[#4811](https://github.com/apache/camel-k/issues/4811)

Use generated trait

[#4795](https://github.com/apache/camel-k/issues/4795)

Upgrade to Go 1.21

[#4776](https://github.com/apache/camel-k/issues/4776)

1st Integration after Camel K runtime version update failing

[#4759](https://github.com/apache/camel-k/issues/4759)

KameletBinding could not find a topic with a different \`metadata.name\` and \`topicName\`.

[#4747](https://github.com/apache/camel-k/issues/4747)

Provide alternative publishing strategy via pipeline

[#4542](https://github.com/apache/camel-k/issues/4542)

Build waiting condition

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).