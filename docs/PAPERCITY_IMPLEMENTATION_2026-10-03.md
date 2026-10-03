# paperCity — Core and facilities implementation checkpoint

October 3, 2026. The project has progressed from authored design artifacts to a locally implemented and tested simulation engine. This note supersedes the earlier design-only checkpoint for Core and facilities. Growth, policies, persistence, and the city interface remain future stages.

## Verified status

- **667 product test executions passed:** 544 existing Core cases and 123 facilities/economy cases. Counts include parameterized executions.
- **10 Core and 12 facilities authored scenarios** were compared with actual engine results. Every explicitly specified field in the 12 facilities scenarios matched; the original expected values were preserved.
- **12 facilities performance conditions passed** a provisional development budget: 15, 64, and 128 assets, each simulated for 1,000 and 10,000 days, with all records retained or consumed in 30-day chunks.
- **Core performance passed** its existing provisional budget using 12 fresh timing runs and four separate memory runs after the final code changes.
- The implementation and evidence were verified locally. This showcase update publishes documentation; it does not publish the game source or establish a release, public CI result, deployment, or independent reviewer approval.

## What is implemented

The Core owns immutable state and configuration, explicit integer units, configurable calendar boundaries, strict JSON parsing, deterministic records, and daily/monthly validation. Simulation calculation is separate from rendering, storage, network access, and wall-clock controls.

The facilities layer implements nine types: housing, farm, factory, power plant, shop, warehouse, park, hospital, and road. Construction and enabled-state commands apply at the first calculation day of a request. A command batch is validated before economic rules run. Failed requests return the original submitted state and empty result records when the declared simulation failure contract applies.

Enabled roads form a simple undirected connectivity graph anchored at the initial district. Enabled and reachable facilities can operate. Disabled and disconnected assets remain observable and continue to incur their configured maintenance treatment.

Daily calculation follows an explicit dependency order:

1. Allocate labor to generators and determine power supply.
2. Reserve power for housing and facility priorities.
3. Allocate the remaining labor within supported job capacity.
4. Calculate production, warehouse-supported food delivery, and actual consumption.
5. Apply services, happiness, and pollution effects.
6. Preserve daily observations and perform one month-end settlement when due.

Allocation uses integers, proportional distribution, largest remainders, and stable identifier tie-breaking. Power limits supported jobs; production does not multiply the power fraction a second time. Unused reserved power is explicitly accounted for.

Monthly business tax and maintenance use accumulated daily activity. Taxes round down and maintenance rounds up at settlement, with the rounding basis recorded. Disabling a facility on the last day does not erase its earlier activity. Four daily ledgers explain food, treasury, happiness, and pollution changes; typed events and facility observations preserve the causal details.

## Version and compatibility boundaries

The facilities experiment uses explicit `pc-core-draft-3`, `pc-balance-v2`, `pc-state-v2`, and `pc-phase2-rules-v1` contracts. It exposes separate facilities/economy APIs and reuses the existing pure scalar calculation and observation kernels. It does not silently migrate an old state.

The existing Core source, tests, authored examples, and measurement tools remained byte-identical during Phase2. Event versions remain explicit: the facilities stream begins its sequence at one and distinguishes happiness and pollution saturation; the earlier Core event contract remains unchanged.

Declared rule-evaluation failures preserve the submitted state. Programming errors and exceptional runtime failures propagate under their defined contract. This is a contract for returned in-memory values; external side effects, database rollback, persistent exactly-once delivery, and concurrent-controller safety are not established.

## Review and regression findings

Core review reproduced two classes of defects before repairing them: impossible accumulated observations after subtracting the final day, and diagnostics/configuration handling for integers too large for decimal serialization. Thirteen new checks failed before the fixes; all 16 added regression cases passed afterward, taking the Core baseline to 544.

