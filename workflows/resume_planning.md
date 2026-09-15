# Resume Planning Workflow
Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose
This workflow determines where planning currently stands and selects the smallest justified next planning action.
It is the navigation entry before any create_* planning workflow.
The governing principle is:
**RESUME BEFORE CREATE.**
The system first loads continuity state, validates existing plans, and resumes from the lowest appropriate level. It creates a new object only when no valid object exists at that level or a justified revision requires replacement.
The core flow is:
User Request
->
Identify Athlete
->
Load Planning State
->
Check Data Freshness
->
Resolve Active Hierarchy
->
Load Minimum Sufficient Context
->
Validate Existing Plan Assumptions
->
Determine Planning Scope
->
Route to Appropriate Workflow
This workflow does not create the plan it selects.

## Required Interfaces
- [Planning State Schema](../schemas/planning_state.md)
- [Context Summary Schema](../schemas/context_summary.md)
- [Athlete State Schema](../schemas/athlete_state.md)
- [Competition Context Schema](../schemas/competition_context.md)
- [Build Athlete State Workflow](./build_athlete_state.md)
- [Review Training Workflow](./review_training.md)
- [Audit Existing Plan Workflow](./audit_existing_plan.md)
- [Create Cycle Workflow](./create_cycle.md)
- [Create Mesocycle Workflow](./create_mesocycle.md)
- [Create Week Workflow](./create_week.md)
- [Create Session Workflow](./create_session.md)
- [Update Planning State Workflow](./update_planning_state.md)
- [Update Context Summary Workflow](./update_context_summary.md)
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md)
Logical read operations in this workflow are storage-agnostic. Names such as get_planning_state() describe contracts, not implemented code.

## Step 1. Interpret the User Request
Identify:
- athlete;
- requested outcome;
- explicit planning level if stated;
- time horizon;
- whether the request is create, continue, review, revise, or inspect;
- any new evidence or changed constraint;
- urgency;
- whether the user explicitly requests higher-level redesign.
An explicit request to revisit a higher level may expand scope, but the existing structure and consequences should still be loaded before revision.
If athlete identity is unresolved, request only the information needed to select the correct continuity record.

## Step 2. Load Planning State
Conceptually call get_planning_state() for the athlete and horizon.
Load:
- authoritative Planning State version;
- active Cycle reference;
- active Mesocycle reference;
- active Week reference;
- current or pending Session reference;
- last-completed references;
- current Athlete State reference;
- Competition Context reference;
- last Review and Summary references;
- current priorities;
- active constraints;
- Carry-Forward Items;
- invalidation flags;
- next required action;
- updated_at.
If no Planning State exists, do not infer an empty history. Establish whether the athlete is new, the store is incomplete, or continuity must be reconstructed from available active records.

## Step 3. Check Planning-State Authority
Confirm:
- correct athlete and horizon;
- active version;
- no unresolved version conflict;
- status is usable;
- referenced objects exist;
- parent-child references are coherent;
- timestamps and update provenance are available;
- no newer Planning State supersedes the loaded record.
If authority cannot be established, mark the continuity question unresolved and retrieve only the records needed to identify the current version.
Do not choose the most convenient version.

## Step 4. Check Data Freshness
Evaluate freshness relative to the requested decision.
Check:
- Planning State update time;
- current Athlete State effective period;
- Competition Context verification;
- active plan version;
- last Review;
- last Summary;
- relevant Carry-Forward Items;
- recent constraint changes.
Use **CURRENT**, **AGING**, **REVIEW_REQUIRED**, **STALE_FOR_DECISION**, or
**UNKNOWN** when useful.
No universal expiration days are defined.
A Session decision may require very recent tissue and exposure information. A Cycle decision may use older Profile data while requiring a current strategic Athlete State.
If Athlete State is stale for the decision, route first to [Build Athlete State Workflow](./build_athlete_state.md) with the existing State and new evidence.

## Step 5. Resolve the Active Hierarchy
Construct the current hierarchy from references and statuses:
Cycle
->
Mesocycle
->
Week
->
Session
For every level, identify:
- active object;
- status;
- version;
- parent reference;
- last completed object;
- unresolved review or close requirement;
- summary status;
- validity flag.
A null active object and a completed prior object commonly imply the next object may need creation. They do not prove that creation is appropriate before review, summary, and state updates are complete.
### Hierarchy Consistency
Flag inconsistencies such as:
- active child with no valid parent;
- multiple active objects at one level;
- completed object still marked current;
- Session completed but Review missing;
- Week closed without required Summary;
- active pointer referencing a superseded plan;
- next action inconsistent with hierarchy.
Route inconsistent structures to continuity repair or [Update Planning State Workflow](./update_planning_state.md) before planning.

## Step 6. Determine the Pending Close Sequence
Before advancing to the next planning block, check whether the prior block has completed its information cycle.
For a completed Session:
Session Complete
->
Review Training
->
Athlete State Update when needed
->
Week-level continuation
For a closed Week:
Week Execution
->
Week Review
->
Week Summary
->
Athlete State Update
->
Planning State Update
->
Next Week Planning
For a closed Mesocycle or Cycle, require the applicable Review, Summary, Athlete State update, and Planning State pointer update before creating the next level.
Do not route directly from completed Week N to create Week N+1 when required review, state, or summary work is pending.

