# Uncertainty and agent supervision

Research proposal by Jack Hunter. Updated September 8, 2026.

**Status:** I have not run the experiments proposed here. The project needs compute, repeatable task environments, and verified access to model measurements.
I have used Claude to develop the questions and protocol. This page presents the research plan and does not report a result.

## Abstract

An AI agent can report success after taking a wrong turn in a long task.
I want to test whether uncertainty measurements help a supervisor choose when to continue, replan, rewind, or delegate.
The proposed study compares supervisors with different observations while holding the task, model, action set, and compute budget fixed.

At selected decision points, the study would restore the same environment state and assign different supervisor actions across repeated branches.
An independent evaluator would score task completion and boundary violations.
The study would measure whether uncertainty improves those outcomes beyond behavior-only supervision and fixed intervention schedules.
A negative result would narrow which observations deserve the cost of collecting them.

## What I mean by latent-space reasoning

My broader interest is how internal model computation relates to visible answers and agent behavior.
This proposal starts with observations that a provider or local model exposes.
Token probabilities and answer disagreement are proxies. They do not reveal all hidden states or prove what a model internally represents.

Continuous latent reasoning is a separate research direction.
The [Coconut paper](https://arxiv.org/abs/2412.06769) studies computation through continuous hidden states in place of explicit reasoning tokens.
This proposal does not claim to implement Coconut or obtain hidden internal traces from a hosted model.

## Hypotheses

1. Uncertainty observations predict later task failure after controlling for task type, progress, and token use.
2. A supervisor using those observations improves accepted task completion at a fixed resource budget.
3. Any gain from richer local measurements decreases when the same observations are reduced to a hosted API capability level.

The relationship between uncertainty during intermediate work and confidence in a final answer is an open question here.
I do not assume instruction tuning creates a reliable confidence gap. The study must first establish whether the measured gap predicts anything.

## Proposed experiment

The initial task set would use software or tool-use environments with reproducible state and objective completion checks.
Training, development, and final evaluation would use separate task families. The final evaluator would remain hidden during policy development.

The protocol would compare these conditions:

| Condition | Supervisor observations |
| --- | --- |
| Fixed schedule | Task state and a predetermined intervention rule |
| Behavior baseline | Progress, tool errors, retries, elapsed time, and token use |
| Text observations | The baseline plus observable uncertainty markers |
| Distribution observations | The baseline plus supported token-probability measurements |
| Sample disagreement | The baseline plus disagreement across multiple continuations |

Every condition would receive the same allowed actions and total budget.
Additional samples consume that budget. A single continuation cannot estimate disagreement across continuations.
The [semantic entropy study](https://www.nature.com/articles/s41586-024-07421-0) motivates separating meaning disagreement from token-level uncertainty.
Its published findings do not validate the proposed supervisor policy.

For each chosen intervention point, I would save the environment, task history, tool state, and randomization metadata.
Each branch would start from that snapshot. Branches would use isolated files and no shared mutable memory.
Restoration checks must pass before a branch contributes to the experiment.

Within each restored state, action assignment would be randomized across repeated runs.
The evaluator would score the final artifacts without seeing the supervisor condition.
Analysis would preserve the shared task and fork structure instead of treating every branch as an independent sample.

## Measurements

| Measurement | Proposed definition |
| --- | --- |
| Accepted completion | Fraction of tasks that pass the independent evaluator |
| Boundary violation | Unauthorized action, cross-task state access, or other preregistered constraint breach |
| Human intervention | Tasks that need an operator to resume useful work |
| Resource use | Model tokens, sampled branches, tool calls, elapsed time, and cost |
| Failure prediction | AUROC, precision-recall curves, and calibration on held-out task families |
| Intervention value | Difference in accepted completion between paired supervisor conditions |
| Unnecessary intervention | Interventions that consume resources without improving the scored outcome |
| Observation missingness | Missing fields with a cause, recorded separately from measured zero |

I would report absolute completion differences, uncertainty intervals, and the corresponding resource costs.
The protocol would freeze the minimum useful improvement, primary comparisons, exclusions, and stopping rule before final evaluation.
Sample size would follow pilot variance and a power analysis. I have not selected or reached a final sample size.

## Measurement limits

Provider capabilities must pass a dated probe before use. Unavailable probabilities stay missing.
A top-k probability list is a partial distribution; entropy calculations must account for that limit.
Comparisons would record model version, tokenizer, sampling settings, task family, and trace visibility.

Observable reasoning text can omit or distort internal computation.
Tool failures, a broken snapshot, or an exhausted context window can also look like a reasoning failure.
Instrument checks must distinguish those cases before I interpret the result.

I would reject the practical hypothesis if uncertainty adds no useful held-out improvement after its resource cost.
Any positive finding would apply first to the tested models, task families, and observation levels.
Replication on other tasks and providers would be a separate experiment.
