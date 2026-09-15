# Feedback-Decision Core Model
Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose
This document defines how the 100m Performance Planning system represents feedback after training or competition actually occurs.
It specifies the relationships among:

- planned intervention,
- prescription,
- intended and actual exposure,
- achieved quality,
- observation,
- response across time,
- interpretation,
- athlete-state estimation,
- evidence weighting and confidence,
- decision states,
- decision scope and escalation,
- revised prescription,
- and the next planning cycle.

This document answers:

> After training actually occurs, what happened, what was observed, what can reasonably be inferred, how should the decision-relevant athlete-state estimate change, and how does that information enter the next planning decision?

It defines feedback, state update, and decision objects.
It does not provide:

- a monitoring-test catalogue,
- a readiness checklist or score,
- universal change thresholds,
- progression or transition criteria,
- a fixed decision tree,
- a training diary template,
- a medical diagnosis system,
- or an ordered audit procedure.

The governing boundary is:

Model ≠ Rule ≠ Workflow.

---
## 1. Definition of the Feedback Loop
The Feedback Loop is the evidence-guided process by which actual events and observations revise the planning system's current beliefs and future prescriptions.
Its core relationship is:

Plan
→ Prescription
→ Actual Exposure
→ Observed Response
→ Interpretation
→ Updated Athlete State
→ Decision
→ Revised Prescription
→ New Actual Exposure.

The loop returns new information to the Plan.
It does not replace strategic direction with random daily adjustment.

### 1.1 Forward and Corrective Information
The system contains two linked information directions.
Top-down direction provides:

Objective
→ Performance Problem
→ Intervention Hypothesis
→ Prescription
→ Expected Exposure and Response.

Bottom-up correction provides:

Actual Exposure
→ Observation
→ Interpretation
→ Updated Athlete State
→ Revised Decision.

Top-down direction constrains what the plan is trying to accomplish.
Bottom-up correction constrains what the system can continue to believe after contact with reality.
Neither direction is sufficient alone.

### 1.2 Core Feedback Objects
| Object | Definition | Boundary |
|---|---|---|
| Planned Intervention | Prospective intervention hypothesis selected within the Plan | Does not establish execution |
| Prescription | Executable instruction for a task or session | Records intent, not outcome |
| Intended Exposure | External exposure expected from correct execution | Prospective representation |
| Actual Exposure | Work and conditions actually encountered | Supplied through the Stimulus-Dose-Cost interface |
| Achieved Quality | Extent to which actual execution retained properties required by the intended stimulus | Task-specific, not equivalent to effort |
| Observation | Time-stamped descriptive information obtained from a source | Does not contain its causal explanation |
| Measurement | Observation produced by a defined measurement procedure | One observation source among several |
| Observed Response | Observed change or state following exposure | Does not uniquely identify cause |
| Expected Response | Prospective range or pattern considered compatible with the intervention hypothesis | Comparison reference, not guaranteed outcome |
| Candidate Interpretation | One plausible explanation connecting observations to latent state | May compete with alternatives |
| Athlete-State Estimate | Current decision-relevant representation of the athlete under uncertainty | Partial estimate, not complete biological truth |
| Confidence | Qualitative support assigned to a specific claim | Claim-specific, not a global certainty score |
| Decision State | Semantic class describing how the current plan may relate to new information | Operational criteria belong to Rules |
| Decision Scope | Lowest planning level whose assumptions or prescription require reconsideration | Distinct from decision state |
| Revised Prescription | New or retained executable instruction produced after decision | Re-enters the exposure loop |

### 1.3 Feedback Is Not Automatic Correction
Feedback does not guarantee a correct interpretation.
Every transition can contain:

- missing information,
- measurement error,
- normal variation,
- contextual change,
- competing explanations,
- delayed response,
- and model error.

The feedback loop must therefore preserve both the current interpretation and the uncertainty attached to it.

### 1.4 Feedback Record
A feedback event should be representable through:

- `decision_context`,
- `planned_intervention`,
- `prescription`,
- `intended_exposure`,
- `actual_exposure`,
- `achieved_quality`,
- `observations`,
- `observation_context`,
- `expected_response`,
- `observed_response`,
- `candidate_interpretations`,
- `prior_state_estimate`,
- `updated_state_estimate`,
- `confidence`,
- `decision_state`,
- `decision_scope`,
- `revised_prescription`,
- and `unresolved_uncertainty`.

This schema defines the information relationship.
It does not prescribe an execution sequence or form layout.

---
## 2. Planned Exposure and Actual Exposure
[Stimulus-Dose-Cost Core Model](./03_stimulus_dose_cost_model.md) defines intervention, dose, intended stimulus, planned exposure, actual exposure, achieved quality, cost, and risk.
04 consumes those objects after execution and connects them to observation, response, state update, and decision.

### 2.1 Prescription
A Prescription is the planned instruction presented for execution.
It may specify a task, dose, quality, context, and intended stimulus.
Its existence proves only that an instruction was recorded.
It does not establish that the task was completed, the target quality was reached, or the intended stimulus occurred.

### 2.2 Intended Exposure
Intended Exposure is the external exposure expected if the prescription is executed under its assumed conditions.
It provides the prospective reference against which actual exposure can be described.
It is distinct from expected internal response and expected adaptation.