## Step 7. Load the Hot Context
Default Current or Hot context is:
- Planning State;
- current Athlete State;
- Competition Context;
- active plan references;
- active Carry-Forward Items;
- invalidation flags;
- next required action.
This is the minimum continuity frame for every planning request.
Do not load complete history by default.

## Step 8. Load Level-Appropriate Context
Use progressive retrieval and a decision-specific default.
### Next Session
Default context:
- current Planning State;
- current Athlete State;
- active Week;
- current or pending Session reference;
- latest relevant Session Review;
- active constraints and Carry-Forward Items;
- Competition Context when relevant.
### Next Week
Default context:
- current Planning State;
- current Athlete State;
- active Mesocycle;
- completed current Week Review and Summary;
- previous one or two relevant Week Summaries as an initial range;
- Competition Context;
- active constraints and Carry-Forward Items.
"One or two" is a practical starting range, not a hard rule.
### Next Mesocycle
Default context:
- current Planning State;
- current Athlete State;
- active Cycle;
- previous Mesocycle Summary;
- recent relevant Week Summaries;
- Competition Context;
- active strategic constraints and Carry-Forward Items.
### New Cycle
Default context:
- Athlete Profile;
- current Athlete State;
- previous Cycle Summary;
- latest relevant Mesocycle Summary;
- Competition Context;
- active long-horizon constraints and Carry-Forward Items.
### Existing Plan Review
Load the plan object under review, its assumed Athlete State, relevant Actual Exposure and Review records, and the summaries needed to evaluate its current assumptions.
Default ranges are retrieval starting points. Decision relevance and information sufficiency govern expansion.

## Step 9. Apply Progressive Retrieval
Use:
Default Context
->
Is information sufficient for the current decision?
- Yes: stop retrieval.
- No: retrieve the next deeper relevant historical layer.
->
Reassess sufficiency.
Possible deeper layers are:
1. recent Session records and Reviews;
2. additional Week Summaries;
3. completed Mesocycle Summaries;
4. previous Cycle Summary;
5. selected archived raw records or assessments.
Retrieve the narrowest source set that could resolve the named uncertainty.
Do not load all history because more context might be useful.
## Step 10. Expand Context Only When Triggered
Valid expansion triggers include:
- unresolved contradiction;
- possible recurring injury or tissue pattern;
- uncertain bottleneck history;
- current response conflicts with a recent Summary;
- historical baseline is needed;
- active Mesocycle assumption cannot be evaluated;
- competition planning requires prior competition response;
- suspected repeated failure pattern;
- source correction challenges a Summary;
- current confidence is inadequate for the decision consequence.
For every expansion, record:
- question being resolved;
- next layer requested;
- expected decision value;
- source scope;
- stop condition.
Do not expand because data exist.

## Step 11. Validate Existing Plan Assumptions
Existing does not mean valid.
Before reusing an active plan, check:
- terminal objective remains current;
- Competition Context remains compatible;
- current Athlete State remains within assumed bounds;
- active constraints remain compatible;
- priorities remain applicable;
- current performance problem and Candidate Bottleneck have not materially
  shifted;
- completed exposure and response do not invalidate the intended direction;
- plan version remains authoritative;
- unresolved Carry-Forward Items are represented;
- no higher-consequence flag requires review.
Use [Audit Existing Plan Workflow](./audit_existing_plan.md) when a structured validity review is required.
Permitted validity outputs include:
- **VALID_TO_CONTINUE**;
- **VALID_WITH_LOCAL_UPDATE**;
- **REVIEW_REQUIRED**;
- **PAUSE_REQUIRED**;
- **INVALIDATED**;
- **CANNOT_DETERMINE**.
Blind reuse is prohibited.

## Step 12. Determine the Smallest Justified Planning Scope
Start at the lowest level capable of addressing the request and evidence.
Typical relationships are:
- isolated task or Session issue -> Session or Week;
- repeated Week-level trend -> Week or Mesocycle;
- sustained challenge to Mesocycle hypothesis -> Mesocycle;
- changed competition target or strategic objective -> Cycle;
- stale Athlete State -> Athlete State update before plan revision;
- completed exposure without Review -> Review before next creation.
Escalate only when evidence challenges assumptions owned by a higher level.
A poor day does not by itself justify rebuilding the Cycle.
Record:
- initial scope;
- evidence;
- assumption challenged;
- selected scope;
- reason lower scope is insufficient;
- confidence;
- unresolved alternatives.

