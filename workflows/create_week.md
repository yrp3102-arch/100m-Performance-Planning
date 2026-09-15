# Create Week Workflow

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This workflow creates a Week / Microcycle as a near-term exposure organization
unit.

It answers:

> What exposures must occur in the near term for the Mesocycle to remain on
> course, and how should those exposures coexist in time?

A Week does not merely fill Monday through Sunday.

It translates Mesocycle intent into required exposures, protected quality,
recovery opportunities, conditional Sessions, and provisional placement.

The calendar serves the exposure structure.

It does not determine that structure before priorities and demands are known.

Use the following interfaces:

- [Plan Core Model](../core_models/01_plan_model.md)
- [Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md)
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
- [Priority Allocation Rules](../rules/priority_allocation.md)
- [Stress Organization Rules](../rules/stress_organization.md)
- [Constraint Handling Rules](../rules/constraint_handling.md)
- [Conditional Appropriateness Rules](../rules/conditional_appropriateness.md)
- [Plan Comparison Rules](../rules/plan_comparison.md)
- [Progression Rules](../rules/progression.md)
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md)

---

## Required Inputs

| Input | Required meaning | Source or boundary |
|---|---|---|
| Mesocycle Objective | Current adaptation problem and Desired Exit State | From [Create Mesocycle Workflow](./create_mesocycle.md) |
| Current Athlete State | Most recent decision-relevant estimate | Must include confidence and relevant uncertainty |
| Current Priorities | Primary, Maintain, Minimal, and Temporarily Withdrawn allocations | Do not silently redefine them at Week level |
| Required Exposure Direction | Exposure characteristics needed to keep the Mesocycle on course | More specific than Mesocycle intent, less specific than a Session prescription |
| Recent Actual Exposure | Work and conditions actually encountered | Prescription alone is insufficient |
| Recent Response | Observed response, interpretation, trend, and unresolved explanations | Use evidence-weighted state update |
| Competition and Calendar Constraints | Races, travel, fixed obligations, available dates, and deadlines | Competition is an exposure and stressor |
| Available Training Opportunities | Real days, times, duration, facilities, coaching, and environment | Calendar slots do not imply that all should be filled |
| Tissue and Recovery State | Current local tolerance, fatigue, recovery opportunity, and restrictions | General readiness cannot override relevant local constraints |
| Dose Direction | Increase, Maintain, Reduce, Stabilize, Redistribute, Explore, or Temporarily Withdraw | Must retain the affected task-specific dimension |
| Stress Requirements | Quality, overlap, sequence, recovery, and interference constraints | From the Mesocycle and Stress Organization Rules |

If a current hard constraint makes the Mesocycle objective infeasible, stop
ordinary Week construction and return a `mesocycle_review_flag`.

If the problem can be resolved by local placement or dose modification, keep
the review at Week or Session scope.

---

## Step 1. Confirm Weekly Intent

Answer in one sentence:

> What must this Week accomplish for the current Mesocycle to remain on course?

The statement should identify:

- the current adaptation problem;
- the required near-term state or exposure contribution;
- the Primary allocation;
- relevant competition or recovery context;
- and the most important constraint.

Do not define Weekly Intent as completion of a list of sessions.

Do not create a new objective that is absent from the Mesocycle.

If current evidence weakens the inherited objective, retain the discrepancy and
raise the appropriate review flag.

**Step output:** `weekly_intent` and `mesocycle_alignment`.

---

## Step 2. Define Required Exposures

Identify required exposures before assigning calendar days.

Represent each exposure by role:

- Primary Exposure;
- Maintenance Exposure;
- Minimal Exposure;
- Competition Exposure;
- Recovery Opportunity;
- or Conditional Supporting Exposure.

For each exposure, state:

- target object;
- role in Weekly Intent;
- intended stimulus or recovery function;
- required quality characteristics;
- relevant dose dimensions;
- acceptable timing relationships;
- expected cost and residual demand;
- constraints;
- and whether an intervention candidate is already available.

Do not substitute an exercise label for an exposure definition.

When a method has not been selected, emit:

`Candidate Intervention Required`

or:

`External Retrieval May Be Invoked`.

Any retrieved candidate must still pass 03 interpretation, feasibility, and
conditional appropriateness.

**Step output:** `required_exposures`.

---

## Step 3. Define Exposure Importance

Map every exposure to the inherited priority allocation.

