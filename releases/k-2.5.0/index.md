# Apache camel-k 2.5.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17.

## Apache Camel-K

| Download | Signature and checksum |
| --- | --- |
| [camel-k-client-2.5.0-linux-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-linux-amd64.tar.gz) (Linux AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-linux-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-linux-amd64.tar.gz.sha512) |
| [camel-k-client-2.5.0-linux-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-linux-arm64.tar.gz) (Linux ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-linux-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-linux-arm64.tar.gz.sha512) |
| [camel-k-client-2.5.0-darwin-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-darwin-amd64.tar.gz) (Darwin AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-darwin-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-darwin-amd64.tar.gz.sha512) |
| [camel-k-client-2.5.0-darwin-arm64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-darwin-arm64.tar.gz) (Darwin ARM64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-darwin-arm64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-darwin-arm64.tar.gz.sha512) |
| [camel-k-client-2.5.0-windows-amd64.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-windows-amd64.tar.gz) (Windows AMD64 CLI) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-windows-amd64.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-client-2.5.0-windows-amd64.tar.gz.sha512) |
| [camel-k-sources-2.5.0.tar.gz](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-sources-2.5.0.tar.gz) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-sources-2.5.0.tar.gz.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.5.0/camel-k-sources-2.5.0.tar.gz.sha512) |
| [sbom.json](https://archive.apache.org/dist/camel/camel-k/2.5.0/sbom.json) (SBOM) | [PGP Signature](https://archive.apache.org/dist/camel/camel-k/2.5.0/sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-k/2.5.0/sbom.json.sha512) |

## Git tag checkout

Release is tagged with `v2.5.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-k.git
cd camel-k
git checkout v2.5.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#5901](https://github.com/apache/camel-k/issues/5901)

Support Service trait annotations

[#5887](https://github.com/apache/camel-k/issues/5887)

Release 2.5.0

[#5874](https://github.com/apache/camel-k/issues/5874)

Camel-K creating new KnativeService instead of updating the existing one

[#5869](https://github.com/apache/camel-k/issues/5869)

Deprecate IntegrationProfile

[#5868](https://github.com/apache/camel-k/issues/5868)

Service Binding deprecation and removal

[#5864](https://github.com/apache/camel-k/issues/5864)

Give configurable SizeLimit to emptyDir volumes in mount trait

[#5863](https://github.com/apache/camel-k/issues/5863)

Support Camel 4.8 cloud native properties

[#5855](https://github.com/apache/camel-k/issues/5855)

Jolokia is failing (again)

[#5838](https://github.com/apache/camel-k/issues/5838)

BuilderTrait nodeSelector configuration not working for jvm builds

[#5837](https://github.com/apache/camel-k/issues/5837)

Mark Kotlin as deprecated

[#5836](https://github.com/apache/camel-k/issues/5836)

Integration reconciler error after operator re-install

[#5793](https://github.com/apache/camel-k/issues/5793)

Add ingressClassName field to Ingress trait

[#5758](https://github.com/apache/camel-k/issues/5758)

Error: io.quarkus.vertx.http.runtime.TrustedProxyCheckPartConverter not a subtype

[#5755](https://github.com/apache/camel-k/issues/5755)

Possible deadlock between integration builds

[#5752](https://github.com/apache/camel-k/issues/5752)

Sourceless failure with operator applied ksvc

[#5746](https://github.com/apache/camel-k/issues/5746)

Camel runtime 3.13.0 nightly failure

[#5740](https://github.com/apache/camel-k/issues/5740)

Provide Helm Artefacts as part of snapshots, pre-releases and final-releases

[#5739](https://github.com/apache/camel-k/issues/5739)

Drop support for Tracing trait

[#5737](https://github.com/apache/camel-k/issues/5737)

Drop support for Registry trait

[#5735](https://github.com/apache/camel-k/issues/5735)

Drop support for Swagger (Openapi v2.0) in favour of Openapi 3.0

[#5729](https://github.com/apache/camel-k/issues/5729)

Deprecate openapi trait in favour of Camel openapi setting

[#5723](https://github.com/apache/camel-k/issues/5723)

Move github actions to use Minikube

[#5720](https://github.com/apache/camel-k/issues/5720)

Upgrade to Golang 1.22

[#5522](https://github.com/apache/camel-k/issues/5522)

Enhance environment trait to include values from secrets/configmaps

[#5417](https://github.com/apache/camel-k/issues/5417)

Add a trait func which should check the presence of CamelCatalog before execution

[#5307](https://github.com/apache/camel-k/issues/5307)

Bump kubernetes dependencies to 1.29

[#5211](https://github.com/apache/camel-k/issues/5211)

Upgrade controller-runtime to latest version

[#5088](https://github.com/apache/camel-k/issues/5088)

Quartz builds failing to start when using native builds

[#4661](https://github.com/apache/camel-k/issues/4661)

Reproducible builds

[#4395](https://github.com/apache/camel-k/issues/4395)

Kamelets versioning or Kamelets Catalog definition

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).