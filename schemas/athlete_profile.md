# Athlete Profile Schema

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This schema defines the slow-changing information used to answer: Who is the
athlete for the purposes of 100m performance planning?

Athlete Profile provides durable background and operating context. It does not
represent current Athlete State, explain observations, diagnose a condition, or
prescribe training. This is a semantic contract for natural-language or
structured input, not a mandatory intake questionnaire.

## 1. Shared Data Semantics

### 1.1 Information Requirement

| Class | Meaning |
|---|---|
| **Required** | Its absence would materially distort the current basic planning decision or prevent a minimally usable Athlete State. |
| **Decision-Dependent** | It is needed when the current decision question, bottleneck hypothesis, risk, or uncertainty depends on it. |
| **Optional / Additional** | It may enrich context, but its absence does not block the current decision. |

Requirement is decision-relative, not a permanent property of a metric or
field. A field may change class when the decision changes.

### 1.2 Data Status

Important items may be marked **Known**, **Approximate**, **Reported**,
**Measured**, **Historical**, **Unverified**, **Missing**, or
**Not Applicable**. Statuses may be combined.

Missing is not zero, normal, favorable, absent, or not applicable.

### 1.3 Proportionate Metadata

Consequential items may include value, status, source, date or period,
qualitative confidence, material uncertainty, and decision relevance. Metadata
is required only when it changes interpretation or traceability.

## 2. Identity and Basic Context

| Information object | Boundary |
|---|---|
| Athlete identifier or alias | Use a stable reference; collect personal identifiers only when operationally necessary. |
| Age or developmental context | Preserve exact or approximate status. |
| Sex | Record when provided and relevant to interpretation or competition classification. |
| Primary event | Identify the event currently organizing the plan. |
| Secondary events | Include when they affect preparation, competition, or transfer reasoning. |
| Height | Preserve date and method when those details matter. |
| Body mass | Treat as time-stamped rather than permanently current. |

A stable identifier, primary event, and sufficient age context are commonly
close to Required. Anthropometric details are often Decision-Dependent or
Optional / Additional. These are defaults, not universal rules.

## 3. Training Age and Experience

### 3.1 Training-Age Objects

The profile may represent:

- sprint training age;
- strength training age;
- plyometric or jump-training experience when relevant;
- structured versus informal training;
- continuity and interruptions in recent structured preparation.

Calendar years alone are insufficient. Training age may be discontinuous,
event-specific, and approximate.

### 3.2 Previous Structured Training

Relevant history may include broad preparation types, high-speed exposure,
strength and plyometric exposure, competition exposure, familiar monitoring
practices, and major changes in methods or environment.

Historical exposure does not prove current capacity or tolerance.

### 3.3 Coaching and Competition Background

Record prior and current coaching environment, technical supervision,
competition level, typical competition frequency, event specialization history,
and experience with rounds, travel, or high-priority races when relevant.

Competition level describes context. It is not a direct measure of a
performance determinant.

## 4. Performance History

### 4.1 100m History

The profile may include:

- historical 100m personal best;
- date and competition context;
- representative recent-season performances;
- electronic or hand timing status;
- wind reading and legality when known;
- indoor or outdoor context;
- known surface or measurement limitations.

A personal best is a historical outcome. It does not by itself represent
current competitive capacity or current competition expression.

### 4.2 Supporting Performance History

Relevant 60m, 200m, split, or other race results may be retained as supporting
outcomes, contextual evidence, or proxies.

Supporting performance is not the terminal 100m criterion. Improvement in a
supporting result does not establish improved competitive 100m performance.

### 4.3 Record Quality

Consequential records should preserve relevant date, setting, timing method,
wind, surface, race round, source, and verification status. Unknown conditions
remain Missing or Unknown; they are not assumed legal or comparable.

## 5. Injury and Medical Context

Record only supplied information, including:

- prior injury history;
- recurrent tissue problems;
- surgery or rehabilitation history when relevant;
- current medical restrictions;
- rehabilitation status and responsible professional, if known;
- prior exposure restrictions;
- unresolved medical information affecting planning.

