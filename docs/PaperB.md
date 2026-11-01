# PaperB

PaperB is the isolated reusable-module research track within the existing Kanna repository. Its seven experiments cover ledger inspection, reports, event records, numeric risk checks, paired comparison, recovery reconciliation, and a minimal broker-adapter boundary.

## November 1, 2026 — candidate CI verified; independent review pending

The latest **unmerged** candidate now has successful dedicated experiment CI on **Ubuntu/Windows × Python 3.11/3.12**. Each of the four downloaded receipts contains **87 passing tests and eight probes**, and each job log separately records **ten runner-contract tests**. Artifact ZIP digests and executable-source equivalence were checked with an explicit LF/CRLF policy.

The existing common pull-request CI also has a successful second attempt; it was checked rather than rerun. The dedicated experiment workflow was enabled only for one manual dispatch and immediately restored to its previous paused state.

The official merged research baseline is still **82 tests/five probes**. The three dependent drafts remain unmerged, and their independent-review gate is not closed by CI success. A clean-archive local rerun passed 87 tests/eight probes; 46 supplementary checks were author verification, not independent review. Existing logic-verified states, fake-adapter limits and user/commercial-validation limits are unchanged.

[November 1 CI evidence and remaining gates](PAPERB_CI_2026-11-01.md)

## October 31 checkpoint — 002/007 candidate (historical CI state)

The merged research baseline remains **82 tests and five probes**. Three dependent drafts remain unmerged: **84/six → 85/seven → 87/eight**. The latest candidate has **30 / 10 / 10 / 9 / 11 / 13 / 4** tests for experiments 001–007.

Windows/Python **3.14.7 and 3.12.10** passed all **87 tests and eight probes**, with no skips, errors or assertion failures. Ten runner-contract checks remain separate. The new probe executed 41 boundary/CLI, 1,000 randomized, 300 synthetic-completion integration scenarios and ten synthetic fixtures.

002 now rejects duplicate normalized CSV headers and parses malformed P/L through an owned Decimal context. Its two new regression methods failed before repair; two reverted-fix mutants were detected. **002 is logic-verified pending independent review.** Its first-seen trade-ID policy is preserved, including exclusion of a later correction for an ID already encountered in an invalid P/L row.

007 implementation is unchanged. Duplicate submissions create separate fake orders, new instances restart their IDs and externally clearing the public order list can allow ID reuse. No idempotency, global/durable ID uniqueness, partial-fill handling or real broker execution is implemented by these checks. ACCEPTED is not a fill.

Candidate CI jobs had no executed steps; their annotation reports payment/spending-limit ineligibility. Status remains **CI pending — Actions limit**. No new operating collection, order, deployment, user trial or commercial validation occurred.

**Immediate next gate: independent review of the dependent draft bundle, executable CI and separate merge decisions.** The next proposed validation baseline is 87 tests/eight probes. Later weekly focus 003/004 follows candidate cleanup; additional experiments do not close pending review gates.

[002/007 evidence and limits](PAPERB_002_007_2026-10-31.md)

## Earlier same-day follow-up — 001/006 candidate

The merged research baseline is still **82 tests + five probes**. The earlier unmerged 004/005 candidate has **84 tests + six probes**. A new draft stacked on that candidate has **85 tests + seven probes**: **30 / 8 / 10 / 9 / 11 / 13 / 4** for 001–007.

Windows/Python 3.14.7 and 3.12.10 passed the full 85-test candidate and all seven probes. The new 001/006 probe adds 54 boundary/CLI, 1,000 randomized, 300 prefix/replay integration scenarios and ten synthetic contract fixtures. Runner-contract checks passed 10/10; one deliberately reverted header guard was detected by assertions.

001 now rejects duplicate normalized CSV headers before processing rows. One regression method covers 12 failing-before subtests. 006 had no new defect and its implementation is unchanged. Both remain **logic-verified**, with independent review pending. The new candidate and its parent remain draft and unmerged.

These integration checks compare synthetic prefix, replayed and duplicate-tail states. They do not perform a process kill, database recovery or automatic repair. No new operating-record collection, market request, order, user trial or commercial validation occurred.

The earlier 001/006 plan proposed 85 tests/seven probes and a 002/007 focus; the later follow-up above supersedes that next-scope proposal. New candidate jobs returned no executed steps; the annotation reports payment/spending-limit ineligibility. Status is **CI pending — Actions limit**, with no successful remote CI.

[001/006 follow-up details](PAPERB_001_006_2026-10-31.md)

## Earlier same-day checkpoint — 004/005 candidate


The merged research baseline contains **82 tests**: **29 / 8 / 10 / 9 / 9 / 13 / 4** for experiments 001–007, with five deterministic weekly probes.

A separate **unmerged draft candidate** contains **84 tests**: **29 / 8 / 10 / 9 / 11 / 13 / 4**, with six deterministic probes. Windows/Python 3.14.7 and 3.12.10 passed the candidate's complete local runner. Ten runner-contract tests and two detected reverted-fix mutants are separate evidence.

The 004 Risk Guard / 005 Shadow Comparator follow-up executed 54 boundary scenarios, 1,000 randomized scenarios, 300 integration scenarios and 10 sanitized fixtures. The two candidate repairs reject duplicate normalized CSV headers and isolate malformed P/L parsing from the caller's Decimal state.

**005 is logic-verified pending independent review of the changed contract.** A local pass does not establish test-verified status for that revision, user-tested status, deployment, operating adoption or commercial demand.

## Evidence and remaining gates

- The earlier October 31 cycle repaired direct Decimal event encoding; that merged checkpoint remains distinct from the later review candidate.
- Remote jobs for the candidate did not start because of account payment/spending-limit eligibility. This is **CI pending — Actions limit**, not a successful CI run or an executed test failure.
- The dedicated experiment workflow remains manually disabled. This documentation update does not enable or rerun workflows.
- Main/Lab code, settings, schedulers and orders were not changed by the experiment cycle. An offline read-only audit of the completed October 26–30 trading week is separate from prototype verification.
- The earlier 004/005 plan proposed 84 tests/six probes and a 001/006 focus. The later follow-up above supersedes that proposed next scope.
- No user trial, release, profitability or commercial validation is claimed.

[October 31 validation and limitations](PAPERB_WEEKLY_2026-10-31.md) · [Module overview](../README.md#4-paperb-and-reusable-module-pipeline)

## Working boundaries

- Source remains under `experiments/`; module identifiers and history are preserved.
- Test and probe counts measure declared contracts, not product readiness.
- Raw operating records, credentials, personal data and private implementation links are excluded from this showcase.
- Operating adoption, deployment and actual operation require separate validation and decisions.

The October 17 checkpoint of 79 tests and three probes is historical. Later checkpoints supersede its current-status numbers without rewriting that evidence.
