# Audit Existing Plan Workflow

Version: 0.1
Status: Draft
Date: 2026-09-14

## Purpose

This workflow converts the Plan Model into an ordered evaluation process. It uses the interfaces defined in [`../core_models/01_plan_model.md`](../core_models/01_plan_model.md).

---

The Evaluation Procedure converts the Plan Model into an ordered decision
process.

Its purpose is to prevent the system from jumping directly from:

Training Content

to

Good / Bad Plan.

A plan should instead be evaluated through a sequence of increasingly
specific questions.

The evaluation process has two major stages:

Ex Ante Evaluation

and

Ex Post Evaluation.

Ex Ante Evaluation asks:

"Was this a reasonable plan given the information available before
implementation?"

Ex Post Evaluation asks:

"What actually happened, what did we learn, and what should change?"

These questions must remain separate.

---

## Step 1 — Define the Evaluation Object

Before evaluating a plan,
the system must identify exactly what is being evaluated.

The object may be:

- a full Cycle,
- a Mesocycle,
- a Week,
- a Session,
- a Task,
- or a proposed modification.

The evaluation scale matters.

A Session should not be judged as if it were an entire Cycle.

A Cycle should not be judged only from one poor Session.

The system should define:

- the planning level,
- the relevant time period,
- the intended objective,
- and the decision that must be made.

---

## Step 2 — Confirm the Target and Current Problem

The system should identify:

- the terminal 100m performance objective,
- the current planning objective,
- the current performance problem,
- and the priority of that problem.

The system should ask:

"What problem is this plan supposed to solve?"

If the objective is unclear,
the plan cannot yet be meaningfully evaluated.

Proxy improvement must not substitute for the target.

For example:

increased 1RM

does not independently prove that a sprint-performance problem has been
solved.

---

## Step 3 — Check Minimum Information Sufficiency

The system should determine whether enough decision-relevant information is
available.

Relevant information may include:

- athlete characteristics,
- current state,
- training history,
- recent exposure,
- competition timeline,
- recovery capacity,
- tissue status,
- facilities,
- lifestyle constraints,
- and relevant measurement conditions.

The system should distinguish:

Missing Information

from

Decision-Critical Missing Information.

If missing information would materially change the preferred action,
the system should:

- obtain the information,
- reduce the decision scope,
- use a conservative reversible option,
- or return "cannot yet determine."

It must not silently invent the missing value.

---

## Step 4 — Evaluate Structural Validity

Before asking whether the plan is optimal,
the system should determine whether the plan is structurally valid.

The system should check:

- objective clarity,
- dose interpretability,
- internal consistency,
- temporal consistency,
- resource feasibility,
- priority coherence,
- recovery coherence,
- monitoring coherence,
- correction pathways,
- and traceability.

If the plan fails a necessary structural condition,
the first action should normally be:

Repair the Plan Structure.

Fine-grained optimization should not begin while the basic plan remains
internally defective.

Operational structural-validity rules are defined in:

`rules/structural_validity.md`

---

## Step 5 — Identify Hard Constraints

The system should define the feasible planning space.

Relevant hard constraints may include:

- competition deadlines,
- medical restrictions,
- safety restrictions,
- tissue limitations,
- facility limitations,
- available time,
- recovery ceiling,
- and decision-critical uncertainty.

The system should then remove clearly infeasible options.

The sequence is:

Objective

→ Hard Constraints

→ Feasible Planning Space.

The system should not compare an infeasible plan against feasible plans as if
they were equivalent candidates.

---

## Step 6 — Evaluate Conditional Appropriateness

For each structurally valid and feasible option,
the system should ask whether the plan is appropriate for:

- this athlete,
- this objective,
- this current state,
- this training history,
- this competition calendar,
- this time horizon,
- this recovery environment,
- this tissue status,
- these facilities,
- these lifestyle constraints,
- and this level of uncertainty.

The system should explicitly distinguish:

"This method can work"

from

"This method is appropriate here and now."

