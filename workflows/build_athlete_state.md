# Build Athlete State Workflow
Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose
This workflow converts incomplete, mixed-quality athlete information into a
time-stamped, decision-relevant Athlete State under uncertainty.
It accepts natural-language reports, historical records, training experience,
measurements, observations, competition information, constraints, and prior
state. It classifies and maps those inputs before constructing a state estimate.
The workflow seeks minimum sufficient information for the current planning
decision. It does not seek a complete athlete database.
It does not create a plan, select exercises, diagnose injury, impose a fixed
test battery, produce a giant questionnaire, search for interventions, redefine
the schemas, or collapse readiness into a single score.
Raw Athlete Information is not yet Athlete State.
The core information flow is:
Raw Athlete Information
-> Source and Data Classification
-> Schema Mapping
-> Current Decision Context
-> Information Sufficiency Check
-> Initial or Provisional Athlete State
-> Decision-Relevant Information Gaps
-> Targeted Follow-Up or Assessment Request
-> Updated Athlete State
-> Planning Readiness Decision
Every transition may retain missing information, conflict, and uncertainty.

## Required Interfaces
This workflow uses these definitions and rules without duplicating them:
- [Athlete Profile Schema](../schemas/athlete_profile.md)
- [Athlete State Schema](../schemas/athlete_state.md)
- [Performance Assessment Schema](../schemas/performance_assessment.md)
- [Competition Context Schema](../schemas/competition_context.md)
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md)
- [Constraint Handling Rules](../rules/constraint_handling.md)
It hands completed packages to:
- [Create Cycle Workflow](./create_cycle.md)
- [Create Mesocycle Workflow](./create_mesocycle.md)
- [Create Week Workflow](./create_week.md)
- [Create Session Workflow](./create_session.md)
Post-training information may enter from
[Review Training Workflow](./review_training.md).
Schemas define what data objects mean. This workflow defines how available
information is obtained, classified, mapped, checked, and assembled.

## Workflow Entry Modes
The same core logic supports all entry modes.
### New Athlete
Little or no trusted Profile or Athlete State exists. Build only the minimum
Profile and State needed for the named decision.
### Existing Athlete
A prior Profile and State exist. Verify recency and relevance, then update only
dimensions affected by new evidence or context.
### Partial Athlete Record
Some historical results or training records exist, but current State is
incomplete. Preserve usable records and seek only information that could change
the current decision.
### Competition Update
A competition date, role, entry status, or constraint changed. Update
Competition Context and every State dimension materially affected.
### Post-Training Update
A Review Training output supplies new Actual Exposure, Observed Response,
Candidate Interpretations, confidence, or decision information.
Previous State
+
New Evidence
->
Updated State
Do not restart intake or re-ask stable Profile information.

## Update Modes
### INITIAL BUILD
Use when no sufficiently current State exists. The output may still be partial
or provisional. Initial does not mean complete.
### STATE UPDATE
Use when a prior State exists. Classify relevant dimensions as:
- **Changed**;
- **Unchanged**;
- **Expired**;
- **Uncertain**;
- **Newly Assessed**;
- **No Longer Decision-Relevant**.
Unchanged does not mean permanently stable. Expired means too old for the
current decision; no universal expiration period is imposed.

## Step 1. Define the Planning Context
### Objective
Identify the decision this Athlete State must support before requesting more
information.
### Actions
Record:
- athlete identifier or provisional alias;
- requested decision and planning level;
- decision horizon;
- commitment and reversibility;
- consequence of error;
- competition relevance;
- known constraints;
- information deadline;
- entry mode and update mode.
Typical contexts include creating a first Cycle, updating a Mesocycle,
organizing a Week, creating a Session, evaluating competition preparation, or
updating State after training.
Do not request multi-year history merely because it may be interesting. A
next-session decision may require current tissue, fatigue, exposure, and
constraint information before extensive history.
Higher-commitment decisions may require stronger information support than local,
conservative, reversible decisions.
### Output
**Planning Context**, including the named decision and its evidence standard.

