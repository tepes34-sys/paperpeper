# paperpeper · paperA · think · paperCity · TCC

> A public showcase of operating systems, reliability experiments, reusable modules, design decisions, a small cross-domain simulation prototype, and a transaction-checking product candidate.

[Portfolio completion assessment](docs/PORTFOLIO_PROGRESS_2026-10-04.md) · [October 4, 2026 work and validation notes](docs/WORKLOG_2026-10-04.md) · [October 3, 2026 work and validation notes](docs/WORKLOG_2026-10-03.md) · [September 30, 2026 work notes](docs/WORKLOG_2026-09-30.md) · [Earlier paperpeper experiments and validation records](https://github.com/tepes34-sys/paperpeper/blob/216cefe28df3b909d9e50f3f8fc4b0497d918904/README.md)

## 1. paperpeper

U.S. equity paper trading, an isolated Lab, and reusable reliability experiments.

**October 4 final checkpoint:** safety repairs merged; 604 tests ran with no failures and one skip. Three actual saved prompts were compared with prepared instructions. Independent comparison of 41 repaired cells found zero mismatches; one additional exact target-close repair brings the batch to 42 measured cells, with two unresolved cases.

Raw operating records remain private and live trading stays disabled. Normal scheduled review/pick/daily observations on October 5–6 remain pending; saved configuration and CI are separate evidence.

[Current evidence and operating gates](docs/WORKLOG_2026-10-04.md#1-paperpeper)

## 2. paperA

A Shadow Reliability Lab testing invariants, recovery, and portability with virtual market events. Design Freeze v1.0 is preserved; V1 runtime support remains Windows.

**October 4 later checkpoint: steps 8–12 implemented and tested; scheduler preparation through step 14 deployed as a pinned candidate.** Steps 1–7 are merged; four stacked draft changes for the later work still await independent review and main integration.

Safety/operator recovery, the public quotation adapter, read-only reports/alerts, ten controlled fault scenarios and actual process-kill restart equivalence are implemented. Final-candidate CI passed **440 full tests on Windows and 358 portable tests on Ubuntu**, each with Python 3.11/3.12. The 14-day normal fixture retains 456 fills and 912 independent amount comparisons; these are offline evidence.

Two actual Windows tasks and the initial database are installed. Initial off-session execution and audit succeeded with zero requests, cycles or financial activity. **The October 5 full-day trial and actual seven-day reliability remain pending.** Trial success would enable October 6–12; CLEAN samples alone may extend through October 26. The PC must remain powered on and the configured user signed in. No power-loss or profitability claim is established.

[Design and validation gates](PAPERA_PLAN.md) · [Current work notes](docs/WORKLOG_2026-10-04.md#3-papera)

## 3. think

**September 30 checkpoint: 11 approved decisions; 12 design OPEN items resolved.** The October 3 numerical-contract proposal defines seven review principles for paperA and TCC and remains **PROPOSED**. October 4 project-specific fixes and regression evidence do not approve that proposal or establish a new shared invariant.

A design documentation layer that separates discussions, approved decisions, and enduring conditions verified across projects. Cross-project reproduction and adoption remain separate gates.

[Current proposal boundary](docs/WORKLOG_2026-10-04.md#4-think-and-other-tracks) · [Document structure and transfer process](docs/WORKLOG_2026-09-30.md#3-think)

## 4. GPT Lab and reusable-module pipeline

GPT Lab is the small-module experiment track extracted from operating problems and recurring infrastructure patterns.

**October 3 independent rerun: 7/7 experiments · 56/56 tests passed.** The earlier checkpoint was 55 tests. Explicit experiment CI coverage remains a separate follow-up.

| ID | Experiment | Role |
|---|---|---|
| 001 | Ledger Inspector | Detect ledger and transaction inconsistencies |
| 002 | Report Generator | Build statistics from completed trade records |
| 003 | Trading Black Box | Preserve decisions, events, and causal context |
| 004 | Risk Guard | Enforce pre-action safety limits |
| 005 | Shadow Comparator | Compare paired strategy results |
| 006 | Reconciler | Compare expected and observed state |
| 007 | Broker Adapter | Define a broker-independent order boundary |

test-verified means the defined automated contract passed independent reruns. It does **not** mean user-tested, commercially validated, or production-ready.

A second discovery pass identified **008–017** as reusable-module candidates from live paper-trading operations:

Scheduler Health Auditor, Data Quality Classifier, API Budget Monitor, Freshness Gate, Environment Isolation Guard, Decision Reason Analytics, Cost/Fee Simulator, CSV Contract Validator, Idempotency/Duplicate Run Detector, and Report Manifest/Artifact Registry.

These are **discovery candidates only** unless separately implemented and verified.

## 5. paperCity — simulation experiment

paperCity is a small city-management simulation exploring whether reliability ideas remain useful outside trading.

**October 3 implementation checkpoint: Core and nine facilities/economy types implemented locally; 667 product test executions passed (544 Core + 123 Phase2).** The 12 facilities authored scenarios matched actual results. A 12-condition facilities long-run matrix and a fresh Core performance recheck passed provisional development budgets.

The engine implements construction/enabled-state commands, road connectivity, integer power/labor allocation, food flows, service effects, and monthly settlement. On October 4, the 667-test suite was reproduced and six independent checks passed. Phase3 growth/decline design review added zero-population and closed-facility boundaries and separates actual observations from hypothetical evaluation. Values remain proposed; no Phase3 implementation or source publication is claimed. Policies, persistence, UI, and playtesting remain future gates.

[Implementation, regressions, measurements, and limits](docs/PAPERCITY_IMPLEMENTATION_2026-10-03.md) · [paperCity v0.1 prototype plan](docs/PAPERCITY_V0_1_PLAN.md)

## 6. TCC — Transaction Consistency Checker

**October 4 checkpoint: v0.1.0 read-only core, CLI, Python API, and package implemented against the v0.1-r1 contract.** Actual product validation passed 18 unit tests and 55 external acceptance cases. Repeated acceptance runs preserved inputs and produced deterministic output.

A separate review identified an inherited Decimal default-context defect; the repair and regression were rechecked. A fresh Windows Python 3.12.14 installation worked outside the source repository. The reviewed version is merged in its private development repository; post-merge CI passed on Windows/Linux with Python 3.10/3.12.

The tool checks the supported normalized transaction CSV contract, including duplicate IDs, malformed rows, finite amounts, exact CREDIT/DEBIT totals, and optional expected final balance. It reports diagnostics without repairing source records.

A separated participant/facilitator trial kit was reviewed and merged. The participant archive was unpacked, installed offline in a fresh location, and exercised through five commands. The archive is a local trial artifact, without a public package-release claim. External usability, CSV preparation effort, willingness to pay, pricing, and revenue remain unverified. Private implementation and package-installation evidence do not constitute a public package release or sale readiness.

[TCC product direction and validation gates](docs/TCC_V0_1_PLAN.md)

## Estimated current-version completion

| Project | Estimate | Main remaining gate |
| --- | ---: | --- |
| Paperpeper | 90% | Normal October 5–6 scheduled evidence; two unresolved measurements |
| PaperA | 80% | Independent review/main integration, full-day trial, real seven-day and clean samples |
| TCC | 80% | Independent user trials and distribution decision |
| GPT Lab | 80% | Explicit experiment CI and documented downstream reuse validation |
| Think | 70% | Proposal review/approval, shared invariant evidence and cross-project adoption |
| PaperCity | 35% | Growth, policies, persistence, UI, integrated playtesting and balance |

Editorial scope estimates with roughly 5–10 percentage points of judgment uncertainty; required gates remain mandatory. Each project has a different completion target. These percentages do not measure profitability, commercial validation or release readiness. [Targets, weighted rationale and consolidated evidence](docs/PORTFOLIO_PROGRESS_2026-10-04.md).

## Public disclosure policy

This showcase is **English-only**. Publish as much useful, non-sensitive evidence as possible. Clearly distinguish design approval, code implementation, automated tests, live operating verification, discovery candidates, and future plans.

Exclude credential values, secrets, account identifiers, personal data, private discussion transcripts, and raw operating records.

## Reading the records

The [October 4 note](docs/WORKLOG_2026-10-04.md) preserves operating safety, TCC trial preparation and earlier implementation history. The [later portfolio report](docs/PORTFOLIO_PROGRESS_2026-10-04.md) adds PaperA steps 8–14 preparation, actual candidate installation and remaining real-session gates. The October 3 and September 30 notes retain their dated evidence. GPT Lab retains its earlier checkpoint; scheduled operation, actual users, and later implementation remain separate gates.

---

Software research project. Not financial advice.