Historical history and current condition remain distinct. Current tissue
availability belongs in [Athlete State](./athlete_state.md).

This schema does not diagnose. No injury report is not evidence of no injury,
and missing information is not medical clearance.

## 6. Training Environment

Record stable or recurring access to:

- suitable track and surface;
- weather-protected sprint space;
- gym and relevant equipment;
- timing technology and its precision;
- video capability;
- training partners;
- coaching or supervision;
- transport and venue access;
- recurring climate constraints.

Availability should include frequency, reliability, and material limitations.
Environment constrains feasible options; it does not establish appropriateness.

## 7. Time and Lifestyle Constraints

Relevant recurring objects may include:

- training days available;
- session-duration limits;
- work or school schedule;
- predictable high-demand periods;
- travel obligations;
- recurring sleep schedule when decision-relevant;
- caregiving or logistical obligations.

Record the planning implication when known. Transient changes belong in Athlete
State or Competition Context rather than becoming permanent profile facts.

## 8. Preference and Adherence Context

The profile may record strong exercise preferences or aversions, adherence
history, practical tolerance for complexity, preferred training setting, and
record-keeping practices that affect execution.

These items are usually Optional / Additional. They may become
Decision-Dependent when adherence or execution reliability is in question.
Preference does not override the performance problem or safety constraints.

## 9. Profile Data Quality

### 9.1 Sources

Sources may include athlete report, coach report, competition record, training
record, measurement record, supplied professional restriction, or system
inference. Inference remains labeled as inference.

### 9.2 Time Validity

Slow-changing does not mean timeless. Preserve the relevant date or period.
Stale information may remain historically useful while losing current
decision authority.

### 9.3 Conflict

When sources conflict, preserve competing accounts, their dates and sources,
adjust confidence, and expose the unresolved implication. Do not choose the
convenient value without justification.

## 10. Minimum Profile for Planning

A minimally usable profile should ordinarily establish:

- stable athlete identifier;
- primary event and current performance goal;
- sufficient age or developmental context;
- approximate sprint and strength training history;
- usable 100m history or explicit missing status;
- supplied medical or rehabilitation restrictions and related uncertainty;
- available training time and major recurring constraints;
- usable facility and coaching context;
- provenance and uncertainty of consequential claims.

This is a minimum information structure, not a giant questionnaire.

If missing information does not block a conservative decision, proceed with
**PARTIAL_STATE** or **PROVISIONAL_STATE**. If it blocks the current decision,
record **DECISION_BLOCKED_BY_MISSING_INFORMATION** and identify the missing item
and blocked decision.

## 11. Natural-Language Mapping

A statement such as "I run about 11.4, have not done much top-speed work this
month, my hamstring feels a little tight, and I can train four days per week"
may map to:

- approximate, reported performance history or assessment;
- recent high-speed Exposure State;
- current tissue observation with unresolved interpretation;
- recurring weekly availability.

Preserve qualifiers such as "about," "recently," and "a little." Mapping does
not create precision, diagnosis, or causal conclusions.

## 12. Interfaces and Boundaries

- [Athlete State Schema](./athlete_state.md) stores the current
  decision-relevant state estimate.
- [Performance Assessment Schema](./performance_assessment.md) stores assessment
  questions and measurement or observation records.
- [Competition Context Schema](./competition_context.md) stores the active
  competition horizon.
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
  defines terminal performance, determinants, indicators, and bottlenecks.
- [Constraint Handling Rules](../rules/constraint_handling.md) govern how
  constraints affect decisions.
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md) govern action
  under incomplete or conflicting information.

Profile records do not choose priorities, establish readiness, select
interventions, or determine a plan.

## 13. Profile Invariants

1. Athlete Profile and Athlete State remain distinct.
2. Historical information is not presumed current.
3. Missing information is not zero, normal, favorable, or no problem.
4. Requirement class depends on the current decision.
5. Source, date, and confidence remain visible when they affect use.
6. Reported, measured, and inferred information remain distinguishable.
7. Medical context is recorded without diagnosis.
8. Supporting performance does not replace competitive 100m performance.
9. Natural-language input does not require a fixed intake form.
10. Additional data must earn its place through decision relevance.