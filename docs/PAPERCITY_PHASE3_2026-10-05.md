# PaperCity Phase 3 — Local implementation and author review

**October 5, 2026: P3-A–F implemented and tested locally; author boundary review completed.** Latest suite: **1,099 passed = 544 Core + 123 facilities/economy + 432 growth**. Proposed balance values remain experimental. Separate independent approval, source PR/integration and remote CI are pending at this publication cutoff.

## Stage evidence

| Stage | Implemented scope | New executions | Full suite at that checkpoint |
| --- | --- | ---: | ---: |
| P3-A | Explicit V3 state/configuration, strict loaders/hash, actual accumulators and lifecycle records | 104 | 771 |
| P3-B | Actual monthly conditions, migration and pure resource admission probes | 52 | 823 |
| P3-C | Closure/reopening counters, actual upkeep, sequential paid reopening | 70 | 893 |
| P3-D | Paid resettlement, all-or-nothing command batch, residential occupancy classes | 102 | 995 |
| P3-E | Real daily/monthly coordinator, conserved ledgers, events, output checks and split replay | 76 | 1,071 |
| P3-F | Actual long-run scenarios, competing demand and performance tooling | 12 | 1,083 |
| Author review | Two reproduced defects, minimal fixes and boundary regressions | 16 | 1,099 |

Counts are parameterized test executions. Historical checkpoint totals are not added together. Authored arithmetic, hypothetical resource candidates and real engine advancement are distinct evidence.

## Actual execution scenarios

| Scenario | Observed result | Limit |
| --- | --- | --- |
| GROW, 120 days | Population 100→102, then housing capacity prevents further inflow | One authored housing-limited city |
| CRISIS, 120 days | Power disabled on day 31; power/employment/activity/tax drop; populations 102/91/81/72 and business closure on day 90 | Explicit experimental crisis settings |
| RECOVER, 160 days | Same 90-day crisis prefix; power restored on day 91; paid 16000 reopening on day 150; actual factory activity from day 151 | Business recovery, without proof of general population/happiness recovery |
| ZERO, 1,200 days | Crisis reaches zero on day 870; no automatic inflow; separate paid seed 20 and rejection/rollback controls | No free food/assets; depleted crisis city does not automatically qualify for resettlement |
| CHATTER, 330 days | Alternating low/high months do not immediately close businesses; two bad months close them; opportunity counter resets; one factory reopens on day 300 | Combined demand must preserve earlier admissions; stable ID priority is not a fairness policy |
| COMPETITION, 121 days | Each store is viable alone, but combined demand fails the threshold; one is admitted on day 120 and becomes active next day | Explicit demand/seed overrides; no universal city-success claim |

Reopening candidates do not overwrite actual closed-facility observations or create current tax revenue. Closed-business upkeep, manual enabled intent and actual operating availability remain distinct. Paid resettlement does not create assets or food. Residential occupancy classes are not a land-area density or housing-upgrade implementation.

## Reproduced defects and fixes

- **P3R01, P2:** separate valid items could total income 24000 under cap 23999 or upkeep 6180 under cap 6179; upkeep 4980 plus reopening 16000 could exceed a 20979 expense cap. The actual month-plan validator now checks each side's total, and the input-linked result checker bounds total monthly expense including reopening. Over-limit advancement returns the original input state and empty records. Twelve regressions cover each total at cap−1/cap/cap+1 and internally consistent over-limit output rejection without evaluating Rules again.
- **P3R02, P2:** an open-month snapshot with current population 100 and latest monthly after-population 102 was accepted; a zero-after-month snapshot could carry 21 despite configured seed 20. Open-month population must retain the latest monthly after value, except zero can remain zero or become the configured resettlement seed. Two forged-state/JSON cases are rejected, and two real next-day/mid-month resettlement controls remain valid.

Before the money fix, the 12 config-valid regression cases had 6 failures/6 passes; the two config-valid population regressions failed before their fix. Afterward, the relevant 196 executions and full 1099 suite passed without failures/errors/skips. The full suite ran in 437.78 seconds. A state validator checks feasible relations, without authenticating the entire historical record.

## Modified-source performance recheck

| Actual days | Return path | Elapsed seconds | Process peak MiB | Local budget result |
| --- | --- | ---: | ---: | --- |
| 1,000 | Retain all records | 48.88 | 37.12 | PASS |
| 1,000 | Consume daily | 53.26 | 28.44 | PASS |
| 10,000 | Retain all records | 487.26 | 119.35 | PASS |
| 10,000 | Consume daily | 525.76 | 28.68 | PASS |

Same preselected local experimental budgets:120/1200 seconds for 1000/10000 days,512 MiB retained or 128 MiB daily-consumed process peak. Each cell used a fresh process and one 12-facility authored city. Source/tool/config/fixture/budget identity was checked during measurement. Both paths and the earlier P3-F results match in final state, all ordered-record digests/counts and monthly population. All six sampled actual scenario records also match the earlier P3-F run.

Native process peak includes preparation and differs from traced Python allocations; those measurements are not interchangeable. One sample per cell does not establish statistical reliability, a speed improvement, maximum 128-facility performance, a release SLA or gameplay balance.

## Current boundary and next step

Author review is not a separate independent reviewer's approval. Existing Core/facilities/economy source, V3 schema and default experimental settings were preserved. The cumulative Phase 3 source is still local/uncommitted at this publication cutoff. Next: independent review preparation, source PR/remote validation, then a separate Phase 4 policy slice. Persistent save/recovery, UI, City Black Box, external playtesting and release remain later work.

[October 5 cross-project evidence](WORKLOG_2026-10-05.md) · [Prototype plan](PAPERCITY_V0_1_PLAN.md)

## Follow-up after the initial publication

The cumulative experimental Phase3 source and author fixes have now been committed and pushed to an isolated branch, with a draft change prepared for separate review. The tested local source and committed source match exactly. Windows and Ubuntu Python 3.12 passed 1,099 tests per job for both push and pull-request runs; all four downloaded result files confirmed 544 Core + 123 facilities/economy + 432 growth, with no failures, errors or skips. Those repeated jobs are not four distinct supported environments or 4,396 unique tests.

Separate reviewer approval, main integration and game-balance adoption remain pending. Phase4 policy preparation is DESIGN_ONLY: a two-tax-control first slice, explicit command timing/no-change/rollback, nonretroactive daily tax accrual and one monthly rounding step, and 12 planned checks. The current engine has no company-level after-tax cash/profit state; changing city tax receipts alone does not implement a policy tradeoff. No policy code, product-policy test or adopted balance result is claimed.