### 2.3 Actual Exposure
Actual Exposure is the external work and conditions that actually occurred.
It includes material deviations from prescription, such as:

- work completed or omitted,
- achieved velocity, load, duration, or range,
- actual rest and density,
- substitutions or added tasks,
- competition or testing exposure,
- environmental conditions,
- and symptoms or constraints that altered execution.

Subsequent interpretation must begin from actual exposure rather than the original task label.

Prescription ≠ Actual Exposure.

### 2.4 Achieved Quality
Achieved Quality describes whether actual execution retained the properties needed for the intended exposure and stimulus.
Quality can affect whether:

- the intended stimulus plausibly occurred,
- the exposure changed identity,
- the expected response remains relevant,
- and the intervention can be evaluated as implemented.

A prescribed high-velocity session does not establish meaningful high-velocity exposure when the required velocity or task organization was not achieved.

### 2.5 Exposure Reconciliation
Exposure Reconciliation is the descriptive relation between what was intended and what occurred.
It may show:

- matched exposure,
- partial exposure,
- substituted exposure,
- additional exposure,
- altered quality,
- or indeterminate exposure.

These are descriptive states.
Rules or workflows may define how they are assigned operationally.

---
## 3. Observation Model
An Observation is a time-stamped descriptive statement about an event, output, condition, experience, or change.
An observation should remain separable from the explanation assigned to it.
For example:

`The standardized 30m time was slower than the current reference.`
is an observation.
`The athlete is neurally fatigued.`
is an interpretation.

Observation ≠ Interpretation.

### 3.1 Observation
An observation can concern:

- actual exposure,
- achieved quality,
- task output,
- competition performance,
- local tissue report,
- subjective state,
- technical organization,
- environmental or lifestyle context,
- or a constraint change.

The observation describes what the source supports.
It must not silently expand into a broader construct claim.

### 3.2 Measurement
A Measurement is an observation produced through a defined instrument, protocol, scale, or coding procedure.
Measurement is one observation source.
Other sources can include direct athlete report, coach observation, training log, competition record, or documented contextual change.
Non-instrumented observations can be decision-relevant while retaining limits in precision, reliability, and interpretation.

### 3.3 Context
Observation context describes conditions that can alter the value or meaning of an observation.
Relevant context may include:

- actual exposure preceding the observation,
- athlete baseline and recent trend,
- measurement protocol,
- device and operator,
- timing of collection,
- environmental conditions,
- current performance problem,
- current fatigue and tissue state,
- sleep, travel, or lifestyle disruption,
- competition proximity,
- and expected response.

The same numerical change can support different interpretations under different contexts.

### 3.4 Observation Quality
Observation Quality is the degree to which an observation can support the current inference.
Relevant dimensions include:

- reliability,
- validity for the claimed construct,
- sensitivity to the expected change,
- protocol consistency,
- source credibility,
- completeness,
- comparability with the reference,
- relevance to the current decision,
- and uncertainty.

Observation quality is multidimensional.
It should not be reduced to a universal score when different weaknesses have different consequences.

### 3.5 Observation Representation
An observation should be representable through:

- `source`,
- `timestamp_or_window`,
- `observed_object`,
- `value_or_description`,
- `protocol`,
- `reference`,
- `context`,
- `quality_limits`,
- `decision_relevance`,
- and `uncertainty`.

This representation is method-agnostic.
It can accept future monitoring technologies without changing the core model.

### 3.6 Observation Boundaries
Observed Data ≠ Athlete State.

Observed Data informs an Athlete-State Estimate.
A measured change can be real while its meaning remains unresolved.
A stable measurement can also fail to detect a relevant change when the measure is insensitive or poorly matched to the current problem.

---
## 4. Response Model
A Response is a change or state observed after an exposure and considered potentially related to it.
Temporal order is necessary for an exposure-response claim, but it is not sufficient to establish causality.
Response must be represented across relevant time scales.

### 4.1 Immediate Response
Immediate Response occurs during or close to the exposure.
It may describe:

- achieved output,
- change across repetitions,
- technical stability,
- perceived effort,
- local symptoms,
- task completion,
- or acute cost.

Immediate response can clarify what exposure occurred.
It does not by itself establish recovery demand or persistent adaptation.

### 4.2 Short-Delay Response
Short-Delay Response is observed after the immediate task but before longer recovery or adaptation can be assumed.
It may inform:

- early fatigue,
- local tissue response,
- emerging soreness or discomfort,
- sleep or daily function,
- and the conditions entering the next relevant task.

The category is relational to the exposure and next decision.
It has no universal hour boundary.

### 4.3 Delayed Response
Delayed Response is an observation that emerges or persists after the initial response period.
It may concern recovery cost, performance suppression, tissue response, restored task capability, or continuing disruption.
Different response dimensions can follow different time courses.
The passage of 24, 48, or 72 hours does not by itself establish recovery.
These times can be observation opportunities, not universal biological deadlines.

### 4.4 Repeated Trend
A Repeated Trend is a pattern supported across multiple sufficiently comparable observations or exposures.
It may include:

- stable output with stable cost,
- improving output with similar cost,
- stable output with declining cost,
- declining output with increasing cost,
- repeated failure to achieve intended exposure,
- or recurring tissue or technical disruption.