Classify its scheduling protection as:

- Protected;
- Required but Movable;
- Conditional;
- Optional;
- or Replaceable.

This classification does not create new priority states.

It describes how the Week preserves existing priorities during organization.

For each exposure, record:

- what resource must be protected;
- what could be modified without changing its role;
- what can be removed first if cost rises;
- and what change would require Mesocycle review.

Primary quality should receive the strongest protection.

The combined cost of Maintenance, Minimal, and supporting exposures must not
silently consume the resources reserved for Primary work.

**Step output:** `exposure_importance` and `protected_resources`.

---

## Step 4. Estimate Stress and Cost

Interpret each candidate intervention through the
[Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md).

Apply the [Stress Organization Rules](../rules/stress_organization.md).

For each exposure, represent:

- intended external dose;
- achieved-quality requirement;
- high-output demand;
- mechanical demand;
- local tissue stress;
- metabolic demand;
- technical and attentional demand;
- recovery cost;
- opportunity cost;
- competition-expression cost;
- risk;
- residual-cost relationship;
- and uncertainty.

Do not collapse distinct dimensions into an unsupported total load score.

When information is incomplete, use a qualitative profile and state what
cannot yet be determined.

**Step output:** `weekly_stress_cost_map`.

---

## Step 5. Organize Exposures in Time

Place exposures only after their roles and demand profiles are visible.

Evaluate:

- clustering of compatible demands;
- separation required to protect quality or tissue tolerance;
- within-session and between-session sequencing;
- local tissue overlap across different labels;
- residual cost carried into later exposures;
- recovery opportunities;
- competition placement;
- facility and schedule constraints;
- and the cost of transitions or additional training days.

High / Low may be used when it is a conditionally appropriate solution.

It must not impose a fixed frequency, fixed sequence, or universal day
classification.

For each provisional placement, record:

- the exposure or cluster;
- its time relationship to adjacent exposures;
- the rationale;
- the state required at entry;
- the expected residual state at exit;
- and the uncertainty that could change placement.

The output may use named days when real calendar constraints are known.

The organization must not begin by filling seven generic day slots.

**Step output:** `provisional_exposure_placement` and
`recovery_opportunities`.

---

## Step 6. Protect Primary Quality

Identify the execution conditions required for the Primary stimulus to retain
its intended identity.

Protect, where relevant:

- athlete state at entry;
- time and facility access;
- adequate recovery from prior exposure;
- required velocity, output, or technical stability;
- attention and coaching capacity;
- safe deceleration or movement space;
- and freedom from avoidable supporting-work interference.

Primary work should not be placed predictably inside the strongest residual
cost unless that state is part of the explicitly intended stimulus.

When fatigue is intentionally part of the exposure, define the acceptable
quality relationship in advance.

Do not reinterpret unplanned quality collapse as successful exposure.

If Primary quality cannot plausibly be protected within the feasible calendar,
compare a modification, redistribution, replacement, or Mesocycle review.

**Step output:** `primary_quality_protection`.

---

## Step 7. Define Conditional Sessions

Classify each provisional Session as:

- Fixed;
- Conditional;
- Optional;
- or Replaceable.

`Fixed` means the time or role is constrained strongly enough that moving it
would materially change the Week.

It does not mean the planned volume must be completed regardless of state.

`Conditional` means execution depends on stated Athlete State, environment,
Actual Exposure, or response conditions.

`Optional` means omission does not compromise the current minimum Weekly Intent.

`Replaceable` means the exposure role remains required but the selected method
can change if another feasible method better preserves the intended stimulus.

For every Conditional or Replaceable Session, state:

- the condition being tested;
- the preserved objective;
- the available decision states or alternative exposure;
- and the level to review if the condition fails.

Do not lock every Session before current state is known.

**Step output:** `session_status_map`.

---

## Step 8. Define Weekly Dose Direction

Translate the Mesocycle dose direction into a near-term relationship relative
to recent Actual Exposure.

Use one or more of:

- Increase;
- Maintain;
- Reduce;
- Redistribute;
- Stabilize;
- Explore;
- or Temporarily Withdraw.

For each direction, identify:

- target exposure;
- task-specific dose dimension;
- recent Actual Exposure used as the comparison;
- expected benefit;
- expected cost;
- interaction with other exposures;
- and uncertainty.

The Weekly direction does not require every Session to change in the same way.

