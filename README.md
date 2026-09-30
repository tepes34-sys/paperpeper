# paperpeper · paperA · think

> A public showcase of an operating system, a reliability lab, and a design discussion layer, with their roles and verification principles.

[September 30, 2026 work notes](docs/WORKLOG_2026-09-30.md) · [Earlier paperpeper experiments and validation records](https://github.com/tepes34-sys/paperpeper/blob/216cefe28df3b909d9e50f3f8fc4b0497d918904/README.md)

## 1. paperpeper

U.S. equity paper trading, an isolated Lab, and experiments with reusable tools.

The focus of today's notes is **the source of truth and the timestamp of each observation**. Execution logs, databases, CSV files, and dashboards may describe different points in time. Checks distinguish missing source data from an outdated derived report. When an alert appears, its evidence is verified before deciding whether to change the code.

The notes also cover temporary files in recurring tasks and lock verification. Sequential reuse, concurrent acquisition, process interruption, and recovery require separate tests.

[Problems, verification principles, and next questions](docs/WORKLOG_2026-09-30.md#1-paperpeper)

## 2. paperA

A **Shadow Reliability Lab** that uses public market events to test invariants, recovery, and portability.

Fixed fixtures and explicit input contracts make calculations reproducible. Experiment identity and numeric precision are checked at the boundaries. Real candles are kept separate from missing intervals, no-trade classifications require evidence, and state changes are preserved together with the Black Box events that explain them.

OS locks and database constraints serve different defensive roles. Fixture tests, automated tests, and live operating observations are treated as distinct evidence. Findings transferred to another market must be reproduced independently in the target environment.

[Design and validation gates](PAPERA_PLAN.md) · [Detailed work notes](docs/WORKLOG_2026-09-30.md#2-papera)

## 3. think

A design documentation layer that separates GPT/Claude discussions, approved decisions, and enduring conditions verified across projects.

Think records proposals and discussion. Decision records approval, rationale, and scope. Invariant records failure cases and actual test evidence. Opinions alone do not establish implementation requirements; approved decisions are connected to project pull requests.

Topics include time, prices, gaps, recovery, strategy inputs, event capture, locks, costs, precision, and state transitions. Revised decisions supersede only the relevant provisions while preserving earlier records. Principles move between projects through Portable Improvement Notes, followed by independent reproduction and regression testing.

[Document structure, design topics, and transfer process](docs/WORKLOG_2026-09-30.md#3-think)

## Reading the records

The detailed work note is organized by the three projects. Earlier public experiment and validation records remain available through the versioned link above.

---

Software research project. Not financial advice.
