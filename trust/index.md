# Why Apache Camel

Apache Camel has been running in production since 2007. Some of the largest organizations in the world (banks, airlines, hospitals, government agencies, and Fortune 10 companies) route business-critical traffic through Camel every second of every day.

That kind of reliance has to be earned, and it cannot be claimed with a logo or a badge. We earn it the same way on every release: in the open, on a predictable schedule, with security handled transparently, and as a community that answers to no single vendor. Everything below is a matter of public record: you do not have to take our word for any of it. That is what we mean by _trust by default_, and it is the reason to choose Apache Camel.

## A predictable release cadence

Camel ships a new release almost every month, so fixes and improvements reach you in weeks rather than years. Designated **Long Term Support (LTS)** releases receive bug and security fixes for up to a year, giving you a stable target you can plan around. We treat backward compatibility as a feature: the rare breaking change is always documented in the [Migration and Upgrade](../manual/migration-and-upgrade.md) guide, so an upgrade never holds a surprise. The data backs this up: [272 releases over 19 years with zero gaps](../blog/2026/06/camel-always-on/index.md) and a core API so stable that [code from the first commit in 2007 still compiles unchanged](../blog/2026/06/camel-dna-19-years/index.md).

[See the releases](../download/)

## Security handled in the open

Every reported vulnerability is handled through the Apache Software Foundation’s coordinated disclosure process and published as a full, PGP-signed advisory, an unbroken public track record that goes back to 2013. A canonical [Security Model](../manual/security-model.md) documents exactly where the trust boundaries sit and what is in or out of scope, fixes are delivered across every supported LTS line, and we proactively review and harden the framework rather than wait for someone else to find the problem.

[Security & advisories](../security/)

## A busy advisory page is a good sign

Camel 4.21.0 fixed and disclosed [**32 vulnerabilities**](../security/), and every one of them got a full public advisory. The 4.18.3 and 4.14.8 LTS releases shipped the backports within four days. That is what an active security effort looks like from the outside, not a framework springing leaks. Researchers across the industry report their findings to the ASF’s private security list, and we go looking ourselves: when one component turns out to mishandle inbound message headers, we sweep the connector portfolio for the same pattern instead of patching only the one that was reported. That is why advisories arrive in families, and why every reporter is credited by name in the advisory that follows.

Each one costs work you never see: triage against the [Security Model](../manual/security-model.md), a fix with regression tests, a CVE assignment, and a written, signed advisory carrying the affected version ranges and a workaround you can apply today — and then the backport. **26 of those 32 fixes were carried all the way back to the 4.14.x LTS line**, so teams on the older LTS get them without a major upgrade. None of it becomes public until the fixes have shipped, and we publish even when a hardening change has no known exploit path — because the alternative is asking you to trust a silence you cannot check. For the full timeline and the process behind the July 2026 batch — including two fixes that turned out to be incomplete and a vulnerability we introduced ourselves — read [Built to Patch Fast](../blog/2026/07/camel-security-advisories-4.21.0/index.md).

[See every advisory](../security/)

## A vendor-neutral community

Camel is an Apache Software Foundation project, governed by a meritocratic community under the ASF’s open and vendor-neutral model. No single company controls its roadmap, and no one can take it away from you. Development happens entirely in the open on public mailing lists and chat, and anyone is free to read the code, propose a change, review a release, or verify a fix for themselves. The numbers tell the story: [1,500+ contributors from 450+ companies across 20+ countries](../blog/2026/06/camel-by-the-numbers/index.md). And behind those contributors, the [same core engineering team](../blog/2026/07/camel-who-maintains/index.md) has maintained Camel since 2009 — through multiple acquisitions — contributing 80–95% of all commits every single year. When you hit a bug in a component written ten years ago, the person who wrote it is likely still an active committer.

[Meet the community](../community/)

## Proven in production

More than 100 known organizations run Apache Camel in production: UPS processing tens of billions of messages a day, CERN, SAP’s Integration Suite, alongside banks, airlines, healthcare providers, and national governments across six continents. Commercial platforms from Red Hat, SAP, and others are built directly on Camel. Companies don’t contribute patches to software they evaluate — [450+ corporate email domains in the git history](../blog/2026/06/camel-by-the-numbers/index.md) prove production usage no case study can match. One of those stories in detail: [Echonect](../blog/2026/07/echonect-fifteen-years-apache-camel/index.md), one of Europe’s larger SMS gateways, has run on Camel for fifteen years — 500+ messages per second per node, 99.97% uptime, same team, same architecture.