Facilities review added regressions for impossible earlier facility activity and a stored maintenance accumulator exceeding the configured limit on a zero-day request. Those invalid inputs were accepted before the fixes and rejected afterward. A fresh-process import test also verifies the repair of a command-module circular import.

Tests cover schema and type boundaries, immutability, canonical hashes, commands and connectivity, all nine roles, shortages and partial allocation, service caps, rounding, ledgers, event identity, late failures, configurable month lengths, and split execution. JSON state roundtrips include days 0, 1, 29, 30, and 31. Small allocation combinations are exhaustively checked and seeded facility combinations add integration coverage.

## Facilities performance observations

The measurements below use Windows and CPython 3.12.14. Wall time **includes Python allocation tracing**. Peak allocation is measured by `tracemalloc`, not process RSS. Each condition has one sample and is judged against a budget fixed before measurement.

| Assets | Days | Record handling | Traced seconds | Peak Python MiB | Result |
| --- | ---: | --- | ---: | ---: | --- |
| 15 | 1,000 | Consume 30-day chunks | 12.21 | 1.15 | PASS |
| 15 | 1,000 | Retain all | 11.64 | 7.67 | PASS |
| 15 | 10,000 | Consume 30-day chunks | 126.72 | 1.34 | PASS |
| 15 | 10,000 | Retain all | 118.54 | 79.28 | PASS |
| 64 | 1,000 | Consume 30-day chunks | 39.64 | 1.17 | PASS |
| 64 | 1,000 | Retain all | 34.68 | 21.95 | PASS |
| 64 | 10,000 | Consume 30-day chunks | 356.15 | 1.31 | PASS |
| 64 | 10,000 | Retain all | 349.99 | 224.19 | PASS |
| 128 | 1,000 | Consume 30-day chunks | 66.62 | 1.68 | PASS |
| 128 | 1,000 | Retain all | 64.85 | 40.14 | PASS |
| 128 | 10,000 | Consume 30-day chunks | 631.20 | 1.68 | PASS |
| 128 | 10,000 | Retain all | 640.52 | 402.11 | PASS |

For each workload, the two paths produced the same final state digest and total record counts. The largest workload generated **1,280,000 facility observation rows**. Chunked execution commits success per request; it does not have the same failure boundary as one atomic 10,000-day request. Equal long-run final states and counts do not assert a record-by-record comparison of all long-run outputs.

The provisional facilities ceilings are 512 MiB for retaining all records and 32 MiB for chunk consumption, with workload-specific traced time limits. Earlier samples from intermediate source versions were preserved separately and excluded from the final assessment. All final facilities and Core measurements were run serially on the same final source fingerprint.

## Core performance recheck

Core timing was measured **without allocation tracing**, three repeats per day-count/record-path group. Separate runs measured memory. These times should not be compared directly with the traced facilities table.

| Days | Record handling | Median seconds | Slowest seconds |
| --- | --- | ---: | ---: |
| 1,000 | Retain all | 4.14 | 4.17 |
| 1,000 | Consume daily | 4.43 | 4.57 |
| 10,000 | Retain all | 41.66 | 42.42 |
| 10,000 | Consume daily | 44.70 | 44.97 |

The 10,000-day Core memory runs observed approximately 13.63 MiB when retaining records and 1.37 MiB when consuming daily. The existing provisional budget was preserved; an earlier PASS was not reused for changed source.

## Remaining gates

The current population is fixed and the economic values are synthetic verification inputs. Passing tests and development budgets does not validate fun, balanced long-run finances, varied winning strategies, population growth, closures, or a playable game.

The next functional stage is **Phase3 growth and decline design**. Later gates cover policies, persistence/reconciliation, City Black Box integration, the city interface, and playtesting. Existing reliability-module reuse remains a candidate until its benefit is demonstrated in this project.

[Prototype plan](PAPERCITY_V0_1_PLAN.md) · [October 3 portfolio worklog](WORKLOG_2026-10-03.md#6-papercity)
