# paperA — 24/7 Shadow Market Lab

> A small, isolated crypto shadow-trading lab designed to stress-test reusable trading infrastructure without placing real orders.

## Why paperA exists

Paperpeper's U.S. equity workflow naturally has long idle windows during Korean daytime hours and weekends. paperA uses a 24/7 crypto market only as a **high-frequency source of events** so reliability logic can be exercised faster.

The primary goal is **not** to prove that a crypto strategy is profitable or transferable to stocks. The goal is to generate enough realistic market events to test collectors, state transitions, recovery logic, reconciliation, and reporting.

## Project boundary

- **No live trading**
- **No exchange account integration in V1**
- **No API keys required in V1**
- Public market data only
- Separate repository/runtime/database/scheduler from Paperpeper
- Any reusable improvement must return through Paperpeper Lab before Main

## Initial scope

| Area | V1 decision |
|---|---|
| Market | Crypto spot market |
| Symbols | BTC, ETH, SOL |
| Data | Public OHLCV / market data |
| Candle | 5-minute |
| Evaluation | Every 15 minutes |
| Storage | SQLite |
| Strategies | Two deliberately simple shadow strategies |
| Orders | Virtual only |
| Runtime | Korean daytime + weekends initially; 24/7 later if useful |

## Reference flow

```text
Public Market Data
        ↓
Collector
        ↓
Freshness / Validation
        ↓
Candle Store
        ↓
Candidate / Signal Engine
        ↓
Shadow Entry
    ┌───────┴───────┐
Strategy A       Strategy B
    ↓               ↓
Virtual Exit / State
        ↓
Ledger
        ↓
Black Box / Reconciler
        ↓
Daily Report
```

## What we are actually testing

### Reliability first

1. Duplicate-event prevention / idempotency
2. Restart recovery
3. Missing-candle catch-up
4. Stale quote rejection
5. Persistent open-position state
6. A/B pair consistency
7. Ledger consistency
8. Reconciler mismatch detection
9. Black-box event completeness
10. Scheduler continuity

### Strategy second

The first strategies should remain intentionally simple. They are traffic generators for the engine, not a claim of market edge.

Example structure:

- Strategy A: simple trend/volume entry with fixed virtual exit rules
- Strategy B: same entry sample with a different exit policy

Crypto-specific parameters are **not** promoted directly into U.S. equity trading logic.

## Validation gates

The first meaningful checkpoint is operational rather than financial:

- 7 consecutive operating days
- 700–1,000+ decision events
- 0 duplicate virtual orders
- 0 unexplained ledger mismatches
- successful restart recovery
- successful missing-data catch-up
- stale-data blocking verified
- failure events captured by the black box

After the baseline run, deliberate fault injection can be added:

- process termination during an evaluation cycle
- repeated candle delivery
- missing candle interval
- delayed/stale quote
- temporary data-source disconnect
- malformed market payload
- ledger/state mismatch

## Roadmap

### Phase 1 — Minimal collector
- Public market-data connection
- BTC / ETH / SOL
- 5-minute candle persistence
- basic freshness checks
- SQLite schema

### Phase 2 — Shadow engine
- candidate generation
- virtual entry
- A/B state separation
- virtual exits
- minimal daily report

### Phase 3 — Reliability layer
- idempotency
- restart recovery
- catch-up
- black-box logging
- reconciliation

### Phase 4 — Scheduled operation
- independent scheduler
- Korean daytime + weekend operation
- runtime health summary
- no dependency on an active Claude/ChatGPT session

### Phase 5 — Fault injection
- controlled crash/restart
- duplicates
- missing data
- stale data
- state disagreement

### Phase 6 — Reuse review
Classify findings into:

**Safe infrastructure candidates**
- collector hardening
- freshness logic
- retry/reconnect behavior
- idempotency
- reconciliation
- black-box logging
- report generation

**Requires stock-specific revalidation**
- signal scoring
- position-state rules
- timing assumptions

**Do not transfer directly**
- crypto profitability
- crypto stop/target values
- crypto volatility thresholds

## Roles

- **Claude:** implementation, tests, local runtime integration, scheduler setup
- **ChatGPT:** architecture, validation criteria, failure-case design, independent review
- **Owner:** final approval and promotion decisions

## Relationship to Paperpeper

paperA is a separate testbed, not a new production branch.

```text
paperA
  ↓  reusable finding
Paperpeper Lab
  ↓  stock-specific regression + operating validation
Paperpeper Main
```

A passing result in paperA is evidence that infrastructure is reusable under another event stream. It is **not** evidence that a trading strategy will work in U.S. equities.

## Expected value

A small V1 should already provide useful operating samples. The highest-value target is V2–V3 territory: enough recovery, idempotency, catch-up, black-box, and reconciliation logic to make paperA a practical stress environment without letting it grow into a second full trading project.

---

**Status:** Planned  
**Created:** 2026-09-30  
**Live trading:** Out of scope

Software research project. Not financial advice.
