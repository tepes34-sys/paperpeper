# paperpeper · paperA · think · paperCity · TCC

> A public showcase of operating systems, reliability experiments, reusable modules, design decisions, a small cross-domain simulation prototype, and a transaction-checking product candidate.

[September 30, 2026 work notes](docs/WORKLOG_2026-09-30.md) · [Earlier paperpeper experiments and validation records](https://github.com/tepes34-sys/paperpeper/blob/216cefe28df3b909d9e50f3f8fc4b0497d918904/README.md)

## 1. paperpeper

U.S. equity paper trading, an isolated Lab, and experiments with reusable tools.

The focus of today's notes is **the source of truth and the timestamp of each observation**. Execution logs, databases, CSV files, and dashboards may describe different points in time. Checks distinguish missing source data from an outdated derived report. When an alert appears, its evidence is verified before deciding whether to change the code.

[Problems, verification principles, and next questions](docs/WORKLOG_2026-09-30.md#1-paperpeper)

## 2. paperA

**September 30 checkpoint: Design Freeze v1.0 · steps 1–4 merged · 88 tests passed.**

The fixed 14-day public-market fixture contains **12,096 candles** and produced **163 entry-eligible candidates**. An offline rerun reproduced the measurement. A one-day fixture session verifies **109 runs / 108 cycles**; scheduled reliability evaluation remains a separate gate.

A **Shadow Reliability Lab** that uses public market events to test invariants, recovery, and portability.

[Design and validation gates](PAPERA_PLAN.md) · [Detailed work notes](docs/WORKLOG_2026-09-30.md#2-papera)

## 3. think

**September 30 checkpoint: 11 approved decisions; 12 design OPEN items resolved.** The common invariant layer still requires cross-project reproduction and actual test evidence.

A design documentation layer that separates GPT/Claude discussions, approved decisions, and enduring conditions verified across projects.

[Document structure, design topics, and transfer process](docs/WORKLOG_2026-09-30.md#3-think)

## 4. GPT Lab and reusable-module pipeline

GPT Lab is the small-module experiment track extracted from operating problems and recurring infrastructure patterns.

**Verified checkpoint: 7/7 experiments test-verified · 55/55 tests passed.**

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

## 5. paperCity — planned prototype

paperCity is a small city-management simulation concept for testing whether the reusable reliability ideas remain useful outside trading.

The v0.1 target is a numerical and policy-driven city where agriculture, industry, commerce, electricity, housing, and public services interact. Successful operation expands the city; persistent failures can cause closures, population outflow, and visible contraction.

It is currently a **design plan, not a released game or completed integration**. Candidate reuse experiments include Ledger Inspector for city accounting consistency, Black Box for causal event history, Reconciler for persisted-state checks, and Shadow Comparator as a later basis for policy A/B simulations.

[paperCity v0.1 prototype plan](docs/PAPERCITY_V0_1_PLAN.md)

## 6. TCC — Transaction Consistency Checker

**October 2, 2026 checkpoint: selected as the first paid-product candidate; implementation has not started.** A dedicated local directory exists but contains no project files yet.

TCC is a proposed standalone tool for finding inconsistencies in transaction CSV files and explaining the findings. Candidate checks include duplicate records, malformed rows, non-finite numbers, and discrepancies in totals or reconstructed ledger state.

The next milestones are to define the v0.1 scope and input/output contract, assess reuse of Ledger Inspector, and build a runnable CLI with synthetic examples and tests from a fresh installation. These are planned capabilities; no TCC release, completed tests, external user validation, pricing, or revenue is claimed.

[TCC product direction and validation gates](docs/TCC_V0_1_PLAN.md)

## Public disclosure policy

This showcase is **English-only**. Publish as much useful, non-sensitive evidence as possible. Clearly distinguish design approval, code implementation, automated tests, live operating verification, discovery candidates, and future plans.

Exclude credential values, secrets, account identifiers, personal data, private discussion transcripts, and raw operating records.

## Reading the records

The detailed September 30 work note covers paperpeper, paperA, and think. The current README additionally surfaces the reusable-module pipeline, the later paperCity prototype plan, and the October 2 TCC planning checkpoint. Earlier public experiment and validation records remain available through the versioned link above.

---

Software research project. Not financial advice.
