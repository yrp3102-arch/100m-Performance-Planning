# Session {Session ID}

Version: 0.1
Status: Draft
Date: 2026-09-15

> **VIEW CONTRACT** - This is the execution interface for one Session. It
> presents a prescription already produced by the Session workflow. It does not
> select training tasks, invent dose, or implement feedback rules.

> **ILLUSTRATIVE ONLY** - Braced fields and task blocks describe presentation
> structure. They contain no athlete prescription or fixed training values.

Source interfaces:

- [Create Session Workflow](../workflows/create_session.md)
- [Athlete State Schema](../schemas/athlete_state.md)
- [Planning State Schema](../schemas/planning_state.md)
- [Visual System](./visual_system.md)
- [Week Template](./week_template.md)
- [Review Template](./review_template.md)

## SCAN - Do This Now

The first screen must show the following in this order.

### Session Identity

| Field | Value |
|---|---|
| Session | {title and reference} |
| Date / Slot | {date or planned slot} |
| Lifecycle status | {authoritative status} |
| Execution condition | {FIXED / CONDITIONAL / OPTIONAL / REPLACEABLE} |
| Parent Week | {reference} |
| Session role | {Primary / supporting / maintenance / minimal / competition / recovery} |
| Version | {prescription version} |
| Last update | {date and source} |

Do not infer PLANNED, MODIFIED, or CANCELLED without an authoritative source.

### Today's Objective

**PRIMARY OBJECTIVE:** {one concise action-oriented statement}

**Intended stimulus:** {stimulus description beyond exercise label}

**Relation to Week:** {one line}

**Objective confidence:** {canonical confidence label}

### Active Warning

> **WARNING - {warning title or None}**
>
> - Affected work: {task or whole Session}
> - Required action: {modify, stop, review, or external action}
> - Source and confidence: {reference and confidence}

> **REVIEW REQUIRED - {scope or None}**
>
> - Do not continue: {affected action}
> - Until: {review condition or external input}
> - Destination: {review workflow or responsible source}

A Warning must appear before task detail. It must not be hidden in Notes.

### Primary Work Snapshot

| Task | PLANNED dose | Rest / Recovery | Quality standard | STOP / MODIFY IF |
|---|---|---|---|---|
| {task label} | {task-specific dose dimensions} | {recovery condition} | {observable useful-quality criterion} | {supplied stop or modification condition} |

The task label does not define the stimulus. The Planned dose is not Actual
Exposure.

### Entry-State Check

| Decision-relevant dimension | Required or expected state | Current observation | Disposition |
|---|---|---|---|
| Performance / execution | {entry assumption} | {current information} | {Proceed / Modify / Review / Cannot Determine} |
| Fatigue and recovery | {entry assumption} | {current information} | {disposition} |
| Tissue state | {availability or restriction} | {current information} | {disposition} |
| Environment / facility | {required condition} | {current information} | {disposition} |

Missing information does not render as acceptable. Do not create a composite
readiness score.

### Session-Wide Stop Conditions

> **STOP / MODIFY IF**
>
> - {quality deterioration condition supplied by the plan};
> - {tissue Warning condition};
> - {technical breakdown condition};
> - {unexpected response condition};
> - {environment or equipment condition};
> - {higher-level Review trigger}.

Stop Conditions have at least the same visibility as dose.

### Conditional Disposition

> **CONDITIONAL - {Session or task}**
>
> - IF: {entry trigger}
> - THEN: {execute the stated role and dose bounds}
> - ELSE: {modify, replace, omit, or review}

CONDITIONAL is not OPTIONAL. OPTIONAL work receives a separate label.

## TRAINING FIELD VIEW

TRAINING FIELD VIEW is the COMPACT Session projection for phone, small PDF card,
Notion callout, or future app.

It displays only:

### Objective

{Primary Objective}

### Main Work

{ordered Primary task blocks}

### Dose

{task-specific Planned dose}

### Rest

{recovery interval or condition}

### Quality

{observable quality criterion}

### Stop

{prominent Stop or Modify conditions}

### Warning

{active Warning, Review Required, or None}

This projection may omit long rationale, historical detail, secondary metrics,
and full provenance. It must not omit conditionality, active Warning, Stop
Conditions, or critical uncertainty.

## EXECUTE - Full Session

### Primary Work

#### Task {ID}: {Task Label}

| Field | Value |
|---|---|
| Status | {ACTIVE / CONDITIONAL / OPTIONAL / REPLACEABLE / withdrawn} |
| Priority | PRIMARY |
| Purpose | {relationship to Session Objective} |
| Intended stimulus | {stimulus beyond label} |
| Transfer hypothesis | {brief sprint-relevant relationship when supplied} |
| Dose | {task-specific dimensions} |
| Recovery | {between repetition, set, or task as relevant} |
| Intensity / intent | {execution intent or supported intensity descriptor} |
| Quality standard | {observable criterion} |
| Stop condition | {task-specific stop criterion} |
| Adjustment | {allowed modification or replacement} |
| Source | {Session output field or Rule reference} |

Repeat only for tasks supplied by the Session workflow.

#### Sprint Dose Projection

Use relevant fields only:

- distance or exposure duration;
- repetitions and sets;
- recovery;
- intensity or intent;
- timing or velocity criterion;
- execution quality;
- surface or environment when material.

#### Strength Dose Projection

Use relevant fields only:

- exercise or task;
- sets and repetitions;
- load, RPE, or velocity when supplied;
- rest;
- intent;
- quality;
- stop or adjustment condition.

#### Plyometric Dose Projection

Use relevant fields only:

- task;
- contacts or repetitions;
- sets;
- intent;
- quality;
- surface when material;
- stop or adjustment condition.