## Step 2. Collect Existing Athlete Information
### Objective
Use available information before asking the athlete for more.
### Candidate Sources
- natural-language athlete report;
- prior Athlete Profile;
- prior Athlete State;
- competition results;
- assessment data;
- training logs;
- video observations;
- coach notes;
- supplied medical or rehabilitation restrictions;
- Competition Context;
- Review Training output.
For each source, preserve source class, date or period, original wording when
needed, verification status, measurement conditions, decision relevance, and
obvious missing context.
Do not repeat a question when sufficiently reliable, current, and relevant
information already exists.
### Natural-Language Intake
Accept ordinary language. For example:
> I ran six 30s yesterday. My hamstring is a little sore this morning, walking
> is fine, and I race next week.

Extract recent sprint exposure, delayed tissue observation, walking context,
competition proximity, unresolved interpretation, source, and time.
Do not require JSON.
### Output
**Raw Information Set**, with source and time preserved.

## Step 3. Classify Information by Source and Type
### Objective
Prevent statements, measurements, interpretations, and constraints from being
treated as equivalent.
### Information Types
#### Historical Fact
Examples include historical 100m PB, training age, prior coaching environment,
and past injury report. Historical does not imply current.
#### Current Observation
A time-stamped description, such as soreness today or unstable recent
execution.
#### Measurement
A value produced through a described process, such as a 30m time. A number is
not automatically reliable.
#### Athlete-Reported Interpretation
An interpretation such as "I feel slow." Retain it as subjective evidence
without converting it into objective fact.
#### Coach or System Interpretation
A proposed explanation such as a Candidate Bottleneck or fatigue hypothesis.
Keep evidence and confidence attached.
#### Constraint
A factor limiting feasible action, such as available days, facility, supplied
medical restriction, tissue availability, or competition deadline.
#### Unknown
Information absent, unassessed, stale, or unavailable for the current decision.
#### Conflict
Relevant items supporting materially different accounts.
### Source Classes
Allow **Measured**, **Athlete Reported**, **Coach Observed**,
**Historical Record**, **Estimated**, **Derived**, and **Unverified**.
Subjective information is not automatically invalid. Measurement is not
automatically reliable. Consider quality, context, recency, relevance, and
consequence of error.
### Output
**Classified Information Set**, with no interpretation promoted to fact.

## Step 4. Map Information to Schemas
### Objective
Assign each item to its correct semantic object.
### Athlete Profile Mapping
Map training age, long-term performance history, coaching background, stable
environment, recurring constraints, historical medical context, and adherence
context.
Do not place transient fatigue or today's tissue report in Profile.
### Athlete State Mapping
Map Current Performance State, Current Performance Problem, Candidate
Bottleneck, current priority output, Fatigue and Recovery, Tissue, Technical,
Exposure, Adaptation Trend, Competition Readiness, Active Constraints, Current
Uncertainty, and confidence.
Historical PB may contextualize State but does not become a current condition.
### Performance Assessment Mapping
Map assessment question, protocol, conditions, result, unit, timing method,
source, observation, reliability, comparability, decision relevance, and
missing or proposed assessment.
Measurement and observation remain separate from interpretation.
### Competition Context Mapping
Map primary and secondary competitions, role, date, entry status, rounds,
travel, known conditions, constraints, and uncertainty.
Do not invent a date. **No Confirmed Competition** is valid.
### Multiple-Object Use
One source may inform several objects without contradictory copies. A historical
100m PB primarily belongs in Profile. A recent race also creates an Assessment
record and may inform Current Performance State.
Store the underlying record once where practical and reference it from
interpretation.
### Output
**Schema-Mapped Information Set** with explicit ownership and references.

