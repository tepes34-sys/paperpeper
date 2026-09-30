# paperA — Design Freeze v1.0

> Isolated crypto shadow-market lab for stress-testing reusable trading infrastructure. No live orders, no account integration, no API keys.

## Status

**DESIGN FROZEN v1.0 · 2026-09-30**  
Implementation has not started.

paperA exists to generate frequent, realistic market events during Korean daytime hours and weekends. It is not intended to prove crypto profitability or transfer a crypto strategy directly into U.S. equities.

## Frozen V1 scope

| Area | Decision |
|---|---|
| Market data | Upbit Quotation REST |
| Symbols | KRW-BTC, KRW-ETH, KRW-SOL |
| Currency | KRW only |
| Candle | 5-minute OHLCV |
| Session | 09:00–18:00 KST every day |
| Evaluation | Every 15 minutes |
| Entry cutoff | Last new entry at 17:00; blocked from 17:15 |
| Session close | 18:00 SESSION_END |
| Storage | SQLite |
| Runtime | Windows Task Scheduler, short run every 5 minutes |
| Orders | Virtual only |
| Account/API key | None |

## Core principle

**Reliability first, strategy second.**

Primary targets are idempotency, restart recovery, missing-data backfill, stale-data blocking, state persistence, ledger consistency, reconciliation, Black Box capture, safe mode, quarantine, and deterministic reporting.

## Session model

- 09:00: warm-up run loads recent candles for SMA20.
- 09:15–17:00: normal evaluation and entry allowed.
- 17:15–17:45: candidates are recorded but new entries are blocked.
- 18:00: normal exit logic runs first; remaining positions use the real session-end candle for SESSION_END.
- Missing session-end price → QUARANTINED. No estimated or stale fill.

### Run vs cycle

- run = one process invocation
- operational cycle = one regular 5-minute collection/processing slot
- warm-up run = session-start preparation

When the 09:00 warm-up is a separate invocation, record **109 runs/day = 1 warm-up + 108 operational cycles**. Reliability statistics must not mix these terms.

## Shared candidate / A-B model

Entry candidates are generated once outside either strategy. Each strategy records TAKEN or an explicit SKIP reason.

### Strategy A
- shared SMA20 upward-cross candidate
- time exit after 4 evaluation ticks / 60 minutes
- SESSION_END

### Strategy B
- same shared candidate
- +0.6% TP
- -0.4% SL
- 16-tick / 4-hour MAX_HOLD
- SESSION_END

If a strategy exits a symbol on a decision tick, same-tick re-entry is prohibited and recorded as **SKIP_SAME_TICK_EXIT**.

Fair comparison uses only paired candidates where A and B both entered and both positions remained CLEAN.

## Reliability vs performance

Every position carries **integrity = CLEAN | AFFECTED**.

A position becomes permanently AFFECTED after recovery processing, stale/safe-mode exposure, quarantine, injected-fault exposure, or a recovered exit.

- Operational reliability includes every event.
- Strategy performance uses only CLEAN + LIVE positions under the current strategy version.
- Ledger retains all activity including explicit VOID reversals.

## Missing intervals

Only real exchange OHLCV belongs in the candle table. Upbit no-trade and missing-interval state is stored separately in **interval_status** with NO_TRADE / MISSING / CONFIRMED.

No synthetic null-price candle is passed to strategy logic.

## Safety model

- NORMAL: collection yes / exits yes / entries yes
- SAFE: collection yes / exits yes / entries no
- HALT: collection no / exits no / entries no

Gap handling:
- G0: recovered in same run
- G1: 1–3 missed evaluation ticks, recovered; WARNING
- G2: 4+ missed ticks, recovered; symbol SAFE
- G3: backfill fails; open position QUARANTINED

Unknown prices are never used for forced exits. Long-unresolved quarantined positions may be kept or explicitly VOIDed with compensating ledger events.

## Core invariants

1. At most one entry for the same strategy, symbol, and decision tick.
2. Every fill price comes from a real exchange candle.
3. At most one OPEN/QUARANTINED position per strategy and symbol.
4. Candidate generation is strategy-independent.
5. Historical recovery never creates a new entry.
6. AFFECTED never returns to CLEAN.
7. paperA cannot import Paperpeper modules.
8. Ledger mismatches are surfaced, never silently corrected.

## Validation gates

### Track 1 — operational reliability, fixed 7-day evaluation

- ≥99% operational-cycle success outside fault-test windows
- ≥99.9% collection after backfill
- 0 unresolved G3 gaps outside test windows
- ≥1,400 decision events
- 0 duplicate virtual entries/exits
- duplicate-defense path observed at least once
- 0 unexplained ledger mismatches
- reconciliation on every operational cycle
- 0 OPEN positions after session end
- all planned fault-injection scenarios pass

### Track 2 — strategy sample, 7–21 days

- ≥30 CLEAN entries/exits per strategy
- ≥20 paired CLEAN samples
- Strategy B observes at least one TP and one SL

If the sample is insufficient, time is extended rather than loosening strategy conditions.

## Fault injection

Planned scenarios include transactional crash, short/long network gaps, failed backfill, simulated 429/418, stale data, duplicate engine call, KILL switch, and missing SESSION_END candle. Injected events are tagged and excluded from CLEAN performance samples.

## Transfer path to Paperpeper

Reusable findings move through a Portable Improvement Note (PIN):

**FOUND → REPRODUCED_A → FIXED_A → EXTRACTED → LAB_REPRODUCED → LAB_FIXED → REGRESSION_PASSED → MAIN_REVIEW → ADOPTED / REJECTED**

Paperpeper Lab must independently reproduce the invariant using U.S.-equity fixtures before Main review.

## Planned implementation order

1. Store the frozen design and measure candidate frequency from a 14-day Upbit fixture.
2. Build schema/version/currency checks.
3. Build fixture-based collector.
4. Add run-once lifecycle, lock, session handling, and Black Box.
5. Add shared candidates and pure A/B strategies.
6. Add transactions, idempotency, LIVE/RECOVERED handling, SESSION_END.
7. Add ledger, reconciliation, and VOID handling.
8. Add SAFE / quarantine / acknowledgement flow.
9. Connect the public Upbit adapter.
10. Add reports and ALERT artifacts.
11. Add controlled fault injection.
12. Pass restart-equivalence testing.
13. Register Task Scheduler and run a one-day trial.
14. Begin the seven-day reliability run; extend only strategy sampling if needed.

## Repository separation

Planned local paths:

- C:\Users\CSW\Desktop\paperA — source repository
- C:\paperA-data — DB, config, logs, reports, backups

The implementation will live in a dedicated paperA repository. This file remains a public design summary.

## Roles

- **Claude:** implementation, tests, local runtime, Task Scheduler
- **ChatGPT:** architecture, validation gates, failure-case review, independent review
- **Owner:** final approval and promotion decisions

---

**Design:** Frozen v1.0  
**Implementation:** Not started  
**Live trading:** Out of scope

Software research project. Not financial advice.