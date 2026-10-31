# PaperB weekly validation — October 31, 2026

## Two checkpoints on the same date

The first October 31 cycle completed an isolated research-branch integration with **82 baseline tests and five deterministic probes**. It repaired a direct-event Decimal normalization mismatch in the event-recording experiment.

The later 004/005 follow-up is an **unmerged draft candidate**, with **84 baseline tests and six probes**. It is an additional run on October 31, not evidence from the following week.

| Experiment | Merged baseline | Draft candidate |
|---|---:|---:|
| 001 Ledger Inspector | 29 | 29 |
| 002 Report Generator | 8 | 8 |
| 003 Trading Black Box | 10 | 10 |
| 004 Risk Guard | 9 | 9 |
| 005 Shadow Comparator | 9 | 11 |
| 006 Reconciler | 13 | 13 |
| 007 Broker Adapter | 4 | 4 |
| **Total** | **82** | **84** |

## Locally executed verification

The original 82-test baseline and five probes passed after directing temporary files to a writable test folder. The initial temporary-file permission failures were retained as environment evidence, not counted as product defects.

The changed candidate passed all 84 tests and six probes on Windows/Python **3.14.7** and **3.12.10**, with no skips, expected failures, assertion failures or errors. The final candidate commit was checked again with the full runner on Python 3.14.7. Documentation synchronization reused these dated receipts; it did not rerun product tests.

Separate checks:

- **10/10** runner-contract tests.
- **2/2** deliberately reverted-fix mutants detected by assertion failures.
- **54** explicit boundary scenarios: 45 risk checks and nine comparator checks.
- **1,000** randomized scenarios: 500 per focused module.
- **300** risk-to-CSV-to-comparator integration scenarios.
- **10** stored sanitized fixtures.

The new probe therefore executes **1,364 supplementary scenarios**. These scenarios are separate from the 84 unittest methods. Repeating a probe on two Python versions does not create twice as many independent samples.

## Defects and corrected behavior

### Duplicate CSV headers

A CSV with two normalized `pnl` columns silently used the later value. The candidate rejects duplicate column names after trimming whitespace and refuses the ambiguous file. A new regression covers identical and whitespace-normalized duplicates.

### Malformed P/L parsing

Malformed numeric text changed the caller's sticky Decimal error flag and produced different diagnostics depending on its trap settings. The candidate uses an owned parsing context, preserves the caller's state, reports invalid syntax consistently and still accepts a later valid correction.

Both new regression methods failed before repair and passed afterward. The executed contracts found **two new defects, both repaired, and zero recurring defects**. Risk Guard produced no new defect in these checks.

## Contract and state limits

005 changes from **test-verified to logic-verified**, pending independent review of the revised contract. This downgrade preserves the distinction between local author validation and independent verification.

004 remains a numeric position-cap and cash-buffer core. Rejecting a protection-status string supplied as a numeric argument does not implement or validate an operating protection gate. Integration scenarios use synthetic policies and P/L values; they do not reproduce Main/Lab strategy performance.

Of the ten sanitized fixtures, six adapt shapes observed in operating records, two derive from source contracts and two are synthetic numeric boundaries. They contain invented identifiers and values. Shape adaptation is not production replay, and ten fixtures do not mean ten operating incidents.

## Separate read-only operating evidence

For the completed **October 26–30 U.S. trading week**, each of the two paper environments recorded **425 of 425 scheduled invocations** with exit code zero and no traceback. The inspected scheduled slots had no missing, duplicate or more-than-60-second-late starts.

One environment nevertheless recorded **one quote-provider failure** and **one unhealthy monitor row**. The audit did not establish that those two rows described the same event. Zero scheduled-execution failures therefore does not mean zero faults or universally fresh quotes.

The current-week shadow entry cohort contained 17 source-pick groups: five pairs completed on both sides, eleven pairs open on both sides and one pair completed on only one side. Open results were not replaced with zero P/L. Five completed pairs do not establish strategy superiority, statistical significance or commercial value.

The audit used read-only database connections and query-only transactions, without application imports, market API requests or order execution. Database-file hashes matched before and after inspection. Separate database/log reads were not one simultaneous system snapshot. Raw records and financial account details remain private.

## CI, publication and next scope

Remote candidate jobs had no executed steps; their annotation reports payment/spending-limit ineligibility. Status is **CI pending — Actions limit**. Local success is not a CI pass. The dedicated experiment workflow remains manually disabled; this publication did not rerun or enable it.

The candidate is still draft and unmerged. No operating deployment, user trial, release, live trading or commercial validation was performed. Publishing this worklog does not integrate experimental code.

Next proposed baseline: **84 tests plus six probes**, with ten runner-contract tests separate. Next focus: **001 Ledger Inspector / 006 Reconciler**, especially header integrity, caller-context preservation and missing/duplicate/recovery boundaries. The next intended weekly checkpoint is November 7; no future result is assumed.

[PaperB overview](PaperB.md) · [Portfolio](../README.md#4-paperb-and-reusable-module-pipeline)
