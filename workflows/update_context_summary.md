# Update Context Summary Workflow
Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose
This workflow creates, promotes, revises, and closes structured Context Summaries while preserving raw records and historical provenance.
It determines:
- when a Summary is needed;
- which source scope it represents;
- what information earns promotion;
- how State Delta and trends are compressed;
- which unresolved items carry forward;
- how prior Summary versions remain traceable;
- when lower-level detail leaves default context.
It does not delete athlete history, analyze every Session again, construct Athlete State, or implement a storage vendor.
Compression is not deletion.

## Required Interfaces
- [Context Summary Schema](../schemas/context_summary.md)
- [Planning State Schema](../schemas/planning_state.md)
- [Athlete State Schema](../schemas/athlete_state.md)
- [Review Training Workflow](./review_training.md)
- [Build Athlete State Workflow](./build_athlete_state.md)
- [Update Planning State Workflow](./update_planning_state.md)
- [Resume Planning Workflow](./resume_planning.md)
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md)
Logical operations such as save_summary() and get_archived_records() describe storage contracts, not current functions or API calls.

## Supported Summary Events
### WEEK_CLOSE
Create or update a Week Summary after Week execution and relevant Review information are complete enough for the next decision.
### MESOCYCLE_CLOSE
Create a Mesocycle Summary after its constituent Weeks, State changes, and exit reason can be represented.
### CYCLE_CLOSE
Create a strategic Cycle Summary after competition outcomes, major State changes, and Cycle closure information are available.
### SUMMARY_REVISION
Create a new Summary version when new evidence, correction, or changed interpretation materially changes historical or decision meaning.
### MANUAL_SUMMARY_REFRESH
Permit a justified refresh when a current decision requires the Summary to incorporate available records that were not previously material.
Do not create a long-horizon Summary after every Session by default.

## Continuity Close Sequence
The default continuity sequence is:
Session Complete
->
Review Training or Detailed Record
->
Week Close
->
Week Summary
->
Athlete State Update
->
Planning State Update
->
Next Week Planning
At higher levels:
Mesocycle Close
->
Mesocycle Summary
->
Athlete State and Planning State Updates
->
Next Mesocycle Decision
Cycle Close
->
Cycle Summary
->
Final Athlete State and Planning State Updates
->
Next Cycle Decision
The exact order may reflect dependency: a Summary may consume an updated Athlete State reference, or its State Delta may support that update. The Planning State must record which products remain pending.
Do not advance directly from Week N execution to Week N+1 creation while required Review, State, Summary, or pointer work remains unfinished.

## Step 1. Identify the Summary Event
Record:
- event type;
- athlete;
- summarized planning object;
- planning level;
- parent object;
- source time span;
- trigger;
- current Summary reference if any;
- requested operation: create, refresh, or revise;
- decision that will consume the Summary.
Confirm that the source planning block exists. Do not summarize an inferred block.

## Step 2. Load the Existing Continuity Context
Retrieve:
- current Planning State;
- current and prior Athlete State references;
- active or closing plan object;
- current Summary version if any;
- lower-level Summaries;
- relevant Session Reviews;
- Competition Context;
- Carry-Forward Items;
- invalidation flags;
- source corrections or new evidence.
Use minimum sufficient source scope. Do not load the full archive by default.

## Step 3. Define and Verify Source Scope
Record:
- included source record references;
- excluded records and why;
- time boundary;
- plan versions represented;
- Review completeness;
- measurement and assessment references;
- known gaps;
- conflicting sources;
- source freshness;
- source quality.
A Summary must not imply coverage beyond its source scope.
If missing sources prevent the intended Summary claim, mark the field Missing or the Summary provisional. Do not invent continuity.

## Step 4. Compare Intended and Actual
For the summarized block, compare:
- intended objective or adaptation problem;
- planned priorities;
- planned key exposures;
- expected response;
- Actual Exposure;
- Achieved Quality;
- actual sequence;
- observed response;
- plan deviations;
- competition exposure;
- changed constraints.
Prescription remains distinct from Actual Exposure.
A deviation is recorded before it is interpreted as success, failure, or cause.