Repeated evidence usually supports stronger inference than an isolated observation.
The required amount of repetition depends on observation quality, decision consequence, and the plausibility of alternatives.

### 4.5 Longer-Term Adaptation Signal
A Longer-Term Adaptation Signal is a pattern considered compatible with persistent change rather than temporary response or random fluctuation.
It should remain linked to:

- actual exposure history,
- comparable observation conditions,
- expected time course,
- target relevance,
- competing explanations,
- and transfer evidence.

It is evidence about adaptation, not adaptation made directly observable.

### 4.6 Response Profile
A response profile should be representable through:

- `exposure_reference`,
- `response_dimension`,
- `observation_time_or_window`,
- `direction_and_magnitude`,
- `comparison_reference`,
- `expected_range_or_pattern`,
- `context`,
- `persistence`,
- `cross-observation_consistency`,
- and `uncertainty`.

No single response time point represents the whole profile.

---
## 5. Observation and Interpretation
Interpretation is an evidence-constrained explanatory claim about what observations imply for exposure, response, athlete state, adaptation, transfer, cost, risk, or the current model.
Observation and interpretation occupy different logical layers.
The relationship is:

Observation Set
→ Candidate Explanations
→ Evidence-Weighted Interpretation.

This relation is abductive and may remain unresolved.

### 5.1 Candidate Explanations
A Candidate Explanation is one plausible account of the observations under the current context.
The same observation can be compatible with:

- real capability change,
- temporary fatigue,
- altered technical organization,
- changed tissue state,
- measurement error,
- environmental change,
- execution difference,
- or random variation.

The existence of several candidates does not require them to be equally plausible.

### 5.2 Interpretation Claim
An interpretation claim should identify:

- the observations being explained,
- the latent state or relationship proposed,
- the exposure and temporal context,
- the mechanism or rationale,
- supporting evidence,
- conflicting evidence,
- important alternatives,
- confidence,
- and unresolved information.

Interpretation must not claim more than the observations and evidence can support.

### 5.3 Multiple Competing Interpretations
Multiple interpretations may remain active when available observations do not distinguish among them.
The system can represent:

- a leading interpretation,
- plausible alternatives,
- interpretations weakened by evidence,
- and an unresolved set.

Forced selection is not required.

### 5.4 Causal Attribution
Temporal association and response consistency can strengthen a causal claim.
They do not eliminate confounding, concurrent exposures, regression to normal variation, measurement change, or model error.
Causal confidence should increase only to the degree that relevant alternatives are reduced.

### 5.5 Interpretation Boundary
04 represents candidate interpretations and their confidence.
It does not define a universal diagnostic algorithm.
Operational tests for accepting, rejecting, or acting on an interpretation belong to Rules and Workflows.

---
## 6. Athlete State
Athlete State is the current decision-relevant representation of the athlete under uncertainty.
It is maintained to support planning decisions.
It is not a complete copy of the athlete's biological, psychological, technical, or social reality.

### 6.1 Athlete State as a Decision-Relevant Estimate
An Athlete-State Estimate contains only distinctions that can materially inform the current or foreseeable planning decisions.
Its content depends on:

- the terminal objective,
- current performance problem,
- active intervention hypotheses,
- competition timeline,
- constraints,
- and the cost of being wrong.

More state dimensions do not automatically improve the estimate.

### 6.2 Partially Observable State
Athlete State is latent and only partially observable.
No measurement, observation, or readiness score directly reveals the full state.
The model therefore uses:

Observed Data
→ Evidence about State Dimensions
→ Athlete-State Estimate.

The estimate can be incomplete, internally contested, or uncertain.

### 6.3 State Dimensions
A compact athlete-state representation may include:

- current performance state,
- current performance problem,
- candidate or provisional bottleneck,
- current fatigue and recovery state,
- tissue state,
- technical stability,
- adaptation trend,
- exposure tolerance,
- competition-expression state,
- active constraints,
- and unresolved uncertainty.

These dimensions must not be forced into one total readiness score.
Each dimension can have its own evidence, time course, and confidence.

### 6.4 State Estimate Representation
A state estimate should be representable through:

- `state_dimension`,
- `current_claim`,
- `time_scope`,
- `supporting_observations`,
- `conflicting_observations`,
- `candidate_explanations`,
- `prior_estimate`,
- `confidence`,
- `decision_relevance`,
- and `unresolved_information`.

State belongs to a time and decision context.
It should not be presented as a permanent athlete trait without appropriate evidence.

### 6.5 State Update
A State Update is a change to the current estimate caused by decision-relevant new evidence.
The conceptual relation is:

Prior State Estimate
× New Observation Set
× Observation Quality
× Context
× Existing Evidence
× Consequence of Error
→ Updated State Estimate and Confidence.

The multiplication signs indicate interaction, not a calculable formula.
New evidence can:

- support the prior estimate,
- weaken it,
- refine its scope,
- replace it with a better-supported estimate,
- increase uncertainty,
- or leave it materially unchanged.

State update does not require every new observation to change the state estimate.

### 6.6 State Continuity
The prior estimate remains relevant because athlete state has continuity across time.
New information should not mechanically erase stable evidence.
The weight of prior information depends on its relevance, recency, stability, and compatibility with the current context.
Persistent reliance on outdated information is also invalid when athlete state or constraints have materially changed.