## Step 5. Separate Observation From Interpretation
### Objective
Prevent premature causal conclusions.
For every consequential current claim, represent:
Observation
->
Candidate Interpretations
->
Current State Estimate
Example observation:
- flying 20m was slower than a sufficiently comparable historical baseline.
Candidate Interpretations may include:
- reduced maximum-velocity capability;
- acute or accumulated fatigue;
- poor measurement conditions;
- insufficient recent high-speed exposure;
- technical instability;
- random variation.
The Current State Estimate remains provisional until evidence supports stronger
inference.
### Rules
- Measurement is an observation source, not a cause.
- A slower sprint does not uniquely identify a MaxV deficit.
- A low strength value does not uniquely identify a sprint bottleneck.
- Athlete report does not become physiological diagnosis.
- Coach observation may support interpretation but remains source-labeled.
- Several interpretations may remain active.
- **Cannot Determine** is permitted.
### Output
**Observation-Interpretation Map** with supporting evidence, conflicts,
alternatives, and confidence.

## Step 6. Establish the Initial Athlete Profile
### Objective
Construct the minimum useful slow-changing background record.
### Actions
Populate available Profile categories:
- identity and basic context;
- training age and experience;
- performance history;
- supplied injury and medical context;
- training environment;
- time and lifestyle constraints;
- preference and adherence context;
- source, date, and data quality.
Mark unavailable decision-relevant items **Missing**.
Do not force completion of Optional / Additional fields.
Do not infer no injury from no injury information.
Do not convert a historical result into current performance status.
Ask whether the Profile is sufficient to interpret the current State and
planning context. If yes, stop Profile collection. If no, identify the exact
missing item and affected decision.
### Output
**Athlete Profile Summary**, with references and visible uncertainty.

## Step 7. Establish the Initial Athlete State
### Objective
Construct the current decision-relevant estimate from mapped evidence.
### State Dimensions
Represent when relevant:
- Current Performance State;
- Current Performance Problem;
- Candidate Bottleneck;
- Current Priority State if already decided;
- Fatigue and Recovery State;
- Tissue State;
- Technical State;
- Exposure State;
- Adaptation Trend;
- Competition Readiness;
- Active Constraints;
- Current Uncertainty;
- State Confidence.
### Missing Dimensions
Use:
- **Unknown**;
- **Not Assessed**;
- **Provisional**;
- **Unresolved**;
- **Cannot Determine**;
- **Not Applicable**.
Do not fill a blank merely to make the record complete. A defensible inference
must be labeled **Derived**, **Estimated**, or **Provisional**, with evidence and
uncertainty.
### Candidate Bottlenecks
Keep distinct:
Observed Weakness
!=
Candidate Bottleneck
!=
Confirmed Cause
Allow multiple candidates, retained alternatives, unresolved alternatives, or
no current bottleneck conclusion.
For each candidate, record linked performance problem, supporting and
conflicting evidence, mechanistic relevance, transfer uncertainty, and
confidence.
Do not force a single bottleneck.
### Multidimensional Readiness
Keep performance, fatigue, recovery, tissue, motivation, sleep, technical
stability, and competition expression distinguishable.
Do not create a composite readiness score without a separate validated model.
### Output
**Initial Athlete State**, time-stamped and confidence-labeled.

## Step 8. Establish Competition Context
### Objective
Represent the competition horizon that changes decision value, urgency, or
risk.
### Actions
Record when available:
- primary and secondary competitions;
- date or bounded date uncertainty;
- competition role and priority;
- entry status;
- sequence and turnaround;
- rounds;
- travel;
- known conditions;
- competition constraints;
- competition uncertainty.
Competition may simultaneously be terminal performance opportunity, specific
exposure, stress event, and feedback source.
If no event is confirmed, record **No Confirmed Competition**.
A provisional planning horizon may follow the athlete's goal, but it must remain
provisional and contain no invented event date.
### Output
**Competition Context Summary** and its implications for recency and decision
consequence.

