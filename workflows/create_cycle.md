# Create Cycle Workflow

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This workflow creates the strategic state trajectory for the full competitive
horizon.

It answers:

> Where is the planning system trying to move the athlete across the available
> competitive horizon, and what strategic conditions govern that movement?

A Cycle is a strategic decision level.

It is not a long daily calendar, a fixed phase sequence, or an advance list of
Session prescriptions.

Long-horizon specificity belongs in objectives, priorities, constraints,
desired state transitions, competition structure, and review conditions.

Prescription specificity increases only when more current information becomes
available at lower planning levels.

Use the following model and rule interfaces:

- [Plan Core Model](../core_models/01_plan_model.md)
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
- [Priority Allocation Rules](../rules/priority_allocation.md)
- [Constraint Handling Rules](../rules/constraint_handling.md)
- [Conditional Appropriateness Rules](../rules/conditional_appropriateness.md)
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md)
- [Stage Transition Rules](../rules/stage_transition.md)

---

## Required Inputs

| Input | Required meaning | If incomplete |
|---|---|---|
| Terminal 100m Objective | Competitive outcome, target context, and relevant horizon | Keep the objective provisional; do not replace it with a proxy |
| Current Athlete State | Decision-relevant estimate with confidence and uncertainty | Reduce strategic specificity or obtain decision-critical information |
| Competition Calendar | Known competitions, importance, deadlines, rounds, travel, and uncertainty | Mark uncertain dates and preserve scheduling flexibility |
| Training History | Training age, recent and historical exposure, adaptation, tolerance, and interruption | Avoid assuming unobserved tolerance or responsiveness |
| Major Constraints | Medical, safety, tissue, time, facility, lifestyle, recovery, and information constraints | Define the feasible strategic space before selecting priorities |
| Current Performance Problems | Observed race or segment problems and their context | Retain `Cannot Determine` when diagnosis is not supported |
| Candidate Bottlenecks | Plausible limiting relationships with evidence and alternatives | Label provisional candidates and competing explanations |
| Planning Horizon | Time available for development, transfer, stabilization, and expression | Exclude trajectories that cannot fit the useful horizon |
| Important Uncertainty | Unknowns capable of changing strategy or competition preparation | State how uncertainty limits commitment or triggers review |

An input is sufficient only relative to the Cycle decision.

Missing detail that belongs to a future Session does not block strategic
planning.

Missing information that could change the terminal objective, feasible space,
competition structure, or strategic trajectory does block confident Cycle
completion.

---

## Step 1. Define the Terminal Objective

State competitive 100m performance as the terminal criterion.

Record:

- the target competition or competitive horizon;
- the performance outcome sought;
- the conditions under which outcomes will be interpreted;
- the role of secondary goals;
- and uncertainty in the objective or calendar.

Supporting indicators may describe candidate changes or evaluation signals.

They must not replace the competitive 100m objective.

If the stated objective is only a proxy, restate the relationship:

Proxy or Supporting Outcome

→ Intended Performance Relationship

→ Competitive 100m Objective.

If that relationship cannot be stated, flag the objective for review before
constructing the trajectory.

**Step output:** `terminal_objective` with scope, horizon, performance criterion,
supporting outcomes, and uncertainty.

---

## Step 2. Define the Competition Structure

Classify known competitions by planning role:

- Primary Competition;
- Secondary Competition;
- Benchmark Competition;
- or unresolved role.

Record for each relevant competition:

- date or date range;
- importance;
- expected rounds or race density;
- travel and environment;
- performance opportunity;
- expected exposure and stress role;
- recovery implication;
- and confidence in the information.

Competition is both a performance opportunity and an Actual Exposure.

It must enter load, recovery, and review assumptions.

Do not add competition to a normal training structure without accounting for
what it replaces, satisfies, or disrupts.

Identify fixed deadlines separately from flexible review dates.

**Step output:** `competition_structure` and `fixed_deadlines`.

---

## Step 3. Establish the Current Athlete State

Represent Athlete State as the current decision-relevant estimate defined by
the [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md).

Include only state dimensions that can affect Cycle decisions, such as:

- current competitive and sprint performance;
- current Performance Problem;
- Candidate Bottleneck status;
- fatigue and recovery context;
- tissue state and exposure tolerance;
- technical stability;
- adaptation and detraining context;
- competition-expression state;
- active constraints;
- and uncertainty.

