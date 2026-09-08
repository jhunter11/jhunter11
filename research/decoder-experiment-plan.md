# Decoder experiment plan

Jack Hunter. September 8, 2026. Proposed study, with no completed decoder evaluation.

## Model and decision

The supervisor would combine recent agent activity with uncertainty measurements to estimate recovery value.
A small decoder-only language model would encode the visible trajectory: messages, tool calls, results, and recent artifact changes.
A temporal input branch would encode entropy, surprisal, progress, repeated actions, tool errors, latency, and context use.
Prediction heads would estimate failure risk and the expected value of each allowed intervention.

Candidate interventions are continue, restore the task brief, replan, return to a saved state, or delegate a bounded subtask.
Each action needs a fixed definition before collection. Delegation must preserve the task's permissions and isolation rules.
The initial study would use a small action set that the environment can replay and score reliably.

The training target would be each action's expected improvement over continuing, with resource cost and delay recorded separately.
I would derive the action ranking from those values. A single winning-action label would discard the size of the estimated differences.
If the estimates are too uncertain, the supervisor would abstain and use the predefined fallback.
An immediate permissions or safety violation would follow a fixed stop rule outside the learned policy.

## Collecting intervention evidence

1. Choose software or tool-use tasks with reproducible environments and objective completion checks.
2. Record the task history and telemetry available before each decision point.
3. Sample decision points after failures, entropy spikes, and ordinary progress to avoid collecting only visibly difficult states.
4. Save the environment, files, tool state, agent history, and randomization metadata.
5. Verify restoration and branch isolation before collecting outcomes.
6. Randomly assign allowed actions across restored branches and repeat trials with recorded seeds.
7. Score final artifacts without showing the evaluator which supervisor condition produced them.

An entropy spike alone cannot establish which repair would help. I need the branch outcomes to estimate that difference.
No branch may read a sibling's results, and no training feature may include an observation from after the decision point.
The pilot would first check whether any intervention produces a useful improvement over continuing and a neutral interruption control.

## Comparisons

I would first compare a fixed schedule, an entropy threshold, an entropy-spike count, and a supervisor using behavior alone.
Behavior includes progress, retries, tool failures, elapsed time, and token use.
The decoder comparisons would use trajectory text alone, numerical telemetry alone, and their combination.
A separate sample-disagreement condition would require multiple continuations and charge their cost to the same total budget.

Every condition would have the same task model, action set, task split, and total resource budget.
Task families would stay separate across training, development, and final evaluation. Branches from one task would stay in one split.
Model selection and calibration would use training and development data only. I would freeze the configuration before final evaluation.

## Measurements and stopping rules

The primary outcome would be accepted task completion at a fixed budget, compared with the strongest baseline chosen on development tasks.
I would report absolute completion differences, intervals that preserve task grouping, and the cost of the additional observations.
Secondary measures would include harmful interventions, constraint violations, operator requests, tool calls, tokens, and elapsed time.

For failure prediction, I would measure precision-recall performance, AUROC, and probability calibration on held-out tasks.
Those scores would describe prediction quality. The intervention study must separately measure whether acting on a prediction improves completion.
I would also record how often the supervisor interrupts a run that would otherwise succeed.

Before final collection, I would freeze the useful effect size, primary comparisons, exclusions, and stopping rule.
Sample size would follow pilot variance and a power analysis. Those values remain undecided.
If uncertainty adds no useful improvement after cost, I would keep the simpler supervisor and report that result.

## Instrument limits

Each model backend needs a dated capability check. The record must distinguish full distributions, bounded estimates from partial distributions, and unavailable measurements.
Missing telemetry must stay distinguishable from measured zero, including after feature extraction.
Comparisons must record model version, tokenizer, sampling settings, probability coverage, and the point at which each measurement enters the trace.

A broken tool parser, stale snapshot, or exhausted context window can look like a model failure.
Collection must separate those faults before they become training labels.
The first deliverable would be a reproducible collection check and a small public trace fixture, followed by the decoder implementation.
