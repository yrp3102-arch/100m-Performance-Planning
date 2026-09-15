# Create Session Workflow

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This workflow converts a Week-level exposure requirement into an executable
training prescription for the current Athlete State and conditions.

It answers:

> What should be executed now, what stimulus is intended, what counts as useful
> exposure, and what conditions justify modification or stopping?

The Session is the highest-prescription-specificity level in the top-down
planning system.

It defines task, relevant dose dimensions, rest, quality, stop conditions,
supporting work, and recording fields.

It does not blindly execute planned volume.

Use the following interfaces:

- [Plan Core Model](../core_models/01_plan_model.md)
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
- [Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md)
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
- [Conditional Appropriateness Rules](../rules/conditional_appropriateness.md)
- [Constraint Handling Rules](../rules/constraint_handling.md)
- [Plan Comparison Rules](../rules/plan_comparison.md)
- [Progression Rules](../rules/progression.md)
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md)

---

## Required Inputs

| Input | Required meaning | Source or boundary |
|---|---|---|
| Week Intent | Near-term objective the Session must serve | From `session_brief` produced by [Create Week Workflow](./create_week.md) |
| Session Role and Status | Primary, supporting, maintenance, minimal, competition, or recovery role; Fixed, Conditional, Optional, or Replaceable status | Role does not establish actual stimulus |
| Current Athlete State | Latest decision-relevant state estimate | Update immediately before prescription when relevant information changed |
| Recent Actual Exposure and Response | What occurred, Achieved Quality, Observed Response, and interpretation | Prescription history alone is insufficient |
| Current Priority | Target allocation and protected resource | Primary, Maintain, Minimal, or Temporarily Withdrawn |
| Candidate Intervention | Existing candidate or explicit retrieval need | Every candidate requires 03 interpretation |
| Environment and Equipment | Surface, space, weather, timing, equipment, and coaching access | Must permit safe delivery of intended exposure |
| Tissue State and Constraints | Local tolerance, symptoms, restrictions, and relevant uncertainty | Medical restrictions remain hard boundaries |
| Time Available | Real Session duration and schedule conditions | Do not reduce required rest merely to fit excess content |
| Expected Response | Immediate and delayed response hypothesis | Defines the feedback comparison, not a guaranteed outcome |

If decision-critical input is unavailable, apply the
[Uncertainty Handling Rules](../rules/uncertainty_handling.md).

Possible outputs include a reduced-scope prescription, a reversible option,
`Cannot Determine`, or a higher-level review flag.

---

## Step 1. Define the Session Objective

State one Primary Objective.

The Primary Objective must identify:

- the Week exposure requirement;
- the target Performance Problem, determinant, capacity, or expression need;
- the intended Session contribution;
- and the condition that makes the contribution meaningful.

Supporting Objectives are optional.

For every Supporting Objective, state:

- why it has current marginal value;
- what resource it consumes;
- how it remains compatible with the Primary Objective;
- and what happens to it if cost rises.

Do not begin with a task list.

If no coherent Primary Objective can be stated, stop prescription construction
and return the inconsistency to Week review.

**Step output:** `session_objective`, `primary_objective`, and any
`supporting_objectives`.

---

## Step 2. Confirm Current State

Use the latest available information to compare the current state with the
entry-state assumptions in the Session brief.

Review only decision-relevant dimensions, including where applicable:

- recent performance and exposure;
- fatigue and recovery state;
- local tissue state;
- technical stability;
- exposure tolerance;
- motivation or attention when it affects execution;
- environment;
- and unresolved uncertainty.

Separate Observation from Interpretation.

Do not infer state from a single readiness score or isolated low-quality signal.

Select an execution disposition:

- `Proceed` when the prescription remains conditionally appropriate;
- `Modify` when the objective remains valid but task, dose, order, or condition
  should change;
- `Temporarily Withdraw` when the exposure is currently unjustified;
- or `Replace` when the exposure role remains required and another feasible
  intervention better preserves the intended stimulus.

These are Session execution dispositions.

Any feedback Decision State must retain the terminology and evidence rules of
the [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md).

A material mismatch affecting several Sessions triggers Week review.

A mismatch challenging the adaptation problem triggers Mesocycle review.

**Step output:** `current_state_confirmation`, `execution_disposition`, and
review flag if required.

