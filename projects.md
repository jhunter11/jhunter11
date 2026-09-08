# Project notes

These notes give a public description of work whose source stays private.
They describe implemented components or documented plans, with no claim of deployment, customers, or validated returns.

## AI workflow systems

The private Jarvis workspace supplies the source for the curated [Jarvis Control](https://github.com/jhunter11/jarvis-control) snapshot.
The public snapshot shows the task queue, model policy, memory interfaces, and authorization checks.
Runtime configuration and operational records stay private.

A separate local memory service uses SQLite and MCP to share project context between tools.
The [Multi-Agent Memory MCP](https://github.com/jhunter11/multi-agent-memory-MCP) repository provides the public implementation and synthetic evaluation.

I also built a scheduled workflow prototype with budget records, task outcomes, review steps, and integrity checks.
Its business-specific instances remain private. The public [Agentic Quant Operator](https://github.com/jhunter11/agentic-quant-operator) archive shows related control patterns.

## Research infrastructure

EquityLab is a private Python research framework for equity and ETF strategies.
Its design includes timestamped events, later-bar execution, transaction costs, walk-forward evaluation, and checks for data leakage.
The project records rejected candidates and contaminated earlier analyses. I do not claim a validated strategy or approved capital use.

The private PMQS extension adds adverse-execution stress tests, expanding-window evaluation, capture checks, and settlement reconciliation.
The [public PMQS core](https://github.com/jhunter11/pmqs) contains the replay and evidence-checking primitives.

Several older market-research repositories contain earlier models or experiments.
The maintained public examples are [Event Contracts](https://github.com/jhunter11/eventcontracts), PMQS, and the [calibration study](https://github.com/jhunter11/casino-line-modeling).
Backup repositories and transferred experiment files remain private.

## Document and review workflows

A private New Jersey property-research prototype tracks candidate records, numeric assumptions, review questions, and draft decision packets.
It separates draft preparation from actions that require a person.
The source, property records, contact details, and legal working notes remain private.

The [uncertainty and supervision proposal](research/uncertainty-and-agent-supervision.md) is the public account of my current research direction.
It contains proposed methods and measurements. I have not run its confirmatory experiments.