A plan may remain theoretically valid while becoming conditionally
inappropriate.

---

## Step 7 — Evaluate Adaptive Capacity

The system should determine whether the plan contains a credible update
mechanism.

It should ask:

- What will be monitored?
- What response is expected?
- What would justify maintaining the plan?
- What would justify progression?
- What would justify reduction?
- What would justify modification?
- What would justify temporary withdrawal?
- What would justify transition?

The plan should be capable of responding to meaningful information without
reacting excessively to noise.

A plan that cannot change is incomplete.

A plan that changes constantly without sufficient evidence is unstable.

---

## Step 8 — Compare Feasible Plans

If multiple plans remain feasible and appropriate,
the system should compare them using decision-relevant dimensions.

These may include:

- expected 100m-relevant benefit,
- recovery cost,
- opportunity cost,
- risk,
- uncertainty,
- reversibility,
- time to benefit,
- competition availability,
- execution reliability,
- monitoring value,
- and unnecessary complexity.

The system should first check for Pareto dominance.

If one option is:

- no worse on the relevant dimensions,
- and meaningfully better on at least one important dimension,

it should generally be preferred.

If plans involve genuine trade-offs,
the system should state those trade-offs explicitly rather than hiding them
inside an arbitrary total score.

---

## Step 9 — State the Decision and Its Confidence

The evaluation should produce a clear decision.

Possible outputs may include:

- Accept,
- Accept with Modification,
- Maintain,
- Progress,
- Reduce,
- Modify,
- Temporarily Withdraw,
- Transition,
- Reject as Structurally Invalid,
- Reject as Infeasible,
- or Cannot Yet Determine.

The decision should also state confidence where useful.

Possible confidence language may include:

- High Confidence,
- Moderate Confidence,
- Low Confidence,
- Provisional,
- Exploratory,
- or Unresolved.

The system should explain what limits confidence.

---

## Step 10 — Record the Decision Rationale

Before implementation,
the system should preserve the reasoning available at the time.

The record should include:

- the current problem,
- the relevant athlete state,
- the selected plan,
- the major alternatives considered,
- the key constraints,
- the expected benefit,
- the expected cost,
- the major uncertainty,
- the expected response,
- and the planned review point.

This record is necessary for later evaluation.

Without it,
the system may incorrectly judge the original decision using information that
was only available afterward.

---

## Step 11 — Audit Actual Execution

After implementation,
the system should determine what actually occurred.

It should distinguish:

Prescription

from

Execution.

Relevant questions include:

- Was the planned training actually completed?
- Was the intended velocity or output achieved?
- Was the planned dose actually delivered?
- Were substitutions made?
- Were rest intervals changed?
- Did environmental conditions change?
- Did symptoms alter execution?

A plan cannot be evaluated only from what was written.

The system must establish the actual exposure.

---

## Step 12 — Audit the Response

The system should compare:

Expected Response

with

Observed Response.

Relevant observations may include:

- immediate training quality,
- sprint performance,
- technical stability,
- local tissue response,
- fatigue,
- sleep,
- recovery time,
- next-session performance,
- and repeated trends.

The system should ask:

- Was the response within the expected range?
- Was the cost greater or smaller than expected?
- Did the intended adaptation appear?
- Did a new constraint emerge?
- Did the original hypothesis remain plausible?

---

## Step 13 — Separate Execution Failure from Model Failure

An unfavorable result can arise for different reasons.

The system should distinguish among:

Prescription Failure

Execution Failure

Measurement Failure

Recovery Failure

Constraint Change

and

Model / Hypothesis Failure.

For example:

A MaxV method should not be declared ineffective if the athlete never reached
the intended velocity.

Likewise,
a training method should not be credited for improvement if the measurement
protocol changed substantially.

The system should first identify what actually failed.

---

## Step 14 — Update the Athlete State

Observed response should update the estimate of the athlete's current state.

Possible changes may include:

- improved capacity,
- improved tolerance,
- reduced tolerance,
- accumulated fatigue,
- altered tissue status,
- changed priority,
- changed competition readiness,
- or increased uncertainty.

The updated state becomes input for the next planning decision.

Therefore:

Plan Evaluation

is not the end of planning.

It is part of the next planning cycle.

---

## Step 15 — Update the Plan at the Appropriate Level

The system should modify the smallest planning level justified by the evidence.

Examples:

A poor repetition may change:

- the remaining Session.

A poor Session may change:

- the Week.

A repeated pattern may change:

- the Mesocycle.

A major injury,
competition-calendar change,
or persistent failure of the current model may change:

- the Cycle.

The system should not rewrite the entire training system when a local
adjustment is sufficient.

Likewise,
it should not keep making local adjustments when evidence indicates that the
higher-level assumption is wrong.

---

## Step 16 — Evaluate Decision Quality Separately from Outcome

The final outcome must not be used as the sole criterion for judging the
original decision.

The system should evaluate:

Decision Quality

using the information available at the time of the decision.

It should evaluate:

Outcome

using the observed result.

Possible combinations include:

Good Decision + Good Outcome

Good Decision + Poor Outcome

Poor Decision + Good Outcome

Poor Decision + Poor Outcome.

A favorable competition result does not automatically validate every part of
the plan.

An unfavorable result does not automatically prove that the original plan was
irrational.

Outcomes should update future beliefs,
not erase the distinction between reasoning quality and randomness,
noise, or unforeseen events.

---

## Step 17 — Preserve Unresolved Questions

Not every evaluation should end with certainty.

The system should preserve unresolved questions such as:

- Was the improvement caused by the targeted intervention?
- Was the dose sufficient but not yet expressed?
- Was recovery cost underestimated?
- Was the measurement too noisy?
- Is the athlete approaching a maintenance state?
- Is the current method losing marginal value?

These questions should inform future monitoring and planning.

The system should not force closure when the evidence remains ambiguous.

---

## Complete Evaluation Procedure

The complete evaluation sequence is:

1. Define the evaluation object.
2. Confirm the target and current problem.
3. Check minimum information sufficiency.
4. Evaluate structural validity.
5. Identify hard constraints.
6. Define the feasible planning space.
7. Evaluate conditional appropriateness.
8. Evaluate adaptive capacity.
9. Compare feasible plans.
10. State the decision and confidence.
11. Record the decision rationale.
12. Implement the plan.
13. Audit actual execution.
14. Audit the observed response.
15. Distinguish execution failure from model failure.
16. Update athlete state.
17. Update the plan at the appropriate level.
18. Re-evaluate when conditions change.

The process can be summarized as:

Context
→ Problem
→ Information
→ Structural Validity
→ Constraints
→ Feasible Options
→ Conditional Appropriateness
→ Comparison
→ Decision
→ Prescription
→ Actual Exposure
→ Response
→ Updated State
→ Revised Decision.

---

## Evaluation Invariants

The system should preserve the following principles:

1. Do not evaluate training content without defining the objective.
2. Do not optimize a structurally invalid plan.
3. Do not compare infeasible plans as normal alternatives.
4. Do not hide decision-critical missing information.
5. Do not confuse theoretical effectiveness with current appropriateness.
6. Do not evaluate prescription without checking actual execution.
7. Do not confuse proxy improvement with 100m performance improvement.
8. Do not interpret a single outcome as complete evidence of plan quality.
9. Do not let new information retroactively distort what was knowable at the
   time of the original decision.
10. Update the smallest planning level justified by the evidence.
11. Escalate to higher-level revision when repeated evidence challenges a
    higher-level assumption.
12. Preserve uncertainty when the available evidence does not justify closure.

The purpose of plan evaluation is not to label plans as simply "good" or
"bad."

Its purpose is to determine:

whether the plan is structurally valid,

whether it is appropriate under current conditions,

whether it is preferable to available alternatives,

whether it produced the intended exposure and response,

and what should happen next.
