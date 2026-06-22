# Generating SBOMs

A Software Bill of Materials (SBOM) is a machine-readable inventory of every component in your software: direct dependencies, transitive dependencies, and their versions. SBOMs have become a key building block in supply chain security, enabling automated vulnerability scanning and license compliance analysis.

With the EU Cyber Resilience Act (CRA) requiring SBOM delivery for software sold in the EU, and US Executive Order 14028 making SBOMs a federal procurement expectation, many organizations now treat SBOM generation as a hard requirement.

## Camel releases ship with SBOMs

Starting from Camel 4.0.3, every release ships with PGP-signed CycloneDX SBOMs (JSON and XML) covering all Camel modules and their dependencies. These are available on the [download page](/download/) alongside the release artifacts.

## Generating SBOMs for your own applications

To produce an SBOM for _your_ Camel application (as opposed to the framework itself), choose the approach that matches your runtime.

### Camel CLI

The Camel CLI has a built-in `sbom` command that generates an SBOM for your integration project without any extra tooling.

```bash
camel sbom
```

This produces a `sbom.json` file in CycloneDX format by default.

To use SPDX format instead:

```bash
camel sbom --sbom-format=spdx
```

To generate for a specific target runtime:

```bash
camel sbom --runtime=spring-boot
```

```bash
camel sbom --runtime=quarkus
```

The output format can be switched between JSON and XML:

```bash
camel sbom --sbom-output-format=xml
```

See the [camel sbom command reference](jbang-commands/camel-jbang-sbom.md) for all available options.

### Camel Spring Boot

Spring Boot 3.3+ has [built-in SBOM support](https://spring.io/blog/2024/05/24/sbom-support-in-spring-boot-3-3/): it generates a CycloneDX SBOM during the build, packages it inside the uber jar at `META-INF/sbom/application.cdx.json`, and can expose it via an actuator endpoint. Since Camel Spring Boot runs on top of Spring Boot, this automatically covers Camel and all its transitive dependencies — no extra plugin or Camel-specific configuration needed.

### Camel Quarkus

Quarkus has its own dependency resolver that differs from standard Maven resolution, which means the generic CycloneDX Maven plugin will not capture the full dependency graph. Instead, use the native [Quarkus CycloneDX extension](https://quarkus.io/guides/cyclonedx). Add it to your project:

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-cyclonedx</artifactId>
</dependency>
```

This generates a distribution SBOM automatically every time you build. You can also generate a dependency SBOM before building with `mvn quarkus:dependency-sbom`.

## Analyzing SBOMs

Once generated, an SBOM can be fed into vulnerability scanners and compliance tools. For example, [OWASP Dependency-Track](https://dependencytrack.org/) can ingest CycloneDX SBOMs and continuously monitor for known CVEs across your dependency tree.