## Step 5. Extract State-Changing Evidence
Identify evidence that changed or may change:
- Current Performance State;
- Current Performance Problem;
- Candidate Bottleneck;
- priority;
- Fatigue and Recovery State;
- Tissue State;
- Technical State;
- Exposure State;
- Adaptation Trend;
- Competition Readiness;
- Active Constraints;
- confidence.
For each candidate change, record source, time, direction, relevance, alternative explanations, confidence, and affected decision.
Do not recreate Athlete State inside the Summary. Record State Delta and reference the authoritative State versions.

## Step 6. Identify Repeated Trends
A trend may be supported by repeated or convergent evidence across comparable events.
Check:
- performance direction;
- expected versus observed response;
- recovery pattern;
- tissue response;
- technical or execution consistency;
- exposure tolerance;
- transfer evidence;
- recurring constraint effect;
- repeated failure classification.
Record source events, context, comparability, exceptions, alternatives, confidence, and decision relevance.
No fixed number of occurrences establishes a trend.
One small fluctuation usually remains at Session or Week level. A high-consequence exception may be promoted without being mislabeled a trend.

## Step 7. Identify Important Exceptions
Retain an isolated event when it materially changes:
- current Athlete State;
- safety or tissue availability;
- plan validity;
- competition participation;
- constraint;
- confidence;
- next decision.
Record the event as an exception, its context, immediate consequence, unresolved meaning, and whether it should carry forward.
Do not generalize from one exception beyond the evidence.

## Step 8. Preserve Uncertainty and Conflict
For each compressed claim, preserve:
- Known, Measured, Reported, Derived, or Estimated status;
- Missing or Unknown;
- Provisional interpretation;
- competing explanations;
- Conflict;
- Unresolved;
- Cannot Determine;
- qualitative confidence.
Conflicting sources remain visible. Do not average them into a false conclusion.
Compression must not increase certainty merely because detail is removed.

## Step 9. Determine Carry-Forward Items
Ask whether information remains decision-relevant after the summarized block closes.
Carry-forward candidates include:
- Active Constraint;
- Active Tissue Concern;
- Unresolved Uncertainty;
- Current Bottleneck Hypothesis;
- Competition Deadline;
- Important Benchmark;
- Open Decision Question;
- unresolved measurement issue;
- recurring response pattern;
- promised review condition.
For each candidate, record source, current relevance, affected decision, confidence, next trigger, proposed owner, and exit condition.
Old but active consequences should move into Current Athlete State or Planning State Carry-Forward Items. They should not survive only through deep retrieval.

## Step 10. Create the State Delta
Represent:
- initial Athlete State reference;
- final or current Athlete State reference;
- dimensions changed;
- dimensions unchanged despite expected change;
- new constraints;
- retired constraints;
- confidence changes;
- bottleneck evolution;
- unresolved attribution;
- source evidence.
State Delta is not a replacement for either Athlete State version.

## Step 11. Create Decision Implications
State what the Summary changes for:
- next planning level;
- priority;
- plan validity;
- Competition Context;
- required Review;
- information need;
- additional assessment;
- Carry-Forward State;
- retrieval needs;
- confidence.
If no higher-level decision implication exists, the information may remain Archive Only.
Do not generate the next plan inside this workflow.