Separate observations from interpretations.

Retain the source, context, reliability, relevance, and confidence of major
state claims.

Do not compress the state into a single readiness score.

**Step output:** `cycle_start_state` with evidence, confidence, and unresolved
questions.

---

## Step 4. Identify Strategic Performance Problems

Use the [100m Performance Core Model](../core_models/02_100m_performance_model.md)
to distinguish:

- Terminal Outcome;
- Race or Segment Outcome;
- Performance Determinant;
- Underlying Capacity or Constraint;
- and Observable Indicator.

For each strategic problem, record:

- the observed performance issue;
- the race context in which it occurs;
- candidate explanations;
- Candidate Bottleneck or limiting-constraint claims;
- supporting and conflicting evidence;
- expected 100m relevance;
- and confidence.

Do not infer a bottleneck from weakness, association, or proxy status alone.

Permitted outputs include:

- Supported Performance Problem;
- Provisional Bottleneck;
- Multiple Candidate Bottlenecks;
- and `Cannot Determine`.

When identification is incomplete, define what information could change the
strategic choice.

**Step output:** `strategic_performance_problems`.

---

## Step 5. Identify Major Constraints

Apply the [Constraint Handling Rules](../rules/constraint_handling.md).

Separate:

- Hard Constraints that define the feasible planning space;
- Soft Constraints that influence comparison;
- and unresolved conditions whose consequence is decision-critical.

At Cycle scope, consider:

- competition deadlines;
- medical and rehabilitation restrictions;
- safety and tissue limitations;
- facility and environment access;
- available training time;
- lifestyle and travel demands;
- recovery ceiling;
- and information constraints.

Remove strategically infeasible trajectories before comparing their expected
benefit.

When a constraint makes the original objective infeasible, revise or qualify
the objective rather than preserving an impossible trajectory.

**Step output:** `cycle_constraints`, `feasible_strategic_space`, and unresolved
constraint conflicts.

---

## Step 6. Allocate Strategic Priorities

Apply the [Priority Allocation Rules](../rules/priority_allocation.md).

Assign each decision-relevant target one allocation state:

- Primary;
- Maintain;
- Minimal;
- or Temporarily Withdrawn.

For each allocation, record:

- the target object;
- its relationship to the Performance Problem;
- expected marginal value;
- transfer path;
- major resource claim;
- recovery and opportunity cost;
- risk and uncertainty;
- time to useful benefit;
- and reallocation conditions.

Primary claims must remain scarce relative to available resources.

Do not assign every generally important quality to Primary.

Do not treat Minimal as guaranteed maintenance or Temporarily Withdrawn as
permanent irrelevance.

**Step output:** `strategic_priority_allocation`.

---

## Step 7. Define the Strategic State Trajectory

Describe the intended trajectory before naming phases or assigning months.

Use the relationship:

Current State

→ Intermediate State or States

→ Competition-Ready State.

For each state transition, specify:

- the relevant Performance Problem;
- the intended decision-relevant state change;
- the strategic priority served;
- the expected direction of exposure;
- the principal constraints;
- the expected transfer relationship;
- the evidence that would support transition;
- and uncertainty.

The trajectory should be strategically specific and prescription-light.

It must not assign future daily distances, repetitions, loads, or recovery
intervals that depend on information not yet available.

Traditional labels such as block, accumulation, realization, or competition
phase may describe a selected solution.

They must not determine the trajectory before the state problem is defined.

**Step output:** `strategic_state_trajectory`.

---

## Step 8. Define the Mesocycle Sequence

Partition the trajectory into decision units only where distinct adaptation
problems or desired state transitions justify them.

Each provisional Mesocycle brief must contain:

- inherited Cycle intent;
- current or anticipated adaptation problem;
- intended start-state assumption;
- desired state change;
- Primary allocation;
- Maintain, Minimal, and Temporarily Withdrawn allocations where relevant;
- required exposure direction;
- major stress and recovery constraints;
- competition relationship;
- expected response direction;
- exit condition;
- and unresolved uncertainty.

Do not define a Mesocycle merely by assigning a fixed number of weeks.

