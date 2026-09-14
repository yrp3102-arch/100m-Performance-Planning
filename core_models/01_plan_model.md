# Plan Core Model

Version: 0.1
Status: Draft
Date: 2026-09-14

## Purpose

This document defines what a training plan is,
what information it must contain,
and how the 100m Performance Planning system evaluates plan quality.

This document defines the core model of a training plan: its objects,
relationships, dimensions, invariants, and interfaces.

It does not contain the operational rulebooks or ordered execution procedures
used to apply the model. Those materials are linked from the relevant model
interfaces below.

---
## 1. Definition of a Training Plan

A training plan is a time-constrained and updateable decision structure
for directing training toward a defined performance objective.

It exists in relation to:

- a specific athlete,
- a defined performance goal,
- the athlete's current state,
- training history,
- available time,
- competition constraints,
- recovery capacity,
- available resources,
- uncertainty,
- and observed response.

A training plan is therefore more than a schedule of exercises.

A complete plan must connect:

Goal
→ Athlete State
→ Training Problem
→ Priority
→ Stimulus
→ Dose
→ Temporal Organization
→ Monitoring
→ Response
→ Decision Update.

The plan may contain predetermined training sessions,
but predetermined sessions do not constitute the entire plan.

A valid planning system must also specify how the original prescription
can be maintained, progressed, reduced, modified, withdrawn, or
transitioned when relevant conditions change.

Therefore, within the 100m Performance Planning system:

Training Plan ≠ Exercise List

Training Plan ≠ Weekly Schedule

Training Plan ≠ Periodization Model

Training Plan ≠ Fixed Prediction of Adaptation

Instead:

Training Plan = Direction + Prescription + Constraints + Feedback + Update Rules

Periodization is treated as one component of planning:
the organization of emphasis, load, and performance expression across time.

Programming is treated as the process of converting planning objectives
into specific stimuli, doses, sequences, and progression or regression rules.

Training prescription is the executable expression of a decision at the
session or task level.

Monitoring is the process of collecting information needed to evaluate
whether the expected stimulus and response actually occurred.

Autoregulation is the bounded modification of the prescription according
to predefined or interpretable information about the athlete's current
or recent response.

These components belong to the same planning system but must not be
treated as synonyms.

## 2. Minimum Information Structure

A training plan must contain enough information to support execution,
evaluation, comparison, and revision.

"Minimum" refers to minimum informational sufficiency.

It does not mean that every plan must display every variable in a single
document or table.

Relevant information may be stored across athlete records, competition
calendars, monitoring systems, session plans, and historical logs,
provided that the planning system can retrieve and verify it.

A complete training plan should contain the following information groups.

### 2.1 Objective

The plan must define:

- the primary performance target,
- the relevant competition or testing window,
- the current phase objective,
- and the priority of that objective relative to competing goals.

Without a defined objective, the system cannot determine which
adaptations justify their cost.

---

### 2.2 Athlete and Current State

The plan must be grounded in relevant information about the athlete.

This may include:

- training age,
- competitive level,
- recent sprint performance,
- current training exposure,
- known responses to previous training,
- tissue status,
- recent interruptions,
- and relevant individual constraints.

The same training dose may be insufficient, appropriate, or excessive
for different athletes or for the same athlete at different times.

---

### 2.3 Stimulus and Dose

The plan must identify what adaptation is being targeted and how the
training stimulus will be delivered.

Dose information should be interpretable.

Depending on the task, this may include:

- exercise or sprint task,
- actual or target velocity,
- intensity reference,
- distance or duration,
- repetitions,
- sets,
- rest intervals,
- frequency,
- external load,
- contact volume,
- and other task-specific parameters.

Exercise names alone do not define a stimulus.

---

### 2.4 Time and Sequence

The plan must specify how training elements relate across time.

This includes:

- within-session order,
- spacing between important sessions,
- weekly organization,
- mesocycle placement,
- competition timing,
- travel,
- and other hard scheduling constraints.

A collection of individually reasonable sessions may still form an
unreasonable plan if their sequence produces excessive overlap or
insufficient recovery.

---

### 2.5 Recovery Assumptions

The plan must make its recovery assumptions visible.

This may include:

