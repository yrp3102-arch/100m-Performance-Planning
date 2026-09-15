# Cycle Overview

Version: 0.1
Status: Draft
Date: 2026-09-15

> **VIEW CONTRACT** — This is the strategic roadmap for a competitive horizon.
> Populate it from the Cycle workflow and referenced state records. Do not add
> daily prescriptions, fixed phase names, or future Session detail.

> **ILLUSTRATIVE ONLY** — Tokens in braces and repeated blocks show presentation
> structure. They contain no athlete data, calendar commitment, or training dose.

Source interfaces:

- [Create Cycle Workflow](../workflows/create_cycle.md)
- [Planning State Schema](../schemas/planning_state.md)
- [Athlete State Schema](../schemas/athlete_state.md)
- [Competition Context Schema](../schemas/competition_context.md)
- [Context Summary Schema](../schemas/context_summary.md)
- [Visual System](./visual_system.md)

---

## Identity and Status

| Field | Value |
|---|---|
| Cycle | {cycle name or cycle reference} |
| Athlete | {athlete reference} |
| Lifecycle status | {status supplied by the authoritative planning record} |
| Version | {cycle version} |
| Competitive horizon | {start boundary to terminal competition or horizon} |
| Current position | {active Mesocycle reference, review point, or not yet active} |
| Last material update | {date and source event} |
| View density | STANDARD |

Allowed lifecycle labels are `DRAFT`, `PLANNED`, `ACTIVE`, `MODIFIED`,
`COMPLETED`, `CANCELLED`, `PAUSED`, `SUPERSEDED`, and `INVALIDATED`.
Render only a status supplied by an authoritative source; never infer one from
dates or apparent completion.

---

## SCAN — Strategic Direction

### Terminal Objective

**Competitive 100m objective:** {one or two lines}

**Target context:** {competition, round, conditions, or horizon used to
interpret the objective}

**Supporting outcomes:** {supporting outcomes and their relationship to the
terminal objective; use None when absent}

**Objective confidence:** {STRONG SUPPORT, MODERATE SUPPORT, PROVISIONAL, WEAK
SUPPORT, UNRESOLVED, or CANNOT DETERMINE YET}

### Current Position

**YOU ARE HERE:** {Cycle position} -> {active Mesocycle or next review event}

**Current strategic state:** {one-line decision-relevant state summary}

**Next fixed deadline:** {competition deadline or None known}

### Strategic Performance Problem

**Observed problem:** {supported race or segment problem}

**Candidate bottleneck or limiting constraint:** {supported, provisional,
multiple candidates, or Cannot Determine}

**Why it matters now:** {relationship to the terminal objective and horizon}

**Athlete alert:** {source-supplied STABLE or WATCH; source-mapped WARNING or REVIEW REQUIRED; never infer}

**Claim confidence:** {canonical confidence label}

Do not turn an alert label into a diagnosis. Preserve observation,
interpretation, confidence, and source mapping as separate fields.

### Primary Constraints

- **Hard boundary:** {highest-consequence active hard constraint or None}
- **Feasible-space effect:** {what the constraint excludes or changes}

### Strategic Priority Snapshot

| Allocation | Current object or objects | Strategic role | Reallocation trigger | Confidence |
|---|---|---|---|---|
| `PRIMARY` | {scarce leading investment} | {problem and state-change relationship} | {review condition} | {confidence} |
| `MAINTAIN` | {preservation target or None} | {what must be retained} | {review condition} | {confidence} |
| `MINIMAL` | {bounded footprint or None} | {optionality, familiarity, or exploration} | {review condition} | {confidence} |
| `TEMPORARILY WITHDRAWN` | {withdrawn target or method, or None} | {reason and expected consequence} | {re-entry condition} | {confidence} |

Priority allocation is distinct from lifecycle status and from progression
decisions such as `MAINTAIN` or `PROGRESS`.

### Active Exceptions

> **WARNING — {warning title or None}**
>
> - **Affected decision:** {decision or planning level}
> - **Required response:** {review, modification, or external action}
> - **Source and confidence:** {source reference and confidence}