## Step 9. Evaluate Information Sufficiency
### Objective
Determine whether current information supports the named decision.
Apply the
[Uncertainty Handling Rules](../rules/uncertainty_handling.md).
### Sufficiency Questions
Ask:
- Is the target decision explicit?
- Is there a minimally usable current Athlete State?
- Are relevant constraints represented?
- Are high-consequence tissue or medical uncertainties visible?
- Is Competition Context adequate for this decision?
- Are observations separate from interpretations?
- Are material measurements sufficiently contextualized?
- Would a missing item plausibly change the decision?
- Can a conservative and reversible decision proceed?
- Is the State current enough?
An incomplete record is not automatically unplannable.
### Sufficiency States
#### SUFFICIENT
Information supports the current decision at its required commitment level.
#### SUFFICIENT_WITH_UNCERTAINTY
Planning may proceed while explicit uncertainty remains. The decision stays
bounded by that uncertainty.
#### PARTIAL_STATE
A usable State exists for some decisions, but not for specified
higher-commitment or higher-scope decisions.
#### DECISION_BLOCKED_BY_MISSING_INFORMATION
A named missing item directly prevents the named decision.
Record:
- missing information;
- blocked decision;
- why it is critical;
- feasible acquisition route;
- timing;
- whether an alternative conservative decision remains possible.
### Stop Condition
If the current decision is sufficiently supported, stop intake.
The existence of more measurable variables does not justify more questions.
### Output
**Information Sufficiency State** and rationale.

## Step 10. Identify Decision-Relevant Information Gaps
### Objective
Identify only missing information that could change the current decision.
### Gap Test
For each possible gap, ask:
> If this information were known, could it change the preferred decision,
> confidence, constraint interpretation, or important-risk response?

If no, do not seek it now.
### Gap Representation
Record:
- missing or uncertain object;
- current decision affected;
- plausible outcomes;
- how outcomes could change the decision;
- consequence of error;
- current confidence;
- feasible source;
- acquisition cost;
- latest useful time;
- whether the gap blocks planning.
### Requirement Classification
Assign:
- **Required**;
- **Decision-Dependent**;
- **Optional / Additional**.
The same information may change class when the decision changes.
### Output
Ranked **Decision-Relevant Information Gaps**.

## Step 11. Ask Targeted Follow-Up Questions
### Objective
Reduce the highest-value uncertainty with the least athlete burden.
### Question Priority
Prioritize qualitatively through:
Decision Impact
x
Uncertainty Reduction
x
Consequence of Error
x
Acquisition Cost
This is a relationship model, not a numeric formula.
Use **High**, **Moderate**, or **Low** priority when useful.
### Question Standards
A question must be:
- minimal;
- specific;
- answerable;
- connected to a named decision;
- sensitive to information already available;
- limited to the detail needed now.
Ask one to five highest-value questions at a time. Use fewer when one answer may
make the remaining questions irrelevant.
Prefer questions that clarify a high-consequence restriction, establish a
decision deadline, reconstruct recent Actual Exposure, distinguish a material
interpretation, reveal a binding constraint, or establish comparability.
Do not ask all possible Profile or assessment questions.
### Stop Rule
After each answer, repeat the sufficiency check. Stop asking when the current
decision becomes sufficiently supported.
### Output
**Targeted Follow-Up Request**, or **No Further Questions Required**.

## Step 12. Request Additional Assessment When Justified
### Objective
Request assessment only when questions and existing information cannot resolve
a decision-relevant uncertainty, and a result could change the decision.
### Trigger Conditions
Assessment is justified when:
- a material decision question remains unresolved;
- existing observations are insufficient or poorly comparable;
- the measurement category is relevant to the uncertainty;
- plausible results would change action, interpretation, confidence, or
  important-risk handling;
