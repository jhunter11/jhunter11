# Uncertainty and agent supervision

Working research notes by Jack Hunter. Updated September 8, 2026.

This project is incomplete. I have prototype telemetry and intervention code, exploratory analyses, and a design for a small decoder-only supervisor.
I have not completed or validated that decoder. The hidden-state probe is a separate proposed experiment.

## Abstract

I want to test whether an agent's uncertainty signals can help choose its next recovery action.
A failed tool call or an entropy spike would give the supervisor a decision point.
It would read the recent trajectory and numerical telemetry, then estimate the value of continuing, replanning, or another allowed intervention.
The decoder would encode the trajectory text. A second input branch would encode entropy, progress, tool errors, and other measurements.

Predicting a failure is only one part of this problem. I also need evidence that a particular intervention helps at that state.
The proposed experiment would compare actions from restored copies of the same task state, with repeated trials and independent outcome checks.
I would then test the supervisor on separate task families, accounting for the cost of collecting signals and intervening.
I have no validated recovery improvement to report.

## What the entropy signal means

Here, token entropy measures how spread out a model's next-token probability distribution is.
An entropy spike means that this measurement rises relative to an earlier window under the same measurement setup.
The spike is a candidate signal. It can occur during useful exploration, and an agent can also fail with low entropy.

The prototype includes entropy and surprisal calculations, history features, and policies that score possible interventions.
The proposed decoder would extend that work by reading recent trajectory text alongside the numerical signals.
It would suggest a supervisory action, such as replanning or restoring task context. It would not select every tool call.

A partial top-k probability list does not give full-distribution entropy by itself. Missing probabilities need a missingness record.
The [semantic entropy study](https://pmc.ncbi.nlm.nih.gov/articles/PMC11186750/) groups multiple generated answers by meaning to measure answer uncertainty.
That motivates a separate comparison with repeated continuations. Its findings do not establish whether my proposed recovery policy works.

## Current files

- [Decoder experiment plan](decoder-experiment-plan.md) describes the proposed inputs, recovery actions, comparisons, and evaluation.
- [Work so far](work-so-far.md) separates the existing prototypes and exploratory records from work still planned.
- [Hidden-state probe](hidden-state-probe.md) describes a later experiment that would need direct access to a local model's activations.

I use Claude and other coding tools to develop the research plan and implementation.
