# paperpeper · paperA · think · paperCity · TCC

> A public showcase of operating systems, reliability experiments, reusable modules, design decisions, a small cross-domain simulation prototype, and a transaction-checking product candidate.

[October 4, 2026 work and validation notes](docs/WORKLOG_2026-10-04.md) · [October 3, 2026 work and validation notes](docs/WORKLOG_2026-10-03.md) · [September 30, 2026 work notes](docs/WORKLOG_2026-09-30.md) · [Earlier paperpeper experiments and validation records](https://github.com/tepes34-sys/paperpeper/blob/216cefe28df3b909d9e50f3f8fc4b0497d918904/README.md)

## 1. paperpeper

U.S. equity paper trading, an isolated Lab, and experiments with reusable tools.

**October 4 checkpoint:** checkpoint crash/retry consistency, exact target-close validation, malformed-response isolation, and performance-review write safety are repaired and merged. The suite ran **604 tests, with no failures and one skip**.

The actual saved performance-review prompt was reopened and matched against the prepared instructions. A controlled paper-only measurement repair used exact target-close evidence; measurements without sufficient evidence stayed unfilled. Raw operating records remain private, and live trading remains disabled.

Saved instructions, merged code, and CI do not establish that the next normal scheduled review, pick, or daily checkpoint has executed successfully. Those operating observations remain pending.

[Current evidence and operating gates](docs/WORKLOG_2026-10-04.md#1-paperpeper)

## 2. paperA

**October 4 checkpoint: Design Freeze v1.0 preserved; the numerical boundary repairs are reviewed and merged.** Post-merge CI passed 97 full tests on Windows and 34 portable tests on Linux, each on Python 3.11/3.12. V1 runtime support remains Windows.

The fixed 14-day fixture still contains 12,096 candles and yields 163 entry-eligible candidates. The independent exact oracle compared 1,512 observations without mismatch across 36 Decimal-context conditions. Candidates and fixture sessions are not executed strategy trades or scheduled reliability evidence.

**Step 5A is locally implemented and saved:** one immutable candidate result is shared with A-v1 and B-v1. Its 20 new tests bring the local Windows Python 3.12.14 suite to 117 full tests and 54 portable tests. This change remains uncommitted, without new independent review or remote CI. A/B exits, entries, strategy decisions, persistence, recovery, and scheduled operation are subsequent gates.

A Shadow Reliability Lab that uses public market events to test invariants, recovery, and portability.

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

The engine implements construction/enabled-state commands, road connectivity, integer power/labor allocation, food delivery and consumption, service effects, happiness/pollution, and monthly tax/maintenance settlement. The current population is fixed and balance values are synthetic. Growth/decline, policies, persistence, City Black Box integration, UI, and playtesting remain future gates.

[Implementation, regressions, measurements, and limits](docs/PAPERCITY_IMPLEMENTATION_2026-10-03.md) · [paperCity v0.1 prototype plan](docs/PAPERCITY_V0_1_PLAN.md)

## 6. TCC — Transaction Consistency Checker

**October 4 checkpoint: v0.1.0 read-only core, CLI, Python API, and package implemented against the v0.1-r1 contract.** Actual product validation passed 18 unit tests and 55 external acceptance cases. Repeated acceptance runs preserved inputs and produced deterministic output.

A separate review identified an inherited Decimal default-context defect; the repair and regression were rechecked. A fresh Windows Python 3.12.14 installation worked outside the source repository. The reviewed version is merged in its private development repository; post-merge CI passed on Windows/Linux with Python 3.10/3.12.

The tool checks the supported normalized transaction CSV contract, including duplicate IDs, malformed rows, finite amounts, exact CREDIT/DEBIT totals, and optional expected final balance. It reports diagnostics without repairing source records.

External usability, CSV preparation effort, willingness to pay, pricing, and revenue remain unverified. Private implementation and package-installation evidence do not constitute a public package release or sale readiness.

[TCC product direction and validation gates](docs/TCC_V0_1_PLAN.md)

## Public disclosure policy

This showcase is **English-only**. Publish as much useful, non-sensitive evidence as possible. Clearly distinguish design approval, code implementation, automated tests, live operating verification, discovery candidates, and future plans.

Exclude credential values, secrets, account identifiers, personal data, private discussion transcripts, and raw operating records.

## Reading the records

The [October 4 note](docs/WORKLOG_2026-10-04.md) records the completed operating repairs, TCC implementation/review/merge, PaperA numerical repairs, and locally saved step 5A, with remaining gates separated. The October 3 and September 30 notes retain their dated evidence. The later October 3 paperCity implementation record is preserved, and no new GPT Lab or paperCity run is claimed by this update.

---

Software research project. Not financial advice.
