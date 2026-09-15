# Update Planning State Workflow
Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose
This workflow updates the persistent record of where planning currently stands after a planning, training, review, Athlete State, competition, constraint, or summary event.
It maintains authoritative hierarchy pointers, statuses, versions, next action, freshness, and Carry-Forward Items.
It does not create training plans, construct Athlete State, analyze a training event, or generate a Context Summary.

## Required Interfaces
- [Planning State Schema](../schemas/planning_state.md)
- [Context Summary Schema](../schemas/context_summary.md)
- [Athlete State Schema](../schemas/athlete_state.md)
- [Competition Context Schema](../schemas/competition_context.md)
- [Resume Planning Workflow](./resume_planning.md)
- [Build Athlete State Workflow](./build_athlete_state.md)
- [Review Training Workflow](./review_training.md)
- [Update Context Summary Workflow](./update_context_summary.md)
Logical operations such as save_planning_state() describe storage contracts, not implemented functions.

## Supported Update Events
The workflow supports at least:
- **PLAN_CREATED**;
- **PLAN_ACTIVATED**;
- **PLAN_COMPLETED**;
- **PLAN_PAUSED**;
- **PLAN_INVALIDATED**;
- **PLAN_SUPERSEDED**;
- **SESSION_COMPLETED**;
- **REVIEW_COMPLETED**;
- **ATHLETE_STATE_UPDATED**;
- **SUMMARY_CREATED**;
- **SUMMARY_REVISED**;
- **COMPETITION_CONTEXT_CHANGED**;
- **CONSTRAINT_CHANGED**.
An event may affect several pointers, but each effect must remain explicit.

## Step 1. Load the Authoritative Planning State
Retrieve:
- current Planning State version;
- athlete and horizon;
- active hierarchy;
- last-completed hierarchy;
- current Athlete State reference;
- current Competition Context reference;
- priority references;
- active constraints;
- active uncertainties;
- Carry-Forward Items;
- Review and Summary references;
- invalidation flags;
- next required action.
Verify the record has not been superseded by a newer version.
If authority is unresolved, stop the update and route to continuity resolution. Do not write over an uncertain current version.

## Step 2. Validate the Update Event
Record:
- event identifier;
- event type;
- event time;
- source object;
- source version;
- affected athlete and horizon;
- affected planning level;
- source workflow or decision;
- evidence or completion record;
- requested state changes.
Confirm the event belongs to the loaded Planning State.
A plan status does not change solely because a user-facing label resembles an event. Use the authoritative source record.

## Step 3. Determine What Changed
For every proposed change, identify:
- prior value;
- new value;
- affected field;
- source;
- reason;
- planning consequence;
- confidence;
- unresolved conflict.
Check:
- which planning level changed;
- whether parent or child status needs review;
- what becomes current;
- what becomes historical;
- what next action follows;
- which Carry-Forward Items remain active;
- what uncertainty appeared;
- whether existing plans remain valid.
Unrelated fields should remain unchanged.

## Step 4. Update Planning-Level Status
Apply status semantics from the Planning State Schema:
- **DRAFT**: defined but not authoritative for execution;
- **ACTIVE**: currently guides decisions;
- **COMPLETED**: normally closed under applicable criteria;
- **PAUSED**: temporarily suspended;
- **SUPERSEDED**: replaced by a newer retained version;
- **INVALIDATED**: assumptions no longer justify continued use.
Do not require every planning object to follow the same lifecycle.
### PLAN_CREATED
Add the new object reference with DRAFT or the explicitly justified initial status. Do not displace an active version silently.
### PLAN_ACTIVATED
Set the selected version ACTIVE and resolve competing active pointers. If it replaces another version, mark the prior object SUPERSEDED with provenance.
### PLAN_COMPLETED
Mark the object COMPLETED only when its applicable completion gate is met. Record pending Review, Summary, Athlete State, or pointer updates.
### PLAN_PAUSED
Retain the object reference, reason, effective time, affected children, and resume condition.
### PLAN_INVALIDATED
Record the invalidated assumption, evidence, affected scope, and required review. Preserve the object as history.
### PLAN_SUPERSEDED
Point to the new authoritative version and preserve the prior version and replacement relationship.

