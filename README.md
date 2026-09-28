# Paperpeper

> An AI-assisted algorithmic trading research project focused on experimentation, paper trading, risk controls, and reproducible analysis.

**Paperpeper** is a personal R&D project exploring how AI-assisted research, systematic trading logic, isolated experiments, and human review can work together.

This repository is the **public showcase** for the project. The private development environment, operational data, credentials, and working production code are intentionally kept separate.

## What Paperpeper explores

- **Paper trading** — testing trading logic without placing real orders
- **Risk controls** — position sizing, exposure limits, entry validation, and safety gates
- **Strategy experiments** — comparing alternative strategies in isolated environments
- **Trading observability** — understanding why a trade happened and what happened afterward
- **Data integrity** — detecting inconsistent records, duplicate actions, and ledger problems
- **AI-assisted development** — using AI for research, analysis, implementation support, and project review

## Project model

```text
Research / Ideas
       ↓
   GPT Lab
       ↓
Small prototypes
       ↓
Human review
       ↓
Isolated strategy testing
       ↓
Private production system
```

Experiments are deliberately separated from the operating system. A prototype does not automatically become part of the main trading workflow.

## Current areas

### Trading Core
Research around reusable components for paper trading, risk management, trade records, and execution safety.

### Strategy Lab
A sandbox for testing alternative strategy ideas without silently changing the main strategy.

### Trading Black Box
An exploration of reproducible trade histories:

```text
Signal → Risk Check → Decision → Order/Fill → Exit → Result
```

The goal is to answer not only *what happened?* but also *why did it happen?*

### Trade / Ledger Inspector
A small-tool concept for inspecting trading records and detecting issues such as missing records, duplicates, balance mismatches, and inconsistent positions.

This is currently an exploration candidate, not a released product.

## Public vs. private

This repository contains only material intentionally selected for public viewing.

**Public here**
- Project overview
- Selected experiment notes
- Sanitized examples
- Screenshots and demonstrations
- Reusable tools if intentionally released

**Kept private**
- API keys and credentials
- Personal trading/account data
- Operational databases
- Private research inputs
- Production source code
- Internal configuration

## Status

Paperpeper is an evolving hobby/R&D project. Features shown here may be experimental, incomplete, changed, or abandoned as evidence accumulates.

The current focus is to improve the private system first, while identifying small components that may also be useful as independent tools.

## Disclaimer

Paperpeper is a software and research project, not financial advice. Public materials in this repository should not be interpreted as investment recommendations or claims of future trading performance.

---

Built through an ongoing human + AI development workflow.
