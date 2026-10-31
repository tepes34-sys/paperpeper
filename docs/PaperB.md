# PaperB

PaperB is the isolated reusable-module research track within the existing Kanna repository. Its seven experiments cover ledger inspection, reports, event records, numeric risk checks, paired comparison, recovery reconciliation, and a minimal broker-adapter boundary.

## Current checkpoint — October 31, 2026

The merged research baseline contains **82 tests**: **29 / 8 / 10 / 9 / 9 / 13 / 4** for experiments 001–007, with five deterministic weekly probes.

A separate **unmerged draft candidate** contains **84 tests**: **29 / 8 / 10 / 9 / 11 / 13 / 4**, with six deterministic probes. Windows/Python 3.14.7 and 3.12.10 passed the candidate's complete local runner. Ten runner-contract tests and two detected reverted-fix mutants are separate evidence.

The 004 Risk Guard / 005 Shadow Comparator follow-up executed 54 boundary scenarios, 1,000 randomized scenarios, 300 integration scenarios and 10 sanitized fixtures. The two candidate repairs reject duplicate normalized CSV headers and isolate malformed P/L parsing from the caller's Decimal state.

**005 is logic-verified pending independent review of the changed contract.** A local pass does not establish test-verified status for that revision, user-tested status, deployment, operating adoption or commercial demand.

## Evidence and remaining gates

- The earlier October 31 cycle repaired direct Decimal event encoding; that merged checkpoint remains distinct from the later review candidate.
- Remote jobs for the candidate did not start because of account payment/spending-limit eligibility. This is **CI pending — Actions limit**, not a successful CI run or an executed test failure.
- The dedicated experiment workflow remains manually disabled. This documentation update does not enable or rerun workflows.
- Main/Lab code, settings, schedulers and orders were not changed by the experiment cycle. An offline read-only audit of the completed October 26–30 trading week is separate from prototype verification.
- Next proposed baseline: **84 tests + six probes**, subject to candidate review/integration. Next focused modules: **001 Ledger Inspector / 006 Reconciler**.
- No user trial, release, profitability or commercial validation is claimed.

[October 31 validation and limitations](PAPERB_WEEKLY_2026-10-31.md) · [Module overview](../README.md#4-paperb-and-reusable-module-pipeline)

## Working boundaries

- Source remains under `experiments/`; module identifiers and history are preserved.
- Test and probe counts measure declared contracts, not product readiness.
- Raw operating records, credentials, personal data and private implementation links are excluded from this showcase.
- Operating adoption, deployment and actual operation require separate validation and decisions.

The October 17 checkpoint of 79 tests and three probes is historical. Later checkpoints supersede its current-status numbers without rewriting that evidence.
