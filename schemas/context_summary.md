# Context Summary Schema
Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose
A Context Summary is structured compression of completed planning and training information for future decisions.
It answers:
- What was intended?
- What actually happened?
- What changed?
- What meaningful trend appeared?
- What matters for the next decision?
- What remains unresolved?
A summary is decision-relevant state compression. It is not an arbitrary natural-language recap, a raw-data replacement, or the current Athlete State.
The core transformation is:
Previous State
+
New Evidence
->
State Delta
+
Important Exceptions
+
Decision-Relevant Trends
+
Unresolved Issues
+
Next Decision Implications

## 1. Summary Identity
Every summary should support:
| Field | Meaning |
|---|---|
| summary_id | Stable identifier. |
| summary_level | Session Review, Week, Mesocycle, or Cycle. |
| summarized_object | Planning block or event represented. |
| athlete_reference | Athlete whose history is summarized. |
| parent_reference | Parent planning object when applicable. |
| source_scope | Included source records and boundaries. |
| status | DRAFT, ACTIVE, SUPERSEDED, or INVALIDATED. |
| version | Current summary version. |
| previous_version | Prior version when revised. |
| created_at | Initial creation time. |
| updated_at | Most recent material revision time. |
| authoring_process | Workflow or process that created the summary. |
| storage_reference | Adapter-neutral external persistence reference. |
The summary must identify its time span and source scope. A reader should know what is included and excluded.

## 2. Summary Levels
### 2.1 Session-Level Record and Review
Session raw records preserve the highest resolution:
- prescription;
- Actual Exposure;
- Achieved Quality;
- conditions;
- immediate observations;
- delayed observations where attached;
- source measurements.
[Review Training Workflow](../workflows/review_training.md) produces event-level analysis.
A second Session Summary is not required by default when the Session Review already provides a compact, structured, traceable record.
Session Review is not a Week Summary. It analyzes one event or review object rather than compressing a cross-event pattern.
### 2.2 Week Summary
A Week Summary compresses the completed Week and its relevant reviews for the next Week or higher-level decision.
### 2.3 Mesocycle Summary
A Mesocycle Summary compresses state change, priority evolution, response, transfer evidence, and unresolved issues across the completed Mesocycle.
### 2.4 Cycle Summary
A Cycle Summary preserves strategic history: objective, major sequence, competition results, important state changes, major revisions, and lessons relevant to a future Cycle.
Higher summary level means broader decision scope and lower default resolution. It does not mean lower evidential care.

## 3. Shared Summary Semantics
### 3.1 Information Status
Summary fields may use:
- **Known**;
- **Measured**;
- **Reported**;
- **Derived**;
- **Estimated**;
- **Provisional**;
- **Conflict**;
- **Unresolved**;
- **Missing**;
- **Not Applicable**.
Compression must not upgrade uncertainty. Missing is not resolved, and Estimated is not Measured.
### 3.2 Confidence
Use claim-specific qualitative confidence consistent with source quality, comparability, recency, convergence, and consequence of error.
A summary may contain strong confidence in Actual Exposure and unresolved confidence in causal interpretation.
### 3.3 Source References
Every material claim should be traceable to one or more:
- raw record;
- plan version;
- Session Review;
- measurement or assessment;
- Athlete State version;
- decision record;
- lower-level summary;
- competition record;
- supplied constraint or report.
The summary selects and organizes evidence. It does not sever provenance.
### 3.4 Missing Fields
Not every field must contain data. Use Missing, Unknown, or Not Applicable rather than inventing content for structural completeness.

## 4. Compression Logic
Compression should retain information that changes:
- Athlete State;
- priority;
- constraint;
- confidence;
- Candidate Bottleneck;
- competition planning;
- next decision;
- long-term risk;
- plan validity.
If an item changes none of these and has no unresolved consequence, it may be
**Archive Only**.
Compression does not reproduce every input in shorter words.
### 4.1 State Delta
State Delta records:
- prior State reference;
- final or updated State reference;
- dimensions changed;
- direction and practical meaning of change;
- dimensions expected to change but unchanged;
- confidence change;
- source evidence;
- unresolved attribution.
### 4.2 Important Exception
An exception is an event that is materially relevant despite not forming a trend.
Examples include a high-consequence tissue warning, major execution failure, competition disruption, unusual exposure, or measurement correction.
Exceptions retain context and should not be converted automatically into a persistent trend.
### 4.3 Decision-Relevant Trend
A trend requires repeated or convergent evidence sufficient for the stated claim.
Record:
- trend target;
- observation window;
- source events;
- comparability;
- direction;
- alternative explanations;
- confidence;
- decision implication.
No universal occurrence threshold is defined.
### 4.4 Unresolved Issue
An unresolved issue records:
- question or conflict;
- source evidence;
- competing explanations;
- decision affected;
- consequence of error;
- current confidence;
- carry-forward need;
- next review or information trigger.
Unresolved issues do not disappear when lower-level records leave default context.

