# Review Training Workflow

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This workflow converts completed training or competition exposure into an
evidence-weighted planning update.
It answers:
> After execution, what actually happened, what can reasonably be inferred,
> how should the Athlete-State Estimate change, and which planning level should
> act next?
The governing sequence is:
Planned Intervention
→ Actual Exposure
→ Observed Response
→ Contextualized Observation
→ Candidate Interpretations
→ Evidence-Weighted Athlete-State Update
→ Decision State
→ Decision Scope
→ Revised Planning Action.
This is an Execution Feedback Review.
It is not a plan generator, readiness checklist, monitoring catalogue, fixed
threshold system, or medical diagnostic process.
Use the following model and rule interfaces:
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
- [Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md)
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
- [Plan Core Model](../core_models/01_plan_model.md)
- [Progression Rules](../rules/progression.md)
- [Stage Transition Rules](../rules/stage_transition.md)
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md)
- [Constraint Handling Rules](../rules/constraint_handling.md)

## Workflow Boundary

This workflow begins after an exposure has occurred or after an observation
window relevant to that exposure has opened.
It reviews:
- what was planned;
- what was actually executed;
- what was observed across relevant time scales;
- what the observations may mean;
- what changed in the current Athlete-State Estimate;
- and what planning action is justified.
It does not reproduce the plan-quality audit in
[Audit Existing Plan Workflow](./audit_existing_plan.md).
That Workflow asks whether an existing plan is structurally valid, feasible,
conditionally appropriate, coherent, and preferable among alternatives.
This Workflow asks what execution and response now imply for the next planning
decision.
It also does not generate the revised plan.
It returns control to one of:
- [Create Session Workflow](./create_session.md);
- [Create Week Workflow](./create_week.md);
- [Create Mesocycle Workflow](./create_mesocycle.md);
- or [Create Cycle Workflow](./create_cycle.md).
The stable boundaries are:
Planned Session ≠ Actual Session.
Prescription ≠ Actual Exposure.
Observation ≠ Interpretation.
Observed Response ≠ Final Explanation.
Single Session ≠ Stable Trend.
Decision Update ≠ Automatic Full-Plan Rewrite.

## Required Inputs

| Input | Required meaning | Missing-information treatment |
|---|---|---|
| Planned Session or Week Intent | The objective, exposure role, and higher-level intent being reviewed | Preserve the known scope; do not invent the original rationale |
| Prescribed Intervention | The executable task and conditions that were specified | If absent, Prescription Failure may remain plausible |
| Intended Stimulus | The exposure properties the prescription was meant to produce | Do not infer it from the exercise label alone |
| Planned Dose | The task-specific dose dimensions and quality boundaries | Mark unavailable dimensions as unknown |
| Expected Response | The prospective response pattern and cost considered compatible with the hypothesis | If absent, perform descriptive review and limit hypothesis evaluation |
| Actual Exposure | What the athlete completed and encountered | Reconstruct before interpreting response |
| Achieved Quality | Whether execution retained properties required by the intended stimulus | Do not equate completion or effort with quality |
| Immediate Observations | Relevant observations during or close to exposure | Keep raw description separate from explanation |
| Delayed Observations | Relevant observations after the immediate period | Use response-specific observation windows, not universal deadlines |
| Recent Trend | Comparable prior exposure and response information | If unavailable, do not label one event a stable trend |
| Prior Athlete-State Estimate | Previous decision-relevant state with confidence | New evidence updates rather than automatically erases it |
| Current Priority | Primary, Maintain, Minimal, or Temporarily Withdrawn allocation | Keep allocation state distinct from Decision State |
| Active Constraints | Medical, safety, tissue, time, recovery, environment, lifestyle, and information constraints | Apply hard boundaries before selecting action |
| Competition Proximity | Competition role, time, expression requirement, and exposure context | Include competition as outcome, stress, and information source |
| Unresolved Uncertainty | Existing unknowns and competing interpretations | Preserve any uncertainty not reduced by the review |
If inputs support only part of the review, output `Partial Review` and state
which conclusions remain supportable.
If missing or unreliable information prevents the required distinction, output
`Cannot Yet Determine` with the information needed to reduce uncertainty.
Do not convert missing values into zero, normal, recovered, tolerated, or
unchanged.

