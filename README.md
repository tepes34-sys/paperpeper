# Paperpeper

> An AI-assisted algorithmic trading research project focused on experimentation, paper trading, risk controls, and reproducible analysis.

**Paperpeper** is a personal R&D project exploring how AI-assisted research, systematic trading logic, isolated experiments, and human review can work together.

This repository is the **public showcase**. Operational code, credentials, private data, databases, and internal configuration remain in a separate private environment.

## Current checkpoint

The first GPT Lab experiment series has reached a reproducible engineering checkpoint:

- **7 isolated prototypes**
- **55 automated tests**
- **55/55 passed in an independent local re-run**
- **7/7 prototypes currently test-verified**

`test-verified` has a deliberately narrow meaning here: the implementation passed the automated tests for its documented contract and was independently re-run. It does **not** mean user-tested, production-ready, commercially validated, profitable, or suitable for live trading.

## Experiment series

| # | Experiment | Focus | Status |
|---|---|---|---|
| 001 | Trade / Ledger Inspector | Detect ledger and trade-record integrity problems | test-verified |
| 002 | Trade Report Generator | Generate basic statistics from validated completed trades | test-verified |
| 003 | Trading Black Box | Preserve structured decision/event context for later analysis | test-verified |
| 004 | Risk Guard | Apply small pre-order position and cash safety rules | test-verified |
| 005 | Strategy Shadow Comparator | Compare strategies using paired trade samples | test-verified |
| 006 | Crash Recovery / Reconciler | Compare expected and observed cash/position state | test-verified |
| 007 | Broker Adapter Kit | Explore a broker-independent order boundary | test-verified |

These are intentionally small cores rather than finished products.

## How experiments evolve

```text
Research / Ideas
       ↓
   GPT Lab
       ↓
Small isolated prototype
       ↓
Document the logic contract
       ↓
Automated tests
       ↓
Independent review / adversarial inputs
       ↓
Fix + regression tests
       ↓
Independent re-run
       ↓
test-verified
       ↓
user-tested (only after separate usability evidence)
```

Independent review has already found issues that initially passed narrower tests, including broken test discovery, malformed source edits, validation-order bugs, serialization edge cases, and normalization collisions. Those findings are treated as regression-test inputs rather than hidden as failed attempts.

## Verification levels

- **prototype** — minimal implementation exists; independent verification is pending.
- **logic-verified** — expected behavior and invariants are documented and the core logic has been reviewed.
- **test-verified** — the actual test runner and independent review pass the currently documented contract.
- **user-tested** — a separate usability stage requiring an independent user/environment, realistic sanitized data, completion of the core workflow, failure-path feedback, and recorded observations.

A status may move backward when code or tests change.

None of these levels represents market demand, willingness to pay, investment performance, or production readiness.

## What Paperpeper explores

- **Paper trading** — testing trading logic without placing real orders
- **Risk controls** — position sizing, exposure limits, entry validation, and safety gates
- **Strategy experiments** — comparing alternative strategies in isolated environments
- **Trading observability** — understanding why a trade happened and what happened afterward
- **Data integrity** — detecting inconsistent records, duplicate actions, and ledger problems
- **AI-assisted development** — using AI for research, prototyping, implementation support, and independent review

## Public vs. private

This repository contains only material intentionally selected for public viewing.

**Public here**
- Project overview and engineering checkpoints
- Selected experiment descriptions
- Sanitized examples and demonstrations
- Verification methodology
- Reusable tools if intentionally released

**Kept private**
- API keys and credentials
- Personal trading/account data
- Operational databases and runtime state
- Private research inputs
- Production source code
- Internal configuration

## Next

The next milestone is not simply adding more code. Selected experiments will be evaluated for **user testing**: can another person or a clean environment complete the intended workflow from the documentation, understand the output, and recover from invalid input without private project context?

Follow-up design items remain experimental and will be prioritized by observed usability rather than by feature count.

## Status

Paperpeper is an evolving hobby/R&D project. Experiments may change, be rejected, or remain internal as evidence accumulates.

The private trading system remains the primary project. Public material is a deliberately sanitized record of selected engineering ideas and validation progress.

## Disclaimer

Paperpeper is a software and research project, not financial advice. Public materials should not be interpreted as investment recommendations, live-trading guarantees, profitability claims, or claims of future performance.

---

Built through an ongoing human + AI development workflow.
