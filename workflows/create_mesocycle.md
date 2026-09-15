# Create Mesocycle Workflow

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This workflow creates a Mesocycle as a decision unit organized around a current
adaptation problem and a desired Athlete State change.

It answers:

> What is the most important current adaptation problem, and what state change
> should occur before this Mesocycle is exited?

A Mesocycle is not created merely because a fixed number of weeks has been
assigned.

Calendar duration is a provisional horizon or review window.

The governing identity is:

Current Adaptation Problem

→ Desired State Change

→ Priority Allocation

→ Required Exposure Direction

→ Expected Response

→ Exit or Revision Condition.

Use the following interfaces:

- [Plan Core Model](../core_models/01_plan_model.md)
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
- [Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md)
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
- [Priority Allocation Rules](../rules/priority_allocation.md)
- [Stress Organization Rules](../rules/stress_organization.md)
- [Progression Rules](../rules/progression.md)
- [Stage Transition Rules](../rules/stage_transition.md)
- [Constraint Handling Rules](../rules/constraint_handling.md)
- [Conditional Appropriateness Rules](../rules/conditional_appropriateness.md)
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md)

---

## Required Inputs

| Input | Required meaning | Source or boundary |
|---|---|---|
| Cycle Intent | Terminal objective, strategic trajectory, competition relationship, and inherited constraints | From `mesocycle_brief` produced by [Create Cycle Workflow](./create_cycle.md) |
| Current Athlete State | Most recent decision-relevant state estimate | Update inherited assumptions with current evidence; do not silently alter Cycle strategy |
| Current Performance Problem | The present race or segment problem requiring planning attention | Keep separate from proxy and training-method labels |
| Candidate Bottleneck | Supported, provisional, multiple, or unresolved limiting explanation | Must retain confidence and alternatives |
| Current Priorities | Inherited allocation and any evidence requiring confirmation | Primary, Maintain, Minimal, Temporarily Withdrawn |
| Recent Exposure and Response | Actual Exposure, Achieved Quality, Expected Response, Observed Response, and relevant trend | Use 04; do not infer from prescription alone |
| Constraints | Current hard and soft constraints | Re-establish feasible space when conditions change |
| Competition Proximity | Time, role, stress, and expression requirement of upcoming competition | Does not automatically prescribe a taper |
| Uncertainty | Unknowns capable of changing objective, intervention, dose direction, or exit | Apply decision-specific sufficiency |

If the inherited Cycle brief and current evidence conflict, preserve both and
raise a `higher_level_review_flag`.

Do not resolve the conflict by silently rewriting Cycle intent.

---

## Step 1. Define the Current Adaptation Problem

State the problem in one concise sentence.

The statement must identify:

- the relevant 100m performance outcome or determinant;
- the current Athlete State;
- the Candidate Bottleneck or limiting constraint;
- and why the problem matters within Cycle intent.

The statement must not begin with a preferred exercise.

Use the relationship:

Observed Performance Problem

→ Candidate Explanation

→ Candidate Bottleneck or Constraint

→ Adaptation Problem.

If the problem cannot be stated without inventing a bottleneck, do not
mechanically generate the Mesocycle.

Return one of:

- Defined Adaptation Problem;
- Provisional Adaptation Problem;
- Multiple Candidate Problems;
- or `Cannot Determine`.

When uncertainty permits a bounded plan, state what the Mesocycle is intended
to learn as well as change.

**Step output:** `adaptation_problem` with evidence, confidence, and Cycle
relationship.

---

## Step 2. Define the Desired State Change

Represent the transition as:

Start State

→ Desired Exit State.

The Start State must use current information rather than only the state assumed
when the Cycle was written.

The Desired Exit State should define decision-relevant change in terms such as:

- improved sprint-relevant capability or expression;
- improved tolerance of a required exposure;
- reduced limiting fatigue or constraint;
- stabilized technical organization;
- retained strategically important capacity;
- or increased confidence in a bottleneck or intervention hypothesis.

Do not define success solely as completion of planned sessions or improvement
of a distant proxy.

Record:

- target state dimension;
- current estimate;
- desired direction or bounded state;
- expected relevance to 100m performance;
- useful time horizon;
- evidence capable of supporting the state change;
- and uncertainty.

**Step output:** `start_state` and `desired_exit_state`.

---

## Step 3. Confirm Priority Allocation

Apply the [Priority Allocation Rules](../rules/priority_allocation.md) to current
conditions.

Confirm or revise the inherited states:

- Primary;
- Maintain;
- Minimal;
- Temporarily Withdrawn.

For each object, retain:

- its role in the adaptation problem;
- expected marginal value;
- transfer potential;
- recovery and opportunity cost;
- risk and uncertainty;
- and the work it may displace.

