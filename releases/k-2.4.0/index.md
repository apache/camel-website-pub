# Apache camel-k 2.4.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-2.4.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-2.4.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-2.4.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-2.4.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-2.4.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-client-2.4.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-2.4.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-sources-2.4.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-sources-2.4.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.4.0/camel-k-sources-2.4.0.tar.gz.sha512) |
| [sbom.json](https://archive.apache.org/dist/camel/camel-k/2.4.0/sbom.json) (SBOM) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.4.0/sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.4.0/sbom.json.sha512) |

## Git tag checkout

Release is tagged with `v2.4.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v2.4.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#5706](https://github.com/apache/camel-k/issues/5706)

Integration status condition typo

[#5680](https://github.com/apache/camel-k/issues/5680)

OpenAPI & Telemetry traits skipped for sourceless

[#5678](https://github.com/apache/camel-k/issues/5678)

Release 2.4.0

[#5666](https://github.com/apache/camel-k/issues/5666)

Jolokia trait failure

[#5654](https://github.com/apache/camel-k/issues/5654)

Add support for mounting volumes with mount trait

[#5652](https://github.com/apache/camel-k/issues/5652)

Add TimeoutSeconds to knative-service trait

[#5632](https://github.com/apache/camel-k/issues/5632)

Installation tests are unstable

[#5620](https://github.com/apache/camel-k/issues/5620)

Trait annotations saved on the IntegrationKit resource

[#5615](https://github.com/apache/camel-k/issues/5615)

Deprecate \`kamel install\` and change default installation to kustomize/helm/olm?

[#5601](https://github.com/apache/camel-k/issues/5601)

Set default containers resources

[#5598](https://github.com/apache/camel-k/issues/5598)

Bring back Quarkus native test in PR

[#5577](https://github.com/apache/camel-k/issues/5577)

Consistently support "cloudEventsType" property in Pipes source/sink

[#5541](https://github.com/apache/camel-k/issues/5541)

Promote Integration operator warning

[#5537](https://github.com/apache/camel-k/issues/5537)

Unable to specify any CloudEvent attributes or extensions, except for \`type\`

[#5535](https://github.com/apache/camel-k/issues/5535)

Pipe with Addressable as \`sink\` does crash and does not report anything on the status

[#5531](https://github.com/apache/camel-k/issues/5531)

Pipe not correctly reconciled after updating it

[#5529](https://github.com/apache/camel-k/issues/5529)

property "type" must be provided when reading from the Broker

[#5528](https://github.com/apache/camel-k/issues/5528)

Incorrect status handling of beersource when it can not connect to its 3rd party web-service

[#5484](https://github.com/apache/camel-k/issues/5484)

Remove CAMEL\_K\_TEST\_SKIP\_PROBLEMATIC flag

[#5481](https://github.com/apache/camel-k/issues/5481)

Disable Jib telemetry/update check

[#5476](https://github.com/apache/camel-k/issues/5476)

JVM trait refactoring

[#5472](https://github.com/apache/camel-k/issues/5472)

Skip surefire when building the IntegrationKit

[#5460](https://github.com/apache/camel-k/issues/5460)

Add a deploy make target

[#5446](https://github.com/apache/camel-k/issues/5446)

Knative Trigger creation is only based on event type attribute

[#5407](https://github.com/apache/camel-k/issues/5407)

Remove container.imageWasKit

[#5351](https://github.com/apache/camel-k/issues/5351)

Health trait: Inconsistent Integration condition ready status

[#5315](https://github.com/apache/camel-k/issues/5315)

fatal error: concurrent map read and map write

[#5314](https://github.com/apache/camel-k/issues/5314)

Deprecate Spectrum publishing strategy

[#5309](https://github.com/apache/camel-k/issues/5309)

Sourceless Integration status show default provider/version

[#5304](https://github.com/apache/camel-k/issues/5304)

TestHelmOperatorUpgrade error

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).