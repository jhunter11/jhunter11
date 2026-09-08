# Work so far

Jack Hunter. Status reviewed September 8, 2026.

My current work includes private prototype code and exploratory experiment records.
These public notes describe their scope. They do not provide a reproducible release of the private implementation or a validated decoder result.

## Existing components

- Telemetry code calculates entropy and selected-token surprisal, with distinct exact, bounded, and unavailable observation states.
- History features include entropy summaries, progress changes, repeated text, tool errors, and generated tokens per step.
- Replay code saves task snapshots and runs intervention branches, with checks for restoration and isolation.
- Prototype policies score interventions relative to continuing, including action costs, delay costs, and a threshold for intervention.
- Experiment records contain pilot comparisons of simple statistics and learned predictors, plus corrections to measurement and model-selection errors.

These components support experimentation, but their presence does not establish reliable collection or useful intervention performance across models.
The reviewed history-feature code still substitutes zero when a signal has never appeared. It also carries some earlier observations forward.
The planned study needs explicit missingness and measurement-age inputs so the supervisor can distinguish an absent signal from low entropy.

## What the exploratory work changed

The experiment log records that selecting a transformer configuration on all available pilot data overstated its later evaluation performance.
After nested model selection, the recorded transformer comparison fell below a simple entropy-spike count baseline.
That makes the count baseline a required comparison for the proposed decoder study.
These public notes draw on the experiment log. They do not include a fresh reproduction of those runs.

The pilots concern failure prediction and signal analysis. They do not establish that a decoder chooses a better recovery action.
Earlier predictor comparisons also used architectures that differ from the proposed decoder-only text supervisor.
I therefore keep those experiments separate from any claim about the decoder design.

## Next work

I need to validate the collection path, publish a small trace fixture, and implement the decoder's text and numerical input branches.
Then I can collect controlled intervention outcomes and compare the resulting policy with simpler supervisors on held-out tasks.
The [experiment plan](decoder-experiment-plan.md) sets out that sequence. Compute access and reliable measurements still constrain the larger study.
The [hidden-state probe](hidden-state-probe.md) remains a later proposal with no completed experiment.