## Step 1. Define the Review Object

Identify the object and evidence scope before interpreting outcomes.
Supported review objects include:
- Single Task;
- Session;
- Week / Microcycle;
- Mesocycle Exposure Pattern;
- and Competition.
Record:
- `review_object`;
- `review_window`;
- `planning_level`;
- `higher_level_intent`;
- `current_priority`;
- `decision_required`;
- and `evidence_cutoff`.
Use the same feedback architecture at every scale.
Change the review object and evidence scope rather than duplicating a different
logic for each scale.
A Session Review may rely mainly on one prescription and its immediate or
delayed response.
A Week Review integrates several related Actual Exposures and their recovery
relationships.
A Mesocycle Review evaluates repeated evidence against the adaptation and
transfer hypothesis.
A Competition Review treats the event as:
- a performance outcome;
- an Actual Exposure;
- a stress event;
- and an information source.
Do not judge a Cycle solely from a single ordinary Session or race outcome.
**Step output:** `review_object_definition`.

## Step 2. Reconstruct Actual Exposure

Review Actual Exposure before interpreting response.
Start from the execution record created by
[Create Session Workflow](./create_session.md), then reconcile it with the
prescription.
Record only decision-relevant differences in:
- prescribed and completed tasks;
- planned and completed dose;
- achieved intensity, velocity, load, duration, density, or other relevant
  dimension;
- achieved quality;
- rest and recovery conditions;
- substitutions and omissions;
- interruptions;
- execution strategy;
- surface, weather, equipment, timing, and environment;
- competition rounds or repeated exposures;
- and missing execution data.
Represent the comparison as:
Prescribed Task and Planned Dose
versus
Actual Exposure and Achieved Quality.
Classify the exposure relationship as:
- Broadly Matched;
- Partially Matched;
- Meaningfully Divergent;
- or Insufficiently Recorded.
These categories describe exposure agreement.
They do not yet explain the response or select a Decision State.
If Actual Exposure materially differs from the assumed exposure, do not
attribute the Observed Response directly to the original intervention
hypothesis.
**Step output:** `planned_vs_actual_exposure` and exposure-agreement status.

## Step 3. Record Immediate Response

Record relevant observations during or close to the Actual Exposure.
Possible observation domains include:
- sprint or task performance;
- change across repetitions;
- movement or technical stability;
- achieved force, velocity, or power expression;
- perceived effort or unexpected difficulty;
- local tissue sensation;
- task completion;
- acute cost;
- and competition execution.
This is not a mandatory measurement list.
Select observations according to the intended stimulus, Expected Response,
current priority, risk, and decision that may follow.
For every retained observation, record:
- source;
- time or observation window;
- observed object;
- value or description;
- protocol or collection condition;
- comparison reference;
- context;
- quality limitations;
- and decision relevance.
Write the observation descriptively.
Do not encode a causal interpretation inside the observation field.
When a meaningful tissue or safety warning appears, flag it immediately and
apply hard constraints before continuing ordinary review.
The Workflow may Modify or Temporarily Withdraw exposure and request external
professional assessment within the applicable boundary.
It must not diagnose injury, issue medical clearance, or override an existing
medical restriction.
**Step output:** `immediate_response_observations` and any warning flag.

## Step 4. Record Delayed Response

Record observations that emerge, persist, or resolve after the immediate
exposure period.
Possible domains include:
- local tissue response;
- soreness or discomfort;
- fatigue and recovery experience;
- sleep and daily function;
- motivation when it affects execution;
- warm-up behavior;
- restoration of task capability;
- next-task performance;
- and delayed competition cost.
Monitor only domains capable of changing interpretation, confidence, Athlete
State, risk, or planning action.
The relevant observation window depends on:
- the Actual Exposure;
- response dimension;
- athlete history;
- tissue and recovery state;
- next required exposure;
- and consequence of incomplete recovery.
Twenty-four, forty-eight, and seventy-two hours may be observation
opportunities.
They are not universal recovery thresholds.
Different response dimensions may follow different time courses.
If a response is not yet interpretable, mark `Delayed Interpretation` rather
than assuming recovery or failure.
**Step output:** `delayed_response_observations` and open observation windows.