A total-volume increase can coexist with reduction of a high-consequence local
dimension, or redistribution can preserve total exposure while changing its
temporal cost.

Do not manufacture universal progression thresholds.

**Step output:** `weekly_dose_direction`.

---

## Step 9. Define Contingencies

Define bounded responses to plausible disruptions without building a rigid
decision tree.

Relevant contingencies may include:

- higher-than-expected delayed cost;
- inability to achieve Primary quality;
- local tissue warning;
- changed facility or weather;
- shortened training time;
- competition schedule change;
- missed Session;
- unexpected competition exposure;
- or ambiguous response.

For each material contingency, state:

- the assumption affected;
- the exposure that remains essential;
- what can be moved, reduced, modified, replaced, or removed;
- what must not be compressed into later recovery space;
- and the smallest review scope.

Missed work is not a debt that must automatically be repaid.

If reorganization would violate a hard constraint or Mesocycle priority, return
a review flag rather than forcing calendar completion.

**Step output:** `weekly_contingencies`.

---

## Step 10. Define Weekly Review Questions

Define the questions needed to determine whether the Week kept the Mesocycle on
course.

Questions should address:

- Did required exposures actually occur?
- Was the intended stimulus achieved?
- Was Primary quality protected?
- Did organization create the expected recovery opportunities?
- Were tissue and residual costs as expected?
- Did competition satisfy or disrupt an exposure need?
- Did the Weekly dose direction occur in Actual Exposure?
- Does the observed pattern support the Mesocycle hypothesis?
- What uncertainty remains decision-relevant?
- What is the smallest justified update?

Specify the observation source and comparison context for each question.

Do not collect information that cannot alter interpretation, confidence,
decision, or risk handling.

**Step output:** `weekly_review_questions` and feedback destination.

---

## Week Output

The completed Week must output:

- `mesocycle_objective_reference`;
- `weekly_intent`;
- `current_athlete_state`;
- `required_exposures`;
- `exposure_importance`;
- `weekly_stress_cost_map`;
- `provisional_exposure_placement`;
- `primary_quality_protection`;
- `session_status_map`;
- `weekly_dose_direction`;
- `recovery_opportunities`;
- `weekly_contingencies`;
- `weekly_review_questions`;
- `expected_response_reference`;
- `session_briefs`;
- `unresolved_uncertainty`;
- and any `mesocycle_review_flag` or `cycle_review_flag`.

The output may contain provisional day and time placement.

It must preserve the ability of a Session to respond to current Athlete State
without silently changing Weekly Intent.

---

## Session Handoff

Each `session_brief` supplied to
[Create Session Workflow](./create_session.md) must include:

- `week_intent_reference`;
- session role and status;
- Primary and supporting objectives;
- target exposure and priority allocation;
- candidate intervention or retrieval need;
- intended stimulus;
- relevant dose direction and bounds;
- quality requirements;
- entry-state assumptions;
- prior and following exposure relationships;
- stress, tissue, and recovery constraints;
- available time, environment, and equipment;
- expected response;
- contingency options;
- Actual Exposure recording requirements;
- and feedback destination.

The Session may refine the prescription using current information.

If the current state invalidates the Session but not the Week, modify at
Session scope.

If the change affects several exposures or the recovery relationship among
them, return a `week_review_flag`.

---

## Feedback and Escalation Interface

Session anomaly

→ review Session first.

Repeated or connected near-term pattern

→ review Week.

Repeated evidence challenging the adaptation hypothesis

→ flag Mesocycle review.

Strategic assumption, competition structure, or feasible-space change

→ flag Cycle review.

Apply the smallest justified update while preserving high-consequence warning
signals that may require immediate broader action.

---

## Week Completion Gate

The Week is complete when:

- Weekly Intent clearly inherits the Mesocycle objective;
- required exposures are defined before calendar placement;
- each exposure has a role and protection level;
- multidimensional stress and cost are represented;
- clustering, separation, sequencing, tissue overlap, and residual cost are
  considered;
- Primary quality and real recovery opportunities are protected;
- Sessions are classified as Fixed, Conditional, Optional, or Replaceable;
- Weekly dose direction is tied to recent Actual Exposure;
- contingencies prevent automatic compression of missed work;
- review questions can change a decision;
- and escalation conditions remain explicit.

If these conditions cannot be satisfied, return a provisional Week or the
appropriate higher-level review flag rather than filling a seven-day template.
