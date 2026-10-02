# paperCity v0.1 — Prototype Plan

**Status:** planned prototype

paperCity is a small city-management simulation concept designed to test whether the reusable reliability modules developed around paperpeper can remain useful outside trading.

The game is not intended to compete with large city builders. Its first question is simpler:

> Can a city feel alive when the player mainly makes numerical and policy decisions, while growth and decline become visible on the map?

## Core loop

**Observe → decide → simulate → react → grow or decline → explain**

The player starts with a small settlement and manages agriculture, industry, commerce, power, housing, and public services.

Successful operation should expand population, active land, building density, and economic activity. Persistent failures should have visible consequences: business closures, unemployment, population outflow, dark or inactive districts, and eventual contraction.

## v0.1 simulation

### Core resources

- Population
- Budget
- Food
- Electricity
- Jobs
- Happiness
- Pollution

### Initial facilities

1. Housing
2. Farm
3. Factory
4. Power plant
5. Shop
6. Warehouse / logistics facility
7. Park
8. Hospital
9. Road

Facilities are intentionally few. The prototype should first prove that their interactions create meaningful decisions.

Examples:

```text
Stable food + power
→ more jobs
→ population inflow
→ more commercial demand
→ higher tax revenue
→ district expansion
```

```text
Power shortage
→ lower factory output
→ closures
→ unemployment
→ lower consumption
→ store closures
→ weaker tax revenue
→ service cuts
→ population outflow
```

## Time model

The current design uses continuous simulation with pause and speed controls rather than strict turn-based play.

Candidate baseline:

- about 1 real second = 1 in-game day
- pause / 1× / 2× / 5× / 10×
- facility operation evaluated daily
- taxes, maintenance, migration, and growth/decline evaluated monthly

This is a design target, not a fixed implementation contract yet.

## Visual direction

The preferred prototype style is a **2D isometric miniature city with a modern numerical UI**.

Visuals should communicate state rather than pursue detailed 3D rendering.

Growth may appear as:

- more active tiles
- denser or taller housing
- more traffic and lights
- expanded industrial and commercial areas

Decline may appear as:

- vacant housing
- closed shops
- inactive factories
- reduced traffic and lighting
- deactivated outer districts

## Proposed implementation stack

- Python — simulation and economic rules
- SQLite — state, history, and Black Box records
- JSON — facility and policy balancing data
- pytest — unit and regression tests
- Pygame — initial rendering candidate
- Git/GitHub — versioned design and verification evidence

## Reusable module experiments

paperCity is also a portability test.

| Existing module / pattern | paperCity experiment |
| --- | --- |
| Ledger Inspector | Detect inconsistent city finance, production, and consumption records |
| Trading Black Box | City Black Box explaining population drops, closures, and budget changes |
| Reconciler | Compare persisted state with reconstructed simulation state |
| Shadow Comparator | Later basis for Shadow City policy A/B experiments |
| Main / Lab separation | Candidate split between stable play and experimental rules |

These are **reuse targets**, not claims that the integrations already exist.

## Verification plan

Development should proceed in independently testable slices:

1. Core city-state engine
2. Nine facility types
3. Growth and decline rules
4. Policy effects
5. Save / restore and reconciliation
6. City Black Box
7. UI consistency

Automated long-run simulations (roughly 1,000–10,000 ticks/turn-equivalents depending on the final clock model) should also look for:

- negative or impossible state
- runaway money/resource creation
- unavoidable collapse
- dominant single-strategy play
- save/restore divergence
- unexplained state transitions

## v0.1 completion target

- one city
- seven core resources
- nine facility types
- about ten policy controls
- visible growth and contraction
- save / load
- City Black Box
- simple 2D city view
- automated tests for core rules
- long-run simulation checks

## Later candidates

**v0.2:** Shadow City A/B, events, stronger industry identities, stage-based unlocks.

**v0.3:** population cohorts, logistics, firms, transportation, advanced industries.

An era/progression system is intentionally deferred. A later version may use city-development stages such as settlement → agricultural town → early industrialization → electrification → mass production → modern service city.

---

This document describes a prototype direction, not a released game or completed implementation.