- expected residual cost,
- available sleep and recovery time,
- low-load activity,
- competition or travel stress,
- and known lifestyle constraints.

A day labeled "recovery" or "Low" must not be assumed to be low-cost
without examining its actual content and residual effect.

---

### 2.6 Progression and Regression

The plan must define how training can change.

It should specify the conditions under which the system may:

- Maintain,
- Progress,
- Reduce,
- Modify,
- Temporarily Withdraw,
- or Transition.

Progression must not be defined only as adding volume or reaching the next
calendar week.

---

### 2.7 Monitoring

The plan must identify which observations are relevant to its decisions.

Monitoring should specify:

- what is measured,
- how it is measured,
- what reference or baseline is used,
- how measurement noise is handled,
- and what decisions the information can influence.

Collecting data without a decision purpose does not constitute useful
monitoring.

---

### 2.8 Stop and Transition Conditions

The plan must contain a path for stopping, reducing, or changing training.

This includes:

- session stop rules,
- abnormal tissue-response rules,
- progression failure,
- stage exit criteria,
- return conditions,
- and handling of missing or unreliable information.

A plan that only defines how to continue but not how to stop or change is
incomplete.

---

### 2.9 Competition Expression

The plan must connect training development with the intended competition.

Relevant information may include:

- priority competitions,
- competition density,
- rounds,
- travel,
- taper objectives,
- pre-competition exposure,
- and alternative competition windows.

Training development and competition preparation must not be treated as
independent systems.

---

### 2.10 Decision Rationale

Important decisions should retain enough rationale to be reviewed later.

This may include:

- the problem being addressed,
- the working hypothesis,
- the expected adaptation,
- the evidence or prior experience supporting the decision,
- the expected response,
- the major uncertainty,
- and the review point.

This allows the system to distinguish:

a poor decision,

from

a reasonable decision that produced an unfavorable outcome.

---

### Minimum Sufficiency Rule

A plan does not need maximum information.

It needs enough information to answer:

1. What are we trying to change?
2. Why is this currently a priority?
3. What stimulus will be used?
4. What dose will be delivered?
5. How is it organized in time?
6. What cost and recovery are expected?
7. What will be monitored?
8. What will cause maintenance, progression, reduction, or modification?
9. How does this relate to the competition objective?
10. What important uncertainty remains?

If the available information is insufficient to answer a decision-critical
question, the system must mark the plan as information-incomplete rather
than silently inventing the missing value.

---

## 3. Plan Quality Model

Plan quality has three irreducible dimensions:

- Structural Validity,
- Conditional Appropriateness,
- Adaptive Capacity.

They are related but not interchangeable. A plan may be structurally valid but
inappropriate for the current athlete; a plan may be appropriate at the time
of prescription but lack a credible way to update when conditions change; and
a plan may produce a favorable result while still containing structural defects.

Structural validity is evaluated before fine-grained comparison of expected
training effectiveness. Conditional appropriateness and plan comparison apply
only within the feasible planning space. Adaptive capacity preserves decision
quality after actual exposure and response provide new information.

### 3.1 Structural Validity

Structural validity refers to whether a training plan is internally coherent,
interpretable, executable, and reviewable before considering whether it is
optimal for a specific athlete.

A plan must be structurally valid before its conditional appropriateness or
comparative value can be meaningfully evaluated. The operational checks are
defined in [Structural Validity Rules](../rules/structural_validity.md).

### 3.2 Conditional Appropriateness

Conditional appropriateness refers to whether a structurally valid training
plan is suitable for a particular athlete under a particular set of conditions.

Appropriateness is relational. It depends on the interaction between:

Plan
→ Athlete
→ Goal
→ Current State
→ Training History
→ Time
→ Constraints
→ Uncertainty
→ Observed Response.

A plan can be structurally valid and still be inappropriate. The operational
condition checks and re-evaluation rule are defined in
[Conditional Appropriateness Rules](../rules/conditional_appropriateness.md).

### 3.3 Adaptive Capacity
Adaptive capacity refers to the ability of a training plan to remain useful
when relevant conditions change.

A plan should not be judged only by whether its initial prescription was
reasonable.

It should also be judged by whether it can detect meaningful change,
update its interpretation, and modify future decisions without losing the
overall performance objective.

Adaptive capacity does not mean constant change.