### 6.7 State and Medical Boundaries
Tissue and exposure-tolerance information can modify the planning state.
The Athlete-State Estimate does not independently diagnose injury, determine pathology, or issue medical clearance.
External medical or rehabilitation decisions enter the model as authoritative constraints within their defined scope.

---
## 7. Expected vs Observed Response
Expected Response is the prospective pattern considered compatible with the intervention hypothesis after a defined actual exposure and time context.
Observed Response is the evidence obtained after exposure.
The valid comparison is:

Expected Response given Actual Exposure and Context
versus
Observed Response under the same Exposure and Context.
Comparing observed response only with the written prescription can misclassify an execution or exposure problem as an adaptation failure.

### 7.1 Expected Response Object
An expected-response object should identify:

- the intervention hypothesis,
- the exposure assumed,
- the response dimensions expected,
- the direction or acceptable pattern,
- the relevant time scale,
- expected cost,
- uncertainty,
- and observations capable of informing the claim.

An expected response is not a promised outcome or a fixed threshold.

### 7.2 Agreement
Agreement between expected and observed response can support the current hypothesis when:

- actual exposure matched the assumption,
- observations were sufficiently valid and comparable,
- the time scale was appropriate,
- and important competing explanations remain limited.

Agreement raises support only in proportion to the evidence quality.

### 7.3 Deviation
Deviation can challenge one or more assumptions concerning:

- prescription,
- execution,
- actual exposure,
- dose-response,
- recovery cost,
- tissue tolerance,
- adaptation time,
- transfer,
- the performance model,
- or the intervention hypothesis.

Deviation does not identify which assumption failed.

### 7.4 Patterned Deviation
A repeated pattern such as declining performance with increasing cost usually challenges the active hypothesis more strongly than one isolated unfavorable observation.
Likewise, stable performance with decreasing cost may support improved tolerance without proving improvement in terminal performance.
The model preserves both outcome and cost dimensions.

### 7.5 Unexpected Positive Response
An unexpectedly favorable response can update beliefs while retaining uncertainty about cause.
It must not automatically validate every element of the plan or every proposed mechanism.
Positive surprise and negative surprise are both information.

---
## 8. Evidence Weighting and Confidence
Evidence Weighting is the qualitative assignment of influence to observations and prior information when forming an interpretation or state update.
It is claim-specific and context-dependent.
It is not a universal readiness algorithm.

### 8.1 Evidence-Weighting Dimensions
Relevant dimensions include:

- reliability,
- validity for the current claim,
- relevance to the decision,
- recency,
- repeated trend,
- measurement and protocol quality,
- comparability of context,
- fidelity of actual exposure,
- consistency with other evidence,
- athlete-specific history,
- evidence-source applicability,
- and consequence of error.

No dimension independently determines weight in every decision.

### 8.2 Recency and Persistence
Recent evidence may better represent a rapidly changing state such as acute fatigue.
Longer-term repeated evidence may better represent persistent capacity or adaptation.
Recency does not automatically outweigh stable history, and history does not automatically outweigh a material current change.
The relevant time scale belongs to the state dimension being estimated.

### 8.3 Cross-Signal Consistency
Agreement among sufficiently independent and relevant observations can strengthen an interpretation.
Apparent agreement among several measures of the same underlying source or error does not provide equivalent independent support.
Conflicting evidence should remain disaggregated until the conflict can be interpreted.

### 8.4 Asymmetric Consequences
Evidence requirements can depend on the consequence of being wrong.
A noisy, low-consequence performance fluctuation may justify stability while more evidence accumulates.
A credible high-consequence tissue or safety signal may justify a conservative action before repeated exposure is available.
This asymmetry does not make the warning signal a complete diagnosis.

### 8.5 Confidence States
Confidence is attached to a defined interpretation, state estimate, or decision rationale.
Permitted qualitative states include:

| Confidence state | Meaning |
|---|---|
| Strong Support | Converging, relevant, sufficiently reliable evidence supports the claim and material alternatives are limited |
| Moderate Support | Relevant evidence supports the claim while meaningful limitations or alternatives remain |
| Provisional | The claim is currently useful but depends on limited or indirect evidence |
| Weak Support | Some evidence is compatible with the claim but does not distinguish it well from alternatives |
| Unresolved | Material competing interpretations remain without a justified leader |
| Cannot Determine Yet | Available information is insufficient for the required distinction or decision |

These states do not imply numerical probabilities.
Confidence may differ across state dimensions within the same athlete.

### 8.6 Evidence-Proportional Update
State change and decision scope should be proportional to the quality, relevance, and consequence of the new evidence.
A single low-quality observation should not overturn a stable long-term estimate without a reason tied to consequence or context.
Repeated high-quality deviation can justify broader revision when it challenges a higher-level assumption.

---
## 9. Signal, Noise, and Stability
Signal is variation that provides decision-relevant information about exposure, response, athlete state, constraint, or model validity.
Noise is variation that does not support the proposed change in interpretation at the required confidence.
Normal Variation is expected within-athlete fluctuation under sufficiently comparable conditions.
Meaningful Deviation is a difference large, consistent, relevant, or consequential enough to alter interpretation, confidence, or decision scope.
These categories are conditional on the measurement, athlete, context, and decision.