## 5. Week Summary
### 5.1 Identity and Scope
Support:
- Week identity;
- parent Mesocycle;
- Week version;
- date range;
- source Session and Review references;
- created_at;
- summary version and status.
### 5.2 Intended and Actual Work
Represent:
- Weekly Intent;
- planned key exposures;
- Actual key exposures;
- Achieved Quality;
- important plan deviations;
- omitted or substituted exposures;
- competition exposure when applicable.
Prescription and Actual Exposure remain distinct.
### 5.3 Response and Trend
Represent when supported:
- performance trend;
- recovery and fatigue trend;
- tissue response;
- technical or execution trend;
- exposure tolerance;
- expected versus observed response;
- relevant measurement change.
Single fluctuations may remain exceptions or unresolved observations.
### 5.4 Priority and Constraint Status
Include:
- priority status and material change;
- constraint changes;
- active tissue concern;
- competition deadline change;
- assumption or validity challenge.
### 5.5 State and Decision Output
Include:
- Athlete-State Delta;
- important exceptions;
- unresolved questions;
- Decision Outcome;
- implications for next Week;
- escalation implication;
- confidence and uncertainty;
- carry-forward candidates.
Do not require every field to contain data.

## 6. Mesocycle Summary
### 6.1 Starting Structure
Represent:
- Mesocycle identity and parent Cycle;
- initial adaptation problem;
- initial Athlete State;
- desired State change;
- initial Candidate Bottleneck hypotheses;
- priority structure;
- major exposure strategy;
- initial constraints and uncertainty.
### 6.2 Actual Development
Represent:
- what actually changed;
- what did not change;
- performance trend;
- bottleneck evolution;
- priority evolution;
- recovery and tissue pattern;
- technical or execution development;
- transfer evidence;
- major deviations;
- important decisions and revisions.
Supporting adaptation does not establish competitive transfer without relevant evidence.
### 6.3 Close and Handoff
Represent:
- exit reason;
- completion, pause, invalidation, or supersession status;
- final Athlete-State Delta;
- remaining constraints;
- unresolved issues;
- implications for next Mesocycle;
- Cycle-level implications;
- carry-forward items;
- confidence and uncertainty;
- source references;
- version.
The Mesocycle Summary should not reproduce every Week.
## 7. Cycle Summary
### 7.1 Strategic Starting Point
Represent:
- Cycle identity and version;
- terminal objective;
- initial strategic Athlete State;
- major strategic priorities;
- competition structure;
- planned Mesocycle sequence;
- initial constraints and uncertainty.
### 7.2 Strategic Development
Represent:
- key Athlete-State changes;
- competitive 100m performance development;
- important bottleneck changes;
- important constraint changes;
- actual major Mesocycle sequence;
- competition outcomes;
- major decision revisions;
- what appeared to work;
- evidence that supports that interpretation;
- what did not change;
- what remained unresolved.
"What appeared to work" remains evidence-bounded. Outcome alone does not prove decision quality or causation.
### 7.3 Strategic Handoff
Represent:
- final Athlete State reference;
- major historical lessons;
- unresolved strategic questions;
- persistent risk or constraint;
- implications for the next Cycle;
- benchmarks worth retaining;
- carry-forward items;
- confidence and uncertainty;
- source references;
- summary version.
A Cycle Summary remains strategic. It should not list every weekly detail.

## 8. Summary Promotion
Information moves to a higher summary level when it changes or may continue to change:
- Athlete State;
- priority;
- constraint;
- confidence;
- bottleneck hypothesis;
- competition planning;
- next decision;
- long-term risk.
### 8.1 Isolated Signal
A small isolated fluctuation usually remains at Session or Week resolution.
An isolated high-consequence exception may be promoted without being labeled a trend.
### 8.2 Repeated or Convergent Evidence
Repeated or convergent evidence may justify promotion:
- repeated similar tissue response across Weeks;
- persistent performance deviation;
- recurring execution problem;
- repeated conflict between expected and observed response;
- stable change in a Candidate Bottleneck hypothesis.
No fixed occurrence count establishes promotion.
### 8.3 Cross-Level Persistence
Information recurring across Mesocycles may become Cycle-level history or, when slow-changing and appropriate, inform Athlete Profile.
Current decision consequences should be promoted into Current Athlete State or Planning State Carry-Forward Items rather than relying on deep-history recall.

## 9. Carry-Forward Interface
A summary should nominate carry-forward items when an issue remains active after the summarized block closes.
Candidate classes include:
- Active Constraint;
- Active Tissue Concern;
- Unresolved Uncertainty;
- Current Bottleneck Hypothesis;
- Competition Deadline;
- Important Benchmark;
- Open Decision Question;
- recurring response pattern;
- unresolved measurement problem.
For each candidate, record current relevance, affected decision, source, confidence, uncertainty, next trigger, and proposed owner.
[Update Planning State Workflow](../workflows/update_planning_state.md) decides how the item is represented in continuity state.
Summary closure does not resolve the item.