---

## Step 3. Select a Candidate Intervention

Select only from candidates that can plausibly produce the required exposure
under current constraints.

Candidates may come from existing project knowledge or future dynamic evidence
retrieval.

This Workflow does not depend on a fixed exercise library.

When no suitable candidate is available, emit:

`Candidate Intervention Required`

and, when appropriate:

`External Retrieval May Be Invoked`.

Interpret every candidate through the
[Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md).

Apply:

- hard-constraint feasibility;
- Conditional Appropriateness;
- target and transfer relevance;
- expected marginal benefit;
- recovery and opportunity cost;
- risk;
- execution reliability;
- and uncertainty.

When several candidates remain, apply the
[Plan Comparison Rules](../rules/plan_comparison.md).

Do not select a task solely because its label resembles the objective.

**Step output:** `selected_intervention`, alternatives considered, conditional
rationale, and confidence.

---

## Step 4. Define the Intended Stimulus

State what stimulus the selected task is intended to produce for this athlete
in this Session.

Represent the relationship:

Training Task

× Dose

× Execution Quality

× Athlete State

× Temporal and Environmental Context

→ Intended Stimulus.

The Intended Stimulus should identify:

- target determinant or supporting capacity;
- relevant external exposure characteristics;
- required execution state and quality;
- expected adaptation or preservation relationship;
- transfer hypothesis;
- and major expected cost.

Exercise Label does not equal Training Stimulus.

If the intended stimulus cannot be distinguished from the method name, the
prescription is not yet interpretable.

**Step output:** `intended_stimulus` and `transfer_hypothesis`.

---

## Step 5. Define the Executable Dose

Define dose using only dimensions relevant to the selected task.

Possible dimensions include:

- distance;
- repetitions and sets;
- exposure duration;
- intensity, velocity, or output;
- external load;
- movement range or task constraint;
- contact count;
- work density;
- within-repetition and between-repetition rest;
- execution quality;
- and placement relative to other work.

For each included dimension, state:

- planned value or bounded range;
- minimum meaningful exposure where supportable;
- planned upper boundary where supportable;
- condition that can change the value;
- and uncertainty.

Do not force every task into the same dose units.

Do not treat planned volume as mandatory completed volume.

Do not reduce rest below the requirement of the intended stimulus merely to fit
the available clock.

**Step output:** `executable_dose` and `dose_boundaries`.

---

## Step 6. Define Quality Criteria

Define what counts as useful Actual Exposure for the Session objective.

Quality criteria must be specific to the task and intended stimulus.

They may concern:

- achieved velocity or output;
- technical stability;
- task completion under intended conditions;
- consistency across repetitions;
- acceptable fatigue-expression relationship;
- safe execution;
- or validity of the measurement context.

For each criterion, state:

- the observed object;
- the method and context of observation;
- the acceptable qualitative or athlete-calibrated relationship;
- and how uncertainty affects interpretation.

Avoid universal thresholds unsupported by the athlete's history or task.

When performance decline is part of an intended stimulus, define its acceptable
boundary before execution.

Do not relabel unexpected technical or performance collapse as planned quality.

**Step output:** `quality_criteria` and `achieved_quality_fields`.

---

## Step 7. Define Stop and Modification Conditions

Define conditions under which continuing the planned exposure would no longer
serve the Session objective or remain feasible.

Relevant conditions include:

- intended quality is no longer achieved;
- a meaningful tissue or safety warning appears;
- Actual Exposure diverges materially from the intended exposure;
- environmental or equipment conditions invalidate the task;
- accumulated cost becomes disproportionate to expected marginal benefit;
- time constraints make required execution or rest impossible;
- or uncertainty becomes decision-critical.

For each condition, state the eligible local response:

- Maintain;
- Reduce;
- Modify;
- Temporarily Withdraw;
- or Replace the intervention while preserving the exposure role.

Progress and Transition remain available only when their existing Rule
conditions are satisfied.

Use [Progression Rules](../rules/progression.md); do not reproduce universal
operational thresholds.

High-consequence tissue or safety signals do not require repeated maximal
exposure before conservative action.

**Step output:** `stop_conditions`, `modification_options`, and escalation
destination.

---

## Step 8. Add Supporting Work

Add supporting work only after the Primary prescription is executable.

