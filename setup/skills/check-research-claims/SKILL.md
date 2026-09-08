---
name: check-research-claims
description: Review research or benchmark claims against saved experiment records before a report or public release.
---

# Check research claims

Find the artifact behind each measured claim. Record its inputs, code revision, evaluation split, selection rule, and result.
If an artifact is missing, label the claim as unverified. Preserve the distinction between a proposal, a prototype, and an evaluated result.

Check whether the reported metric uses held-out data or the same data used to select a model or threshold.
Name selected validation scores as such. Keep synthetic benchmarks distinct from measurements on real tasks.
Report seed count and variation when the records support them.

For an agent experiment, compare methods on the same tasks, tool access, model, and budget.
Separate retry effects from the proposed intervention. Record task completion, cost, and harmful or unnecessary interventions when available.
Entropy can describe a distribution without proving uncertainty or failure. Check what the signal measures before accepting a causal claim.

Retain failed runs and negative results when they affect the conclusion.
Do not turn a design document into an account of work that has run.
Return corrected claims with artifact links and the checks still needed to support them.
