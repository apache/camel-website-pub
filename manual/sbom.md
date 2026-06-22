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

### Camel Spring Boot and Camel Quarkus (Maven projects)

For Maven-based projects (Camel Spring Boot or Camel Quarkus), add the [CycloneDX Maven Plugin](https://github.com/CycloneDX/cyclonedx-maven-plugin) to your `pom.xml`:

```xml
<plugin>
    <groupId>org.cyclonedx</groupId>
    <artifactId>cyclonedx-maven-plugin</artifactId>
    <version>2.9.1</version>
    <executions>
        <execution>
            <phase>package</phase>
            <goals>
                <goal>makeBom</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

Running `mvn package` will then produce a CycloneDX SBOM alongside your application artifact.

This is a standard Maven plugin and works identically for both Camel Spring Boot and Camel Quarkus projects. Nothing Camel-specific is required.

> **Tip**
> Check [the plugin’s repository](https://github.com/CycloneDX/cyclonedx-maven-plugin) for the latest version, and see the plugin documentation for options such as output format (JSON or XML), output directory, and component scope filtering.

## Analyzing SBOMs

Once generated, an SBOM can be fed into vulnerability scanners and compliance tools. For example, [OWASP Dependency-Track](https://dependencytrack.org/) can ingest CycloneDX SBOMs and continuously monitor for known CVEs across your dependency tree.