## Step 12. Generate the Level-Appropriate Summary
### Week Summary
Include:
- Week identity and parent Mesocycle;
- Weekly Intent;
- planned and Actual key exposures;
- important deviations;
- performance trend;
- recovery and fatigue trend;
- tissue response;
- technical or execution trend;
- priority and constraint changes;
- Athlete-State Delta;
- important exceptions;
- unresolved questions;
- Decision Outcome;
- implications for next Week;
- confidence and source references.
Generate at WEEK_CLOSE when relevant Review information is sufficient. If not, mark the Summary provisional or retain a pending state.
### Mesocycle Summary
Include:
- initial adaptation problem and Athlete State;
- desired State change;
- priority structure;
- major exposure strategy;
- what changed and did not change;
- performance trend;
- bottleneck and priority evolution;
- recovery and tissue pattern;
- transfer evidence;
- major deviations and decisions;
- unresolved issues;
- exit reason;
- final Athlete-State Delta;
- implications for the next Mesocycle;
- confidence and source references.
Generate at MESOCYCLE_CLOSE. Do not reproduce every Week.
### Cycle Summary
Include:
- terminal objective;
- initial strategic State;
- major strategic priorities;
- competition structure;
- major Mesocycle sequence;
- key Athlete-State and performance changes;
- bottleneck and constraint changes;
- competition outcomes;
- major decision revisions;
- what appeared to work;
- what remained unresolved;
- important historical lessons;
- final Athlete State;
- implications for the next Cycle;
- confidence and source references.
Generate at CYCLE_CLOSE. Keep strategic resolution rather than weekly detail.
## Step 13. Decide Promotion Versus Archive Only
For each material item, ask whether it changes:
- Athlete State;
- priority;
- constraint;
- confidence;
- Candidate Bottleneck;
- competition planning;
- next decision;
- long-term risk.
If all are substantially no and no unresolved consequence exists, classify the item **Archive Only**.
Promotion level depends on planning level, decision relevance, recurrence, convergence, and current consequence.
It does not depend on fixed elapsed days.

## Step 14. Version the Summary
For a new Summary, record:
- summary_id;
- version;
- status;
- source scope;
- created_at;
- authoring process.
For a material revision, record:
- previous_version;
- new version;
- revision_reason;
- new_evidence;
- changed_fields;
- source changes;
- updated_at;
- impact on State, plan validity, or next decision.
Mark the prior version **SUPERSEDED** and the new version **ACTIVE** when the revision becomes authoritative.
Do not silently overwrite historical interpretation.
A non-semantic typographic correction may use a proportionate correction record.

## Step 15. Prevent Hindsight Rewrite
Separate:
- **Known Then**;
- **Interpreted Then**;
- **Learned Later**;
- **Current Revision**;
- **Revision Reason**.
If later evidence suggests an earlier fatigue interpretation was more likely a measurement issue:
- preserve the original measurement and conditions;
- preserve the original interpretation and confidence;
- attach later evidence;
- create the revised interpretation;
- record when and why it changed.
Do not represent later knowledge as available to the earlier decision.
This preserves evaluation of Ex Ante Decision Quality separately from Ex Post Outcome.

## Step 16. Move Lower-Level Detail Out of Default Context
After an active Summary is saved and verified:
- retain raw records;
- retain Session Reviews;
- retain lower-level plans;
- retain source assessments;
- keep references resolvable;
- remove completed lower-level detail from default hot context when it has no
  unresolved current consequence;
- preserve promoted Carry-Forward Items in hot state.
The lifecycle is:
Raw Record
->
Structured Review
->
Summary
->
Archive or Cold Context
Archive is a retrieval state, not deletion.
Recent detailed data remain default high resolution. Older completed blocks are normally read through Summaries. Archived detail is retrieved only for a decision-relevant reason.

## Step 17. Update Planning State References
Provide [Update Planning State Workflow](./update_planning_state.md) with:
- summary event;
- summarized object;
- active Summary reference;
- version;
- prior version when revised;
- creation or revision time;
- Carry-Forward candidates;
- archive-context transition;
- unresolved issues;
- next decision implications;
- State update need;
- plan validity implication.
Planning State then records the authoritative pointer and next required action.
This workflow does not directly alter hierarchy pointers without the Planning State update contract.

## Step 18. Persist Through a Replaceable Adapter
Conceptually call save_summary() through the active external persistence adapter.
Confirm:
- Summary is retrievable;
- version authority is unambiguous;
- source references resolve;
- prior versions remain traceable;
- raw records remain retained;
- archive status is represented;
- runtime data were not written into the Skill repository.
No Notion API, SQL, or vendor database design is implemented here.
A future first adapter may use Notion or another external store. The Skill defines schema, read contract, update contract, and compression logic.

## Historical Retrieval Strategy
Use:
- recent detailed data -> default high resolution;
- older completed planning blocks -> Summary resolution;
- deep archive -> retrieval only when the current decision requires it.
Valid deep-retrieval reasons include:
- unresolved contradiction;
- historical baseline;
- recurring tissue pattern;
- uncertain bottleneck history;
- prior competition response;
- suspected repeated failure;
- correction of a source record;
- evaluation of a challenged Summary.
Old does not equal irrelevant. Relevance may bring archived evidence back into the decision context.