## 10. Compression and Archive
The default information lifecycle is:
Raw Record
->
Structured Review
->
Summary
->
Archive or Cold Context
**COMPRESSION DOES NOT EQUAL DELETION.**
After a Week closes:
- Session raw records remain stored;
- Session Reviews remain stored;
- the Week Summary becomes the default Week-level representation;
- lower-level detail moves out of default context;
- source references remain resolvable.
Archive means retained, traceable, and excluded from default retrieval. It does not mean erased or judged irrelevant forever.
Recent detailed data remain at high resolution. Older completed blocks normally enter default context through summaries. Deep archive is queried only when the current decision requires it.
Older does not mean irrelevant.

## 11. Summary Versioning
A summary supports:
- version;
- status;
- previous_version;
- revision_reason;
- new_evidence;
- changed_fields;
- source references added or corrected;
- original creation time;
- updated_at;
- responsible process.
A material revision creates a new version:
- Week 05 Summary v1 becomes **SUPERSEDED**;
- Week 05 Summary v2 becomes **ACTIVE**;
- both remain traceable.
Material revisions include new evidence, measurement correction, data correction, changed interpretation, or changed decision meaning.
A simple typographic correction need not create a complex revision chain if it does not change meaning or provenance.

## 12. Historical Perspective and Hindsight Control
A summary must distinguish:
- **Known Then**;
- **Interpreted Then**;
- **Learned Later**;
- **Current Revision**;
- **Revision Reason**.
If a later review suggests that an earlier fatigue interpretation was more likely a measurement problem, preserve:
- the original observation;
- the original interpretation and confidence;
- the later evidence;
- the revised interpretation;
- the revision date and reason.
Do not rewrite the earlier record as though the later knowledge was available at the time.
Summary revision may change the current interpretation while preserving the historical decision context.

## 13. Uncertainty Preservation
Compression must preserve:
- Unknown;
- Missing;
- Provisional;
- Conflict;
- Unresolved;
- Cannot Determine;
- qualitative confidence;
- material alternative explanations.
Conflicting sources are not averaged into a false middle conclusion.
A summary must not transform limited evidence into certainty merely because detail was removed.
**COMPRESSION DOES NOT EQUAL CERTAINTY INFLATION.**

## 14. Raw-Fact Preservation
A summary may select, compress, organize, and cautiously interpret.
It must not:
- invent missing values;
- erase contradiction;
- convert Estimate into Measurement;
- alter Actual Exposure;
- silently change timing or conditions;
- remove source provenance;
- retroactively rewrite a decision record.
Corrections belong in a versioned revision with an explicit reason.

## 15. Summary Freshness and Relevance
Summary resolution depends on:
Planning Level
+
Decision Relevance
+
Recency
It does not depend on a fixed number of elapsed days.
Information may reduce in default resolution when it exits the current decision horizon and has no unresolved consequence.
An older summary may return to higher-resolution retrieval when it supplies a needed baseline, recurring-pattern history, or prior competition response.

## 16. Minimum Summary Completeness
Every active summary should establish:
- identity and level;
- summarized object and time span;
- source scope;
- intended versus actual structure where applicable;
- material State Delta;
- important trend or explicit absence of support;
- important exceptions;
- unresolved issues;
- next-decision implications;
- carry-forward candidates;
- confidence and uncertainty;
- source references;
- version and timestamps.
Fields without evidence remain Missing, Unknown, or Not Applicable.

## 17. Storage-Agnostic Contract
A persistence adapter should be able to:
- retrieve source records by reference;
- retrieve an active summary;
- save a new summary;
- save a revised summary version;
- mark a prior version superseded;
- preserve raw records;
- move detail out of default context;
- retrieve archived detail when requested;
- resolve source provenance.
Operations such as save_summary() and get_previous_cycle_summary() are logical interface names, not implemented functions.
The schema does not define a Notion database, SQL model, or storage API.

## 18. Interfaces
- [Planning State Schema](./planning_state.md) references current summaries and
  carry-forward items.
- [Athlete State Schema](./athlete_state.md) defines current State; a Summary
  records State Delta but is not Current State.
- [Update Context Summary Workflow](../workflows/update_context_summary.md)
  creates, promotes, revises, and archives summary context.
- [Update Planning State Workflow](../workflows/update_planning_state.md)
  updates summary pointers and carry-forward state.
- [Review Training Workflow](../workflows/review_training.md) produces
  event-level analysis used as summary source.
- [Resume Planning Workflow](../workflows/resume_planning.md) retrieves the
  minimum sufficient summary resolution.

## 19. Context Summary Invariants
1. Raw Record and Summary remain distinct.
2. Summary and Current Athlete State remain distinct.
3. Compression does not delete source data.
4. Archive means retained and not read by default.
5. More context does not automatically improve a decision.
6. Summary content is selected by decision relevance.
7. Important unresolved information carries forward.
8. Missing information is not resolved information.
9. Compression preserves uncertainty, conflict, and confidence.
10. A repeated trend is not defined by a universal occurrence count.
11. Isolated high-consequence exceptions may be promoted without becoming a
    trend.
12. Summary revision preserves prior versions and provenance.
13. Later knowledge does not silently rewrite what was known then.
14. Estimate does not become Measurement through compression.
15. Older information is not automatically irrelevant.
16. Storage implementation remains replaceable.
17. Raw athlete history is not automatically deleted.