- the result can arrive in time;
- assessment cost is justified.
### Assessment Cost
Treat assessment as intervention or exposure.
Consider:
- fatigue;
- tissue or injury cost;
- equipment;
- time;
- measurement reliability;
- familiarization or learning effect;
- competition proximity;
- opportunity cost;
- whether existing data are sufficient.
Assessment is not free information.
### Assessment Need Output
Record:
- **Decision Question**;
- **Unknown Variable or State Dimension**;
- **Suggested Measurement Category**;
- **Why It Matters**;
- **What Decision It Could Change**;
- **Urgency**;
- **Expected Information Value**;
- **Fatigue, Tissue, Time, and Opportunity Cost**;
- **Feasibility and Reliability Constraints**.
Request a category such as a recent high-quality flying sprint or velocity
assessment. Do not prescribe a universal protocol or test battery.
Use **EXTERNAL_ASSESSMENT_REQUIRED** when an unresolved issue requires medical,
clinical, or other professional evaluation outside the planning system.
Do not diagnose.
### Output
**Recommended Additional Assessment**, **External Assessment Request**, or
**No Assessment Justified**.

## Step 13. Resolve or Preserve Conflicting Information
### Objective
Keep contradictions visible until evidence justifies resolution.
### Conflict Record
Record:
- **Conflict A**;
- **Conflict B**;
- source and date of each;
- quality;
- contextual differences;
- plausible explanations;
- Current Confidence;
- decision consequence;
- need for additional observation;
- resolution status.
Example:
Athlete report:
- feels fresh.
Performance record:
- three sufficiently comparable sprint exposures below baseline.
Represent **Conflicting Readiness Information**, candidate explanations, and
lower confidence in a simple readiness interpretation.
Do not average the conflict into "medium readiness."
### Resolution States
Use:
- **Resolved**;
- **Provisionally Resolved**;
- **Retained Conflict**;
- **Insufficient Information**;
- **Cannot Determine**.
Resolution requires evidence. Convenience is not evidence.
### Output
**Conflict Register** with alternatives and decision implications.

## Step 14. Update Athlete State and Confidence
### Objective
Integrate new evidence without mechanically replacing prior knowledge.
### Evidence Weighting
Consider:
- reliability;
- relevance;
- recency;
- repeated trend;
- measurement quality;
- comparability;
- consistency with other evidence;
- consequence of being wrong.
A single low-quality observation should not overturn stable relevant history.
A high-consequence tissue warning may justify a conservative update before a
repeated trend exists.
### Update Record
For each changed dimension, record:
- what changed;
- prior state;
- updated state;
- why;
- evidence source;
- Actual Exposure context when relevant;
- confidence before and after;
- what remains unresolved;
- next review trigger.
Record unchanged status only when needed for traceability.
### Information Recency
Judge recency relative to the decision:
- training age changes slowly;
- today's tissue sensation may expire quickly;
- recent high-speed exposure has intermediate relevance;
- competition data change with entry and schedule.
Do not impose universal expiration days.
### Output
**Updated Athlete State**, **Confidence Update**, and **Update Metadata**.

## Step 15. Determine Planning Readiness
### Objective
Decide whether the Athlete-State Package can enter planning.
### READY_FOR_PLANNING
Use when information supports the stated decision, material constraints and
uncertainty are represented, no missing item blocks it, and State is current
enough.
This status does not claim complete knowledge.
### READY_FOR_PROVISIONAL_PLANNING
Use when a conservative or reversible decision can proceed, uncertainty and
assumptions are explicit, and review triggers are defined.
The receiving planning workflow must preserve those conditions.
### MORE_INFORMATION_REQUIRED
Use when one or more targeted athlete or coach questions are needed. Specify the
minimal questions.
### ASSESSMENT_REQUIRED
Use when a decision-relevant measurement or observation is justified and cannot
be replaced by existing information or a lower-cost question.
Specify an Assessment Need, not a universal protocol.
### EXTERNAL_ASSESSMENT_REQUIRED
Use when a supplied restriction, significant unexplained tissue concern, or
other issue requires appropriate external professional evaluation before
specified training decisions proceed.
State which decision is paused. Do not diagnose.
### Readiness Scope
Readiness applies to a named decision and scope. An athlete may be ready for a
conservative Session decision while not ready for a high-commitment Cycle
decision.
### Output
One **Planning Readiness** state, scope, rationale, conditions, and next trigger.

