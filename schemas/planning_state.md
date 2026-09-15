# Planning State Schema
Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose
Planning State is the persistent, decision-relevant record of where planning currently stands.
It enables a later Agent run to resume an existing planning process without reconstructing the Cycle, Mesocycle, Week, and Session hierarchy from raw history.
Planning State answers:
- Which athlete and planning horizon are active?
- Which planning objects currently guide decisions?
- Which objects were most recently completed?
- What is the smallest next required action?
- Which constraints, uncertainties, and unresolved items must carry forward?
- Which references are current enough to use?
- Which plan version is authoritative?
Planning State is not Athlete State, a training plan, a context summary, or raw training history.
This schema defines a storage-agnostic runtime data contract. Runtime instances belong in an external persistent store. The Skill repository contains the schema, rules, and workflows, not live athlete records.

## 1. Planning State Identity
A Planning State record should support:
| Field | Meaning |
|---|---|
| planning_state_id | Stable identifier for this continuity record. |
| athlete_reference | Reference to the athlete whose planning continuity is represented. |
| planning_horizon | Current competition, season, or bounded planning horizon. |
| record_status | Whether this record is current, superseded, or invalidated. |
| plan_version | Version of the authoritative planning structure. |
| created_at | Creation time. |
| updated_at | Most recent material update time. |
| previous_version | Reference to the prior Planning State version when material meaning changed. |
| source_event | Event that produced this version. |
| storage_reference | Adapter-neutral reference used by the external persistence layer. |
The record should have one authoritative active version per athlete and planning horizon. Historical versions remain traceable.

## 2. Skill Logic and Runtime Data
The Skill repository stores:
- schemas;
- rules;
- workflows;
- Core Models;
- theory;
- templates;
- continuity protocol.
An external runtime store may hold:
- athlete records;
- Planning State instances;
- Athlete State instances;
- active and historical plans;
- Context Summaries;
- raw session data;
- reviews;
- assessments;
- decision records.
The runtime store may later use Notion or another adapter. This schema does not depend on Notion, a database product, SQL, or a particular API.
Conceptual operations such as get_planning_state() and save_planning_state() name logical interfaces. They are not implemented functions in this repository.

## 3. Active Planning Hierarchy
Planning State should reference the active hierarchy without duplicating the complete plans.
### 3.1 Cycle Reference
Support:
- active Cycle reference;
- Cycle status;
- Cycle version;
- terminal objective reference;
- effective horizon;
- last completed Cycle reference.
### 3.2 Mesocycle Reference
Support:
- active Mesocycle reference;
- Mesocycle status;
- parent Cycle reference;
- Mesocycle version;
- current stage or adaptation-problem reference;
- last completed Mesocycle reference.
### 3.3 Week Reference
Support:
- active Week or Microcycle reference;
- Week status;
- parent Mesocycle reference;
- Week identifier or sequence position;
- Week version;
- last completed Week reference.
### 3.4 Session Reference
Support:
- current or pending Session reference;
- Session status;
- parent Week reference;
- Session sequence position when relevant;
- Session version;
- last completed Session reference;
- whether its review is complete.
A null active reference means no object is currently active at that level. It does not prove that no historical object exists.

## 4. Planning-Level Status
Planning objects may use these statuses:
| Status | Meaning |
|---|---|
| **DRAFT** | Defined but not yet authoritative for execution. |
| **ACTIVE** | Currently guides planning or execution decisions. |
| **COMPLETED** | Reached its intended close under the applicable completion criteria. |
| **PAUSED** | Temporarily suspended without being completed or abandoned. |
| **SUPERSEDED** | Replaced by a newer authoritative version while retained as history. |
| **INVALIDATED** | Its foundational assumptions no longer justify continued use. |
These meanings do not impose one universal lifecycle. Different planning levels may enter or leave statuses through different events.
Existing does not mean valid. An ACTIVE reference remains subject to assumption validation and may be revised, paused, invalidated, or superseded.

## 5. Current Planning Scope
Represent:
- current planning level;
- current decision object;
- decision scope;
- requested scope when different;
- smallest justified update level;
- current workflow reference;
- next required action;
- next action reason;
- action deadline when relevant;
- planning readiness;
- blocking information if any.
Planning levels may include Cycle, Mesocycle, Week, Session, Review, Athlete State Update, Summary Update, and Planning State Update.
The current scope should identify what the system needs to do next rather than requiring a later Agent to infer it from chronology.