The system should avoid both:

- rigid execution despite meaningful new information,
- and excessive adjustment in response to noise.

The purpose of adaptation is to preserve decision quality under changing
conditions.

---

---

#### Planned Direction and Local Flexibility

The system should distinguish between:

- relatively stable strategic direction,
- and locally adjustable prescription.

Examples of relatively stable elements may include:

- the terminal 100m performance objective,
- major competition windows,
- the current performance problem,
- and broad phase priorities.

Examples of more adjustable elements may include:

- session dose,
- exercise selection,
- sprint distance,
- repetition number,
- rest interval,
- session order,
- weekly placement,
- and supporting work.

The existence of adjustment does not eliminate planning.

Instead:

Direction is planned.

Prescription is revisable.

---

---

#### Information Must Be Action-Relevant

New information should modify the plan only when it has sufficient relevance
to the current decision.

The system should ask:

- Is the information reliable enough?
- Is it specific to the current problem?
- Is it likely to change the preferred action?
- Is the signal stronger than expected measurement noise?
- Is there a meaningful downside to waiting for more information?

Not every fluctuation requires intervention.

A single noisy observation may trigger review without triggering a major plan
revision.

---

---

#### Exposure Must Be Distinguished from Prescription

The system must distinguish between:

Planned Exposure

and

Actual Exposure.

A prescribed MaxV session does not prove that a meaningful MaxV exposure
occurred.

A prescribed strength session does not prove that the intended force or power
stimulus occurred.

The system should record:

- what was planned,
- what was actually completed,
- what quality was achieved,
- and what relevant environmental or execution differences occurred.

Decision updates should be based primarily on actual exposure rather than on
the original plan label.

---

---

#### Immediate Response

The system should evaluate the immediate response to training.

Relevant observations may include:

- achieved sprint velocity,
- timing results,
- movement quality,
- bar velocity,
- RPE,
- local tissue sensation,
- technical stability,
- and unexpected difficulty.

Immediate response can influence whether the current session should:

- continue,
- stop,
- reduce,
- or change.

Immediate success does not prove that the total dose was appropriate.

---

---

#### Delayed Response

The system should also evaluate delayed response.

Relevant observations may include:

- local tissue response,
- soreness,
- subjective fatigue,
- sleep,
- motivation,
- daily function,
- warm-up response,
- and performance in the next relevant task.

Observation points such as 24h, 48h, or 72h may be useful,
but they are not universal biological recovery deadlines.

The system must not automatically classify an athlete as recovered simply
because a fixed number of hours has passed.

---

---

#### Repeated Trend

Single-session data should be interpreted within repeated exposure when
possible.

The system should look for patterns such as:

- stable quality with stable recovery cost,
- improving performance with similar cost,
- stable performance with decreasing cost,
- declining performance with increasing cost,
- persistent tissue irritation,
- or repeated failure to achieve the intended stimulus.

Repeated trend generally supports stronger decisions than isolated
fluctuation.

However, clinically or mechanically important warning signals do not require
multiple repetitions before action is taken.

---

---

#### Adaptation Must Respect Hard Constraints

Adaptive modification is bounded.

The system must not adapt in ways that violate:

- the terminal performance objective,
- competition deadlines,
- medical restrictions,
- safety constraints,
- available facilities,
- known tissue limitations,
- or major recovery constraints.

Autoregulation operates inside the plan.

It does not replace strategic planning.

---

---

#### Avoid Overreaction

Adaptive capacity includes the ability not to change the plan unnecessarily.

The system should resist revision when:

- the observation is likely within normal noise,
- measurement conditions changed,
- the signal is not relevant to the current decision,
- or the current plan has not been tested long enough to produce interpretable
  information.

Frequent change can destroy the ability to learn from training.

The system should prefer the smallest justified modification that addresses
the problem.

---

#### Adaptive Capacity Interface

The system should evaluate adaptation using the sequence:

Plan
→ Actual Exposure
→ Immediate Response
→ Delayed Response
→ Repeated Trend
→ Updated Athlete State
→ Maintain / Progress / Reduce / Modify / Withdraw / Transition
→ New Prescription.

A training plan has high adaptive capacity when it can update local decisions
in response to meaningful information while preserving strategic coherence.

