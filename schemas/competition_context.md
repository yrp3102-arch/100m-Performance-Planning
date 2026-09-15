# Competition Context Schema

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This schema defines competition-related inputs within the current planning
horizon.

A competition may be a terminal performance opportunity, a highly specific
exposure, a stress event, a feedback source, and a constraint on nearby
training. These roles may coexist.

Competition Context records them without deciding the plan, prescribing a
taper, or assuming that every race is a terminal target. It accepts
natural-language or structured input and is not a calendar application.

## 1. Shared Data Semantics

### 1.1 Information Requirement

| Class | Meaning |
|---|---|
| **Required** | Missing information would materially distort the current competition-related decision. |
| **Decision-Dependent** | Information is needed because a scheduling, preparation, expression, or risk question depends on it. |
| **Optional / Additional** | Information adds context but does not block the current decision. |

Requirement is decision-relative. A detail may be Optional during general
planning and Required when the decision concerns the event it describes.

### 1.2 Status and Metadata

A material item may carry value, **Known**, **Approximate**, **Reported**,
**Confirmed**, **Unconfirmed**, **Missing**, or **Not Applicable** status,
source, date last verified, confidence, uncertainty, and decision relevance.

Metadata should be proportionate. Unknown detail is not converted into a
default competition condition.

## 2. Competition-Horizon Identity

Record:

- athlete identifier;
- planning horizon;
- primary event discipline;
- season or competition period;
- date last updated;
- source set;
- material unresolved uncertainty.

The horizon is time-bounded. Events outside it may remain in historical Profile
information rather than active Competition Context.

## 3. Primary Competition

| Object | Meaning |
|---|---|
| Event | The discipline or race entered. |
| Date and time | Confirmed or provisional competition timing. |
| Location | Venue and travel context when relevant. |
| Priority | Current planning priority. |
| Expected role | Intended role within the planning horizon. |
| Entry status | Confirmed, pending, qualified, unconfirmed, or withdrawn. |
| Performance intent | Outcome or expression sought, without guaranteeing it. |
| Governing constraints | Known entry, qualification, or schedule conditions. |

Primary competition commonly approaches Required status because it may define
the planning deadline. A provisional date must not be treated as fixed.

## 4. Secondary Competitions

Each secondary event may include the same core fields as the primary event,
plus its relationship to the primary target.

Permitted roles include:

- **Benchmark**;
- **Rehearsal**;
- **Qualification**;
- **Training Exposure**;
- **Secondary Performance Target**;
- **Low-Priority Competition**.

A role is a planning interpretation, not an inherent property of an event. It
may change as entries, Athlete State, or the calendar changes.

Participation and a recorded result do not silently create primary-target
status.

## 5. Competition Timeline

The timeline may represent:

- time remaining to each event;
- order and clustering of competitions;
- turnaround between races or rounds;
- travel dates;
- entry and qualification deadlines;
- planned review points;
- uncertainty in dates or sequence.

Time to competition is derived from a dated context and changes with the
current date or event date.

The timeline describes temporal constraints. It does not prescribe a fixed
periodization structure, weekly schedule, or taper.

## 6. Competition Conditions

Record known conditions only:

- indoor or outdoor setting;
- track surface;
- timing system;
- expected number and sequence of rounds;
- qualification format when relevant;
- expected environmental conditions;
- altitude or travel context when relevant;
- call-room, reporting, or scheduling demands when material;
- equipment or facility restrictions.

A forecast remains a forecast. Expected conditions retain source, date, and
uncertainty when they affect decisions.

Unknown wind, surface, timing, or round conditions do not become normal
conditions.

## 7. Competition Role in Planning

| Role | Schema meaning |
|---|---|
| **Terminal Target** | A principal opportunity for competitive 100m performance. |
| **Benchmark** | An expected comparison point. |
| **Training Exposure** | Participation is intended partly as a highly specific exposure. |
| **Rehearsal** | The event is used to practice competition expression or logistics. |
| **Qualification** | The result or participation affects access to a later event. |
| **Low-Priority Competition** | The event has a limited claim on preparation resources. |