## Step 5. Establish the Recent Trend

Compare the current Actual Exposure and response with recent sufficiently
comparable exposures and observations.
Check comparability in:
- intended and Actual Exposure;
- dose and achieved quality;
- measurement protocol;
- environmental conditions;
- athlete state at entry;
- competition context;
- and response time scale.
Possible descriptive patterns include:
- stable performance with stable cost;
- improving performance with similar cost;
- stable performance with lower cost;
- declining performance with rising cost;
- persistent tissue irritation;
- repeated failure to achieve intended stimulus;
- inconsistent response without a stable direction;
- and insufficient comparable evidence.
An isolated observation may trigger review, reduce confidence, or support a
bounded local action.
It does not usually establish a stable trend.
Repeated observations are stronger only when they are relevant, sufficiently
comparable, and not repetitions of the same measurement error.
High-consequence warnings do not require repeated harmful exposure before
conservative action.
**Step output:** `recent_trend` with comparability and confidence.

## Step 6. Compare Expected and Observed Response

Retrieve the Expected Response attached to the original planning decision.
Compare:
Expected Response given the Actual Exposure and Context
with
Observed Response under that Exposure and Context.
Do not compare the observed result only with the written prescription when
execution or exposure diverged.
Classify the relationship as:
- Broadly Consistent;
- Partially Consistent;
- Meaningfully Divergent;
- or Insufficient Information.
Evaluate both benefit and cost dimensions.
Relevant comparisons may include:
- intended stimulus versus Achieved Quality;
- expected immediate output versus observed output;
- expected recovery cost versus delayed response;
- expected adaptation direction versus recent trend;
- expected transfer versus sprint expression;
- and expected competition readiness versus competition expression.
Agreement strengthens the hypothesis only in proportion to exposure fidelity,
observation quality, comparability, and exclusion of competing explanations.
Persistent divergence may challenge dose, exposure, recovery, transfer,
bottleneck, intervention, stress-organization, or performance assumptions.
It does not automatically prove method failure.
**Step output:** `expected_vs_observed_response`.

## Step 7. Generate Candidate Interpretations

Convert the contextualized observation set into one or more plausible
explanations.
For each Candidate Interpretation, record:
- the observations being explained;
- the proposed state or relationship;
- Actual Exposure and temporal context;
- supporting evidence;
- conflicting evidence;
- important alternatives;
- scope of the claim;
- confidence;
- and unresolved information.
Possible explanations for an unfavorable performance observation may include:
- inadequate exposure quality;
- acute or residual fatigue;
- measurement noise or protocol change;
- local tissue limitation;
- technical instability;
- environmental difference;
- excessive or insufficient dose;
- recovery mismatch;
- delayed adaptation or expression;
- transfer failure;
- or an incorrect bottleneck or intervention hypothesis.
Do not use a generic label such as `CNS fatigue` as if it were a direct
observation or complete explanation.
Retain multiple interpretations when the available evidence does not
distinguish them.
The Workflow may identify a leading interpretation while preserving plausible
alternatives.
**Step output:** `candidate_interpretations`.

## Step 8. Classify Possible Failure Mode

Use the failure classes defined by the
[Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md):
- Prescription Failure;
- Execution Failure;
- Exposure Failure;
- Measurement Failure;
- Recovery Failure;
- Constraint Change;
- Transfer Failure;
- and Model / Hypothesis Failure.
For each supported or plausible class, record:
- the failed or challenged relationship;
- the observations supporting the classification;
- competing failure classes;
- the scope affected;
- confidence;
- and remaining uncertainty.
Several classes may coexist.
For example, an unclear prescription can contribute to execution divergence,
and poor exposure fidelity can prevent a valid test of the intervention
hypothesis.
An unfavorable outcome must not be classified automatically as Model /
Hypothesis Failure.
If available evidence cannot distinguish the relevant classes, output
`Unresolved Failure Classification`.
**Step output:** `failure_classification`.

## Step 9. Update Athlete State

