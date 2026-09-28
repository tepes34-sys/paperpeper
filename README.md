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

## Next checkpoint

Move selected experiments into **user testing** with a clean environment, realistic sanitized inputs, README-only execution, and failure-path feedback.

Weekly validation will continue to turn newly discovered edge cases into regression tests.

## Scope

Public: experiment summaries, validation progress, sanitized demos, and intentionally released reusable tools.

Private: operational source, runtime data, credentials, account data, and internal configuration.

---

Software research project. Not financial advice.