[Who uses Camel](../community/user-stories/index.md)

## Built to last, not to rewrite

Some frameworks reinvent themselves every few years — new APIs, new concepts, painful migrations. Camel does not. The `from().to()` pattern from the [very first commit in 2007](../blog/2026/06/camel-dna-19-years/index.md) still compiles and runs unchanged today. Four major versions, five technology eras (ESBs, SOA, microservices, cloud-native, AI), and the core DNA has stayed stable. You learn Camel once. Your routes, your patterns, and your team’s expertise carry forward — they do not expire with the next major release.

[Read the story](../blog/2026/06/camel-dna-19-years/index.md)

## A proven bug fix track record

The community has fixed [7,070 out of 7,081 reported bugs](../blog/2026/06/camel-bug-fix-track-record/index.md) — a **99.8% resolution rate** — with a median fix time of **1 day**. That track record has been sustained for 17 of the last 19 years across 350+ connectors and 272 production releases. Only 6 bugs are open today. When something breaks, it gets fixed fast, and the data is there to prove it.

[See the data](../blog/2026/06/camel-bug-fix-track-record/index.md)

## 500+ dependencies kept current

Camel manages over 500 third-party dependencies. Across 20 minor releases, the community made [**2,449 dependency version updates**](../blog/2026/06/camel-dependency-updates/index.md) — an average of 122 per release. This quiet, invisible work keeps the framework secure and compatible, so you are not stuck waiting for a critical library upgrade.

[See the numbers](../blog/2026/06/camel-dependency-updates/index.md)

## SBOMs ship with every release

Every Camel release since 4.0.3 ships with PGP-signed CycloneDX SBOMs (JSON and XML), giving you a machine-readable inventory of every dependency in the framework. Need an SBOM for your own application? The Camel CLI can generate one with a single command (`camel sbom`), and Maven-based projects (Spring Boot or Quarkus) can add the standard CycloneDX plugin. Whether it is the EU Cyber Resilience Act or US Executive Order 14028, the [SBOM box is already checked](../blog/2026/06/camel-sbom-supply-chain/index.md).

[How to generate SBOMs](../manual/sbom.md)

## Secure out of the box

Apache Camel doesn’t just fix vulnerabilities after they are found — it actively prevents insecure configuration from reaching production. Every option in the Camel component catalog carries machine-readable security metadata that identifies whether it is security-sensitive and whether enabling it introduces a known risk. At startup, Camel uses this metadata to validate configuration before a single message is processed.

Camel validates security-sensitive configuration at startup, covering secrets, transport security, serialization, and production-only settings. Components are designed with secure defaults so that the safest configuration is also the easiest one to use.

In **production mode** (`camel.main.profile = prod`), the global default is `fail`: the application refuses to start with any insecure configuration unless explicitly overridden. This is a hard guardrail, not a warning that can be scrolled past. In the default (no-profile) mode, violations are logged as warnings so existing applications are not broken.

[Security Policy Enforcement](../manual/security-policy.md)

## AI already knows Camel

AI coding assistants are remarkably good at Apache Camel — and it is not an accident. [Nineteen years of stable APIs](../blog/2026/06/camel-ai-trained/index.md) mean training data does not go stale, 11,700+ Stack Overflow answers provide real-world examples, and a predictable component model lets LLMs generalize across 350+ connectors. Add a built-in [MCP server](../manual/camel-jbang-mcp.md), machine-readable catalog metadata, a schema-validated YAML DSL, and dedicated [AI integration patterns](../components/next/eips/ai-patterns.md) for building AI-powered routes, and Camel is one of the best-trained integration frameworks for AI-assisted development today.

We measure that rather than claim it. Given the Camel CLI as tools, a frontier model [built all 13 beginner examples](../blog/2026/09/camel-local-model-benchmark/index.md) from a one-line description each. A 22 GB local model running on a laptop went from 0 of 13 with a bare prompt to 12 of 13 once it had the Camel MCP server and error messages that say what to write — and 99 of the 117 things it tripped over along the way were wrong for people too, so they were fixed for everyone and ship in Camel 4.23. It works in the other direction as well: for the 4.22 LTS release, we [pointed a frontier AI model at the codebase](../blog/2026/07/camel-not-afraid-of-ai/index.md) and fixed 165 bugs it found — concurrency races, silent data loss, and security gaps that are hard for humans to spot.

[Read why](../blog/2026/06/camel-ai-trained/index.md)

Trust is not a feeling. It is a record. Camel’s is public and unbroken: every release, every advisory, and every line of code is out in the open for you to check.