Duration may be a planning estimate or review window.

Exit remains conditional on state, evidence, constraints, and competition
timing.

Do not prescribe Sessions at Cycle level.

When a future intervention has not yet been selected, the brief may retain
`Candidate Intervention Required` for lower-level existing-knowledge or
external-retrieval handling.

**Step output:** ordered `mesocycle_briefs` with dependencies and provisional
review windows.

---

## Step 9. Define Competition Integration

For each competition or race cluster, state how it affects:

- strategic priority;
- development versus expression emphasis;
- exposure requirements;
- expected stress and residual cost;
- freshness requirements;
- evaluation opportunities;
- and possible state transition.

Identify which planned work may be replaced, reduced, or reinterpreted because
competition supplies an Actual Exposure.

Preserve the distinction between underlying capacity and competition
expression.

A favorable or unfavorable race outcome must not automatically validate or
invalidate every strategic assumption.

**Step output:** `competition_integration` linked to Mesocycle briefs.

---

## Step 10. Define Review and Revision Points

Define events that open Cycle review without precommitting to automatic Cycle
change.

Review events should include:

- Mesocycle exit or failed exit;
- Primary or Benchmark Competition review;
- major competition-calendar change;
- new or changed hard constraint;
- repeated response deviation that challenges the strategic model;
- important tissue or safety warning;
- persistent transfer failure;
- and major change in the terminal objective.

Apply the principle:

> Update the smallest planning level justified by the evidence.

A Session anomaly normally returns first to Session or Week review.

Escalate to Cycle when evidence challenges the terminal objective, competition
structure, feasible strategic space, or governing trajectory.

**Step output:** `cycle_review_events`, `review_scope`, and escalation interface.

---

## Step 11. Record Major Uncertainty

Apply the [Uncertainty Handling Rules](../rules/uncertainty_handling.md).

For each strategic unknown, record:

- the claim affected;
- why it matters;
- current confidence;
- the consequence of being wrong;
- whether the decision is reversible;
- what information could reduce uncertainty;
- and the review event at which it should be reconsidered.

Do not delay the entire Cycle for detail that is unnecessary at strategic
scope.

Do not create false precision when a major unknown could change the trajectory.

Allowed states include Provisional, Unresolved, and `Cannot Determine`.

**Step output:** `cycle_uncertainty_register`.

---

## Cycle Output

The completed Cycle must output:

- `terminal_objective`;
- `cycle_start_state`;
- `competition_structure`;
- `strategic_performance_problems`;
- `cycle_constraints`;
- `feasible_strategic_space`;
- `strategic_priority_allocation`;
- `strategic_state_trajectory`;
- ordered `mesocycle_briefs`;
- `competition_integration`;
- `cycle_review_events`;
- `cycle_uncertainty_register`;
- and `conditions_requiring_cycle_revision`.

The output must show the rationale connecting:

Terminal Objective

→ Athlete State

→ Performance Problem

→ Candidate Bottleneck

→ Constraints

→ Priority

→ Strategic State Trajectory

→ Mesocycle Brief.

It must not contain daily prescriptions.

---

## Mesocycle Handoff

The selected `mesocycle_brief` is the required higher-level input to
[Create Mesocycle Workflow](./create_mesocycle.md).

The Mesocycle may refine the current state, intervention candidates, dose
direction, and stress requirements using newer information.

It must not silently replace Cycle intent.

If the inherited intent is no longer feasible or supported, return a
`higher_level_review_flag` containing:

- the challenged Cycle assumption;
- the new evidence or constraint;
- the consequence for the trajectory;
- the smallest adequate review scope;
- and confidence.

---

## Cycle Completion Gate

The Cycle is complete when:

- the terminal 100m objective is explicit;
- competition roles and deadlines are represented;
- the current Athlete State and uncertainty are visible;
- strategic Performance Problems and Candidate Bottlenecks are separated;
- hard constraints define a feasible strategic space;
- strategic priorities are allocated;
- the state trajectory precedes the phase sequence;
- Mesocycle briefs include exit and review conditions;
- competition is represented as opportunity and stress;
- and higher-level revision conditions are explicit.

If any missing item can materially change the strategy, return a provisional
Cycle or `Cannot Determine` rather than filling the gap with a conventional
phase template.