> **CONDITIONAL — {conditional item or None}**
>
> - **IF:** {explicit condition or observation}
> - **THEN:** {execute or retain the item}
> - **ELSE:** {alternative, omission, or review route}

`CONDITIONAL` means a stated trigger must be satisfied. `OPTIONAL` means the
item may still be omitted when conditions permit it. Keep those meanings
separate.

### Next Strategic Decision

**Decision:** {smallest next strategic decision}

**Trigger or deadline:** {event, evidence threshold, or fixed date}

**Required information:** {minimum decision-relevant evidence}

**Destination:** {workflow, review, or planning object}

---

## EXECUTE — Strategic Roadmap

At Cycle level, `EXECUTE` means follow the current strategic route and open the
next justified planning decision. It does not mean executing Session doses.

### Competition Structure

| Competition or window | Role | Date status | Performance opportunity | Exposure and stress implication | Confidence |
|---|---|---|---|---|---|
| {competition reference} | {Primary, Secondary, Benchmark, or unresolved} | {FIXED, CONDITIONAL, or unresolved date} | {decision-relevant opportunity} | {what it may satisfy, replace, or disrupt} | {confidence} |

Repeat only for decision-relevant competitions. Show travel, rounds, recovery,
or environmental constraints in the row when they change the route.

### Strategic State Trajectory

**Current State** -> **Intermediate State or States** -> **Competition-Ready
State**

| Transition | Desired decision-relevant change | Priority served | Evidence supporting transition | Principal constraint | Confidence |
|---|---|---|---|---|---|
| {state A -> state B} | {direction or bounded state} | {allocation and object} | {review evidence} | {constraint or uncertainty} | {confidence} |

Use as many transitions as the actual strategy requires. Do not convert the
trajectory into conventional phase names unless the source plan selected and
defined those names.

### Mesocycle Roadmap

Render one block for each ordered `mesocycle_brief`. A future renderer may map
the blocks to a horizontal timeline or stacked cards.

#### {sequence position}. {Mesocycle name or reference}

- **Lifecycle status:** {supplied status or NOT YET CREATED}
- **Current marker:** {YOU ARE HERE or blank}
- **Inherited Cycle intent:** {concise intent}
- **Adaptation problem:** {current or anticipated problem}
- **Desired state change:** {start-state assumption -> desired exit state}
- **Priority emphasis:** {PRIMARY object; other allocations only when relevant}
- **Required exposure direction:** {direction, not a Session prescription}
- **Competition relationship:** {development, expression, benchmark, stress, or none}
- **Major constraint:** {stress, recovery, timing, tissue, facility, or information constraint}
- **Expected response direction:** {decision-relevant direction}
- **Exit condition:** {state, evidence, constraint, or competition condition}
- **Review window:** {provisional window or event; never an automatic exit date}
- **Confidence / unresolved:** {confidence and the most material unknown}

Repeat the block without assuming a fixed number, duration, or naming scheme.

### Competition Integration

| Competition reference | Affected Mesocycle | Development / expression effect | Work replaced, reduced, or reinterpreted | Review need |
|---|---|---|---|---|
| {reference} | {Mesocycle reference} | {effect} | {strategic implication} | {review question or trigger} |

Competition remains both a performance opportunity and an Actual Exposure.

### Key Review Points

| Review event | Strategic question | Evidence to inspect | Default review scope | Escalation condition |
|---|---|---|---|---|
| {event} | {question} | {source or observation} | {smallest justified scope} | {condition requiring Cycle review} |

Calendar time may open review. It does not by itself prove progression,
completion, or transition.

### Conditions Requiring Cycle Revision

| Condition | Challenged assumption | Immediate handling | Required review scope | Status / confidence |
|---|---|---|---|---|
| {revision or invalidation condition} | {objective, competition structure, feasible space, or trajectory} | {pause, preserve, investigate, or route} | {scope} | {status and confidence} |

