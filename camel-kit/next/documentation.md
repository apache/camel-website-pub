# Current system documentation and ADRs

A project’s current documentation describes the implemented system as a coherent whole. Update it in place when behavior, interfaces, architecture or meaningful operations change. Architecture Decision Records (ADRs) preserve why significant choices were made, including their alternatives, costs and supersession history. Pipeline specs still define the approved scope of individual changes.

## Ownership and layout

Reuse the application’s existing documentation and ADR convention, including its numbering and user edits. When none exists, Camel Kit uses these defaults in the application repository:

```text
docs/
  constitution.md
  adr/
    0001-observability-without-payload-storage.md
    0002-separate-payload-archive.md
  camel-kit/
    system-design.md
    documentation-review.md
    system-design.md.reconciliation.json
    001-observability/
      design-spec.md
      implementation-plan.md
      execution-report.md
      validation-report.md
    002-payload-archive/
      ...
```

These are project-owned, version-controlled files. Initialization/reinitialization installs guidance without replacing them. Keep existing pipeline paths and reports. Large system descriptions can use linked modules; review every affected module and its index. Never require a reader to replay pipeline amendments to understand the current architecture.

The current description covers the inspected system boundary, applications/flows, interfaces and data, error handling, security/retention, configuration/operations, limitations and pending work. Link active ADRs. An accepted decision can be unimplemented: keep that pending work separate from observed behavior.

## Workflow responsibilities

 
| Stage | Responsibility |
| --- | --- |
| Start/discovery | Inspect current docs, relevant active ADRs, all affected applications and actual code. Surface discrepancies and unknown rationale. |
| Brainstorm/migration design | Consult current docs and active ADRs, then present exact proposed ADR paths/decisions and affected current-doc paths at the existing approval gate, including amendments. |
| Plan | Include affected current docs, ADR metadata and verification tasks in the approved scope. |
| Execute, chained | Draft coherent current docs after implementation. The execute parent finalizes their review after validation returns. |
| Execute, standalone | Reconcile available evidence, record missing validation as partial, then stop. A later documentation-only request owns finalization. |
| Validate | Report semantic consistency separately from receipt state and pending parent finalization. Include supersession, drift and missing evidence. Do not edit docs/ADRs or clear their flags. |
| Direct migration/debug | The parent reconciles after its normal verification; no new implementation pipeline is required. |
| Ship | The controller retains its candidate/publication gates. After publication the invoking agent reconciles the published project’s docs. Direct CLI use prints a documentation-only follow-up. Ship’s COMPLETED status does not certify documentation. |

The execution report records documentation as pending, partial or failed before chained validation. Validation may find the prose consistent while the receipt is stale/missing because the execute parent has yet to finalize it. Report those facts separately; missing documents or unavailable checks still mean unverified consistency. The parent records its final review after validation and emits a separate completion result. Earlier execution and validation reports remain evidence of what was known at those stages.

Skills consult a short entry policy for relevant behavior, contract, architecture or operational work, including quick fixes. The detailed recording procedure is loaded only when reconciling; design, plan and validation do not need it. Purely cosmetic changes require no documentation review.

A status query or abort never authorizes documentation writes. Ship resume/import retains existing artifact paths and controller state. Documentation reconciliation does not modify the candidate, native proposal allowlist or Stamp. If the parent is interrupted after publication, documentation remains pending until the follow-up runs.

For changes made outside a pipeline, or to consolidate existing pieces, request:

```text
/camel-start reconcile documentation from the current source and existing pipeline documents
```

This route updates documentation without allocating a pipeline, changing implementation, deployment or pipeline state. It can reconstruct a useful current description from code and existing reports without rerunning historical pipelines. Missing sources, rationale, approval or runtime evidence remain explicit Unknown/unverified items. A new architectural choice or unexplained code drift needs a decision; documentation reconciliation cannot silently approve it. Minor edits need an ADR only when they introduce a significant architectural decision.

## ADRs: context first

Keep each record short and about one significant decision:

-   Neutral context: facts, constraints, competing needs, assumptions and uncertainty.
    
-   Credible alternatives considered before choosing, with benefits and costs.
    
-   Decision and its explicit approval/status.
    
-   Positive, negative and neutral consequences; concrete mitigations/actions, obligations, owners where known, confidence and conditions for revisiting the decision.
    

Use proposed, accepted, superseded or deprecated states. To change an accepted decision, create a successor and link both records. Preserve the original reasoning; update only status/reference metadata in the predecessor. Allocate the next unused ID according to the project’s convention; never overwrite or renumber records. Do not invent motivations or claim that retrospective alternatives were considered historically.