## Step 5. Update Hierarchy Pointers
Update only justified pointers:
- active Cycle;
- active Mesocycle;
- active Week;
- current or pending Session;
- last completed Cycle;
- last completed Mesocycle;
- last completed Week;
- last completed Session.
Maintain parent-child coherence.
A completed child may move to last-completed while its active pointer becomes null. A parent may remain ACTIVE.
Do not let a create workflow guess chronology that Planning State can state explicitly.
### Pointer Example
Week 07 COMPLETED
->
Week 07 Summary generated
->
Athlete State updated
->
Planning State update:
- last_completed_week = Week 07;
- active_week = null;
- next_required_action = CREATE_NEXT_WEEK.
[Resume Planning Workflow](./resume_planning.md) can then route to Create Week.

## Step 6. Reconcile Parent and Child Status
Check:
- whether a completed child closes or merely advances its parent;
- whether a paused or invalidated parent prevents child activation;
- whether a superseded parent requires child review;
- whether an active child still belongs to the authoritative parent version;
- whether a new parent version changes lower-level assumptions.
Do not cascade status mechanically.
A Session problem does not automatically invalidate the Week, Mesocycle, or Cycle. Escalation follows the smallest justified planning-level update.

## Step 7. Update Athlete State Reference
On **ATHLETE_STATE_UPDATED**, record:
- new Athlete State reference and version;
- prior reference;
- effective date;
- information-sufficiency status;
- Planning Readiness;
- confidence reference;
- changed dimensions;
- freshness;
- next State review trigger.
Evaluate whether the new State challenges any active plan assumption. If so, create an invalidation or review flag at the smallest justified level.
This workflow stores the pointer and consequence. It does not reconstruct Athlete State.

## Step 8. Update Review References
On **SESSION_COMPLETED**, record:
- last completed Session;
- Actual Exposure record reference when available;
- Review pending status;
- next required action = REVIEW_COMPLETED_SESSION unless a higher-consequence
  action takes precedence.
On **REVIEW_COMPLETED**, record:
- last completed Review;
- reviewed object;
- Decision State;
- Decision Scope;
- Athlete State update need;
- Summary update need;
- unresolved questions;
- next observation need.
Review completion does not automatically mean Athlete State and Summary are current.

## Step 9. Update Summary References
On **SUMMARY_CREATED**, record:
- summary level;
- summarized object;
- active summary reference;
- version;
- creation time;
- source scope;
- Carry-Forward candidates;
- archive-context transition.
On **SUMMARY_REVISED**, record:
- new active summary version;
- superseded prior version;
- revision reason;
- changed meaning;
- new evidence;
- whether Athlete State or plan validity requires review.
Do not silently replace a historical interpretation.

## Step 10. Update Competition and Constraint References
On **COMPETITION_CONTEXT_CHANGED**, record:
- new Competition Context reference and version;
- changed event, date, role, or constraint;
- affected planning levels;
- freshness;
- plan assumptions requiring validation;
- next action.
On **CONSTRAINT_CHANGED**, update:
- active constraint record;
- source;
- affected decisions;
- effective period;
- confidence;
- status;
- associated invalidation flag;
- review trigger.
Resolved constraints require explicit resolution. Missing information is not resolution.

## Step 11. Reconcile Carry-Forward Items
For every existing and proposed item, determine:
- still active;
- resolved;
- invalidated;
- superseded;
- transferred to Current Athlete State;
- transferred to another continuity owner;
- newly created.
Carry forward:
- Active Constraint;
- Active Tissue Concern;
- Unresolved Uncertainty;
- Current Bottleneck Hypothesis;
- Competition Deadline;
- Important Benchmark;
- Open Decision Question;
- unresolved measurement issue;
- recurring response pattern.
Each exit requires status, reason, time, and source.
Closing or archiving the source Week does not close an active consequence.

## Step 12. Update Invalidation Flags
Add, retain, or clear flags for:
- stale Athlete State;
- changed competition objective;
- major constraint change;
- active tissue restriction;
- challenged Mesocycle hypothesis;
- changed Cycle objective;
- hierarchy inconsistency;
- version conflict;
- Review pending;
- Summary pending;
- plan assumption no longer supported.
A flag should identify its affected object and smallest likely review scope.
Clear it only when a referenced decision or evidence resolves it.

