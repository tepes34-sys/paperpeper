# Paperpeper

> AI-assisted algorithmic trading R&D — paper trading, risk controls, strategy experiments, and reusable trading tools.

## v1.5 · Current checkpoint

**7 experiments · 55/55 tests passed · 7/7 test-verified**

Paperpeper uses a private operating system and an isolated **GPT Lab** for small, reusable experiments. Ideas are prototyped away from the trading system, independently reviewed, and only considered further after regression testing.

## Experiments

| # | Experiment | Purpose | Status |
|---|---|---|---|
| 001 | Trade / Ledger Inspector | Find inconsistent trade and ledger records | **test-verified** |
| 002 | Trade Report Generator | Summarize validated completed trades | **test-verified** |
| 003 | Trading Black Box | Preserve structured decision and event context | **test-verified** |
| 004 | Risk Guard | Check position and cash limits before an order | **test-verified** |
| 005 | Strategy Shadow Comparator | Compare strategies on paired trade samples | **test-verified** |
| 006 | Crash Recovery / Reconciler | Detect differences between expected and observed state | **test-verified** |
| 007 | Broker Adapter Kit | Define a broker-independent order boundary | **test-verified** |

## Validation loop

```text
Prototype
   ↓
Logic contract
   ↓
Automated tests
   ↓
Independent review
   ↓
Bug → regression test → fix
   ↓
Independent re-run
   ↓
test-verified
```

Independent review has already exposed issues missed by earlier tests, including test-discovery failures, validation-order bugs, serialization edge cases, and symbol-normalization collisions.

**test-verified** means the documented contract passed its automated tests and an independent re-run. It does not mean `user-tested`.

## Field-derived hardening · 2026-09-28

A community-reported failure pattern was translated into adversarial Lab cases instead of being copied as a feature request.

**Result:** 3 defects reproduced and fixed · 37 Lab tests added · 509 Main regression tests passed · Linux/Windows CI passed · production ledger pre-check found 0 issues.

The hardening covered duplicate exit protection, order/trade identity collisions, invalid market quotes, and ledger reconciliation alerts. Changes were reproduced before fixes, regression-tested, independently reviewed, and promoted from Lab toward Main only after the operating ledger passed a read-only compatibility check.

This established a repeatable loop:

`External failure → adversarial case → Lab reproduction → regression fix → independent review → operating-data check → Main promotion`

## First-session operations check · 2026-09-29

The first paired Shadow A/B paper session recorded seven candidate entries in each strategy. Entry pairs matched, no candidate was missing, and all 14 observed market-data requests succeeded. The isolated Lab ran its scheduled checks and produced a review after a manual export; its Shadow A/B samples remain open, so there is no strategy performance result yet. The Lab suite passed 532 tests (one skipped).

The review also caught a path-resolution error in external check scripts and traced an interrupted export to a desktop-app restart. Both checks were rerun successfully and the review was recovered. Updated research-budget instructions are deployed; their first live usage result is still pending verification.

## Planned reliability checkpoint · 2026-10-03, 08:00 KST

**Plan confirmed on September 30; fixes and operating-environment validation are pending.**

An additional code review reproduced two cases in an isolated environment while all 28 selected existing tests passed: a newly raised breakeven stop could be triggered by a session low recorded before the stop changed, and concurrent callers could both acquire a released lock when file deletion was denied. Occurrence in the operating environment has not been established. Independent reproduction is scheduled before changes.

Saturday's work order:

1. **Weekly inspection:** record scheduler gaps, errors, paper trades, Shadow A/B, and report status before making changes.
2. **Lab reproduction and fixes:** address the two cases with regression tests, plus small operational issues found during inspection.
3. **Main/Lab comparability:** document actual configuration, code version, input period, initial account state, and change timestamps; distinguish controlled replay from live observation.
4. **Read-only broker integration:** validate account, holdings, and balance responses against the broker app. Distinguish request/parse failures from valid zero balances. The paper ledger is not a real-account reconciliation target.
5. **Strategy reporting:** label potentially affected trades and show both full results and results excluding matched A/B recommendation pairs. Preserve historical ledger records and learning flags.
6. **Promotion and integration checks:** promote through a Main-based PR after validation, outside operating hours, without switching branches in the operating checkout.
7. **GPT Lab 001–007:** recheck if time permits; otherwise defer to the following week.

Validation gates include post-change price chronology for raised stops, real two-process lock tests on the mounted filesystem (including interruption and stale-lock recovery), and broker-app comparisons using the same account, currency, balance category, and observation time. Valuation differences caused by quote timing must be explained separately.

Completion reports will distinguish reproduction, changes, test results, operating-PC verification, and remaining limitations. **Live order execution is outside this checkpoint's scope.** Credentials, account identifiers, raw broker responses, and private operating data remain private.

## Next checkpoint

Move selected experiments into **user testing** with a clean environment, realistic sanitized inputs, README-only execution, and failure-path feedback.

Weekly validation will continue to turn newly discovered edge cases into regression tests.

## Scope

Public: experiment summaries, validation progress, sanitized demos, and intentionally released reusable tools.

Private: operational source, runtime data, credentials, account data, and internal configuration.

---

Software research project. Not financial advice.