## 6. Current Athlete State Reference
Support:
- current Athlete State reference;
- Athlete State version;
- effective date or period;
- last Athlete State update;
- information-sufficiency status;
- Planning Readiness status;
- state confidence reference;
- relevant expiry or review trigger;
- prior Athlete State reference when needed.
Planning State points to the authoritative current Athlete State. It does not copy the full state record.
Planning State and Athlete State remain distinct:
- Planning State tracks planning continuity and pointers.
- Athlete State represents the current decision-relevant athlete estimate.

## 7. Current Priorities
Represent current priority outputs through references or a compact summary:
- Primary;
- Maintain;
- Minimal;
- Temporarily Withdrawn;
- effective planning level;
- rationale reference;
- start or effective date;
- review trigger;
- confidence;
- source decision.
Priority status is carried forward until a valid decision revises or retires it. Planning State records the current result; it does not allocate priorities.

## 8. Active Constraints
Carry current constraints that affect feasible planning:
- competition deadline;
- medical or rehabilitation restriction;
- tissue availability constraint;
- recovery ceiling;
- facility or environment constraint;
- time availability;
- travel;
- information constraint;
- execution or adherence constraint.
For each active constraint, support:
- identifier;
- concise description;
- source reference;
- affected planning level or decision;
- effective period;
- status;
- confidence;
- review or exit condition.
Missing constraint information is not interpreted as resolved.

## 9. Active Uncertainties
Represent decision-relevant uncertainty through:
- uncertainty identifier;
- unknown or contested claim;
- affected decision;
- plausible alternatives;
- consequence of error;
- current confidence;
- information needed;
- next observation or assessment reference;
- review trigger;
- current status.
Permitted statuses include **ACTIVE**, **RESOLVED**, **INVALIDATED**, and
**SUPERSEDED**.
Resolved status requires an explicit resolution record. Age alone does not resolve uncertainty.

## 10. Active Carry-Forward Items
A Carry-Forward Item is information originating in an earlier planning block that still changes a current or future decision.
Eligible classes include:
- Active Constraint;
- Active Tissue Concern;
- Unresolved Uncertainty;
- Current Bottleneck Hypothesis;
- Competition Deadline;
- Important Benchmark;
- Open Decision Question;
- unresolved measurement problem;
- recurring response pattern;
- decision condition or promised review.
Each item should support:
- carry-forward identifier;
- class;
- concise statement;
- source record;
- first observed date or block;
- current relevance;
- affected decision;
- confidence and uncertainty;
- current owner object;
- status;
- review trigger;
- exit reason;
- resolution or replacement reference.
An item remains active until explicitly **RESOLVED**, **INVALIDATED**,
**SUPERSEDED**, or otherwise closed with a recorded reason.
Archiving the Week in which an item first appeared does not close it.
If an old issue still affects current decisions, it should be visible in Current Athlete State or Planning State Carry-Forward Items rather than surviving only through repeated deep-history retrieval.

## 11. Important Benchmarks
Planning State may retain compact references to benchmarks needed for current comparison:
- benchmark identity;
- outcome or indicator;
- date and conditions;
- source record;
- comparison use;
- confidence;
- current relevance;
- replacement or expiry condition.
Benchmarks do not replace terminal competitive 100m performance and do not become current State automatically.

## 12. Competition Context Reference
Support:
- current Competition Context reference;
- version;
- primary competition and role;
- nearest decision-relevant deadline;
- entry or schedule uncertainty;
- last update;
- next verification trigger.
The full competition record remains in the Competition Context object.

## 13. Review and Summary References
Represent:
- last completed review;
- review level and object;
- review completion time;
- latest relevant Session Review;
- last Week Summary;
- active Mesocycle Summary;
- previous completed Mesocycle Summary;
- current or previous Cycle Summary;
- last summary update;
- summary versions;
- summary revision pending flag.
A review is event-level analysis. A summary is cross-event compression. Neither is identical to Athlete State.

