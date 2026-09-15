# Week {Week ID}

Version: 0.1
Status: Draft
Date: 2026-09-15

> **VIEW CONTRACT** - This is the Exposure Organization view for one Week or
> Microcycle. Populate it from the Week workflow and referenced state records.
> It does not create training logic, fixed High/Low organization, or a
> seven-day requirement.

> **ILLUSTRATIVE ONLY** - Braced fields and repeated rows describe presentation
> structure. They are not athlete data, fixed dose, or a training plan.

Source interfaces:

- [Create Week Workflow](../workflows/create_week.md)
- [Planning State Schema](../schemas/planning_state.md)
- [Athlete State Schema](../schemas/athlete_state.md)
- [Competition Context Schema](../schemas/competition_context.md)
- [Visual System](./visual_system.md)
- [Mesocycle Template](./mesocycle_template.md)
- [Session Template](./session_template.md)
- [Review Template](./review_template.md)

## Identity and Status

| Field | Value |
|---|---|
| Week | {Week identity} |
| Parent Mesocycle | {reference} |
| Date range | {start to end, or unresolved} |
| Lifecycle status | {authoritative lifecycle status} |
| Version | {plan version} |
| Current position | {current day, Session, Review, or close state} |
| Competition proximity | {decision-relevant event and time relationship} |
| Last material update | {date and source event} |
| View density | STANDARD |

Use only authoritative lifecycle labels. Do not infer PLANNED, MODIFIED, or
CANCELLED from dates or apparent execution.

## SCAN - What Must Happen This Week

This layer should answer within seconds:

- What is the Weekly Intent?
- Which exposure is Primary?
- Where are key exposures placed?
- What is Conditional, Optional, or unavailable?
- Is a Warning or Review Required active?

### Weekly Intent

**Intent:** {one to three lines describing the required Week-level contribution
to the Mesocycle}

**Inherited adaptation problem:** {Mesocycle reference and concise problem}

**Expected Week contribution:** {direction of exposure or State support}

**Intent confidence:** {canonical confidence label}

### Current Athlete State Snapshot

| State dimension | Current decision-relevant state | Alert | Confidence |
|---|---|---|---|
| Performance expression | {current relevant expression} | {STABLE, WATCH, WARNING, REVIEW REQUIRED, or not supplied} | {confidence} |
| Exposure tolerance | {recent relevant tolerance} | {alert} | {confidence} |
| Fatigue and recovery | {multidimensional summary} | {alert} | {confidence} |
| Tissue state | {availability or supplied restriction} | {alert} | {confidence} |
| Technical stability | {only if relevant} | {alert} | {confidence} |

Do not collapse these dimensions into one readiness score. Missing information
must not render as STABLE.

### Priority Allocation

| Allocation | Current target | Required role this Week | Protection or boundary |
|---|---|---|---|
| **PRIMARY** | {primary target or exposure} | {leading current investment} | {what must be protected} |
| **MAINTAIN** | {maintenance target or None} | {preservation exposure} | {upper or interaction boundary} |
| **MINIMAL** | {minimal target or None} | {bounded deliberate footprint} | {why more is not justified} |
| **TEMPORARILY WITHDRAWN** | {withdrawn object or None} | {no current planned exposure} | {review or re-entry condition} |

Priority allocation is separate from Session status and progression decision.

### Active Warning and Exception

> **WARNING - {warning title or None}**
>
> - Affected exposure or decision: {scope}
> - Required response: {modify, stop, review, or external action}
> - Source and confidence: {reference and confidence}

> **REVIEW REQUIRED - {review title or None}**
>
> - Scope: {Session, Week, Mesocycle, or Cycle}
> - Before: {action that must wait or be reviewed}
> - Destination: {workflow or responsible process}

Warnings and Stop Conditions must not be hidden in Notes.

### Conditional and Optional Work

> **CONDITIONAL - {item or None}**
>
> - IF: {entry or State condition}
> - THEN: {execute or retain the planned role}
> - ELSE: {modify, replace, omit, or review}

> **OPTIONAL - {item or None}**
>
> - May be omitted because: {why the minimum Weekly Intent remains intact}
> - Cost or opportunity boundary: {when omission is preferred}

CONDITIONAL means a trigger must be satisfied. OPTIONAL means execution is not
required even when conditions allow it.

### Week at a Glance