These are presentation dimensions, not required fields for every task and not a
fixed exercise library.

### Supporting Work

#### Supporting Task {ID}

| Field | Value |
|---|---|
| Allocation | {MAINTAIN or MINIMAL} |
| Purpose | {support to the Primary Objective} |
| Planned dose | {task-specific dimensions} |
| Cost boundary | {what it must not compromise} |
| Quality / stop | {criterion and condition} |
| Status | {ACTIVE / CONDITIONAL / REPLACEABLE} |

Supporting work must not visually compete with Primary Work.

### Optional Work

> **OPTIONAL - {task or None}**
>
> - Value: {possible contribution}
> - Omit when: {cost, time, or Primary-quality reason}
> - Omission effect: {why the minimum Session Objective remains intact}

### Conditional Work

> **CONDITIONAL - {task or None}**
>
> - IF: {explicit trigger}
> - THEN: {task role and bounded dose}
> - ELSE: {replacement, omission, or review}
> - Decision owner: {Session or Week scope}

### Task Order and Interaction

**Required order:** {ordering relationship}

**Primary-quality protection:** {what must remain protected}

**Overlapping stress:** {tissue, neural, fatigue, or technical interaction}

**Following exposure consideration:** {relationship to next Session or
competition}

Present only relationships supplied by the plan.

### Rest and Recovery Conditions

| Scope | Planned condition | Why it matters | Adjustment interface |
|---|---|---|---|
| Between repetitions | {time or quality condition} | {stimulus or quality relationship} | {supplied adjustment} |
| Between sets | {condition if relevant} | {relationship} | {adjustment} |
| Between tasks | {condition} | {interaction relationship} | {adjustment} |

Recovery is part of dose. Do not hide it in prose.

### Adjustment Options

| Trigger | Allowed response | Preserved objective | Escalation condition |
|---|---|---|---|
| {trigger} | {Maintain / Reduce / Modify / Replace / Temporarily Withdraw / Review} | {what remains stable} | {higher-level challenge} |

The template displays options already produced by workflows and Rules. It does
not create thresholds.

## PLANNED vs ACTUAL

### Planned Prescription

| Task | PLANNED dose | Intended stimulus | Quality standard | Stop condition |
|---|---|---|---|---|
| {task} | {planned dimensions} | {stimulus} | {criterion} | {condition} |

### Actual Exposure

| Task | ACTUAL dose / exposure | Achieved Quality | Deviation | Reason / Context |
|---|---|---|---|---|
| {task} | NOT RECORDED | NOT RECORDED | PENDING | {record after execution} |

Before training, Actual remains NOT RECORDED.

After training, record what occurred. A smaller Actual Exposure after a quality
Stop Condition is not automatically displayed as failure.

Planned 4 x 30 m and Actual 3 x 30 m may be shown only when they are supplied
runtime data. The numbers here are explanatory syntax, not a prescription.

### Exposure Agreement

**Agreement status:** {Aligned / Meaningfully Different / Cannot Determine}

**Interpretation boundary:** {deviation is observation until reviewed}

## Post-Session Record Interface

This section captures the handoff; it does not implement Review Training.

### Actual Exposure

{link or compact record}

### Performance / Execution

{key observations and measurements}

### Immediate Response

{relevant immediate observations}

### Tissue Response

{athlete report or observation, non-diagnostic}

### Unexpected Event

{event, context, and consequence}

### Immediate Decision

{Maintain / Reduce / Modify / Temporarily Withdraw / Review as supplied}

### Review Required?

{Yes / No / Cannot Determine, scope, and destination}

### Feedback Destinations

- [Review Training Workflow](../workflows/review_training.md)
- [Build Athlete State Workflow](../workflows/build_athlete_state.md)
- [Update Planning State Workflow](../workflows/update_planning_state.md)

## EXPLAIN - Why This Session

This section follows execution content.

### Relation to Week

**Weekly Intent:** {reference}

**Session contribution:** {brief relationship}

**Higher-level intent preserved:** {what this Session does not change}

### Current Hypothesis

**Performance problem:** {brief}

**Candidate Bottleneck:** {supported, provisional, multiple, or Cannot
Determine}

**Intervention relationship:** {brief rationale}

### Current Uncertainty

> **PROVISIONAL - {claim or prescription element}**
>
> - Depends on: {assumption or missing information}
> - Narrower action supported: {bounded action}
> - Review trigger: {observation or event}

### Why This Changed

**Previous prescription reference:** {if modified}

**New evidence:** {source}

**Changed field:** {task, dose, condition, warning, or status}

**Decision scope:** {smallest justified level}

Do not place long theory before the execution view.

## Renderer Projection Contract

### COMPACT

Use TRAINING FIELD VIEW.

### STANDARD

Render SCAN, full EXECUTE, Planned vs Actual, Post-Session Record, and concise
EXPLAIN.

### EXPANDED

Add evidence, alternatives, provenance, and change trace without repeating
routine instructions.

On narrow screens, replace tables with stacked Task Cards while preserving
labels and order.

## Session View Invariants

1. Action precedes explanation.
2. Primary Work precedes supporting work.
3. Objective, dose, rest, quality, Stop, and Warning are immediately visible.
4. CONDITIONAL never looks mandatory.
5. OPTIONAL never looks required.
6. Planned dose never looks like completed exposure.
7. Actual remains NOT RECORDED until execution data exist.
8. Stop Conditions are not hidden in Notes.
9. Missing information does not render as STABLE.
10. State dimensions are not compressed into one readiness score.
11. Dose uses task-specific dimensions.
12. Task labels do not define stimulus.
13. The template does not invent dose, thresholds, or exercise selection.
14. Post-Session fields hand off to Review; they do not perform Review.
