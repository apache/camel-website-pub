# Knowledge MCP

The Knowledge MCP server gives the agent release-backed access to Apache Camel documentation, component references, migration guides, CVE advisories, release notes and Jira issues, from a locally cached index rather than a live crawl. Knowledge MCP 0.0.2 accompanies Camel Kit 0.4.1. Its index, built on 2026-09-21, holds 20,367 documents covering the supported 4.18 and 4.22 LTS lines, with release history from 4.18 to 4.22; `camel_docs_index_info` reports the installed corpus.

The server is developed in `knowledge/` in the Camel Kit repository, with its own version line. Source builds use the Maven group `org.apache.camel` and Java package `org.apache.camel.kit.knowledge`. The published 0.0.2 runner retains its original coordinates. `init` configures it automatically; to run it by hand:

```bash
jbang io.github.luigidemasi:camel-kit-knowledge-mcp:0.0.2:runner
```

It speaks stdio and opens no HTTP port by default. For HTTP on localhost add `-Dquarkus.http.host-enabled=true -Dquarkus.http.host=127.0.0.1 -Dquarkus.http.port=9090` before the coordinate.

## Tools

The server exposes seven `camel_docs_*` tools. The workflow manifest allowlists five of them for the generated Camel Kit workflow; the other two remain available to direct MCP clients.

  
| Tool | Purpose | Parameters |
| --- | --- | --- |
| `camel_docs_search` | Hybrid search across component references, EIPs, the user manual, migration guides, getting-started guides and release notes | `query`; optional `version`, `max_results` (default 5, at most 25) |
| `camel_docs_component_info` | Reference documentation, examples and options of one component; exact indexed matches are reported separately from fuzzy full-text fallbacks | `component`; optional `version`, `runtime` |
| `camel_docs_cve_search` | CVE advisories by ID, component, severity or fixed-in version, with CVSS and CWE details when NVD enrichment was available | optional `cve_id`, `component`, `severity`, `version`, `max_results` |
| `camel_docs_release_info` | Release notes of a version with features, fixes and Jira references | `version`; optional `max_results` |
| `camel_docs_jira_lookup` | A Jira issue and the indexed release in which it was fixed | `jira_id` |
| `camel_docs_validate_endpoint` (direct clients) | Deterministic validation of one endpoint URI against the catalog bundled in the server, Camel 4.22.1 in this release; reports unknown components or options and missing required options | `uri` |
| `camel_docs_index_info` (direct clients) | Document count, covered Camel versions, document types, embedding model and search mode of the active index | none |

## Search pipeline

General searches blend Lucene BM25 keyword scoring (20 percent) with a KNN vector search over 384-dimensional Granite embeddings (80 percent), then rerank the candidates with a local cross-encoder before applying the result limit. Keywords keep exact identifiers such as `kafka`, `CVE-2024-22369` or `autoOffsetReset` from being displaced by semantically similar results; vectors find documents whose wording differs from the question. Component lookup uses exact field matching first and marks any full-text fallback as fuzzy.

If the embedding model is unavailable or does not match the index, the server disables vector retrieval and continues with BM25 and the reranker; if the reranker is unavailable, it returns the retrieval order. Embedding and reranking run locally through ONNX Runtime; queries are not sent to an external model API.

 
| Model | Value |
| --- | --- |
| Embedding | granite-embedding-small-english-r2, Q8 ONNX, 384 dimensions, 8,192-token maximum, 2,048 tokens per chunk by default |
| Reranker | ms-marco-MiniLM-L-6-v2, Q8 ONNX |
| Index | Lucene 9.12.1, vectors stored as `KnnFloatVectorField` |

## What is indexed

-   Component and EIP documentation from Apache Camel, Camel Quarkus and Camel Spring Boot, plus the structured catalog metadata: URI syntax, options, producer and consumer properties, examples.
    
-   The CVE advisories published with the Camel website, each with its affected and fixed versions and severity, and CVSS, vector and CWE details when the rebuild could enrich them from NVD or, as a fallback, from the CIRCL vulnerability lookup.
    
-   Release notes with features, fixes, breaking changes and dependency updates, enriched with the Jira issue details.
    
-   Migration guides, user manual chapters and getting-started guides.
    

## Index distribution and cache

The index is published as `knowledge-index.zip` with an `index.json` manifest in a GitHub release of the knowledge repository; it is not inside the MCP Maven artifact, and normal use needs neither a clone of that repository nor the indexer. The server resolves the index lazily on the first knowledge query in each process. The published 0.0.2 runner uses its original manifest location in `luigidemasi/camel-kit-knowledge`; it remains available for existing installations.

Migrated source builds discover releases through `[https://api.github.com/repos/apache/camel-kit/releases](https://api.github.com/repos/apache/camel-kit/releases)`, selecting the newest published `knowledge-index-v1-YYYY.MM.DD-HHMMSS` tag. Product tags, drafts, prereleases and other format channels are ignored. The v1 contract is Lucene 9, the model `granite-embedding-small-english-r2-q8`, 384 dimensions and manifest `formatVersion: 1`. Model/format mismatches are rejected before activation. Legacy manifests can omit format and dimension fields only when they identify the v1 model.