| Day / Slot | Day type | Status | Main exposure or role | Priority | Stress meaning | Active exception |
|---|---|---|---|---|---|---|
| {slot} | {TRAIN / RECOVERY / OFF / COMPETITION / TRAVEL / ASSESSMENT} | {FIXED / CONDITIONAL / OPTIONAL / REPLACEABLE} | {exposure role or no training} | {PRIMARY / MAINTAIN / MINIMAL / WITHDRAWN / N/A} | {supported multidimensional description} | {Warning, condition, or None} |
| {slot} | {day type} | {status} | {exposure role} | {priority} | {stress meaning} | {exception} |
| {slot} | {day type} | {status} | {exposure role} | {priority} | {stress meaning} | {exception} |

Rows are created only for meaningful calendar slots. The view does not require
training every day or assume High/Low organization.

On a narrow screen, render each row as a stacked Day Card in this order:
Day/Status, Main Exposure, Priority, Warning, Condition, then supporting detail.

### Required Exposure Snapshot

| Exposure | Importance | Intended stimulus | Dose direction or bounds | Placement requirement | Completion meaning |
|---|---|---|---|---|---|
| {exposure} | {Required / Supporting / Conditional / Optional} | {intended stimulus} | {task-specific direction, not invented numbers} | {sequence, separation, or timing need} | {what useful Actual Exposure would mean} |
| {exposure} | {importance} | {stimulus} | {direction} | {placement} | {completion meaning} |

The snapshot makes required, supporting, Conditional, and Optional work visually
different. It does not treat all work as equally important.

## EXECUTE - Exposure Organization

### Week Grid

Use the Week-at-a-Glance grid or equivalent stacked cards as the primary
organization surface.

Each active slot should link to or contain a compact Session Brief:

- Session role and status;
- Primary objective;
- target exposure;
- entry-state assumptions;
- intended stimulus;
- dose direction and bounds;
- quality requirements;
- stress and tissue constraints;
- preceding and following exposure relationships;
- contingency;
- Review destination.

The Week view does not duplicate full Session prescription.

### Exposure Role Blocks

#### Primary Exposure

| Field | Presentation |
|---|---|
| Exposure | {required exposure} |
| Role | PRIMARY |
| Intended stimulus | {from Week output} |
| Dose direction | {task-specific direction or bounds} |
| Quality protection | {placement and interference protection} |
| Entry condition | {required State or environment} |
| Review question | {question capable of changing the decision} |

#### Supporting Exposure

| Field | Presentation |
|---|---|
| Exposure | {supporting exposure} |
| Allocation | {MAINTAIN or MINIMAL} |
| Contribution | {support to Weekly Intent} |
| Cost boundary | {what it must not compromise} |
| Replaceability | {method may change while role remains} |

#### Conditional Exposure

| Field | Presentation |
|---|---|
| Exposure | {conditional exposure} |
| Label | CONDITIONAL |
| IF | {trigger} |
| THEN | {planned role} |
| ELSE | {replacement, omission, or review} |
| Decision owner | {Session or Week scope} |

#### Optional Exposure

| Field | Presentation |
|---|---|
| Exposure | {optional exposure} |
| Label | OPTIONAL |
| Value | {possible benefit} |
| Opportunity cost | {what it could displace} |
| Omission effect | {why minimum Weekly Intent remains intact} |

### Multidimensional Stress and Cost Map

Do not display a synthetic total load score unless an upstream model supplies a
valid one.

| Exposure / Slot | Sprint demand | Strength demand | Plyometric demand | Competition demand | Tissue-sensitive demand | Residual or interaction note |
|---|---|---|---|---|---|---|
| {exposure} | {supported description} | {description} | {description} | {description} | {description} | {clustering, separation, or uncertainty} |

Show only dimensions with a defensible planning basis.

### Stress Organization

**Concentration logic:** {which demands are intentionally clustered and why}

**Separation logic:** {which exposures need separation and why}

**Sequencing logic:** {important order relationships}

**Recovery opportunities:** {real opportunities protected by the plan}

**Competition interaction:** {what competition supplies, replaces, or disrupts}

This section presents organization already produced by the Week workflow. It
does not impose High/Low structure.

### Planned Exposure Ledger

| Exposure | PLANNED role | PLANNED dose direction | Status | ACTUAL exposure | Agreement |
|---|---|---|---|---|---|
| {exposure} | {role} | {direction or bounds} | {planned / active / conditional} | NOT RECORDED | PENDING |