## 14. Next Required Decision
The next action should be explicit and may include:
- BUILD_OR_UPDATE_ATHLETE_STATE;
- REVIEW_COMPLETED_SESSION;
- CREATE_NEXT_SESSION;
- CREATE_NEXT_WEEK;
- CREATE_NEXT_MESOCYCLE;
- CREATE_NEW_CYCLE;
- CONTINUE_EXISTING_PLAN;
- REVISE_EXISTING_PLAN;
- UPDATE_CONTEXT_SUMMARY;
- UPDATE_PLANNING_STATE;
- REQUEST_INFORMATION;
- REQUEST_ASSESSMENT;
- PAUSE_FOR_EXTERNAL_ASSESSMENT.
Record:
- action;
- target planning level;
- rationale;
- prerequisites;
- blocking information;
- destination workflow;
- priority or deadline.
This vocabulary is descriptive, not a rigid state machine.

## 15. Invalidation Flags
Flags identify assumptions requiring validation before an existing plan is reused.
Examples include:
- Athlete State materially changed;
- competition target changed;
- major constraint changed;
- active tissue restriction changed;
- Mesocycle hypothesis challenged;
- Cycle objective changed;
- plan version conflict;
- stale current State;
- unresolved review;
- missing required summary;
- parent-child hierarchy inconsistency.
Each flag should include source, affected object, severity or consequence, confidence, and resolution status.
A flag does not automatically force global replanning. It directs validation at the smallest justified planning level.

## 16. Data Freshness
For each critical reference, support:
- effective date;
- last verified date;
- decision horizon;
- freshness status;
- review trigger;
- consequence if stale.
Freshness is decision-relative. No universal expiration days are defined.
A long-term training-history field may remain current longer than a tissue observation. Older does not mean irrelevant, and recent does not guarantee relevance.
Permitted freshness states include **CURRENT**, **AGING**,
**REVIEW_REQUIRED**, **STALE_FOR_DECISION**, and **UNKNOWN**.

## 17. Versioning
A material Planning State update should record:
- version;
- previous version;
- source event;
- changed fields;
- change rationale;
- responsible process;
- updated_at;
- references added, changed, or retired;
- unresolved differences.
Do not silently overwrite a prior continuity state when the change affects planning meaning, authority, or historical interpretation.
A trivial formatting correction need not create a complex revision chain. A change to active pointers, status, next action, or carry-forward meaning does.

## 18. Minimum Planning State
A minimally resumable record should identify:
- athlete reference;
- authoritative record version;
- active and last-completed hierarchy references;
- current planning level;
- current Athlete State reference and freshness;
- Competition Context reference when relevant;
- current priorities;
- active constraints;
- active carry-forward items;
- last review and summary references;
- next required action;
- invalidation flags;
- updated_at.
If these are incomplete, the system should preserve the gap and retrieve only the information required to resolve the current continuity decision.

## 19. Storage-Agnostic Persistence Contract
A persistence adapter should be able to:
- retrieve the authoritative Planning State;
- retrieve referenced current objects;
- save a new Planning State version;
- preserve prior versions;
- resolve references;
- mark objects active, completed, paused, superseded, or invalidated;
- retain archived source records;
- expose provenance.
This is a logical contract. It does not specify database tables, API calls, or vendor-specific properties.

## 20. Interfaces
- [Athlete State Schema](./athlete_state.md) defines the current athlete
  estimate referenced here.
- [Competition Context Schema](./competition_context.md) defines the active
  competition horizon.
- [Context Summary Schema](./context_summary.md) defines compressed historical
  context.
- [Resume Planning Workflow](../workflows/resume_planning.md) reads Planning
  State before selecting a planning workflow.
- [Update Planning State Workflow](../workflows/update_planning_state.md)
  changes pointers, status, carry-forward items, and next action.
- [Update Context Summary Workflow](../workflows/update_context_summary.md)
  creates or revises summaries and updates their references.
- [Build Athlete State Workflow](../workflows/build_athlete_state.md) constructs
  or updates Athlete State; it does not manage continuity pointers.

## 21. Planning State Invariants
1. Resume before create.
2. Planning State and Athlete State remain distinct.
3. Planning State references plans; it does not duplicate them.
4. Existing plans are validated before reuse.
5. Active hierarchy and last-completed hierarchy remain distinguishable.
6. The next required action is explicit.
7. Important unresolved information carries forward until explicitly closed.
8. Missing information is not resolved information.
9. Archiving a source block does not retire its active consequence.
10. Freshness is evaluated relative to the current decision.
11. Older information is not automatically irrelevant.
12. A local problem does not automatically invalidate the whole hierarchy.
13. Material revisions preserve provenance.
14. Runtime athlete data remains outside the Skill repository.
15. Storage implementation remains replaceable.
