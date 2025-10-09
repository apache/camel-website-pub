# Apache camel-k 2.1.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-2.1.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-2.1.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-2.1.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-2.1.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-2.1.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-client-2.1.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-2.1.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-sources-2.1.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-sources-2.1.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.1.0/camel-k-sources-2.1.0.tar.gz.sha512) |

## Git tag checkout

Release is tagged with `v2.1.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v2.1.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#4786](https://github.com/apache/camel-k/issues/4786)

Camel K doesn't install on a restricted namespace

[#4756](https://github.com/apache/camel-k/issues/4756)

Quarkus image hardcoded

[#4752](https://github.com/apache/camel-k/issues/4752)

Release 2.1.0

[#4687](https://github.com/apache/camel-k/issues/4687)

Update to Knative v1.11

[#4648](https://github.com/apache/camel-k/issues/4648)

Separating Java and native image compilation

[#4647](https://github.com/apache/camel-k/issues/4647)

IntegrationPlatform reconciliation should warn or fail when missing registry

[#4618](https://github.com/apache/camel-k/issues/4618)

Let Camel framework manage Kamelets

[#4613](https://github.com/apache/camel-k/issues/4613)

Upgrade to Go 1.19.x or 1.20.x

[#4612](https://github.com/apache/camel-k/issues/4612)

Bump Kubernetes API to 1.27

[#4534](https://github.com/apache/camel-k/issues/4534)

\`kamel promote\` dry run should not validate

[#4424](https://github.com/apache/camel-k/issues/4424)

Security warning messages from the operator pod on Openshift

[#4166](https://github.com/apache/camel-k/issues/4166)

Redesign traits that have runtime dependencies

[#4118](https://github.com/apache/camel-k/issues/4118)

Camel K could go offline

[#4070](https://github.com/apache/camel-k/issues/4070)

Release script utils: Add a release utils script in Camel K CRD

[#4069](https://github.com/apache/camel-k/issues/4069)

Release script utils: Remove examples upload since they don't exist anymore

[#3890](https://github.com/apache/camel-k/issues/3890)

\`kamel promote\` with new tenancy model

[#3753](https://github.com/apache/camel-k/issues/3753)

Use \`govulncheck\` to check security vulnerabilities

[#3175](https://github.com/apache/camel-k/issues/3175)

Split Operator binary from Kamel CLI binary

[#1721](https://github.com/apache/camel-k/issues/1721)

Document installation on air-gapped clusters

[#1656](https://github.com/apache/camel-k/issues/1656)

jib builder

[#1573](https://github.com/apache/camel-k/issues/1573)

kamelets: architecture documentation

[#1503](https://github.com/apache/camel-k/issues/1503)

Delegate installation to external tools

[#1328](https://github.com/apache/camel-k/issues/1328)

Hide platform traits

[#1235](https://github.com/apache/camel-k/issues/1235)

Automatically redeploy on config change

[#682](https://github.com/apache/camel-k/issues/682)

Tekton build strategy

[#355](https://github.com/apache/camel-k/issues/355)

kamel upgrade

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).