### 9.1 Measurement Noise
Measurement noise can arise from instruments, protocol, operator, processing, timing, environment, or reporting inconsistency.
High reliability at group level does not guarantee sensitivity to a small change in one athlete.
More measurements do not solve noise when the protocol remains inconsistent.

### 9.2 Contextual and Biological Variation
Day-to-day variation may arise from ordinary biological fluctuation, competition context, sleep, life stress, environmental change, or differences in recent exposure.
Variation can be real without representing a stable change in capacity or adaptation.

### 9.3 Isolated Observation and Trend
Single Observation ≠ Stable Trend.

An isolated observation can:

- trigger review,
- reduce confidence,
- identify missing context,
- or justify a bounded local action.

It does not usually establish a persistent state change by itself.
Repeated observations are stronger only when they are sufficiently comparable, relevant, and not repetitions of the same error.

### 9.4 Stability as Decision Capability
Adaptive decision quality includes:

- changing the plan when meaningful information appears,
- and preserving the plan when available variation does not justify change.

Failure to change can make a plan rigid.
Unjustified repeated change can make it unstable.
Frequent modification can reduce:

- interpretability,
- exposure consistency,
- learning,
- adaptation opportunity,
- and confidence in causal inference.

### 9.5 Meaningful Change Boundary
The boundary between noise and meaningful deviation cannot be universal across observations.
It depends on:

- measurement error,
- normal variation,
- effect relevance,
- decision consequence,
- reversibility,
- and the cost of waiting.

Operational thresholds belong to Rules or measurement-specific domain knowledge.

---
## 10. Decision States
A Decision State is the semantic relationship between the updated interpretation and the next plan or prescription.
Decision states define what kind of change is under consideration.
They do not define the operational criteria that select that state.
[Progression Rules](../rules/progression.md) and [Stage Transition Rules](../rules/stage_transition.md) implement those criteria.

### 10.1 Maintain
Maintain preserves the current intervention, dose direction, or planning emphasis because no justified change has been adopted.
Maintain is an active decision state.
It can express continued support for the current hypothesis or stability while uncertainty is resolved.

### 10.2 Progress
Progress increases or advances one or more relevant exposure, task, quality, specificity, or performance demands while retaining the current objective.
Progress is not synonymous with adding volume.
Its operational entry and reversal criteria belong to Progression Rules.

### 10.3 Reduce
Reduce lowers one or more exposure or cost dimensions while retaining the target or intervention role.
Reduction can change magnitude, density, frequency, complexity, supporting work, or another task-specific dimension.
The model does not specify which dimension or threshold should change.

### 10.4 Modify
Modify changes the intervention, execution conditions, organization, or method while preserving a visible target problem or intended adaptation.
Modification allows the method to change without silently changing the objective.

### 10.5 Temporarily Withdraw
Temporarily Withdraw removes an intervention or exposure from its current role while preserving the reason, status, and possibility of reintroduction.
It is distinct from declaring the target permanently irrelevant.
Reintroduction criteria belong to Rules.

### 10.6 Transition
Transition changes the current planning phase, priority, or strategic emphasis.
It operates at a broader scope than a local task adjustment when the underlying phase relationship has changed.
Its operational criteria are defined by Stage Transition Rules.

### 10.7 Decision Object
A decision should be representable through:

- `decision_state`,
- `decision_scope`,
- `target_object`,
- `updated_state_basis`,
- `supporting_and_conflicting_evidence`,
- `confidence`,
- `affected_assumption`,
- `prescription_change`,
- `expected_response`,
- `reversibility`,
- `unresolved_uncertainty`,
- and `review_interface`.

This object preserves the rationale without encoding universal decision criteria.

---
## 11. Decision Scope and Escalation
Decision Scope identifies the planning level at which new information requires maintenance or revision.
The planning hierarchy is:

Task
→ Session
→ Week / Microcycle
→ Mesocycle
→ Cycle / Strategy.

The default model principle is:

Update the smallest planning level justified by the evidence.

### 11.1 Task Scope
Task scope concerns a local prescription or execution element without necessarily changing the session objective.
A task-level issue does not by itself invalidate the week or mesocycle.

### 11.2 Session Scope
Session scope concerns the purpose, remaining exposure, or organization of the current session.
It can contain several task changes while leaving the broader weekly direction intact.

### 11.3 Week / Microcycle Scope
Week scope concerns the sequence, distribution, or feasibility of near-term exposures.
It becomes relevant when the new information affects more than one session or the recovery relationship among them.

### 11.4 Mesocycle Scope
Mesocycle scope concerns the current adaptation problem, intervention priority, dose direction, or phase assumption.
It requires evidence that the issue is broader than local execution or transient variation.

### 11.5 Cycle / Strategy Scope
Cycle or Strategy scope concerns the terminal objective, major competition structure, feasible planning space, or persistent failure of the governing model.
It is the broadest update and should not be inferred from one ordinary local fluctuation.

### 11.6 Escalation Relationship
Escalation moves the decision to a higher planning level when evidence challenges an assumption owned by that level.
Escalation depends on:

- the scope of the affected assumption,
- persistence and generality of the evidence,
- consequence of the issue,
- changed hard constraints,
- and confidence that local correction is insufficient.

Escalation need not pass mechanically through every level.
A major constraint or high-consequence event can immediately affect a broad planning scope.