Any change from the Cycle allocation requires an explicit rationale.

A local intervention change can preserve the strategic target.

A target change that contradicts the strategic trajectory requires a
`higher_level_review_flag`.

**Step output:** `mesocycle_priority_allocation` and any allocation conflict.

---

## Step 4. Define Required Adaptation and Exposure Direction

Define what kinds of adaptation and exposure are required without creating a
complete Week.

For each priority object, state:

- intended adaptation or preservation claim;
- target determinant or capability;
- required exposure characteristics;
- relevant quality condition;
- broad frequency or continuity need only when supportable;
- transfer opportunity;
- and incompatible exposure conditions.

Use directional language appropriate to current evidence:

- develop;
- preserve;
- re-establish;
- stabilize;
- expose;
- explore;
- reduce cost;
- or protect expression.

Do not convert exposure direction into future Session details.

Do not assign a universal number of contacts, meters, repetitions, or days.

**Step output:** `required_adaptation_direction` and
`required_exposure_direction`.

---

## Step 5. Interpret Candidate Interventions

Candidate interventions may come from existing project knowledge or a future
external retrieval interface.

This Workflow does not require a fixed exercise library.

When no suitable candidate is available, emit:

`Candidate Intervention Required`

and, when appropriate:

`External Retrieval May Be Invoked`.

Every candidate must be interpreted through the
[Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md).

For each candidate, record:

- training task and execution conditions;
- intended stimulus;
- relevant dose dimensions;
- expected adaptation;
- transfer hypothesis;
- recovery and opportunity cost;
- risk;
- athlete-state dependence;
- temporal dependencies;
- and uncertainty.

Apply the [Conditional Appropriateness Rules](../rules/conditional_appropriateness.md)
and remove candidates excluded by hard constraints.

If several candidates remain, use the
[Plan Comparison Rules](../rules/plan_comparison.md) without hiding trade-offs
inside a false total score.

**Step output:** `interpreted_candidate_interventions`, feasible alternatives,
and conditional preference.

---

## Step 6. Define Dose Direction

Define the intended direction of dose across the Mesocycle.

Permitted directions include:

- Increase;
- Maintain;
- Reduce;
- Stabilize;
- Redistribute;
- Explore;
- or Temporarily Withdraw.

Dose direction must identify the task-specific dimension affected.

It must distinguish:

- development exposure;
- maintenance exposure;
- Minimal exploratory exposure;
- and competition exposure.

Record the expected relationship among:

Dose Direction

→ Expected Stimulus

→ Expected Adaptation

→ Expected Cost.

Do not define universal numerical thresholds.

Do not assume more dose produces more benefit.

Specific Session doses will be defined closer to execution using current
Athlete State.

**Step output:** `dose_direction` with affected dimensions and uncertainty.

---

## Step 7. Define Stress-Organization Requirements

Apply the [Stress Organization Rules](../rules/stress_organization.md).

Define constraints that future Weeks must preserve, including:

- Primary quality requirements;
- major stress-dimension overlap;
- local tissue overlap;
- clustering or separation relationships;
- sequencing dependencies;
- recovery opportunities;
- residual-cost concerns;
- competition stress;
- and known interference risks.

High / Low may be selected as a candidate organization strategy only when its
conditions fit the athlete and selected exposures.

Do not prescribe a fixed number of High days or a permanent weekly template.

State which organizational features are required, preferred, conditional, or
unresolved.

**Step output:** `stress_organization_requirements`.

---

## Step 8. Define Expected Response

State what should be observed if the adaptation and intervention hypotheses are
reasonable.

Expected Response should cover only decision-relevant domains, such as:

- Actual Exposure and Achieved Quality;
- immediate task response;
- delayed recovery and tissue response;
- repeated performance trend;
- longer-term adaptation signal;
- and sprint-relevant transfer or competition expression.

For each expected response, record:

- expected direction or acceptable range;
- relevant time relationship without universal biological deadlines;
- observation source and context;
- competing explanations;
- and what deviation would challenge the current assumption.

Expected adaptation is not guaranteed adaptation.

**Step output:** `expected_response_profile`.

---

## Step 9. Define Monitoring Questions

Retain only questions capable of changing interpretation, confidence, decision
state, decision scope, or risk handling.

Monitoring questions should address:

- whether intended exposure occurred;
- whether quality was achieved;
- whether cost remained within the expected relationship;
- whether the target state is changing;
- whether transfer is appearing;
- whether a constraint changed;
- and whether competing bottleneck explanations remain plausible.

Do not create a generic test catalogue.

For each question, state:

- the decision it can affect;
- the observation source;
- required context or comparability;
- and the uncertainty that remains.

**Step output:** `monitoring_questions` and `observation_requirements`.

---