Update only the decision-relevant Athlete-State dimensions affected by the new
evidence.
Possible dimensions include:
- current performance state;
- current Performance Problem;
- fatigue and recovery estimate;
- tissue state;
- technical stability;
- exposure tolerance;
- Candidate Bottleneck confidence;
- adaptation trend;
- transfer status;
- competition readiness or expression state;
- active constraints;
- and uncertainty.
For each updated dimension, preserve:
- prior estimate;
- new evidence;
- observation quality;
- contextual relevance;
- supporting and conflicting evidence;
- updated estimate;
- confidence;
- and decision consequence.
The update must be proportional to evidence quality, relevance, recency,
comparability, repeated trend, and consequence of error.
One low-quality observation must not mechanically erase stable prior evidence.
New high-quality or high-consequence information may justify a larger update.
Athlete State is partially observable.
Do not compress the update into one readiness score or present it as complete
biological truth.
**Step output:** `updated_athlete_state`.

## Step 10. Update Confidence

Update confidence for each material claim separately.
Claims may concern:
- exposure fidelity;
- response pattern;
- fatigue or recovery interpretation;
- tissue tolerance;
- Candidate Bottleneck;
- intervention value;
- dose-response relationship;
- transfer;
- competition expression;
- or planning constraint.
Use qualitative confidence states:
- Strongly Supported;
- Moderately Supported;
- Provisional;
- Weakly Supported;
- Unresolved;
- or Cannot Determine.
For each change, state whether the claim was:
- strengthened;
- weakened;
- narrowed;
- unchanged;
- replaced by a better-supported claim;
- or left unresolved.
Do not assign numerical probabilities without a defensible quantitative basis.
Confidence must reflect source quality, exposure fidelity, repeated trend,
cross-signal consistency, applicability, and consequence of error.
**Step output:** `confidence_update`.

## Step 11. Select Decision State

Apply the [Progression Rules](../rules/progression.md) and
[Stage Transition Rules](../rules/stage_transition.md).
Select one decision state for each affected planning object:
- Maintain;
- Progress;
- Reduce;
- Modify;
- Temporarily Withdraw;
- or Transition.
Do not recreate the operational criteria for these states in this Workflow.
The selected state must identify:
- target object;
- updated-state basis;
- supporting and conflicting evidence;
- confidence;
- prescription relationship affected;
- reversibility;
- and unresolved uncertainty.
Maintain is a valid active decision when current evidence does not justify
change.
Progress does not automatically mean more volume.
Modify may preserve the target while changing task, dose, execution condition,
or organization.
Temporarily Withdraw does not declare permanent irrelevance.
Transition concerns a broader phase or priority change and requires the
appropriate Rule basis.
**Step output:** `decision_state` and decision rationale.

## Step 12. Select Decision Scope

Select the lowest planning level whose assumptions or prescription require
maintenance or revision:
- Task;
- Session;
- Week / Microcycle;
- Mesocycle;
- or Cycle / Strategy.
Apply:
> Update the smallest planning level justified by the evidence.
Use Session scope when task, dose, order, or execution conditions can be
corrected without changing Weekly Intent.
Use Week scope when evidence affects several Sessions, required exposure
placement, or their recovery relationship.
Use Mesocycle scope when repeated evidence challenges the adaptation problem,
Candidate Bottleneck, priority, intervention direction, dose direction, or
transfer hypothesis.
Use Cycle / Strategy scope when evidence challenges the terminal objective,
competition structure, major feasible space, or strategic state trajectory.
When escalating, state:
- the higher-level assumption challenged;
- the evidence and persistence supporting escalation;
- why local correction is insufficient;
- the consequence of delay or error;
- and confidence.
Important safety, tissue, medical, or other high-consequence constraint signals
may justify immediate conservative action or broader review without waiting for
a repeated trend.
This does not grant authority to diagnose or override external restrictions.
**Step output:** `decision_scope` and `escalation_rationale`.

## Step 13. Define the Next Planning Action

Translate Decision State and Decision Scope into a handoff.
Do not generate the full revised plan inside this Workflow.
Use the following routing relationship:

| Decision scope | Next planning action | Workflow handoff |
|---|---|---|
| Task or Session | Maintain or revise the next executable prescription | [Create Session Workflow](./create_session.md) |
| Week / Microcycle | Reorganize required exposures, dose direction, or recovery relationships | [Create Week Workflow](./create_week.md) |
| Mesocycle | Revise the adaptation problem, priority, intervention direction, or exit decision | [Create Mesocycle Workflow](./create_mesocycle.md) |
| Cycle / Strategy | Revise the strategic trajectory, competition structure, or major constraints | [Create Cycle Workflow](./create_cycle.md) |
The handoff packet must contain:
- Review Object;
- updated Athlete State;
- Decision State;
- Decision Scope;
- challenged assumption;
- planning object to maintain or revise;
- constraints;
- supporting and conflicting evidence;
- confidence;
- unresolved uncertainty;
- and next observation needs.
When the action remains local, preserve higher-level intent.
When higher-level intent is challenged, make the review request explicit rather
than silently changing it in a lower-level Workflow.
**Step output:** `next_planning_action` and `workflow_handoff`.

## Step 14. Record Unresolved Questions

Preserve questions that materially limit interpretation or the next decision.
Relevant questions may include:
- Was the Actual Exposure sufficient for the intended stimulus?
- Was dose too small, excessive, or simply different from plan?
- Was recovery cost underestimated?
- Did context or measurement explain the observed change?
- Is the Candidate Bottleneck incorrect or only weakly identified?
- Has transfer failed, been delayed, or been masked by fatigue?
- Is the observed pattern ordinary variation?
- Is the intervention losing marginal value?
- Has a new constraint changed the feasible plan?
For each question, record:
- why it matters;
- which interpretations remain plausible;
- which decision it could change;
- consequence of remaining wrong;
- and whether action can proceed under uncertainty.
Do not force closure merely to produce a single explanation.
**Step output:** `unresolved_questions`.

## Step 15. Define Next Observation Needs

Identify the minimum additional information likely to improve the next
meaningful decision.
For each proposed observation, state:
- the unresolved question addressed;
- the construct or event observed;
- source and context required;
- comparison needed;
- when the observation becomes relevant;
- how it could change interpretation, confidence, state, action, or risk;
- and the cost of obtaining it.
Do not add monitoring merely because a variable can be measured.
Information has low monitoring value when it cannot change:
- interpretation;
- confidence;
- Athlete-State Estimate;
- planning action;
- or risk handling.
Repeated collection of a signal that cannot distinguish competing explanations
does not necessarily reduce uncertainty.
If no additional observation is worth its cost, record that the current
decision will proceed with explicit residual uncertainty.
**Step output:** `next_observation_needs`.

## Competition Review Application

Competition uses the same fifteen-step workflow.
The Review Object and evidence scope change; the feedback architecture does
not.
Competition Review must reconcile:
- intended race role and preparation assumptions;
- actual warm-up, race, rounds, environment, and execution;
- official or standardized performance outcome;
- race and segment information where valid;
- technical and contextual observations;
- fatigue, freshness, tissue, and recovery response;
- and the competition's effect on subsequent exposure organization.
It should update, where supported:
- competition-expression state;
- Candidate Bottleneck confidence;
- fatigue and freshness interpretation;
- transfer assessment;
- current priority;
- and competition integration.
Competition result is evidence about outcome and expression.
It is not a complete judgment of plan quality, every underlying capacity, or
the entire training model.
Keep Ex Ante Decision Quality distinct from Ex Post Outcome.
A favorable result may coexist with weak original reasoning.
An unfavorable result may coexist with a reasonable decision under the
information available at the time.
Use the outcome to update future beliefs without rewriting what was previously
knowable.

## Safety, Tissue, and Medical Boundary

When a credible high-consequence safety or tissue signal appears:
- preserve the observation and context;
- stop assuming the planned exposure remains feasible;
- apply [Constraint Handling Rules](../rules/constraint_handling.md);
- select a conservative local or broader planning action within authority;
- and request external professional assessment when appropriate.
The Workflow may flag, Modify, Reduce, or Temporarily Withdraw training
exposure.
It must not:
- diagnose pathology;
- issue medical clearance;
- prescribe medical treatment;
- or override a defined medical or rehabilitation restriction.
External professional conclusions enter the next planning decision as
constraints within their stated scope.

