# Athlete State Schema

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

Athlete State is the current decision-relevant representation of the athlete
under uncertainty.

It is not a complete model of the person, a permanent profile, or a single
readiness score. It is a time-bounded estimate maintained so that planning
decisions can use current information.

Observed data inform Athlete State. They are not Athlete State itself.
Measurement is not interpretation, and observation is not conclusion.

## 1. State Record Identity

A state record should identify:

- athlete identifier;
- effective date or period;
- planning decision or horizon it supports;
- prior state reference when available;
- information sources;
- last updated date;
- current completeness status;
- overall unresolved uncertainty.

Permitted completeness states include:

- **CURRENT_STATE**: current enough for the stated decision;
- **PARTIAL_STATE**: some dimensions are missing but bounded decisions remain
  possible;
- **PROVISIONAL_STATE**: the estimate relies on material assumptions awaiting
  confirmation;
- **DECISION_BLOCKED_BY_MISSING_INFORMATION**: specified missing information
  prevents the named decision.

These states describe information sufficiency. They do not grade the athlete.

## 2. Shared Field Semantics

### 2.1 Information Requirement

| Class | Meaning |
|---|---|
| **Required** | Absence materially distorts the current basic decision or prevents a minimally usable state. |
| **Decision-Dependent** | Needed because a specific decision, bottleneck hypothesis, risk, or uncertainty depends on it. |
| **Optional / Additional** | Adds context but does not block the current decision. |

Requirement is assigned relative to the current decision. It is not a permanent
property of a field or metric.

### 2.2 State Value Status

A state item may be:

- **Known**;
- **Estimated**;
- **Uncertain**;
- **Not Assessed**;
- **Missing**;
- **Not Applicable**.

Do not convert Missing or Not Assessed into normal, zero, available, or no
problem.

### 2.3 Evidence Metadata

Consequential state claims may preserve:

- value or concise description;
- observation basis;
- source;
- date or relevant time window;
- qualitative confidence;
- competing explanation;
- decision relevance;
- update trigger.

Metadata should be proportionate to the consequence of error.

## 3. Current Performance State

Current Performance State represents the best current estimate of performance
expression and relevant component outcomes.

### 3.1 Competitive 100m Performance

Record when available:

- recent legal or context-qualified 100m result;
- representative recent competition range;
- timing, wind, round, surface, and environmental context;
- relationship to prior performance;
- confidence in current representativeness.

Competitive 100m performance remains the terminal criterion. A single result
may be affected by fatigue, environment, race execution, and measurement noise.

### 3.2 Race-Structure State

Relevant descriptive dimensions may include:

- start and block-clearance outcome;
- early acceleration outcome;
- late acceleration or transition outcome;
- maximum-velocity outcome;
- speed-maintenance or deceleration outcome;
- velocity or acceleration profile;
- current competition expression.

Each dimension may be Known, Estimated, Uncertain, or Not Assessed.

Race segments are descriptive time-space structures. They are not automatically
independent capacities, and determinants may overlap across segments.

### 3.3 Supporting Indicators

Supporting sprint tests, strength measures, jump measures, technical
observations, and subjective information may inform the state when their
decision relevance is explicit.

Proxy improvement does not establish competitive 100m improvement.

## 4. Current Performance Problem

A Current Performance Problem is a decision-relevant description of the gap
between observed or estimated performance and the relevant target or expected
expression.

Represent:

- problem statement;
- affected terminal or segment outcome;
- observation basis;
- comparison reference;
- time period;
- contextual qualifiers;
- confidence;
- unresolved alternatives;
- decision relevance.

An observed slow split, unstable race expression, or declining performance is a
problem description. It is not automatically a causal explanation or
bottleneck.

If the problem itself cannot yet be established, use **Cannot Determine** rather
than inventing one.

## 5. Candidate Bottleneck

A Candidate Bottleneck is a plausible limiting determinant or constraint that
may explain a current performance problem. It remains a hypothesis until
evidence supports stronger causal status.

For each candidate, record:

- candidate determinant or constraint;
- linked performance problem;
- rationale and mechanistic relevance;
- supporting observations;
- conflicting observations;
- plausible alternatives;
- current level if known;
- athlete-specific relevance;
- trainability considerations;
- transfer uncertainty;
- confidence;
- status: active, retained alternative, weakened, unresolved, or retired.

A weakness relative to a group, norm, or prior score is not automatically a
bottleneck. Association, mechanistic plausibility, trainability, and transfer
remain distinct.

Several candidate bottlenecks may coexist. The schema does not force unique
identification.

## 6. Current Priority State