### 11.7 Local Stability and Higher-Level Revision
The model must avoid two errors:

- rewriting broad strategy for a local, noisy problem,
- and repeatedly patching local prescriptions when the higher-level assumption is failing.

Decision state and decision scope must therefore be represented separately.
The same state, such as Maintain or Modify, can apply at different planning levels.
Operational escalation rules belong to Rules and Workflows.

---
## 12. Failure Classification
Failure Classification identifies where the expected relationship became unsupported.
An unfavorable outcome does not automatically establish method failure.
Several failure classes can coexist.

### 12.1 Prescription Failure
Prescription Failure occurs when the written instruction is incomplete, contradictory, infeasible, or incapable of specifying the intended exposure with sufficient clarity.
The intervention hypothesis may remain plausible even though the prescription was defective.

### 12.2 Execution Failure
Execution Failure occurs when actual performance materially differs from an interpretable and feasible prescription.
It describes the mismatch.
It does not assign blame or establish why the mismatch occurred.

### 12.3 Exposure Failure
Exposure Failure occurs when task completion does not produce the external conditions or achieved quality required for the intended stimulus.
The task can appear completed while the intended exposure remains absent or materially altered.

### 12.4 Measurement Failure
Measurement Failure occurs when the observation cannot support the required comparison or inference because of protocol, device, processing, context, missingness, or recording problems.
It can prevent evaluation without proving that performance or response failed.

### 12.5 Recovery Failure
Recovery Failure occurs when realized recovery demand or available recovery conditions do not support the expected restoration or expression of relevant capability within the required context.
It does not automatically mean that the training stimulus was ineffective.

### 12.6 Constraint Change
Constraint Change occurs when a material assumption about time, environment, tissue status, health, resources, competition, or lifestyle no longer holds.
The original intervention may have been reasonable under the prior constraint set and inappropriate under the new one.

### 12.7 Transfer Failure
Transfer Failure occurs when a supporting adaptation appears to have occurred but does not produce the expected change in sprint-relevant capability, sprint expression, segment outcome, or competitive 100m performance.
The location and timing of the failed transfer link may remain uncertain.

### 12.8 Model / Hypothesis Failure
Model or Hypothesis Failure occurs when observations materially weaken the explanatory relationship connecting performance problem, determinant, intervention, adaptation, or transfer.
This classification requires more than failure to achieve a favorable outcome once.

### 12.9 Failure Attribution Boundary
Failure attribution should preserve:

- the failed relationship,
- the observations supporting the classification,
- competing failure classes,
- confidence,
- and remaining uncertainty.

The model defines failure objects.
Rules define operational classification criteria, and Workflows define the order of audit.

---
## 13. Monitoring Value
Monitoring Value is the expected contribution of an observation source to decision quality relative to the cost and burden of obtaining and interpreting it.
Monitoring exists to support decisions.
The ability to measure a variable does not establish that it should be monitored continuously.

### 13.1 Sources of Monitoring Value
An observation can have value when it can:

- establish actual exposure,
- reduce decision-relevant uncertainty,
- distinguish among candidate interpretations,
- alter confidence,
- alter decision state or scope,
- identify a material constraint change,
- detect a high-consequence warning signal,
- or evaluate expected versus observed response.

Interesting information without a plausible decision relationship may have low monitoring value.

### 13.2 Monitoring Cost
Monitoring can consume:

- time,
- athlete attention and cooperation,
- equipment and interpretation resources,
- physical exposure,
- recovery opportunity,
- and technical focus.

A measurement can alter the state or exposure it is intended to observe.
Monitoring value therefore depends on both information gained and cost imposed.

### 13.3 Method-Agnostic Entry
Future observations from training logs, timing systems, video, athlete reports, competition results, or new measurement methods can enter the model when they preserve:

- source,
- observed construct,
- protocol,
- context,
- quality,
- relevance,
- uncertainty,
- and relationship to the current state estimate or decision.

04 does not require a fixed monitoring technology.

### 13.4 Monitoring Boundaries
04 does not define:

- which jump test to use,
- which timing system to purchase,
- how to score a questionnaire,
- which heart-rate or autonomic metric to collect,
- how to classify a movement from video,
- or how often any specific test must occur.

Those details belong to domain knowledge, evidence records, Rules, or live research.

---
## 14. Decision Quality and Outcome
Decision Quality is the quality of reasoning and choice given the information reasonably available when the decision was made.
Outcome is what occurred after the decision.
They are related but not equivalent.

Decision Quality ≠ Outcome.

### 14.1 Ex Ante Decision Quality
Ex Ante Decision Quality concerns whether the original decision:

- addressed the defined problem,
- used the available evidence appropriately,
- respected known constraints,
- represented expected benefit, cost, risk, and uncertainty,
- compared feasible alternatives at the required scope,
- and preserved a credible update path.

It must be evaluated from the information set available at that time.

### 14.2 Ex Post Outcome
Ex Post Outcome concerns actual exposure, response, adaptation, transfer, cost, and performance after implementation.
It supplies new evidence for future decisions.
It does not retroactively make unavailable information knowable.