If a condition is active, surface `WARNING` or `REVIEW REQUIRED` in SCAN rather
than leaving it only in this table.

---

## EXPLAIN — Strategy Basis

This layer supports review and audit. Keep each rationale brief and traceable.

### Strategic Decision Chain

1. **Terminal objective:** {target and horizon}
2. **Cycle-start Athlete State:** {relevant state claim}
3. **Performance problem:** {observed problem}
4. **Candidate bottleneck:** {working explanation and alternatives}
5. **Constraints:** {feasible-space boundary}
6. **Priority:** {resource allocation consequence}
7. **State trajectory:** {intended strategic movement}
8. **Current Mesocycle brief:** {next bounded decision unit}

### Current Athlete State Basis

- **State reference / version:** {authoritative Athlete State reference}
- **Effective period and freshness:** {period and freshness status}
- **Decision-relevant observations:** {concise facts}
- **Interpretation:** {concise state estimate}
- **Competing explanations:** {alternatives or None supported}
- **Unresolved questions:** {questions that could change Cycle strategy}

### Constraints and Feasible Strategic Space

| Constraint | Class | Strategic effect | Effective period | Exit / review condition | Confidence |
|---|---|---|---|---|---|
| {constraint} | {Hard, Soft, or Unresolved} | {excluded or modified strategic option} | {period} | {condition} | {confidence} |

**Feasible strategic space:** {one to three lines describing what remains
admissible after hard constraints}

### Strategic Uncertainty Register

| Affected claim | Why it matters | Consequence of error | Reversibility | Information that could reduce uncertainty | Review trigger | Confidence |
|---|---|---|---|---|---|---|
| {unknown or conflict} | {decision relevance} | {consequence} | {reversible or difficult to reverse} | {minimum useful information} | {event} | {confidence} |

Keep missing, conflicting, and unresolved information visible. Do not average
conflicting evidence or turn absence into a favorable value.

### Change Trace

- **Previous Cycle version:** {reference or None}
- **New evidence or constraint:** {material change source}
- **Changed fields:** {fields or None}
- **Decision rationale:** {brief reason}
- **Superseded assumptions:** {assumptions or None}
- **Source references:** {plan, state, review, summary, or competition records}

### Mesocycle Handoff

- **Selected brief:** {mesocycle_brief reference}
- **Inherited intent that must remain visible:** {Cycle intent}
- **Start-state assumption to refresh:** {assumption}
- **Priority allocation:** {allocation references}
- **Constraints and competition relationship:** {handoff summary}
- **Uncertainty to carry forward:** {open items}
- **Higher-level review flag:** {None or challenged Cycle assumption with evidence}

---

## Renderer Projection Contract

- `COMPACT` retains identity, objective, current position, PRIMARY allocation,
  active exceptions, current roadmap block, and next decision.
- `STANDARD` renders all SCAN and EXECUTE sections plus concise EXPLAIN fields.
- `EXPANDED` may reveal full rationale, provenance, alternatives, and change
  history without changing semantic values.
- Narrow views stack table rows or roadmap blocks while preserving labels and
  reading order.
- Color, icon, shape, or card styling may reinforce meaning but must never
  replace the visible text label.
- Empty fields render as `Unknown`, `Not Assessed`, `Not Applicable`, or `None`
  according to the source. They are never silently treated as normal.

## View Invariants

1. The Cycle remains a strategic roadmap, not a Session calendar.
2. Current position and active exceptions appear before historical rationale.
3. PRIMARY remains scarce and visually precedes supporting allocations.
4. Lifecycle, priority, conditionality, athlete alert, and confidence remain
   distinct semantic dimensions.
5. Planned direction never implies Actual Exposure or completed adaptation.
6. Conditional work never appears mandatory.
7. Uncertainty remains attached to the claim and decision it affects.
8. Mesocycle exit conditions depend on state, evidence, constraints, and
   competition timing rather than elapsed time alone.
9. A renderer may change density and layout, but not meaning or source status.
10. Missing upstream data stays missing; the View Layer does not invent it.