Record planning priority outputs without deriving them inside the schema.

Permitted states are:

| Priority state | Meaning |
|---|---|
| **Primary** | Receives the strongest current claim on scarce planning resources. |
| **Maintain** | Receives enough exposure to preserve a relevant capability or adaptation. |
| **Minimal** | Receives the smallest justified allocation compatible with current constraints. |
| **Temporarily Withdrawn** | Is deliberately absent for a stated, reviewable reason. |

For each priority, record the target object, rationale reference, effective
period, relevant constraint, confidence, and review trigger.

Priority is a decision output governed by
[Priority Allocation Rules](../rules/priority_allocation.md). A low test score
does not assign itself Primary status.

## 7. Fatigue and Recovery State

Fatigue and recovery are multidimensional and time-dependent. Do not compress
them into a universal readiness score.

Relevant dimensions may include:

- recent performance suppression;
- perceived exertion or unusual effort;
- local and general fatigue reports;
- sleep or lifestyle disruption when relevant;
- recovery between recent exposures;
- motivation or attention where it affects execution;
- expected versus observed recovery pattern;
- confidence and unresolved causes.

Each observation remains separate from its interpretation. "30m time was
slower" is an observation; "neural fatigue" is one possible interpretation.

State estimates should distinguish immediate response, delayed response,
repeated trend, and longer-term adaptation signal without imposing universal
time windows.

## 8. Tissue State

Tissue State represents current exposure availability and reported local
signals without diagnosis.

It may include:

- location and athlete-reported sensation;
- pain or discomfort report;
- onset and temporal pattern;
- recurrent issue reference;
- movement or exposure contexts associated with the report;
- current availability for relevant exposure;
- supplied medical or rehabilitation restriction;
- source and date;
- uncertainty;
- escalation or review need.

Missing tissue information is not proof of full availability. High-consequence
warning information may justify conservative action even before a repeated
trend is established.

The schema records supplied restrictions and observations. Medical diagnosis
and clinical decisions remain outside scope.

## 9. Technical State

Technical State represents current task organization and its stability.

It may include:

- observed technical organization relevant to the current problem;
- repeatability across comparable exposures;
- phase or context in which change appears;
- relationship to speed, fatigue, or environment;
- source, such as video or coach observation;
- competing interpretations;
- confidence;
- assessment status.

Technique is not defined by a universal posture, single trajectory, or isolated
biomechanical variable. Technical observation remains a task-specific indicator.

## 10. Exposure State

Exposure State summarizes recent Actual Exposure needed to interpret current
capacity, tolerance, and response.

Relevant dimensions may include:

- recent sprint exposure;
- recent high-speed exposure;
- acceleration exposure;
- speed-maintenance exposure;
- strength exposure;
- plyometric exposure;
- competition exposure;
- achieved quality and repeatability;
- density and distribution;
- recent unusual or interrupted exposure;
- apparent tolerance;
- missing exposure records.

Exercise labels do not prove stimulus. Prescription does not prove Actual
Exposure. Exposure State should use what was completed and encountered, with
enough task-specific dose context to support interpretation.

Internal Response remains separate from External Dose and Actual Exposure.

## 11. Adaptation Trend

Adaptation Trend represents the current evidence-weighted direction of change
for a specified target.

Permitted qualitative directions include:

- **Improving**;
- **Stable**;
- **Declining**;
- **Mixed**;
- **Unresolved**;
- **Cannot Determine**.

Each trend should identify:

- target outcome, determinant, capacity, or tolerance;
- observation window;
- actual exposures considered;
- expected response;
- supporting and conflicting evidence;
- contextual changes;
- confidence.

A single favorable observation does not automatically establish adaptation.
Repeated evidence usually supports a stronger inference, while important safety
signals may justify action without repetition.

## 12. Competition Readiness

Competition Readiness is one state dimension describing likely expression under
the current competition context. It does not replace the terminal performance
model.

It may represent:

- current performance capability estimate;
- freshness or fatigue relevant to expression;
- technical stability;
- tissue availability;
- recent competition-specific exposure;
- race-execution familiarity;
- travel or environmental constraint;
- confidence and uncertainty.

Capacity and competition expression remain distinct. Improved capacity may be
masked at competition, and a better result does not prove improvement in every
underlying capacity.

## 13. Active Constraints

Record constraints that currently change feasible planning options:

- time;
- facility or environment;
- medical or rehabilitation restriction;
- tissue availability;
- recovery ceiling;
- competition deadline or schedule;
- travel;
- information constraint;
- adherence or execution constraint.