## Step 16. Produce the Athlete-State Package
### Objective
Provide a compact, decision-relevant handoff to planning.
### Required Package Structure
# Athlete State Package
## Planning Context
Include decision, scope, horizon, entry mode, and update mode.
## Athlete Profile Summary
Include only slow-changing context relevant to the decision, with references to
underlying records.
## Current Performance State
Represent terminal and relevant segment outcomes with source, date, and
confidence.
## Current Performance Problem
Describe the problem without embedding an unearned cause.
## Candidate Bottlenecks
List candidates, evidence, alternatives, and confidence. Do not force a unique
bottleneck.
## Current Priority State
Include existing Primary, Maintain, Minimal, or Temporarily Withdrawn outputs
when established. Do not allocate priorities inside this workflow.
## Current Exposure State
Summarize recent Actual Exposure and achieved quality relevant to the decision.
## Fatigue and Recovery State
Keep relevant dimensions separate.
## Tissue State
Record observations, supplied restrictions, availability, and uncertainty
without diagnosis.
## Technical State
Record task-specific organization and stability without a universal technique
template.
## Adaptation Trend
Use Improving, Stable, Declining, Mixed, Unresolved, or Cannot Determine with
the evidence window.
## Competition Context
Include event roles, dates, constraints, and uncertainty.
## Active Constraints
Include decision-relevant time, facility, tissue, medical, recovery,
competition, and information constraints.
## Available Performance Assessments
Summarize relevant records and their quality.
## Current Uncertainty
List unresolved claims, alternatives, consequences, and confidence.
## Information Sufficiency
Use SUFFICIENT, SUFFICIENT_WITH_UNCERTAINTY, PARTIAL_STATE, or
DECISION_BLOCKED_BY_MISSING_INFORMATION.
## Missing Decision-Relevant Information
List only gaps that could change the current decision.
## Recommended Additional Assessment
Include only justified Assessment Needs. Otherwise state none justified.
## State Confidence
Use claim-specific qualitative confidence. Do not create false probabilities.
## Planning Readiness
State readiness, scope, conditions, and destination workflow.
## Last Updated
Include effective time, source set, prior state reference, and next review
trigger.
### Package Compression Rule
The package is not a full archive dump.
Keep raw information in underlying records. The handoff contains the minimum
context needed to use the current State without hiding material uncertainty.
### Output
**Athlete-State Package**, ready for planning or carrying an explicit
information or assessment requirement.

## Planning Workflow Handoff
When readiness is **READY_FOR_PLANNING** or
**READY_FOR_PROVISIONAL_PLANNING**, stop this workflow.
Route by scope:
- full competitive horizon -> [Create Cycle Workflow](./create_cycle.md);
- current adaptation stage -> [Create Mesocycle Workflow](./create_mesocycle.md);
- near-term organization -> [Create Week Workflow](./create_week.md);
- next-session prescription -> [Create Session Workflow](./create_session.md).
The receiving workflow uses the package as input. This workflow does not
continue into plan generation.
If readiness is provisional, preserve unresolved uncertainty, bounded
assumptions, constraints, permitted scope, and review triggers.

## Review Training Interface
[Review Training Workflow](./review_training.md) may provide:
- reconstructed Actual Exposure;
- Achieved Quality;
- immediate and delayed observations;
- recent trend;
- Expected versus Observed Response;
- Candidate Interpretations;
- possible failure classification;
- confidence update;
- Decision State and Decision Scope;
- unresolved questions;
- next observation needs.
These outputs re-enter this workflow as new evidence.
The closed loop is:
Build State
-> Plan
-> Execute
-> Review
-> Build or Update State
-> Re-plan
Review Training interprets what occurred after exposure. Build Athlete State
integrates the decision-relevant result into the current package.

