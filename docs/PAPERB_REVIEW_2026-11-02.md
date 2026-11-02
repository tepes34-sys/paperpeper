# PaperB review and integration — November 2, 2026

The reviewed repair bundle is integrated into the isolated research branch. The research baseline moves from **82 tests/five probes to 94 tests/eight probes**, with **12 runner-contract tests counted separately**. This integration does not deploy experiments into operating systems.

## Executed evidence

| Experiment | Passing tests |
|---|---:|
| 001 Ledger Inspector | 32/32 |
| 002 Trade Report Generator | 12/12 |
| 003 Trading Black Box | 10/10 |
| 004 Risk Guard | 9/9 |
| 005 Shadow Comparator | 13/13 |
| 006 Reconciler | 14/14 |
| 007 Broker Adapter Kit | 4/4 |
| Total | **94/94** |

The final candidate passed dedicated CI on Ubuntu/Windows × Python 3.11/3.12. All four downloaded receipts confirm 94 tests/eight probes, with no failures, errors, skips or manifest problems. Each job log separately confirms 12 runner checks. Artifact digests, exact candidate provenance and all 76 recorded files were checked against Git content, allowing explicitly documented LF/CRLF variants only. The merged tree is identical to the tested final candidate.

| Environment | Actual Python | Tests | Probes | Runner |
|---|---|---:|---:|---:|
| Ubuntu | 3.11.17 | 94/94 | 8/8 | 12/12 |
| Ubuntu | 3.12.15 | 94/94 | 8/8 | 12/12 |
| Windows | 3.11.9 | 94/94 | 8/8 | 12/12 |
| Windows | 3.12.10 | 94/94 | 8/8 | 12/12 |

Common pull-request CI also passed all three jobs. A redundant push run was cancelled. The dedicated workflow was enabled for one manual dispatch, then restored immediately to its paused state. Post-integration common CI is tracked separately.

## Independent review and repairs

Three AI reviewers, separate from the implementation author, completed bounded reviews of 001/005, 002/007 and 006/runner. Their initial failed reviews were preserved. The final executable revision passed the scoped reviews; a separate check confirmed that the subsequent documentation commit changed no executable, test, manifest or probe blob. The independent full aggregate passed 94 tests/eight probes. For unchanged 002/007 files, earlier direct PASS evidence was linked by exact blob identity rather than represented as a new identical-suite run.

The review found additional scientific-notation sum failures in 002/005, short-row handling in 002, zero-exponent arithmetic/resource boundaries in 001/006, optimized-Python probe false greens and non-object receipt failures. Corrections have regressions. Earlier focused work repaired duplicate CSV headers and caller Decimal-context leakage.

An intermediate zero shortcut broke the existing ordinary quantity representation. Existing tests caught it; expected values were retained. A later incomplete repair still requested excessive precision near extreme zero exponents. The final implementation canonicalizes only arithmetic zero internally. Independent bounded checks confirmed ordinary alignment, signed money zero, scalar input representation and context isolation without large allocations.

001/002/005/006 return to **test-verified for their stated bounded contracts**. Existing 003/004/007 states remain unchanged. This is independent AI review, not human review or a user trial.

## Focused scenarios and limits

| Follow-up | Boundary/CLI | Randomized | Synthetic integration | Fixtures |
|---|---:|---:|---:|---:|
| 004/005 | 54 | 1,000 | 300 | 10 |
| 001/006 | 54 | 1,000 | 300 | 10 |
| 002/007 | 41 | 1,000 | 300 | 10 |

These are scenario counts, separate from unit-test methods. Repeating runs on other Python versions does not create new samples. Six initial fixtures abstract operating observations; all values and identifiers are synthetic. Other fixtures derive from source contracts or synthetic boundaries. There are **zero direct operating-case replays**. Fake order acceptance plus explicit synthetic completion is not a broker fill; prefix/replay tests are not actual process-crash or operating-database recovery.

No Main/Lab code, operating database, scheduler, account, credential or order changed. 007 still lacks logical idempotency, global/durable order identity and real/partial-fill behavior. test-verified does not mean user-tested, commercially validated or production-ready.

**Next weekly checkpoint: November 7, 2026. Baseline: 94 tests/eight probes plus 12 separate runner checks. Focus: 003 Trading Black Box / 004 Risk Guard.**

[Project overview](PaperB.md) · [Historical November 1 candidate CI](PAPERB_CI_2026-11-01.md)
