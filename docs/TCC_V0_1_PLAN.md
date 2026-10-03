# TCC — Transaction Consistency Checker

**Checkpoint:** October 3, 2026

**Status:** v0.1-r1 technical contract and acceptance preparation complete; product core and CLI unimplemented; commercial demand unvalidated.

TCC is the first paid-product candidate selected from the reusable-tool experiments. Its proposed purpose is to help a user identify inconsistencies in transaction CSV files and understand what caused each finding.

## Current evidence

- The local project contains a technical contract, design/reuse notes, and 17 synthetic CSV/expected-JSON pairs.
- Ledger Inspector was reviewed as a source of patterns; its original test result is not a TCC product test.
- An external acceptance harness contains 55 cases: 17 examples and 38 additional boundaries.
- The 17-example artifact audit and the harness's own 10 tests passed.
- TCC product acceptance is **NOT_RUN**. No core, CLI, package, or fresh-install result is available.

Expected JSON describes the contract; it is not product output. Contract and sample preparation must be handed over with their actual versions.

[October 3 work and validation notes](WORKLOG_2026-10-03.md#5-tcc)

## Proposed problem and checks

Transaction records can look plausible while containing duplicate IDs, malformed rows, invalid numbers, or disagreements between recorded transactions and expected totals or balances. TCC should make those problems understandable without silently changing the records.

Candidate checks include:

| Area | Question to validate |
| --- | --- |
| Structure | Are required columns and row shapes valid for the chosen schema? |
| Duplicates | Do repeated transaction identifiers indicate a consistency problem? |
| Numbers | Are numeric values valid and finite, and do they meet the agreed field rules? |
| Ledger consistency | Do reconstructed balances or positions agree with the provided expectations? |
| Diagnostics | Can the user locate the affected record and understand the reason? |

The local v0.1-r1 technical contract defines the supported schema, accounting rules, and comparison inputs. The table summarizes the intended behavior; product implementation and execution remain pending.

## Reuse candidate: Ledger Inspector

GPT Lab experiment 001, Ledger Inspector, was reviewed for reuse. Reading, Decimal validation, and test organization inform the design; the trading-ledger core is not directly reused under TCC's different contract. Its earlier automated test checkpoint is documented in the [showcase module pipeline](../README.md#4-gpt-lab-and-reusable-module-pipeline).

That checkpoint applies to the original experiment and its defined contract. It does not establish that TCC has been implemented, independently tested, or validated by users. Reused logic must be reviewed against the new contract and tested again in TCC.

## Proposed v0.1 boundary

- A standalone CSV-checking CLI with a short getting-started guide.
- Explicit input and output contracts with understandable diagnostic reasons.
- Synthetic normal and failing examples covering the supported checks.
- Read-only analysis: report findings rather than automatically repairing source records.
- No dependency on operating trading systems, broker credentials, or live trading APIs.

The local v0.1-r1 technical contract now defines the intended implementation boundary; execution and independent product verification remain pending. Public examples should use synthetic data and contain no personal transaction records or account identifiers.

## Validation gates

| Gate | Evidence needed | Current state |
| --- | --- | --- |
| Scope and contract | Supported schema, accounting assumptions, outputs, and exclusions documented | v0.1-r1 technical preparation complete; product verification pending |
| First runnable version | CLI, sample input/output, and usage guide work together | Pending |
| Automated validation | Tests for normal, duplicate, malformed, non-finite, and reconciliation cases under the contract | 55 external cases prepared; product execution NOT_RUN |
| Fresh installation | A clean environment can follow the guide and reproduce the expected results | Pending |
| External usability | An independent user completes the core task; difficulties and findings are recorded | Pending |
| Commercial validation | Evidence of useful differentiation and willingness to pay | Pending |

The next step is minimal core and CLI implementation against v0.1-r1, followed by actual acceptance execution, fresh installation, and independent review. Future implementation and testing should record their actual evidence separately from this planning checkpoint.

## Commercial hypothesis

The "first dollar" track is an experiment goal. No selling price, completed sale, revenue, or willingness to pay has been established. Passing automated tests will not, by itself, demonstrate usability or commercial value.
