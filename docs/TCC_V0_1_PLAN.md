# TCC — Transaction Consistency Checker

**Checkpoint:** October 2, 2026

**Status:** selected product candidate; implementation not started; commercial demand unvalidated.

TCC is the first paid-product candidate selected from the reusable-tool experiments. Its proposed purpose is to help a user identify inconsistencies in transaction CSV files and understand what caused each finding.

## Current evidence

- The product candidate and name have been selected.
- A dedicated local project directory exists and is empty.
- No TCC source code, CLI, sample files, automated tests, or release is present in that directory.
- The v0.1 scope, supported CSV schema, output contract, and diagnostic reason codes still need to be defined.

Creating the directory and publishing this plan do not establish a working product.

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

This table describes the proposed direction, not a frozen contract or implemented feature set. The supported schema, accounting rules, and comparison inputs must be explicit before implementation.

## Reuse candidate: Ledger Inspector

GPT Lab experiment 001, Ledger Inspector, is a candidate source for reusable validation and ledger-reconstruction logic. Its earlier automated test checkpoint is documented in the [showcase module pipeline](../README.md#4-gpt-lab-and-reusable-module-pipeline).

That checkpoint applies to the original experiment and its defined contract. It does not establish that TCC has been implemented, independently tested, or validated by users. Reused logic must be reviewed against the new contract and tested again in TCC.

## Proposed v0.1 boundary

- A standalone CSV-checking CLI with a short getting-started guide.
- Explicit input and output contracts with understandable diagnostic reasons.
- Synthetic normal and failing examples covering the supported checks.
- Read-only analysis: report findings rather than automatically repairing source records.
- No dependency on operating trading systems, broker credentials, or live trading APIs.

These boundaries are proposals to confirm during scope definition. Public examples should use synthetic data and contain no personal transaction records or account identifiers.

## Validation gates

| Gate | Evidence needed | Current state |
| --- | --- | --- |
| Scope and contract | Supported schema, accounting assumptions, outputs, and exclusions documented | Pending |
| First runnable version | CLI, sample input/output, and usage guide work together | Pending |
| Automated validation | Tests for normal, duplicate, malformed, non-finite, and reconciliation cases under the frozen contract | Pending |
| Fresh installation | A clean environment can follow the guide and reproduce the expected results | Pending |
| External usability | An independent user completes the core task; difficulties and findings are recorded | Pending |
| Commercial validation | Evidence of useful differentiation and willingness to pay | Pending |

The next step is scope and contract definition, followed by implementation and verification. Future implementation and testing should record their actual evidence separately from this planning checkpoint.

## Commercial hypothesis

The "first dollar" track is an experiment goal. No selling price, completed sale, revenue, or willingness to pay has been established. Passing automated tests will not, by itself, demonstrate usability or commercial value.
