# PaperCity Phase 4 tax slice and October 5 closing evidence

**October 5 closing checkpoint: Phase 3 A–F and the Phase 4 tax slice A–F independently reviewed, repaired, and merged into development main.** Final local suite: **1,466 passed = 544 Core + 123 facilities/economy + 438 growth + 361 policy**. Windows and Ubuntu Python 3.12 each passed the same suites after integration; all eight downloaded test-result files were checked. This remains an experimental engine.

Two separate AI reviewers inspected growth/recovery and policy code independently of the implementation author. Both reproduced a P2 ordering defect at facility ID width changes: valid sparse restored cities could fail after construction. The author repaired paired asset/lifecycle ordering in both producers and independent command replay; the reviewers rechecked the fixes and reported no unresolved blocker. Twelve new product regressions cover 10,000 / 100,000 / 1,000,000 sequence boundaries, strict JSON restore, mixed commands, actual advancement and forged-order rejection. Independent scratch checks are recorded separately from the product-test count. This is an independent AI-agent review, not a human code-review or user-trial claim.

## Implemented tax contract

The explicit immutable V4 state has current resident-tax and business-tax controls, absolute-value commands, strict loaders and a balance hash. A changed value charges the configured fee; an unchanged value is free. Mixed construction, enabled-state, resettlement and policy commands retain caller order and publish no partial state or records on declared failure.

Actual daily observations accrue current resident tax and per-facility business tax without retroactively changing earlier days. Monthly settlement floors each facility's accumulated business amount once, sums actual rows, then applies closure, migration, paid reopening and occupancy updates. The open-month policy accumulator resets after settlement. Hypothetical reopening/resettlement resources do not create current tax receipts. Five resource ledgers preserve conservation.

V3 snapshots are not silently promoted into V4. Fresh-city physical inputs and valid V4 snapshots have explicit contracts. The implemented slice contains two tax controls; roughly ten total policy controls remain a prototype target.

## Author and independent evidence

Author review had already repaired an untrusted-output policy-ID path that could throw before producing a diagnostic. Eighteen regressions cover invalid IDs, substituted values/fees/status/family, result counts and order without reevaluating Rules or resource probes. The closing independent ordering repair adds six growth and six policy regressions. Historical checkpoint totals (1,099 growth-stage and 1,454 policy-stage) are superseded for the final source by 1,466 executions, and are not added together.

The final local run has no failures, errors or skips. Growth and policy final revisions passed remote checks; development-main post-merge tests passed on Windows and Ubuntu with Python 3.12. Each operating system ran Core544 + facilities/economy123 + growth438 + policy361 = 1466, across four suite jobs. Repeated CI executions are not additional unique product tests or new supported Python versions. Downloaded result membership and counts were compared with the final local suite.

Independent growth evidence includes direct monthly arithmetic, split equivalence, forged-result rejection, original-state rollback and Rules-origin exception propagation. Policy evidence includes independent actual/input-linked accumulation, per-facility rounding, fees, mixed commands, later-month rollback and cache behavior. All discovered blocking findings were reproduced and independently rechecked after the author's minimal fixes.

## Performance boundary

The earlier Phase 3 author revision has four fresh-process 1,000/10,000-day measurements. The earlier Phase 4 revision has two fresh-process 1,000-day measurements: retain-all 62.451 seconds / 44.656 MiB, daily consumption 63.286 seconds / 35.668 MiB. Both satisfied the preselected 120-second and 512/128-MiB experimental budgets with matching final state and five ordered-record digests.

These performance measurements precede the later author-result-check and closing ID-order repairs. They were not remeasured at the final integration revision. Product regressions and final CI validate the revised behavior; they do not turn older timing samples into final-revision performance evidence. No V4 10,000-day, maximum-facility long-run, statistical reliability, gameplay or deployment SLA is claimed.

## Remaining scope

Next: resolve the P4-BEH behavior contract before adopting coefficients or implementing tax effects on happiness, migration, closure and reopening. The current tax slice changes actual city receipts and charges policy-change fees; it does not yet model company after-tax profit or prove policy tradeoffs. Remaining policy controls, persistence/recovery, City Black Box, UI, game balance, external playtesting and release remain separate gates.

Think's approved decisions and scoped numeric adoption remain complete as separately documented. PaperA's actual trial/seven-day/CLEAN evidence, the older stacked candidate integration, Paperpeper's scheduled observations and TCC external-user evidence retain their existing gates. This closing procedure did not re-audit those operations or change their operating configuration.

[Day worklog](WORKLOG_2026-10-05.md) · [Phase 3 history](PAPERCITY_PHASE3_2026-10-05.md) · [Prototype plan](PAPERCITY_V0_1_PLAN.md) · [Week plan](WEEKLY_PLAN_2026-10-05.md)