Before execution, Actual remains NOT RECORDED. Do not copy Planned values into
Actual fields.

After execution, Actual values may be linked from Session records and Reviews.
A difference is a deviation to interpret, not automatic failure.

### IF / THEN Adjustments

Keep this block easy to find.

#### Adjustment {ID}

**IF:** {State, quality, environment, or constraint condition}

**THEN:** {continue, modify, replace, reduce, withdraw, or review as supplied by
the plan}

**Affects:** {task, Session, or Week}

**Preserves:** {Weekly Intent or higher-level intent}

**Escalate when:** {condition challenging a higher-level assumption}

The template displays operational conditions supplied by workflows or Rules. It
does not invent thresholds.

### Session Briefs

#### {Session Reference}

| Field | Value |
|---|---|
| Slot | {day or time} |
| Status | {FIXED / CONDITIONAL / OPTIONAL / REPLACEABLE} |
| Role | {Primary / supporting / maintenance / minimal / competition / recovery} |
| Objective | {brief objective} |
| Main exposure | {exposure role} |
| Key constraint | {constraint or None} |
| Entry check | {current State requirement} |
| Destination | [Session View](./session_template.md) |

Repeat only for Sessions defined by the Week output.

### Competition, Travel, Recovery, and Assessment Slots

Non-training slots remain first-class Week objects.

For each relevant slot, show:

- type;
- purpose;
- fixed or conditional timing;
- stress or recovery consequence;
- exposure relationship;
- warning or constraint;
- next action.

OFF does not mean missing data. It is an explicit Week role when supplied.

## EXPLAIN - Why This Organization

Keep each explanation brief by default.

### Relation to Mesocycle

**Inherited intent:** {Mesocycle objective reference}

**Week contribution:** {why these exposures and this organization matter now}

**Higher-level assumptions preserved:** {assumptions not changed locally}

### Current State Basis

**State evidence used:** {current Athlete State reference}

**Relevant interpretation:** {brief interpretation}

**Material uncertainty:** {what remains provisional or unresolved}

### Exposure and Placement Rationale

**Why Primary appears first:** {relationship to priority and quality}

**Why demands are clustered or separated:** {interaction and recovery logic}

**Opportunity-cost decision:** {what was limited, omitted, or withdrawn}

### View-Layer Uncertainty

> **PROVISIONAL - {claim or plan element}**
>
> - Depends on: {assumption or missing information}
> - Narrower action still supported: {bounded action}
> - Review trigger: {new evidence or date}

Do not hide uncertainty in routine Notes.

## End-of-Week Review Hook

At Week close, display:

### Planned vs Actual

{References to Planned Exposure, Actual Exposure, and important deviations}

### Key State Changes

{Candidate State Delta or link to Athlete State update}

### Carry-Forward Issues

{active constraint, tissue concern, uncertainty, benchmark, or open question}

### Next Week Implication

{decision implication, not the next Week plan}

### Review and Summary Destinations

- [Review Training Workflow](../workflows/review_training.md)
- [Update Context Summary Workflow](../workflows/update_context_summary.md)
- [Build Athlete State Workflow](../workflows/build_athlete_state.md)
- [Update Planning State Workflow](../workflows/update_planning_state.md)

**Week close status:** {Review pending / Summary pending / State update pending /
Continuity updated}

Do not route directly to the next Week while required Review, State, Summary, or
Planning State work remains pending.

## Renderer Projection Contract

### COMPACT

Retain Week identity, Weekly Intent, Primary allocation, Week-at-a-Glance,
Warnings, Conditional work, and next action.

### STANDARD

Render all SCAN and EXECUTE sections plus concise EXPLAIN and Review Hook.

### EXPANDED

Add fuller evidence, constraints, rationale, source references, and historical
change trace without repeating routine prose.

## Week View Invariants

1. The Week is an Exposure Organization view.
2. Weekly Intent precedes calendar detail.
3. PRIMARY is visually distinct from supporting work.
4. CONDITIONAL never looks mandatory.
5. OPTIONAL never looks required.
6. Training is not required every day.
7. High/Low is not a fixed template.
8. Stress remains multidimensional.
9. Planned Exposure and Actual Exposure remain distinct.
10. Warnings and Stop or adjustment conditions remain visible.
11. Missing information does not render as STABLE.
12. Week detail does not replace Session execution detail.
13. The Review Hook precedes next-Week creation.
14. The template displays planning logic; it does not create it.