The role informs planning value, expected freshness, acceptable cost, and
interpretation. It does not determine them automatically.

## 8. Competition as Exposure, Stress, and Feedback

### 8.1 Exposure

A race may provide specific sprint exposure. Planned participation does not
prove that the intended exposure occurred. Actual rounds, execution, timing,
and achieved quality belong in the Actual Exposure record.

### 8.2 Stress Event

Competition may create acute fatigue, delayed recovery demand, tissue stress,
travel stress, attention cost, and interference with other exposures. These
costs remain multidimensional.

### 8.3 Feedback Source

Competition results and observations may update:

- current competitive performance;
- segment or expression hypotheses;
- competition readiness;
- constraint estimates;
- confidence in the current plan.

A favorable result does not prove that every underlying capacity improved. An
unfavorable result does not by itself prove method failure.

## 9. Competition Constraints

Active constraints may include:

- travel duration and time-zone change;
- event schedule and rounds;
- short recovery windows;
- qualification requirements;
- venue or equipment limitations;
- work, school, or other obligations;
- supplied medical or governing restrictions;
- uncertain entry or schedule status.

Each consequential constraint should state its source, status, affected
decision, and time window.

The schema records constraints. The
[Constraint Handling Rules](../rules/constraint_handling.md) govern how they
affect a decision.

## 10. Competition Uncertainty

Examples include:

- entry not confirmed;
- event date or time uncertain;
- qualification status unresolved;
- round structure unknown;
- travel arrangements incomplete;
- expected conditions based on a weak forecast;
- target role under review.

For each consequential uncertainty, record:

- what is unknown;
- why it matters;
- current confidence;
- when the information is needed;
- whether a conservative decision can proceed;
- whether the missing information blocks the decision.

Use **PROVISIONAL_STATE** or **PARTIAL_STATE** when bounded action remains
possible. Use **DECISION_BLOCKED_BY_MISSING_INFORMATION** when the current
decision cannot proceed.

Missing information is not favorable scheduling, adequate recovery, or
confirmed entry.

## 11. Minimum Competition Context

When competition affects the current plan, a minimally useful context should
ordinarily establish:

- event and current role;
- date or bounded date uncertainty;
- priority relative to other events;
- entry or qualification status;
- known rounds and travel demands when material;
- major constraints;
- uncertainty that could change the decision.

If no competition affects the planning horizon, record that explicitly rather
than inventing a target date.

## 12. Natural-Language Mapping

"Nationals should be on 18 July, entry is not confirmed, and I may need heats
and a final after a long flight" may map to:

- provisional primary-competition date;
- unconfirmed entry;
- possible multi-round demand;
- travel and recovery constraint;
- schedule uncertainty requiring later verification.

Qualifiers remain visible. Mapping does not upgrade them to confirmed facts.

## 13. Interfaces and Boundaries

- [Athlete Profile Schema](./athlete_profile.md) stores durable competition and
  training background.
- [Athlete State Schema](./athlete_state.md) stores current competition
  readiness, expression state, and active constraints.
- [Performance Assessment Schema](./performance_assessment.md) records
  competition results and observations used as assessment evidence.
- [Plan Core Model](../core_models/01_plan_model.md) defines how deadlines,
  priorities, and competitions enter plan structure.
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
  defines terminal performance and competition expression.
- [Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md)
  defines competition exposure and cost as intervention objects.
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
  governs how competition observations update Athlete State.

This schema does not prescribe competition frequency, taper structure, race
strategy, or entry decisions.

## 14. Competition Context Invariants

1. Competition may be target, exposure, stress event, and feedback source.
2. Competition role is explicit and may change.
3. Event priority does not follow automatically from participation.
4. Planned participation does not prove Actual Exposure.
5. Competition result and its interpretation remain distinct.
6. Forecast and confirmed condition remain distinct.
7. Missing context is not converted into favorable assumptions.
8. Requirement class follows the current decision.
9. Competition Context records constraints but does not resolve them.
10. Natural-language input remains valid.