A training plan has low adaptive capacity when it either:

- continues unchanged despite meaningful evidence,
- or changes so frequently that noise replaces planning.

The operational decision states, escalation rules, and decision record are
defined in [Progression Rules](../rules/progression.md). The Transition state
is defined in [Stage Transition Rules](../rules/stage_transition.md).

---
## 4. Plan Hierarchy

Training planning operates across multiple time scales.

Each level should answer a different class of questions.

The hierarchy exists to prevent two common errors:

- using long-term plans to prescribe details that cannot yet be known,
- and allowing short-term fluctuations to erase strategic direction.

The 100m Performance Planning system therefore separates strategic planning,
operational planning, execution, and feedback.

---

### 4.1 Cycle / Season Level

The Cycle level defines the broadest planning context.

It should answer questions such as:

- What is the terminal performance objective?
- What is the competition window?
- Which competitions have the highest priority?
- How much total time is available?
- What major environmental or life constraints exist?
- What broad performance problems are expected to require attention?
- Where must performance eventually be expressed?

The Cycle level provides direction and boundaries.

It should not attempt to predict every future session.

Its role is primarily strategic.

Typical outputs may include:

- target event,
- competition calendar,
- major performance objectives,
- broad training direction,
- major constraints,
- review points,
- and provisional phase structure.

The Cycle is relatively stable,
but it may still be revised when major assumptions change.

---

### 4.2 Mesocycle Level

The Mesocycle level defines the current adaptation problem.

It should answer:

- What is the most important problem now?
- Which capacities currently receive development priority?
- Which capacities should be maintained?
- Which capacities receive minimal exposure?
- Which capacities may be temporarily withdrawn?
- What training stress structure is expected?
- What evidence would justify progression?
- What conditions would justify extension, reduction, or transition?

A Mesocycle should therefore contain:

- a primary objective,
- current athlete-state assumptions,
- priority allocation,
- candidate training methods,
- approximate dose direction,
- monitoring priorities,
- progression rules,
- and exit criteria.

A Mesocycle is not defined only by duration.

Four planned weeks do not automatically create a four-week biological
adaptation period.

Calendar duration provides a review window.

Transition depends on evidence, constraints, and competition timing.

---

### 4.3 Week / Microcycle Level

The Week level organizes training stress and opportunities over several days.

It should answer:

- Which key exposures are required this week?
- How are demanding sessions spaced?
- Where are recovery opportunities?
- What competition, travel, school, work, or weather constraints exist?
- Which elements are fixed?
- Which elements are conditional?
- What can be removed if recovery cost is higher than expected?

The Week level translates Mesocycle priorities into a practical short-term
structure.

Typical outputs may include:

- weekly objective,
- key training exposures,
- session classification,
- ordering of important sessions,
- recovery days,
- optional elements,
- and weekly review criteria.

The Week should not be treated as a rigid container that must be completed.

If conditions change,
the system may move, reduce, modify, or remove training rather than compress
all missed work into the remaining days.

---

### 4.4 Session Level

The Session level converts weekly intent into an executable training
prescription.

It should answer:

- What is the primary purpose of this session?
- What stimulus must actually occur?
- What is the minimum meaningful exposure?
- What is the planned dose?
- What is the acceptable quality range?
- What supporting work is justified?
- What should be removed first if cost rises?
- What are the stop rules?

A session should distinguish between:

Primary Work

and

Supporting Work.

Supporting work must not compromise the primary objective without explicit
reason.

A session prescription may include:

- warm-up,
- sprint task,
- distance,
- repetitions,
- target velocity,
- rest interval,
- strength load,
- contact number,
- supporting exercises,
- quality criteria,
- and stop conditions.

The Session is a prescription.

It is not yet evidence that the intended training stimulus occurred.

---

### 4.5 Task / Exercise Level

The Task level describes an individual training action.

Examples include:

- a sprint repetition,
- a resisted sprint,
- a strength exercise,
- a jump task,
- an isometric action,
- a drill,
- or a recovery activity.

The system should define a task through its purpose and dose,
not through its name alone.

A task may include:

- intended adaptation,
- execution constraints,
- velocity,
- distance or duration,
- load,
- repetitions,
- rest,
- surface,
- technical requirement,
- and termination criteria.