Each supporting element must have:

- an explicit Supporting Objective;
- sufficient expected marginal value;
- a represented dose and cost;
- compatibility with Primary quality;
- acceptable tissue and residual stress;
- and a clear removal or modification condition.

Evaluate the combined cost of all supporting elements.

Several individually small additions can materially increase duration,
attention, tissue loading, or recovery cost.

Supporting work should be removed, reduced, or replaced before it silently
invalidates the Primary Objective.

Do not add content solely to make the Session appear complete.

**Step output:** `supporting_work` and combined-cost check.

---

## Step 9. Define the Actual-Exposure Record

Create the record structure before execution.

Preserve Planned and Actual as separate objects.

The record should contain, where relevant:

- prescribed task and conditions;
- intended stimulus;
- planned dose;
- completed dose;
- achieved intensity, velocity, output, or duration;
- achieved quality;
- actual rest and density;
- substitutions or omissions;
- environmental and equipment conditions;
- tissue observations;
- immediate response;
- reasons for modification or stopping;
- and missing or uncertain data.

Task completion does not prove intended exposure.

The record must allow later classification of Prescription, Execution, Exposure,
Measurement, Recovery, Constraint, Transfer, or Model / Hypothesis failure.

Do not turn observations into causal interpretations inside the raw record.

**Step output:** `actual_exposure_record_schema`.

---

## Step 10. Define the Immediate Review Interface

Define which post-execution information must enter feedback processing.

Send:

- Planned Exposure;
- Actual Exposure;
- Achieved Quality;
- immediate Observed Response;
- context and measurement conditions;
- any stop or modification event;
- any tissue, safety, or constraint change;
- deviation from Expected Response;
- and unresolved uncertainty.

Do not perform the complete feedback audit in this Workflow.

The [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
defines:

Actual Exposure

→ Observed Response

→ Interpretation

→ Updated Athlete State

→ Decision Update.

Route the result first to the smallest relevant scope.

**Step output:** `immediate_feedback_packet` and `feedback_destination`.

---

## Session Output

The completed Session must output:

- `week_intent_reference`;
- `session_objective`;
- `session_role` and `session_status`;
- `current_state_confirmation`;
- `execution_disposition`;
- `selected_intervention`;
- `intended_stimulus`;
- `transfer_hypothesis`;
- `executable_dose`;
- `quality_criteria`;
- `rest_recovery_conditions`;
- `stop_conditions`;
- `modification_options`;
- `supporting_work`;
- `expected_response`;
- `actual_exposure_record_schema`;
- `immediate_feedback_packet`;
- `feedback_destination`;
- `unresolved_uncertainty`;
- and any higher-level review flag.

This output is the executable prescription.

Execution must produce a separate Actual Exposure record.

---

## Feedback and Escalation Interface

Keep a local issue at Session scope when task, dose, order, or execution
conditions can be corrected without changing Weekly Intent.

Return a `week_review_flag` when evidence affects multiple Sessions, placement,
required exposures, or their recovery relationship.

Return a `mesocycle_review_flag` when repeated evidence challenges the current
adaptation problem, Candidate Bottleneck, priority, dose direction, or transfer
hypothesis.

Return a `cycle_review_flag` when evidence challenges the terminal objective,
competition structure, major constraint set, or strategic state trajectory.

One poor repetition or ordinary noisy Session must not automatically rewrite
the Cycle.

A high-consequence constraint or safety change may justify immediate broader
review.

---

## Session Completion Gate

The Session is executable only when:

- it has one explicit Primary Objective;
- its role and status inherit Weekly Intent;
- current Athlete State has been checked against entry assumptions;
- the selected intervention is feasible and conditionally appropriate;
- Intended Stimulus is defined beyond the exercise label;
- dose uses relevant task-specific dimensions;
- useful exposure and Achieved Quality are observable;
- rest and recovery conditions support the intended stimulus;
- stop and modification conditions are explicit;
- supporting work does not compromise the Primary Objective;
- Planned and Actual Exposure can be recorded separately;
- Expected Response and immediate feedback fields are defined;
- and escalation destinations are visible.

If these conditions are not met, return `Modify`, `Temporarily Withdraw`,
`Replace`, `Cannot Determine`, or the appropriate review flag rather than
blindly executing planned volume.