## Data Retention Boundary
The continuity system does not automatically delete athlete history.
Potential future deletion candidates may include temporary cache, duplicate derived artifacts, reconstructable intermediate files, or records explicitly selected under user-authorized data governance.
Deletion policy belongs to a future persistence and data-governance layer.
This workflow archives; it does not delete.

## Storage-Agnostic Operations
A future adapter may provide behavior equivalent to:
- get_planning_state();
- get_current_athlete_state();
- get_source_records();
- get_session_reviews();
- get_recent_week_summaries();
- get_previous_mesocycle_summary();
- get_previous_cycle_summary();
- get_archived_records();
- save_summary();
- supersede_summary();
- archive_from_default_context();
- save_planning_state().
These are conceptual interface names. They are not code and do not constrain the storage technology.

## Review Training Boundary
[Review Training Workflow](./review_training.md) produces event-level analysis:
- Actual Exposure;
- response;
- interpretation;
- Decision State;
- Decision Scope;
- unresolved questions.
This workflow uses those records for cross-event compression.
Review and Summary remain distinct:
- Review asks what happened and what it means at the reviewed event or scope.
- Summary asks what persisted, changed State, matters to a higher decision, or
  remains unresolved across source records.
Do not replace Review with Summary.

## Build Athlete State Boundary
[Build Athlete State Workflow](./build_athlete_state.md) constructs or updates the current Athlete State.
This workflow records State Delta, relevant trends, and implications. It does not redefine or independently replace the authoritative State.
If Summary evidence requires a State update, route to Build Athlete State and then reference the resulting version.

## Failure Modes
Avoid:
### DELETE_AFTER_SUMMARY
Raw data remain archived and traceable.
### SUMMARY_AS_RAW_DATA
A Summary cannot replace source evidence for questions requiring detail.
### SUMMARY_CERTAINTY_INFLATION
Uncertain input remains uncertain in compressed form.
### HISTORY_REWRITE
Later evidence produces a revision rather than silent historical replacement.
### FIXED_TIME_ONLY_COMPRESSION
Planning level, relevance, and recency jointly govern resolution.
### UNRESOLVED_INFORMATION_LOSS
Active consequences move into State or Carry-Forward Items.
### GIANT_CONTEXT_DUMP
A Summary selects decision-relevant information rather than repeating all input.
### NOTION_LOCK_IN
Summary logic remains independent of the persistence adapter.
### DATABASE_IMPLEMENTATION_INSIDE_SKILL
No database schema, query, or vendor API belongs in this workflow.

## Summary Completion Gate
A Summary operation is complete when:
- event and summarized object are explicit;
- source scope and gaps are visible;
- intended and Actual Exposure are distinguished;
- State-changing evidence is extracted;
- trends and exceptions are distinguished;
- uncertainty and conflict remain visible;
- carry-forward candidates are identified;
- State Delta and next-decision implications are stated;
- resolution matches Week, Mesocycle, or Cycle level;
- material revision preserves prior version and reason;
- hindsight perspective is separated;
- raw records remain retained and traceable;
- lower-level detail leaves default context only after Summary verification;
- Planning State update input is produced;
- no athlete history is automatically deleted;
- storage implementation remains replaceable.

## Context Summary Update Invariants
1. Compression does not equal deletion.
2. Raw Record, Review, Summary, and Current State remain distinct.
3. Summary resolution follows planning level, relevance, and recency.
4. No fixed day count causes forgetting or deletion.
5. Important unresolved information carries forward.
6. Repeated trends require contextual evidence, not a universal count.
7. High-consequence exceptions may be promoted without becoming trends.
8. Compression preserves Missing, Conflict, Unresolved, and confidence.
9. Summary revision creates provenance rather than rewriting history.
10. Later knowledge remains distinguishable from what was known then.
11. Estimate does not become Measurement.
12. Archived data remain retrievable.
13. Older information is not automatically irrelevant.
14. Summary generation does not create the next plan.
15. Runtime data remain outside the Skill repository.
16. Persistence implementation remains replaceable.