## Minimum Sufficient Intake
Minimum Sufficient Intake is the smallest set of current, relevant, sufficiently
credible information that supports the named decision at its required
commitment level.
It depends on:
- current decision and scope;
- reversibility;
- consequence of error;
- current Athlete State;
- active constraints;
- competition timing;
- unresolved uncertainty.
Intake is sufficient when additional available information is unlikely to
change the decision, confidence, or important-risk response enough to justify
its acquisition cost.
Completeness is not the objective.

## Failure Modes
The workflow must detect and avoid:
### GIANT_INTAKE_FORM
Collecting broad information without a current decision need.
### FIXED_TEST_BATTERY
Requiring the same assessment set for every athlete and decision.
### READINESS_SCORE_COLLAPSE
Compressing distinct State dimensions into one unsupported score.
### MEASUREMENT_AS_INTERPRETATION
Treating a measured result as its own causal explanation.
### MISSING_AS_NORMAL
Treating unknown information as normal, zero, or favorable.
### SINGLE_BOTTLENECK_FORCED
Selecting one causal bottleneck when evidence supports alternatives.
### OVERQUESTIONING
Continuing intake after the decision is sufficiently supported.
### OUTDATED_STATE_USED_AS_CURRENT
Using stale information without evaluating recency relative to the decision.
### MEDICAL_DIAGNOSIS
Inferring a diagnosis from athlete information.
### PLAN_GENERATION_INSIDE_INTAKE
Creating training content before handoff to the planning workflow.
A detected failure mode must be corrected before readiness is granted.

## Workflow Completion Gate
The workflow is complete when:
- the planning decision and scope are explicit;
- existing information has been used before new questions;
- source, type, and time have been classified;
- information is mapped to the four schemas;
- Profile and State are separated;
- measurement, observation, and interpretation are separated;
- Performance Problem and Candidate Bottleneck are separated;
- missing information remains explicit;
- conflicts remain visible or are evidence-resolved;
- sufficiency is decision-specific;
- only decision-relevant gaps are retained;
- follow-up questions are minimal and prioritized;
- assessment is requested only when justified;
- assessment cost is considered;
- State is time-stamped and confidence-labeled;
- no single readiness score is required;
- Planning Readiness and scope are stated;
- the package is concise enough for planning use;
- no plan has been generated.

## State-Building Invariants
1. Raw information is not yet Athlete State.
2. Athlete Profile and Athlete State remain distinct.
3. Measurement, observation, interpretation, and conclusion remain distinct.
4. Missing information is not zero, normal, favorable, or no problem.
5. An observed weakness does not automatically establish a bottleneck.
6. A measurement does not establish cause.
7. Athlete State is a partially observable, decision-relevant estimate.
8. Information requirements change with the current decision.
9. More data does not automatically improve the decision.
10. Existing reliable information is used before new questions are asked.
11. Follow-up questions target the highest-value unresolved information.
12. Collection stops when the current decision is sufficiently supported.
13. Additional assessment requires decision value greater than relevant cost.
14. Assessment remains an exposure with fatigue, tissue, time, and opportunity
    costs.
15. Contradictions remain visible until evidence justifies resolution.
16. State updates are proportional to evidence quality and consequence.
17. High-consequence warning information may justify conservative action
    without repeated evidence.
18. State information is evaluated for recency relative to the decision.
19. No missing value is invented to complete the record.
20. Derived and estimated values remain labeled.
21. Multiple Candidate Bottlenecks may remain active.
22. No universal readiness score is required.
23. Planning uses the most current decision-relevant State.
24. The workflow stops at the planning handoff.