### 14.3 Decision-Outcome Combinations
| Decision quality | Outcome | Interpretation boundary |
|---|---|---|
| Reasonable | Favorable | Supports continuation of some beliefs but does not prove every mechanism |
| Reasonable | Unfavorable | Requires updating from the outcome without declaring the original decision irrational by result alone |
| Defective | Favorable | Favorable result does not repair structural or reasoning defects |
| Defective | Unfavorable | Outcome and prior reasoning may both require revision, but their errors remain distinguishable |

### 14.4 Outcome Bias
Outcome Bias occurs when the observed result replaces evaluation of what was reasonably knowable before the decision.
Avoiding outcome bias does not protect a prior belief from revision.
It preserves the distinction between learning from outcome and rewriting the history of the decision.

### 14.5 Decision Trace
A decision trace should preserve:

- the information available at decision time,
- the state estimate and confidence,
- the chosen state and scope,
- material alternatives,
- expected exposure and response,
- known uncertainty,
- and the later observed outcome.

This supports learning without conflating reasoning quality and luck.

---
## 15. Feedback Under Uncertainty
Feedback can reduce, preserve, relocate, or increase uncertainty.
It must not manufacture certainty merely because new data exist.
[Uncertainty Handling Rules](../rules/uncertainty_handling.md) implement the operational treatment of missing, conflicting, and decision-critical information.

### 15.1 Ambiguous Response
An Ambiguous Response is compatible with multiple material explanations and does not support a unique state update.
The system can retain a provisional interpretation or leave the issue unresolved.

### 15.2 Incomplete Information
Missing information is decision-relevant only when plausible values could materially change interpretation or action.
Unknown values must not be silently treated as zero, normal, recovered, tolerated, or unchanged.
Not every unknown prevents a narrower or reversible decision.

### 15.3 Conflicting Signals
Conflicting signals are observations that support materially different state estimates or decisions.
They should not be mechanically averaged into one readiness value.
The model preserves their:

- construct specificity,
- source quality,
- context,
- time scale,
- decision relevance,
- and asymmetric consequences.

Conflict can remain unresolved when the evidence does not justify closure.

### 15.4 Delayed Interpretation
Some observations cannot be interpreted at the time they first appear because the response time course, measurement context, or competing explanation remains unresolved.
Delayed interpretation is a legitimate state.
It does not imply that all decisions must be postponed.

### 15.5 Multiple Explanations
The system can retain several candidate explanations with different support levels.
New observations should be valued partly by whether they can distinguish among those explanations.
Repeated collection of data that cannot distinguish them adds volume without necessarily adding information.

### 15.6 Cannot Determine
`Cannot Determine Yet` is a valid output when the current evidence cannot support the distinction required by the decision.
It should preserve:

- what remains indeterminate,
- which information is missing or unreliable,
- why it matters,
- which narrower conclusions remain supportable,
- and the information or external assessment that could reduce uncertainty.

### 15.7 Uncertainty and Action Interface
Decision consequence, reversibility, and the cost of error affect how much uncertainty is acceptable.
04 represents this relationship.
Uncertainty Handling Rules define operational actions such as information acquisition, bounded exploration, conservative modification, or deferral.

---
## 16. Closed-Loop Planning Model
Closed-loop planning combines planned direction with empirical correction.
The complete model relationship is:

Plan and Athlete-State Estimate
→ Performance Problem and Intervention Hypothesis
→ Prescription and Expected Response
→ Actual Exposure and Achieved Quality
→ Observations Across Time
→ Candidate Interpretations
→ Evidence-Weighted Athlete-State Update
→ Decision State and Scope
→ Revised or Maintained Prescription
→ New Actual Exposure
→ Continued Learning.

This is a relationship model, not an automatic pipeline.

### 16.1 Top-Down Direction
Top-down direction preserves:

- the terminal performance objective,
- the current problem and priority,
- hard constraints,
- the intervention hypothesis,
- expected exposure and response,
- and the scope within which local adaptation is allowed.

Feedback has meaning because it is evaluated against these expectations.

### 16.2 Bottom-Up Correction
Bottom-up correction uses actual exposure and response to challenge or support:

- the current athlete-state estimate,
- dose and recovery assumptions,
- intervention value,
- transfer expectations,
- bottleneck hypotheses,
- and higher-level planning assumptions.

Correction can preserve the current plan when the evidence supports stability.

### 16.3 Nested Feedback Loops
Feedback can operate at task, session, week, mesocycle, and cycle levels.
The loops differ in:

- state dimensions involved,
- evidence time scale,
- decision consequence,
- and strength of evidence normally required for revision.

They remain connected because lower-level exposure supplies evidence to higher-level planning.

### 16.4 Closed-Loop Boundary
04 defines the objects and relationships of feedback.
Rules define operational criteria.
Workflows define ordered application.
Templates define how information is collected or displayed.

---
## 17. Feedback-Decision Invariants
The following statements must remain true in every implementation of this Core Model.

1. A prescription records intended action and does not prove actual exposure, achieved quality, realized stimulus, or adaptation.

2. Feedback interpretation must begin from actual exposure rather than the original exercise or session label.

3. Observation and interpretation occupy separate logical layers; a measured change is not its own causal explanation.

4. Response must retain its time scale, and fixed elapsed time does not independently establish recovery or adaptation.

5. An isolated observation usually supports weaker inference than a sufficiently comparable repeated trend.

6. A credible high-consequence warning signal can justify conservative action without waiting for repeated harmful exposure.