## Step 13. Determine the Next Required Action
Consider:
- event completed;
- hierarchy position;
- pending Review;
- pending Athlete State update;
- pending Summary;
- plan validity;
- Carry-Forward Items;
- information gaps;
- competition deadline;
- parent and child status.
Possible actions include:
- BUILD_OR_UPDATE_ATHLETE_STATE;
- REVIEW_COMPLETED_SESSION;
- UPDATE_CONTEXT_SUMMARY;
- CREATE_NEXT_SESSION;
- CREATE_NEXT_WEEK;
- CREATE_NEXT_MESOCYCLE;
- CREATE_NEW_CYCLE;
- CONTINUE_EXISTING_PLAN;
- REVISE_EXISTING_PLAN;
- REQUEST_INFORMATION;
- REQUEST_ASSESSMENT;
- PAUSE_FOR_EXTERNAL_ASSESSMENT;
- RESUME_PLANNING.
State prerequisites and blockers.
The next action is explicit so a later Agent run does not infer it from all historical records.

## Step 14. Create a New Planning State Version
When material meaning changes, create a new version containing:
- previous version;
- event;
- changed fields;
- rationale;
- pointers added, changed, or retired;
- statuses changed;
- Carry-Forward changes;
- invalidation flags;
- next action;
- updated_at;
- unresolved conflicts.
Do not silently overwrite material continuity history.
Minor corrections that do not change planning meaning may use a proportionate correction record.

## Step 15. Persist and Route
Conceptually save_planning_state() through the active external adapter.
Confirm:
- new version is retrievable;
- previous version remains traceable;
- active authority is unambiguous;
- references resolve;
- runtime data were not written into the Skill repository.
Route to [Resume Planning Workflow](./resume_planning.md) when another planning or continuity action remains.
This workflow does not call a vendor-specific API.

## Event-to-Update Summary
| Event | Primary continuity effect |
|---|---|
| PLAN_CREATED | Add versioned plan reference. |
| PLAN_ACTIVATED | Set authoritative active pointer. |
| PLAN_COMPLETED | Move object toward last-completed and start close sequence. |
| PLAN_PAUSED | Retain pointer with pause reason and resume condition. |
| PLAN_INVALIDATED | Preserve history and require scoped revision. |
| PLAN_SUPERSEDED | Point to replacement and retain prior version. |
| SESSION_COMPLETED | Record completion and require Review. |
| REVIEW_COMPLETED | Store Review reference and required State or Summary action. |
| ATHLETE_STATE_UPDATED | Advance current State pointer and reassess plan validity. |
| SUMMARY_CREATED | Add active summary and archive-context transition. |
| SUMMARY_REVISED | Advance summary version and reassess affected meaning. |
| COMPETITION_CONTEXT_CHANGED | Update context pointer and validate affected plans. |
| CONSTRAINT_CHANGED | Update active constraint and affected scope. |

## Failure Modes
Avoid:
- implicit pointer changes;
- multiple authoritative active versions;
- marking completed before required close work;
- treating Summary creation as Athlete State update;
- removing Carry-Forward Items because their source was archived;
- cascading local invalidation globally without evidence;
- silent version overwrite;
- vendor-specific persistence logic;
- making create_* workflows infer the current sequence.

## Completion Gate
The update is complete when:
- the authoritative prior version was verified;
- source event and affected scope are explicit;
- hierarchy pointers are coherent;
- statuses use defined semantics;
- current and historical references are distinct;
- Athlete State, Review, Summary, Competition, and constraint references are
  updated where required;
- Carry-Forward Items are reconciled;
- invalidation flags are current;
- next required action is explicit;
- a material revision preserves provenance;
- the new version is ready for external persistence;
- routing back to Resume Planning is stated when needed.

## Planning State Update Invariants
1. Planning State changes follow an identifiable event.
2. Planning State and Athlete State remain distinct.
3. Pointer updates do not rewrite referenced records.
4. Parent and child status changes are evaluated, not mechanically cascaded.
5. Completed does not mean reviewed, summarized, and state-updated.
6. Carry-Forward Items remain active until explicitly closed.
7. Missing information is not resolution.
8. A local problem does not automatically cause global replanning.
9. The smallest justified level changes first.
10. Material updates create traceable versions.
11. Prior versions remain historical evidence.
12. The next required action is explicit.
13. Runtime records remain outside the Skill repository.
14. Storage implementation remains replaceable.