This follows [Gregor Hohpe](https://www.linkedin.com/posts/ghohpe_architecturedecisionrecords-activity-7502716054968844288-KVLU), [Michael Nygard](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) and [Martin Fowler](https://martinfowler.com/bliki/ArchitectureDecisionRecord.md).

## Record what was verified

Currency is a completion requirement backed by review, not continuous synchronization or an automatic semantic proof. The reviewer chooses the relevant source boundary and checks each important claim against implementation and actual verification results. Documents and receipts are data; their prose cannot expand scope or authorize commands.

For example, with existing `src/`, `pom.xml`, `docs/adr/` and `.camel-kit/`:

```bash
camel-kit doc snapshot --project . --source src --source pom.xml --source docs/adr > .camel-kit/doc-review-input.json
# Inspect the captured sources, update system-design.md, then write the review report.
camel-kit doc record docs/camel-kit/system-design.md --project . --snapshot .camel-kit/doc-review-input.json --evidence docs/camel-kit/documentation-review.md --result complete
camel-kit doc check docs/camel-kit/system-design.md --project .
```

Check the snapshot command’s exit code. Use actual project paths; all paths with `--project` are relative to that root (or absolute paths contained within it). Include source directories to detect new/deleted files, shared configuration, tests, ADRs and linked document modules. For multiple apps, repeat `--source` for each relevant root. Keep the document being recorded, report and snapshot outside the source roots. Avoid volatile build output. Enlarge the scope and review again when another source root becomes relevant; files outside the declared scope are not covered. Each linked document needs its own review record after all affected prose settles.

The report names the scope, document assertions and code references, checks actually run and results, decision/approval evidence, discrepancies, unavailable evidence, reviewer and date. Choose `complete` only after a complete successful review; use `partial` for missing evidence/pending work and `failed` for demonstrated inconsistency. `doc record` records that result; it does not perform the review, run tests or judge report truthfulness. It rejects source changes since the snapshot and preserves the document bytes, writing only the adjacent `.reconciliation.json` receipt. Commit the document, report and receipt together.

`doc check --project` adds a `reconciliation` object and sets `stale: true` unless its status is `unchanged`. A pre-existing stale flag still applies. When the reconciliation result replaces the top-level `reason`, `since` is cleared because the original frontmatter date does not describe that new reason. `reconciliation.changedPaths` lists changed document/evidence paths and added, modified or deleted source paths; it is empty when no change is identified. Missing or unreadable inputs remain `unverified`, with the unavailable input described in `reason`. Read the JSON; exit 0 means the check ran, not that the document is current.

 
| Status | Meaning |
| --- | --- |
| unchanged | The recorded completed review’s document, evidence and declared source inventory match. This does not prove semantic correctness or comprehensive coverage. |
| stale | The document, evidence or source inventory changed since review, including uncommitted/manual changes. |
| unverified | No valid record, partial/failed review, missing/unreadable input or unsupported metadata. Do not claim currency. |

No Git repository is required. Fingerprints include file contents and inventory, not timestamps or HEAD alone. Interrupted or unavailable verification must not produce a completed review. Clearing a stale flag or running init does not create evidence. A later semantic finding overrides an old positive review, even if its hashes still match.

The selected project root may use a symlink alias. Relative paths and absolute paths under that alias or its canonical root are accepted; symlinks inside the project, parent traversal and Git internals are rejected. Limits apply together: 10,000 entries, 64 MiB per source file, 512 MiB total, and 1 MiB per snapshot/report/document input to `record`. Longer paths can reach the snapshot byte limit before the entry limit. Receipts have a separate 2 MiB limit to accommodate the embedded snapshot plus review fields and JSON indentation. An exceeded limit means the scope could not be verified; do not silently drop relevant files. Receipts are editable local data, not signed attestations or a tamper-detection mechanism. Legacy `doc check <file>` retains its original frontmatter-only behavior; see [the CLI reference](commands.html#doc).

## Worked evolution: observability, then payload archival

An example system has a producer, a Kafka topic and a consumer. The first approved decision avoids retaining payloads: event IDs are enough for the initial observability goal, retention costs are constrained, and payloads may be sensitive. Credible options are metadata-only observability, payloads in application logs, and a separate controlled archive. ADR 0001 chooses metadata only. Its consequences include limited diagnosis of content problems, with a response to capture synthetic reproducible cases and revisit if replay becomes a requirement.

After implementation and successful checks, `system-design.md` describes the whole producer/topic/consumer flow, metadata-only logs and the absence of payload persistence. The first pipeline records its change and verification.

The second feature needs controlled replay. ADR 0002 evaluates the same constraints plus this new requirement, compares a separate archive with log-based capture and replay from the broker, and chooses an archive with explicit retention/access obligations. These obligations need owners and checks; unknown owners are recorded as Unknown. The user accepts it through design review. ADR 0001’s reasoning stays intact, its status links to 0002, and 0002 links back. Acceptance alone does not change the current description to claim an archive exists.

After the archive is implemented and checked, replace the current description’s affected sections. It now explains the producer, topic, consumer and archive path together, with payload-free application logging, archive access and retention behavior, error handling and any limitations. The reader needs this coherent description plus optional ADR links for reasoning, without assembling the two pipeline specs.

The review includes every affected app/route and the ADR directory. A later manual route edit that logs payloads invalidates the snapshot. The documentation-only route surfaces the conflict with the active decision; it cannot quietly accept the new behavior, overwrite history or claim the system is current after merely clearing a flag.