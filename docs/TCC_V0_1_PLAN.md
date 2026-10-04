# TCC — Transaction Consistency Checker

**October 4 completion assessment: 80% toward independently usable v0.1.** This is an editorial scope estimate; actual user tasks/feedback and distribution decision remain. Automated tests do not establish user or release readiness. [Weighted assessment and consolidated work](PORTFOLIO_PROGRESS_2026-10-04.md).


**Checkpoint:** October 4, 2026

**Status:** v0.1.0 prototype and separated user-trial kit implemented, reviewed, fresh-install verified, and merged in the development repository; actual user trials and commercial demand remain unvalidated.

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

## October 4 user-trial preparation

Participant instructions, four independent synthetic CSV tasks, feedback form, and wheel are separated from facilitator answers and captured outputs. Review removed answer leakage through task labels, example rows, and comparisons with the normal task.

The participant archive was unpacked and installed offline in a fresh location. Five documented commands reproduced exits 0/1/1/0/1 and installed code matched main. The trial-kit merge and post-merge CI completed without changing the product contract or output format.

The delivery archive remains local. Actual participants, preparation effort, diagnostic comprehension, and external feedback are still pending. No public package release or participant contact is claimed.

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

Next: use the prepared participant kit for 1–3 independent user trials when participants and inputs are available, recording installation, CSV preparation, and diagnostic comprehension. No participant contact or trial completion is claimed by this documentation update.

## Commercial hypothesis

The first-dollar track is an experiment goal. No selling price, completed sale, revenue, or willingness to pay has been established. Automated tests and installation evidence do not establish usability or sale readiness.
