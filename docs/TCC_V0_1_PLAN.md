# TCC — Transaction Consistency Checker

**Checkpoint:** October 4, 2026

**Status:** v0.1.0 prototype implemented, independently reviewed, fresh-install verified, and merged in its private development repository; external usability and commercial demand unvalidated.

TCC is the first paid-product candidate selected from the reusable-tool experiments. It checks the supported normalized transaction CSV contract and explains inconsistencies without modifying source records.

## Current evidence

- The v0.1-r1 contract and 17 synthetic CSV/expected-JSON pairs were prepared at the October 3 checkpoint. The artifact audit and acceptance harness's own 10 tests passed then; these were preparation evidence.
- The product now has a read-only core, CLI, Python API, JSON/text diagnostics, and a wheel without runtime dependencies.
- **18 unit tests and all 55 external acceptance cases actually passed.** Each acceptance case ran twice with deterministic output and unchanged input.
- A separate review found an inherited Decimal.DefaultContext defect. The repair, added regression, and reviewer recheck completed before merge.
- A fresh Windows Python 3.12.14 installation reproduced CLI/module results outside the source checkout, with installed files checked against the source.
- Post-merge CI passed on Windows and Linux, each with Python 3.10 and 3.12. Each of the four environments ran 18 unit tests and 55 acceptance cases.
- The original 42 documentation/sample/expected-result files were preserved byte-for-byte.

Expected JSON is a contract artifact; actual product execution is now recorded separately. A private build and successful installation are not a public package release.

[October 4 evidence and remaining gates](WORKLOG_2026-10-04.md#2-tcc) · [October 3 preparation checkpoint](WORKLOG_2026-10-03.md#5-tcc)

## Implemented v0.1 boundary

The implementation follows the supported normalized transaction schema. It validates required fields and row shape, duplicate transaction IDs, valid finite Decimal amounts, exact CREDIT/DEBIT totals, and an optional expected final balance. Deterministic diagnostics identify the record and reason under that contract.

- Read-only core, CLI, and Python API; no automatic source repair.
- JSON and text output with defined exit codes 0/1/2.
- Explicit file and row limits: 10 MiB and 10,000 data rows.
- Synthetic normal and failing examples, plus actual boundary acceptance.
- No dependency on an operating trading system, broker credentials, or live trading API.
- No claim of arbitrary CSV format support, a complete accounting system, or position reconstruction outside the contract.

## Reuse candidate: Ledger Inspector

GPT Lab experiment 001 informed reading, Decimal validation, and test organization. Its trading-ledger core was not directly reused under TCC's different contract. Its earlier checkpoint remains documented in the [showcase module pipeline](../README.md#4-gpt-lab-and-reusable-module-pipeline).

Original experiment tests remain separate from TCC product validation. TCC's 18 unit tests, 55 actual acceptance cases, fresh installation, and independent review are its own evidence.

## Validation gates

| Gate | Evidence needed | Current state |
| --- | --- | --- |
| Scope and contract | Supported schema, accounting assumptions, outputs, and exclusions | v0.1-r1 implemented; original artifacts preserved |
| First runnable version | Core, CLI, sample input/output, and usage guide | Complete for the defined prototype contract |
| Automated validation | Product tests against normal and boundary cases | 18 unit tests + 55 actual acceptance cases passed |
| Independent review | Separate review and resolution of findings | Completed; Decimal default-context repair rechecked |
| Fresh installation | Clean environment and use outside the source checkout | Verified on Windows Python 3.12.14 |
| Main and CI | Reviewed merge and platform-specific checks | Merged privately; four Windows/Linux Python environments passed |
| External usability | Independent user completes the task; CSV preparation and diagnostic understanding recorded | Pending |
| Commercial validation | Useful differentiation and willingness to pay | Pending |

Next: evaluate a user-provided CSV against the documented input boundary and prepare 1–3 independent user trials when participants and inputs are available. No participant contact or trial completion is claimed by this documentation update.

## Commercial hypothesis

The first-dollar track is an experiment goal. No selling price, completed sale, revenue, or willingness to pay has been established. Automated tests and installation evidence do not establish usability or sale readiness.
