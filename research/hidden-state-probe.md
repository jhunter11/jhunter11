# Hidden-state probe proposal

Jack Hunter. September 8, 2026. Planned experiment. No probe trained or hidden-state result established.

I want to test whether a local model's activations predict later agent failure beyond visible text and uncertainty telemetry.
This would extend the decoder-supervisor study after its collection and evaluation setup works.
It requires direct activation access to the task model. Hosted text or log-probability outputs alone cannot supply those activations.

## Proposed procedure

1. Freeze the task model and record activations at specified layers and decision points before any intervention.
2. Match those activations to the same task prefixes used by the text and telemetry baselines.
3. Start with a regularized linear probe for later task failure, with features and labels aligned to the decision time.
4. Choose layers, pooling, regularization, and calibration on training and development tasks only.
5. Compare the probe with text, entropy, and behavior baselines on separate task families.
6. Run label-shuffle controls and check whether the probe mainly identifies the task, sequence length, or model version.

I would report held-out prediction quality, calibration, activation storage, and inference cost.
Any useful prediction result would need a later intervention test before I used it to claim better agent recovery.
An accurate probe would show that its input contains predictive information. It would not explain how the model reaches its answer.

## Relation to latent reasoning

My interest in latent-space reasoning led to this question about internal measurements and external supervision.
[Coconut](https://arxiv.org/abs/2412.06769) studies reasoning with continuous hidden states fed back into a model.
Those states take the place of explicit reasoning tokens.
This probe proposal would read activations from a frozen task model. It would leave the model's reasoning process unchanged.

Visible reasoning text can also omit influences on a model's answer, as [Turpin and colleagues](https://arxiv.org/abs/2305.04388) show.
That motivates checking additional measurements, without assuming a probe reveals the full internal process.
I have not selected a model, layer set, activation budget, or sample size for this experiment.