The same exercise name may represent different training stimuli under different
implementation conditions.

Therefore:

Exercise Name ≠ Training Stimulus.

---

### 4.6 Actual Result Layer

Actual Result is not another planning period.

It records what actually happened.

The system should distinguish:

Planned Session

from

Actual Session.

Relevant information may include:

- completed repetitions,
- actual sprint times,
- achieved velocity,
- actual load,
- actual rest,
- exercise substitutions,
- missed elements,
- environmental conditions,
- immediate symptoms,
- RPE,
- and technical observations.

The planning system must update itself from actual execution,
not from the assumption that the written plan was completed exactly as
prescribed.

---

### 4.7 Response Layer

The Response layer records what happened after the exposure.

Relevant information may include:

- immediate output change,
- local tissue response,
- subjective fatigue,
- soreness,
- sleep,
- motivation,
- warm-up response,
- next-session performance,
- and repeated recovery patterns.

Response data informs the estimate of the athlete's current state.

It does not automatically prescribe the next action.

Interpretation occurs through the Feedback Decision Model.

---

### 4.8 Benchmark Layer

Benchmarks provide standardized reference points.

Examples may include:

- competition performance,
- 30m performance,
- Fly performance,
- standardized strength performance,
- CMJ,
- RSI,
- body mass,
- or other stable measurements.

Benchmarks should only be used when:

- the protocol is sufficiently standardized,
- the measure answers a relevant question,
- and the testing cost is justified.

Benchmark data should not be confused with daily monitoring.

A benchmark provides a reference.

It does not independently determine readiness or training priority.

---

### 4.9 Information Flow Between Levels

The hierarchy should operate in both directions.

Top-down flow:

Cycle
→ Mesocycle
→ Week
→ Session
→ Task.

This provides:

Direction
→ Priority
→ Organization
→ Prescription.

Bottom-up flow:

Task Execution
→ Actual Result
→ Response
→ Updated Athlete State
→ Week Review
→ Mesocycle Review
→ Cycle Review when necessary.

This provides:

Reality
→ Feedback
→ Revision.

The system therefore combines:

Top-down strategic constraint

with

Bottom-up empirical correction.

---

### 4.10 Different Levels Change at Different Speeds

Not every new observation should modify every planning level.

A poor repetition may change:

- the remaining repetitions in the session.

A poor session may change:

- the next session or the rest of the week.

A repeated pattern may change:

- Mesocycle dose or priority.

A major injury,
competition-calendar change,
or persistent failure of the current model may change:

- the Cycle strategy.

The higher the planning level,
the stronger the evidence normally required for revision.

This protects the system from both rigidity and overreaction.

---

### Hierarchy Invariants

The system should use the following hierarchy:

Cycle / Season
→ Mesocycle
→ Week / Microcycle
→ Session
→ Task.

Execution and feedback should be represented separately as:

Actual Result
→ Response
→ Benchmark / Trend
→ Updated Athlete State.

Planning moves downward from objective to prescription.

Evidence moves upward from execution to revised strategy.

No lower-level decision should contradict a higher-level objective without
explicitly triggering review of that higher-level assumption.

---

## 5. Constraints and Information State

### 5.1 Hard Constraints and Feasible Planning Space
A hard constraint is a condition that defines the feasible planning space.

Hard constraints are not ordinary training variables to be optimized away.

They limit which plans are currently admissible.

The planning system must distinguish between:

Hard Constraints

and

Soft Constraints / Preferences.

A soft constraint may influence plan selection.

A hard constraint can make an otherwise attractive plan infeasible.

Therefore:

Best Expected Training Effect

does not override

Feasibility, Safety, Time, or Non-Negotiable Restrictions.

---

### Constraint Invariants

Before optimizing a training plan,
the system must first define the feasible planning space.

The sequence is:

Objective

→ Identify Hard Constraints

→ Remove Infeasible Options

→ Identify Remaining Soft Constraints

→ Compare Feasible Training Options

→ Select and Monitor.

The system must not choose an infeasible plan merely because its theoretical
training benefit appears higher.

When a hard constraint changes,
the feasible planning space should be updated.

When a hard constraint cannot be satisfied,
the objective or method must change.
The operational identification, conflict handling, and response rules are
defined in [Constraint Handling Rules](../rules/constraint_handling.md).