-   `knowledge.index.path` opens a local index directory directly, without network access.
    
-   `knowledge.index.version=YYYY.MM.DD-HHMMSS` pins an exact published index version.
    
-   `knowledge.index.url` overrides discovery with a specific HTTPS or file manifest, including a mirror or the legacy URL `[https://github.com/luigidemasi/camel-kit-knowledge/releases/latest/download/index.json](https://github.com/luigidemasi/camel-kit-knowledge/releases/latest/download/index.json)`.
    
-   `knowledge.index.releases-url` overrides the GitHub-compatible API endpoint.
    

Downloaded archives are SHA-256 checked and activated atomically in `~/.camel-kit/knowledge-index/`. Failed checks, downloads or activations keep the previous working cache. A pinned client falls back only to its exact cached version. Discovery follows at most ten pages of 100 releases each, with a five-second deadline per page; use an explicit manifest if the list exceeds this bound. The first monorepo index must be published before its discovery endpoint is usable; until then use a local index or explicit legacy manifest.

Rebuild with `./mvnw -B -pl knowledge/index -am -Prebuild-index install` from the repository root. Maintainers review generated data before manually dispatching `Index Release` from `main`; the workflow validates retrieval with working vectors before publication. Index publication is independent of Kit and Knowledge server releases.

## Rebuilding the index

Rebuilding is a maintainer task. From a checkout of the knowledge repository:

```bash
./mvnw -pl index -Prebuild-index -am -B install
```

The rebuild refreshes the Camel website’s release metadata and selects every supported LTS line, adding the latest release line only when it is not an LTS; it then resolves the latest release tags of those lines, renders their documentation, downloads the catalog metadata, parses release notes and advisories, enriches Jira and NVD data, generates or reuses cached embeddings and writes the Lucene files with the manifest skeleton. CVE enrichment needs no API key; requests are rate-limited and cached, and a failed lookup is retried at a later rebuild. The reviewed index is committed, and the manually dispatched release workflow packages and publishes the archive and the completed manifest after a retrieval-quality gate.

 
| Module | Purpose |
| --- | --- |
| `schema` | Lucene field definitions and the document builder |
| `embedding` | Local ONNX embedding and reranker support |
| `indexer` | Version resolution, crawling, parsing, chunking and indexing |
| `index` | The rebuilt Lucene files and the release manifest inputs |
| `mcp` | The Quarkus MCP server exposing the seven tools and resolving the released index |

## The camel-knowledge skill

`/camel-knowledge` is a prescriptive question-and-answer layer over the five allowlisted tools. A standalone question runs in the primary session: component configuration goes to `camel_docs_component_info`, troubleshooting and best-practice questions go to `camel_docs_search`, and the answer cites its sources. When a pipeline stage needs documentation context, the generated instructions isolate the lookup in a read-only research role where the agent has one (Bob 2’s reviewer preset, Antigravity’s reviewer, Qwen’s reviewer leaf, OpenCode’s researcher task) and run it inline on Pi. The role returns a concise answer with references instead of raw search results, and a failed lookup is reported as missing evidence rather than replaced with invented documentation.

## Local model initialization and host effects

The monorepo Knowledge runner loads its bundled embedding and reranking models locally. Tokenizer initialization enforces offline CPU mode, disables DJL telemetry/native downloads and implicit CUDA subprocess discovery. Remove conflicting `DJL_OFFLINE` values other than `true` or `RUST_FLAVOR` values other than `cpu`; startup reports these conflicts before loading native code. These controls set JVM-wide properties (`ai.djl.offline=true`, `RUST_FLAVOR=cpu`, `ai.djl.util.cuda.fork=false`). An absent `jna.platform.library.path` is set to the empty string to prevent JNA’s `ldconfig` subprocess; an explicit value is preserved. Other DJL/JNA users in the same JVM inherit this policy. Run Knowledge as a separate process when an embedding application requires different native-library or GPU discovery behavior. This applies to the monorepo source runtime, not the previously released Knowledge 0.0.2 runner.

Native initialization still writes DJL’s cache (normally `~/.djl.ai/tokenizers`, configurable with `ENGINE_CACHE_DIR` or `DJL_CACHE_DIR`) and ONNX/native temporary files. The embedding model also uses a temporary directory. These paths are separate from the Knowledge index cache.

Stdio is the default and disables the HTTP host. If enabling HTTP/SSE, explicitly configure `quarkus.http.host` and `quarkus.http.port`; the transport has no built-in authentication. Use loopback or provide an authenticated deployment boundary. A local `knowledge.index.path` bypasses index downloads. Endpoint-validation tools inspect catalog metadata and do not execute an endpoint or fetch its URI.