## Review Output

The completed review must return the following structured result.

### Review Object

- object type;
- review window and evidence cutoff;
- higher-level intent;
- current priority;
- and decision required.

### Planned vs Actual Exposure

- prescribed task and Planned Exposure;
- Intended Stimulus;
- Actual Exposure;
- Achieved Quality;
- meaningful deviations and context;
- and exposure-agreement status.

### Immediate Response

- relevant immediate observations;
- source, protocol, context, and reference;
- observation-quality limits;
- and warning flags.

### Delayed Response

- relevant delayed observations;
- open or completed observation windows;
- context and comparability;
- and delayed-interpretation status.

### Recent Trend

- comparable exposures and responses;
- descriptive pattern;
- comparability limits;
- and trend confidence.

### Expected vs Observed Response

- Expected Response conditional on Actual Exposure;
- Observed Response;
- consistency classification;
- benefit and cost comparison;
- and assumptions challenged.

### Candidate Interpretations

- leading interpretation when supported;
- plausible alternatives;
- supporting and conflicting evidence;
- claim scope;
- and uncertainty.

### Failure Classification

- supported or plausible failure classes;
- failed relationship;
- competing classes;
- confidence;
- or `Unresolved Failure Classification`.

### Updated Athlete State

- prior state dimensions;
- evidence-weighted updates;
- unchanged relevant dimensions where useful;
- active constraints;
- and state uncertainty.

### Confidence Update

- claims strengthened, weakened, narrowed, unchanged, replaced, or unresolved;
- qualitative confidence state;
- and evidence limitation.

### Decision State

- Maintain, Progress, Reduce, Modify, Temporarily Withdraw, or Transition;
- target object;
- Rule reference;
- and rationale.

### Decision Scope

- Task, Session, Week / Microcycle, Mesocycle, or Cycle / Strategy;
- smallest-justified-level rationale;
- and any higher-level assumption challenged.

### Next Planning Action

- planning object to maintain or revise;
- selected create_* Workflow;
- handoff packet;
- and preservation or review of higher-level intent.

### Unresolved Questions

- open decision-relevant questions;
- plausible alternatives;
- consequence;
- and residual uncertainty.

### Next Observation Needs

- minimum information capable of changing the next decision;
- source and context;
- expected decision value;
- collection cost;
- and observation window.
The Review Output is a decision handoff.
It is not a comprehensive daily log or the revised plan itself.

## Feedback-to-Planning Interface

The closed loop is:
Create
→ Execute
→ Review Actual Exposure and Response
→ Update Athlete State
→ Select Decision State and Scope
→ Return to the appropriate create_* Workflow
→ Execute again.
The feedback packet must retain enough information for the receiving Workflow
to understand:
- what happened;
- what changed;
- why the update is justified;
- what remains uncertain;
- what action is requested;
- and what higher-level intent must remain stable or be reviewed.
The receiving Workflow owns revised planning at its level.
This Workflow owns the execution-to-decision handoff.

## Review Completion Gate

The review is complete when:
- the Review Object and evidence scope are explicit;
- Actual Exposure has been reconstructed before response attribution;
- observation is separated from interpretation;
- immediate, delayed, repeated-trend, and longer-term evidence are included only
  where relevant;
- Expected and Observed Response are compared under Actual Exposure and context;
- multiple Candidate Interpretations remain possible when evidence requires;
- failure classes are distinguished or left unresolved;
- Athlete State is updated proportionally to evidence;
- qualitative confidence and uncertainty remain claim-specific;
- Decision State calls existing Rules;
- Decision Scope uses the smallest justified planning level;
- high-consequence warnings can trigger conservative action without medical
  diagnosis;
- the next action is handed to the correct create_* Workflow;
- unresolved questions and minimum next observation needs are preserved;
- and the output remains an Execution Feedback Review rather than a plan audit,
  monitoring encyclopaedia, or planning generator.
If the available evidence cannot support a complete review, return `Partial
Review` or `Cannot Yet Determine` with the narrowest supportable conclusion and
the information needed next.