7. Athlete State is a partial, decision-relevant estimate under uncertainty and cannot be fully represented by one readiness score.

8. State estimates must preserve the evidence, context, time scope, confidence, and unresolved alternatives attached to each material claim.

9. New evidence can support, weaken, refine, replace, or leave an estimate unchanged; it must not mechanically overwrite prior evidence.

10. Evidence weight depends on reliability, validity, relevance, recency, repetition, context, exposure fidelity, consistency, and consequence of error.

11. Confidence belongs to a defined claim and must not exceed the quality and applicability of its evidence.

12. Expected response must be compared with observed response under the actual exposure and context, not prescription alone.

13. Deviation from expectation challenges one or more assumptions but does not identify the failed assumption automatically.

14. Signal, noise, normal variation, and meaningful deviation are conditional relationships rather than universal numeric zones.

15. Adaptive capacity includes justified change and justified stability; noise must not drive constant plan revision.

16. Maintain, Progress, Reduce, Modify, Temporarily Withdraw, and Transition are decision states whose operational criteria belong to Rules.

17. Decision state and decision scope are separate; the smallest planning level justified by evidence should be updated first.

18. Higher-level escalation is justified when evidence or consequence challenges an assumption owned by that level, not merely because time has passed.

19. Prescription, execution, exposure, measurement, recovery, constraint, transfer, and model failures must remain distinguishable.

20. Decision quality must be evaluated from information available at decision time and must not be replaced by ex post outcome.

21. Monitoring value depends on its ability to alter relevant information, interpretation, confidence, action, or risk detection relative to its cost.

22. Conflicting or missing information must remain visible and must not be averaged or defaulted into false certainty.

23. `Cannot Determine Yet`, ambiguous response, delayed interpretation, and multiple candidate explanations are legitimate model states.

24. This model defines feedback relationships, state estimates, decision states, and scope; it does not define thresholds, fixed decision trees, or audit order.

---
## 18. Model Interfaces
This Core Model receives actual exposure and observation, updates the decision-relevant state estimate, and returns a decision state and scope to planning.
It does not duplicate adjacent models, Rules, or Workflows.

### Plan Model
[Plan Core Model](./01_plan_model.md) defines plan structure, hierarchy, conditional appropriateness, and adaptive capacity.
04 supplies the Plan Model with:

- reconciled actual exposure,
- interpreted response,
- updated athlete-state estimates,
- confidence and uncertainty,
- decision state,
- decision scope,
- and a revised-prescription interface.

01 determines where these objects sit within the time-constrained planning system.
04 does not create the complete plan or evaluate all plan-quality dimensions.

### Performance Model
[100m Performance Core Model](./02_100m_performance_model.md) defines competitive performance, determinants, indicators, bottlenecks, transfer, and competition expression.
04 uses observations to update confidence in:

- current performance state,
- candidate performance problems,
- bottleneck hypotheses,
- determinant status,
- transfer relationships,
- and competition-expression state.

04 does not redefine performance objects or convert proxies into terminal outcomes.

### Stimulus-Dose-Cost Model
[Stimulus-Dose-Cost Core Model](./03_stimulus_dose_cost_model.md) defines intervention, stimulus, dose, planned and actual exposure, achieved quality, expected adaptation, cost, risk, and uncertainty.
04 takes over at the relationship:

Actual Exposure
→ Observed Response
→ Interpretation
→ Updated Athlete State
→ Decision Update.

04 may update confidence in 03 objects without redefining their dose or cost structure.

### Rules
[Progression Rules](../rules/progression.md), [Stage Transition Rules](../rules/stage_transition.md), and [Uncertainty Handling Rules](../rules/uncertainty_handling.md) implement operational criteria and actions.
Rules determine:

- when evidence is sufficient for a decision,
- when a state should be selected,
- when scope should escalate,
- how uncertainty constrains action,
- and what operational change follows.

04 defines the objects those Rules evaluate.
It does not reproduce their thresholds, criteria, or action procedures.

### Workflows
[Audit Existing Plan](../workflows/audit_existing_plan.md) defines the ordered process for ex ante and ex post plan evaluation.
The Workflow determines when and in what sequence to:

- inspect execution,
- audit response,
- classify failure,
- update state,
- revise the plan,
- and preserve unresolved questions.

04 supplies the feedback-decision model called by that Workflow.
It does not restate the Workflow as a step-by-step manual.

### Observation and Domain Sources
Domain knowledge, evidence records, athlete reports, training logs, measurement systems, video analysis, competition records, and future research can supply observations or interpretation priors.
To enter this model, information must retain its source, construct, context, quality, relevance, uncertainty, and relationship to the current decision.
04 remains independent of any fixed monitoring technology or test catalogue.

### Interface Summary
The cross-model relationship is:

Performance Model
→ defines what performance objects and bottlenecks may change
→ Stimulus-Dose-Cost Model defines the planned intervention and exposure
→ Feedback-Decision Model interprets actual exposure and response, updates athlete state, and returns decision state and scope
→ Plan Model incorporates that update into the next prescription
→ Rules determine operational criteria
→ Workflows determine execution order.

The stable boundary remains:

Performance Object ≠ Intervention Object ≠ Observation ≠ Interpretation ≠ Decision Rule ≠ Workflow.