### 5.2 Information Sufficiency and Uncertainty
A planning system must distinguish between:

Information that is missing

and

Information that is necessary for the current decision.

Not every unknown variable prevents action.

However, when missing information materially affects the expected benefit,
cost, risk, or feasibility of a decision,
the system must not silently replace that information with an assumption.

Insufficient information is therefore decision-dependent.

The relevant question is not:

"Do we know everything?"

The relevant question is:

"Do we know enough to make this decision at an acceptable level of
uncertainty?"

---

### Information Sufficiency Invariants

The system should preserve the following principles:

1. Missing information is not automatically zero, normal, or favorable.
2. Not every unknown prevents action.
3. Information requirements depend on the consequence of the decision.
4. Decision-critical uncertainty must remain explicit.
5. Conflicting signals require interpretation rather than mechanical averaging.
6. Measurement quality matters as much as data availability.
7. More information is not automatically better if obtaining it has meaningful
   cost.
8. Under high uncertainty, reversible and bounded decisions are generally
   preferable to aggressive irreversible changes.
9. "Cannot yet determine" is a legitimate planning output.
10. Confidence must not exceed the quality and relevance of the available
    information.

The system should seek the minimum information necessary to support the next
meaningful decision rather than attempting to eliminate all uncertainty.
The operational treatment of missing, conflicting, and uncertain information
is defined in [Uncertainty Handling Rules](../rules/uncertainty_handling.md).

---
## 6. Plan Comparison Model

Plan superiority is conditional. The relevant question is not which plan is
universally best, but which feasible option is currently preferable for the
athlete, objective, state, time horizon, constraints, and uncertainty at hand.

Necessary conditions come first: minimum information sufficiency, structural
validity, and hard-constraint feasibility determine the comparison set. An
infeasible or structurally defective option is not a normal alternative merely
because its theoretical upside appears large.

Comparison is multi-objective. Decision-relevant dimensions include:

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
- and complexity.

Pareto dominance may remove an option that is no better on all relevant
dimensions and meaningfully worse on at least one. Many decisions instead
involve trade-offs, so there may be no unique universal winner. The system must
not hide these trade-offs with false numerical precision.

Current marginal value matters more than historical reputation. The comparison
must be updated as conditions and observed responses change. Decision quality
must be evaluated from the information available when the decision was made,
and must not be replaced retrospectively by observed outcome.

The operational comparison dimensions, tests, and invariants are defined in
[Plan Comparison Rules](../rules/plan_comparison.md).

---

## 7. Model Interfaces

This Core Model defines what other documents must call; it does not repeat
their operational content.

### Rules

- [Structural Validity Rules](../rules/structural_validity.md) determine how
  Structural Validity is checked.
- [Conditional Appropriateness Rules](../rules/conditional_appropriateness.md)
  determine when a structurally valid plan is appropriate for the current
  athlete and conditions.
- [Progression Rules](../rules/progression.md) and
  [Stage Transition Rules](../rules/stage_transition.md) implement Adaptive
  Capacity decision states.
- [Constraint Handling Rules](../rules/constraint_handling.md) implement
  hard-constraint assessment and feasible-space handling.
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md) implement
  decision-specific information sufficiency and uncertainty handling.
- [Plan Comparison Rules](../rules/plan_comparison.md) implement multi-objective
  comparison among feasible options.

### Workflows

[Audit Existing Plan Workflow](../workflows/audit_existing_plan.md) applies the
model in ordered ex ante and ex post evaluation. Its concise model interface
is:

Context
→ Problem
→ Information
→ Structural Validity
→ Constraints
→ Feasible Options
→ Conditional Appropriateness
→ Comparison
→ Decision
→ Actual Exposure
→ Response
→ Updated State
→ Revised Decision.

### Adjacent Core Models

- [100m Performance Model](02_100m_performance_model.md) supplies the target
  performance problem and direct-performance context.
- [Stimulus, Dose, and Cost Model](03_stimulus_dose_cost_model.md) supplies the
  interpretation of training stimulus, dose, and cost.
- [Feedback Decision Model](04_feedback_decision_model.md) supplies the
  interpretation of feedback and the decision-update model.