## Step 13. Apply Resume Routing
Routing is a conceptual relationship, not a rigid automatic state machine.
### No Authoritative Planning State
Determine whether to:
- build or recover Athlete State;
- reconstruct continuity from existing valid plan records;
- create a new Cycle if no valid Cycle exists.
### No Active Cycle
If prerequisites and Athlete State are sufficient, route to [Create Cycle Workflow](./create_cycle.md).
If a prior Cycle requires closure or summary, complete that first.
### Active Cycle, No Active Mesocycle
If the Cycle is valid and the previous Mesocycle is closed, reviewed, summarized, and reflected in Athlete State, route to [Create Mesocycle Workflow](./create_mesocycle.md).
### Active Cycle and Mesocycle, No Active Week
If parent plans remain valid and the preceding Week close sequence is complete, route to [Create Week Workflow](./create_week.md).
### Active Week, No Current or Pending Session
If the Week remains valid and current Athlete State is sufficient, route to [Create Session Workflow](./create_session.md).
### Completed Session, Review Pending
Route to [Review Training Workflow](./review_training.md).
### Review Complete, State Update Pending
Route to [Build Athlete State Workflow](./build_athlete_state.md) in STATE UPDATE mode.
### Summary Pending
Route to [Update Context Summary Workflow](./update_context_summary.md).
### Planning Pointer Update Pending
Route to [Update Planning State Workflow](./update_planning_state.md).
### Existing Valid Structure
Continue the active plan at the current lowest required level.
### Existing Structure Challenged
Route to Review or revise at the smallest justified level. Permit **REVISE**,
**PAUSE**, **INVALIDATE**, or **SUPERSEDE** when evidence warrants.
### Explicit Higher-Level User Request
Load the relevant active structure and consequences, then route to the requested higher-level review or revision. Do not silently discard lower-level history.

## Step 14. Handle Scope-Escalation Triggers
Potential escalation triggers include:
- competition context materially changed;
- major injury, tissue, or supplied restriction changed;
- Cycle objective changed;
- new evidence challenges the active Mesocycle;
- repeated pattern crosses Week boundaries;
- parent-child inconsistency;
- active plan assumptions no longer support execution;
- user explicitly requests strategic revision.
A trigger requires evaluation; it does not predetermine the final scope.
Preserve local validity where possible. A Cycle may remain valid while its current Week is revised.

## Step 15. Produce the Resume Decision
The Resume Decision should contain:
- athlete and planning horizon;
- authoritative Planning State version;
- resolved active hierarchy;
- current Athlete State reference and freshness;
- Competition Context reference;
- context loaded;
- deeper retrieval performed and why;
- existing-plan validity;
- pending close actions;
- selected planning scope;
- next required action;
- destination workflow;
- prerequisites;
- Carry-Forward Items;
- active invalidation flags;
- uncertainty and confidence.
The output should be sufficient for the destination workflow without dumping the full history.

## Storage-Agnostic Read Contract
A future adapter should be able to support logical retrieval such as:
- get_planning_state();
- get_current_athlete_state();
- get_active_cycle();
- get_active_mesocycle();
- get_current_week();
- get_pending_session();
- get_latest_review();
- get_recent_week_summaries();
- get_previous_mesocycle_summary();
- get_previous_cycle_summary();
- get_archived_records().
These labels do not define real functions, database queries, or Notion API calls. Any storage adapter may implement equivalent behavior.

## Failure Modes
Avoid:
### RECREATE_PLAN_FROM_SCRATCH
Creating a new hierarchy without checking current continuity.
### LOAD_ALL_HISTORY
Loading all raw records before testing minimum context sufficiency.
### STALE_STATE_AS_CURRENT
Using a State without decision-relative freshness validation.
### BLIND_PLAN_REUSE
Continuing an existing plan without validating its assumptions.
### GLOBAL_REPLAN_FOR_LOCAL_PROBLEM
Escalating a local issue beyond the smallest justified level.
### GIANT_CONTEXT_DUMP
Passing full historical detail when a compact decision-relevant handoff is sufficient.
### UNRESOLVED_INFORMATION_LOSS
Allowing an archived source block to hide an active issue.
### NOTION_LOCK_IN
Making routing logic depend on a storage vendor.

## Resume Completion Gate
Resume is complete when:
- athlete and horizon are identified;
- authoritative Planning State is loaded or its absence is resolved;
- active hierarchy and versions are coherent;
- current State and competition references are checked for freshness;
- pending Reviews, Summaries, and State updates are identified;
- hot context is loaded;
- retrieval expanded only when information remained insufficient;
- existing plan assumptions are validated;
- smallest justified planning scope is selected;
- Carry-Forward Items remain visible;
- next required action and destination workflow are explicit;
- no plan has been created inside this workflow.

## Resume Planning Invariants
1. Resume before create.
2. Existing does not automatically mean valid.
3. Planning State and Athlete State remain distinct.
4. Minimum Sufficient Context is the default.
5. More context does not automatically improve a decision.
6. Retrieval stops when information is sufficient.
7. Retrieval expands only to resolve a decision-relevant gap.
8. Old information is not automatically irrelevant.
9. Current unresolved consequences remain in hot state.
10. Completed blocks close through Review, State, Summary, and pointer updates.
11. The smallest justified planning level changes first.
12. Local evidence does not automatically trigger global replanning.
13. Plan versions and hierarchy authority remain explicit.
14. Runtime data remain outside the Skill repository.
15. Storage implementation remains replaceable.