For each constraint, preserve source, status, affected scope, time window,
severity or practical effect, confidence, and review trigger when material.

A historical constraint is not assumed active. An active constraint is not
ignored because its cause is uncertain.

## 14. Current Uncertainty

Current Uncertainty makes decision-relevant unknowns explicit.

Each uncertainty record should state:

- what is unknown;
- which state claim or decision it affects;
- plausible alternatives;
- available evidence;
- consequence of being wrong;
- whether more information could reduce it;
- information-acquisition cost;
- whether conservative action remains possible;
- next useful observation or review trigger.

Permitted outputs include **Candidate Explanation**, **Provisional Bottleneck**,
**Delayed Interpretation**, **Unresolved**, and **Cannot Determine**.

If missing information blocks a named decision, use
**DECISION_BLOCKED_BY_MISSING_INFORMATION**. Otherwise retain a bounded
PARTIAL_STATE or PROVISIONAL_STATE.

## 15. State Confidence

Use qualitative confidence rather than unsupported probabilities:

| Confidence | Meaning |
|---|---|
| **Strong** | Multiple relevant, reliable, and coherent observations support the estimate. |
| **Moderate** | Useful support exists with material limitations. |
| **Provisional** | The estimate is usable conditionally and awaits confirmation. |
| **Weak** | Evidence is limited, indirect, or inconsistent. |
| **Unresolved** | Competing explanations remain materially plausible. |
| **Cannot Determine** | Available information cannot support the required inference. |

Confidence is claim-specific. A state record may contain strong confidence in
one dimension and unresolved status in another.

New evidence should be weighted by reliability, relevance, recency, repeated
trend, measurement quality, cross-signal consistency, and consequence of error.
A low-quality observation does not mechanically overwrite stable prior evidence.

## 16. State Update Metadata

An update should preserve:

- last updated date;
- prior state reference;
- new observations;
- Actual Exposure context;
- interpretation used;
- supporting and conflicting evidence;
- dimensions changed;
- dimensions deliberately retained;
- confidence change;
- decision affected;
- review trigger.

This is update provenance, not a feedback workflow or decision algorithm.
Operational review belongs in
[Review Training Workflow](../workflows/review_training.md).

## 17. Minimum Athlete State

A minimally usable state for a named planning decision should ordinarily
identify:

- current performance state or explicit lack of assessment;
- current performance problem or Cannot Determine;
- candidate bottleneck status and alternatives;
- current priorities;
- recent relevant Actual Exposure;
- material fatigue, recovery, tissue, and technical state;
- active constraints;
- competition timing when relevant;
- material uncertainty and confidence;
- information that blocks or limits the decision.

The minimum is decision-specific. It does not require a complete test battery or
all possible state dimensions.

## 18. Natural-Language Mapping

Natural-language input is mapped into observation, source, time, uncertainty,
and state dimensions. Original wording may be retained for traceability.

"I feel fresh but my hamstring is a little tight" maps to at least two
observations. It does not become a single readiness score, proof of full
recovery, or a diagnosis.

"I have not sprinted fast for a month" maps to reported recent high-speed
Exposure State with an approximate time window. It does not by itself establish
loss of maximum-velocity capacity.

## 19. Interfaces and Boundaries

- [Athlete Profile Schema](./athlete_profile.md) supplies slow-changing context.
- [Performance Assessment Schema](./performance_assessment.md) supplies
  measurement and observation records without embedding causal conclusions.
- [Competition Context Schema](./competition_context.md) supplies active
  competition roles, timing, and constraints.
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
  defines performance problems, determinants, bottlenecks, indicators, and
  competition expression.
- [Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md)
  defines intervention and Actual Exposure inputs.
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
  defines evidence-weighted State Update and decision interfaces.
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md) govern action
  under incomplete information.

Future build-athlete-state workflow logic is outside this schema.

## 20. Athlete State Invariants

1. Athlete Profile and Athlete State remain distinct.
2. Athlete State is decision-relevant, time-bounded, and partially observable.
3. Observed Data inform Athlete State; they are not identical to it.
4. Observation and interpretation remain separate.
5. Performance problem and bottleneck remain separate.
6. Weakness does not automatically establish a bottleneck.
7. Prescription does not establish Actual Exposure.
8. Fatigue, recovery, and readiness are not reduced to one universal score.
9. State updates are proportional to evidence quality and consequence.
10. Missing information is not zero, normal, available, or no problem.
11. Requirement class changes with the decision.
12. Confidence and competing explanations remain visible.
13. Medical information is recorded without diagnosis.
14. The schema records decision outputs but does not implement decision rules.