## Step 10. Define the Progression and Regression Interface

Call the [Progression Rules](../rules/progression.md).

Reference the available decision states:

- Maintain;
- Progress;
- Reduce;
- Modify;
- Temporarily Withdraw;
- and Transition.

Do not copy or replace their operational criteria.

For the current Mesocycle, identify:

- the target object of a possible decision;
- the dose or exposure dimension that may change;
- the evidence source;
- the expected response comparison;
- the smallest plausible decision scope;
- and the review interface.

Decision state and priority allocation state must remain distinct.

**Step output:** `progression_regression_interface`.

---

## Step 11. Define Exit Criteria

Exit criteria define when the current adaptation problem no longer justifies
continuing the Mesocycle in its present form.

Apply the [Stage Transition Rules](../rules/stage_transition.md).

Exit may be supported when:

- the Desired Exit State has sufficient support;
- the Candidate Bottleneck has changed;
- marginal value has declined;
- cost or interference has become disproportionate;
- a constraint has changed;
- competition timing requires a different emphasis;
- the intervention or transfer hypothesis has materially weakened;
- or another problem now has a stronger priority claim.

Calendar elapsed is not sufficient by itself.

Define:

- successful-exit conditions;
- constraint-driven exit conditions;
- hypothesis-failure conditions;
- competition-driven transition conditions;
- evidence and confidence requirements;
- and the destination or review scope.

**Step output:** `mesocycle_exit_criteria`.

---

## Step 12. Define Extension and Early-Exit Conditions

Extension is admissible when:

- the adaptation problem remains relevant;
- the hypothesis remains supported;
- expected progress is incomplete but plausible;
- marginal value remains sufficient;
- constraints permit continuation;
- and extension does not compromise competition preparation.

Early exit is admissible when:

- the Desired Exit State is reached sooner than expected;
- a higher-priority problem emerges;
- a hard constraint removes feasibility;
- repeated evidence challenges the governing hypothesis;
- cost or risk becomes unacceptable;
- or competition timing changes.

Do not extend merely to complete a calendar block.

Do not exit from one noisy observation unless consequence or constraint makes
immediate action justified.

**Step output:** `extension_conditions`, `early_exit_conditions`, and review
scope.

---

## Mesocycle Output

The completed Mesocycle must output:

- `cycle_intent_reference`;
- `adaptation_problem`;
- `start_state`;
- `desired_exit_state`;
- `mesocycle_priority_allocation`;
- `required_adaptation_direction`;
- `required_exposure_direction`;
- `interpreted_candidate_interventions`;
- `dose_direction`;
- `stress_organization_requirements`;
- `competition_context_and_constraints`;
- `expected_response_profile`;
- `monitoring_questions`;
- `progression_regression_interface`;
- `mesocycle_exit_criteria`;
- `extension_conditions`;
- `early_exit_conditions`;
- `unresolved_uncertainty`;
- and any `higher_level_review_flag`.

The output must remain more abstract than a Week.

It defines what exposures and state change are required.

It does not fill calendar days or prescribe every Session.

---

## Week Handoff

The Mesocycle output provides [Create Week Workflow](./create_week.md) with:

- inherited Cycle intent;
- current adaptation problem;
- current Athlete State;
- priority allocation;
- required exposure direction;
- feasible candidate interventions;
- dose direction;
- stress-organization requirements;
- competition constraints;
- expected response;
- monitoring questions;
- and review and exit conditions.

The Week may refine placement, short-horizon dose, and conditional Sessions
using newer information.

It must not silently change the adaptation problem or strategic priority.

When near-term evidence challenges them, the Week returns a
`mesocycle_review_flag` rather than creating a new objective locally.

---

## Feedback and Escalation Interface

Session anomalies first enter Session review.

Repeated or connected near-term patterns can justify Week review.

Repeated evidence that challenges the adaptation problem, bottleneck,
intervention, dose direction, or transfer hypothesis can justify Mesocycle
review.

Evidence that challenges Cycle intent, competition structure, or the feasible
strategic trajectory must be escalated to Cycle review.

Use the smallest planning level justified by the evidence.

---

## Mesocycle Completion Gate

The Mesocycle is complete when:

- the current adaptation problem can be stated clearly;
- Start State and Desired Exit State are explicit;
- priorities are confirmed under current conditions;
- required exposure and dose directions are represented;
- candidate interventions have a 03 interpretation or a retrieval interface;
- stress-organization requirements are explicit;
- Expected Response and decision-relevant monitoring questions are defined;
- progression and regression call existing Rules;
- exit, extension, and early-exit conditions are explicit;
- and uncertainty and higher-level conflicts remain visible.

If these conditions are not met, return a provisional Mesocycle or `Cannot
Determine` rather than substituting a fixed-duration phase template.
