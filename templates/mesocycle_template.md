# Mesocycle

Version: 0.1
Status: Draft
Date: 2026-09-15

> **VIEW CONTRACT** — This is the current adaptation-problem and state-change
> view. Populate it from the Mesocycle workflow and referenced state records.
> Do not turn it into a daily calendar or a fixed-duration biological claim.

> **ILLUSTRATIVE ONLY** — Tokens in braces and repeated blocks show presentation
> structure. They contain no athlete data, fixed exercise, dose, or duration.

Source interfaces:

- [Create Mesocycle Workflow](../workflows/create_mesocycle.md)
- [Create Week Workflow](../workflows/create_week.md)
- [Planning State Schema](../schemas/planning_state.md)
- [Athlete State Schema](../schemas/athlete_state.md)
- [Progression Rules](../rules/progression.md)
- [Stage Transition Rules](../rules/stage_transition.md)
- [Visual System](./visual_system.md)

## Identity and Status

| Field | Value |
|---|---|
| Mesocycle | {name or reference} |
| Parent Cycle | {cycle reference and version} |
| Lifecycle status | {status supplied by the authoritative planning record} |
| Mesocycle version | {version} |
| Review window | {provisional date range or event window} |
| Competition context | {nearest decision-relevant competition and role} |
| Current Week | {active Week reference or not yet created} |
| Last material update | {date and source event} |
| View density | STANDARD |

Allowed lifecycle labels are `DRAFT`, `PLANNED`, `ACTIVE`, `MODIFIED`,
`COMPLETED`, `CANCELLED`, `PAUSED`, `SUPERSEDED`, and `INVALIDATED`.
Render only a source-supplied value. A calendar date does not establish status.

## SCAN — Current Adaptation Decision

This layer should answer quickly: What problem are we solving now, what state
change are we seeking, what is Primary, and what could alter the decision?

### Current Adaptation Problem

**Problem:** {one concise sentence beginning with the performance problem,
current State, bottleneck or constraint, and Cycle relevance}

**Classification:** {DEFINED ADAPTATION PROBLEM, PROVISIONAL ADAPTATION PROBLEM,
MULTIPLE CANDIDATE PROBLEMS, or CANNOT DETERMINE}

**Cycle relationship:** {inherited strategic intent}

**Claim confidence:** {STRONG SUPPORT, MODERATE SUPPORT, PROVISIONAL, WEAK
SUPPORT, UNRESOLVED, or CANNOT DETERMINE YET}

### Desired State Change

**START STATE:** {current decision-relevant estimate}

-> **DESIRED EXIT STATE:** {direction or bounded state that would justify exit}

**100m relevance:** {expected performance relationship}

**Evidence of change:** {evidence capable of supporting the exit-state claim}

**Athlete alert:** {source-supplied STABLE or WATCH; source-mapped WARNING or REVIEW REQUIRED; never infer}

### Priority Structure

| Allocation | Object | Role in this problem | Exposure implication | Reallocation trigger | Confidence |
|---|---|---|---|---|---|
| `PRIMARY` | {leading current investment} | {adaptation or constraint relationship} | {protected direction} | {trigger} | {confidence} |
| `MAINTAIN` | {preservation target or None} | {what must be retained} | {represented maintenance direction} | {trigger} | {confidence} |
| `MINIMAL` | {bounded object or None} | {optionality, exploration, or familiarity} | {small justified footprint} | {trigger} | {confidence} |
| `TEMPORARILY WITHDRAWN` | {target or method, or None} | {why absent now} | {no planned exposure in current role} | {re-entry trigger} | {confidence} |

Allocation labels describe resource priority. They do not describe lifecycle
status or the progression decision state.

### Active Exceptions

> **WARNING — {warning title or None}**
>
> - **Affected exposure or decision:** {object}
> - **Required handling:** {modify, stop, review, or external action}
> - **Source and confidence:** {reference and confidence}

> **CONDITIONAL — {conditional exposure, intervention, or Week intent}**
>
> - **IF:** {explicit condition or observation}
> - **THEN:** {apply the item}
> - **ELSE:** {replacement, omission, or review route}

> **PROVISIONAL — {material hypothesis or state assumption}**
>
> - **Depends on:** {missing, indirect, or conflicting evidence}
> - **Recheck at:** {review event}

`CONDITIONAL` requires a trigger. `OPTIONAL` may be omitted even when feasible.
`REPLACEABLE` permits another route to the same intended stimulus. Keep each
badge separate from lifecycle status.

### Next Decision

**Decision:** {smallest next Mesocycle or Week decision}

**Trigger / deadline:** {response event, review window, or competition deadline}

**Information needed:** {minimum evidence capable of changing the decision}

**Destination:** {Create Week, Review Training, Mesocycle review, or Cycle review}

## EXECUTE — Exposure and Decision Strategy

At Mesocycle level, `EXECUTE` defines required adaptation, exposure, dose
direction, and Week constraints. It does not prescribe calendar days or every
Session.

### Required Adaptation and Exposure Strategy

| Priority object | Intended adaptation or preservation | Required exposure characteristics | Quality condition | Continuity need | Transfer opportunity | Incompatible condition |
|---|---|---|---|---|---|---|
| {object} | {develop, preserve, re-establish, stabilize, expose, explore, reduce cost, or protect expression} | {directional characteristics} | {quality required for meaning} | {broad need only when supported} | {sprint or competition relationship} | {condition that defeats the intent} |

Use `FIXED`, `CONDITIONAL`, `OPTIONAL`, or `REPLACEABLE` beside an exposure only
when the source decision supports that execution meaning.

### Interpreted Candidate Interventions

| Candidate | Execution conditions | Intended stimulus | Expected adaptation | Transfer hypothesis | Cost / risk | Feasibility | Confidence |
|---|---|---|---|---|---|---|---|
| {candidate task or Candidate Intervention Required} | {conditions that establish its identity} | {stimulus} | {adaptation claim} | {path and opportunity} | {recovery, tissue, interference, opportunity, or uncertainty} | {feasible, excluded, conditional, or unresolved} | {confidence} |

Show alternatives and trade-offs when no candidate has a justified lead. An
exercise name alone does not establish a stimulus.

### Dose Direction

| Exposure object | Task-specific dimension | Direction | Exposure role | Expected stimulus | Expected adaptation | Expected cost | Confidence |
|---|---|---|---|---|---|---|---|
| {object} | {dimension} | {INCREASE, MAINTAIN, REDUCE, STABILIZE, REDISTRIBUTE, EXPLORE, or TEMPORARILY WITHDRAW} | {development, maintenance, Minimal exploratory, or competition} | {direction} | {direction} | {cost profile} | {confidence} |

This is directional. Session distance, repetitions, sets, loads, contacts,
intensity, and recovery belong closer to execution.

### Stress-Organization Requirements

| Requirement status | Relationship to preserve | Stress dimension | Week implication | Review condition |
|---|---|---|---|---|
| REQUIRED | {quality, sequencing, separation, clustering, or recovery relationship} | {specific demand dimension} | {constraint for future Week construction} | {evidence that reopens it} |
| PREFERRED | {supported preference or None} | {dimension} | {preferred organization} | {when preference yields} |
| CONDITIONAL | {conditional structure or None} | {dimension} | {trigger-dependent implication} | {trigger} |
| UNRESOLVED | {organization question or None} | {dimension} | {flexibility to preserve} | {information needed} |

Do not infer a fixed High / Low structure. If High / Low is selected, name the
relevant stress dimensions and the athlete-specific conditions supporting it.

### Competition Context and Constraints

| Competition / constraint | Role or class | Mesocycle effect | Exposure implication | Deadline / review trigger | Confidence |
|---|---|---|---|---|---|
| {reference} | {competition role, Hard, Soft, or Unresolved} | {development, expression, feasibility, or recovery effect} | {what may be satisfied, replaced, reduced, or protected} | {trigger} | {confidence} |

Competition is an Actual Exposure and stressor. Do not append it to an otherwise
unchanged structure.

### Expected Evolution

| State or response domain | Expected direction | Observation context | Acceptable uncertainty | Deviation that challenges the plan |
|---|---|---|---|---|
| {decision-relevant domain} | {direction or bounded range} | {source and time relationship} | {uncertainty} | {meaningful deviation} |

Expected evolution is a hypothesis, not a promise or a fabricated future
Session result.

### Weekly Roadmap

This section is a projection of existing child Week plans. Source each block
from a `create_week` output or an authoritative Week reference. When a future
Week is not yet defined, render `NOT YET DEFINED`; do not invent its intent,
dose, or calendar placement from the Mesocycle alone.

#### {Week reference or NOT YET DEFINED}

- **Lifecycle status:** {source-supplied status}
- **Weekly intent:** {intent from the Week plan}
- **Priority emphasis:** {allocation and object}
- **Required exposure direction:** {concise direction}
- **Expected progression direction:** {supported direction, not automatic load}
- **Major constraint:** {constraint or None}
- **Competition relationship:** {relationship or None}
- **Review question:** {decision-relevant question}

Repeat only for Weeks that exist or are explicitly represented upstream. A
renderer may show these blocks as a timeline without changing their meaning.

### Monitoring Questions

| Question | Decision affected | Observation source and context | Comparison need | Remaining uncertainty |
|---|---|---|---|---|
| {question capable of changing a decision} | {decision and scope} | {source} | {baseline, protocol, or comparability} | {unknown or alternative} |

Do not display measurements that have no decision purpose merely because they
are available.

### Progression and Regression Interface

| Decision state | Target object / dimension | Evidence source | Expected-response comparison | Smallest scope | Review route |
|---|---|---|---|---|---|
| `MAINTAIN`, `PROGRESS`, `REDUCE`, `MODIFY`, `TEMPORARILY WITHDRAW`, or `TRANSITION` | {object and dimension} | {evidence} | {expected versus observed} | {Session, Week, or Mesocycle} | {destination} |

These are decision states from the existing Rules. They are distinct from the
priority allocation labels above.

### Exit and Continuation Gate

> **CONTINUE IF** — {adaptation problem remains relevant, hypothesis remains
> supported, marginal value remains sufficient, and constraints permit}

> **PROGRESS IF** — {evidence supports changing a named dose or exposure
> dimension while preserving the current problem and feasible space}

> **EXIT / TRANSITION IF** — {desired state is supported, another problem gains
> priority, marginal value declines, or competition timing changes emphasis}

> **REVIEW / INVALIDATE IF** — {hard constraint removes feasibility, repeated
> evidence challenges the hypothesis, or cost, risk, or transfer becomes
> unacceptable}

For each active condition, record:

- **Evidence required:** {source, context, and confidence requirement}
- **Destination:** {next Mesocycle, Cycle review, pause, or other review scope}
- **Current status:** {MET, NOT MET, WATCH, or CANNOT DETERMINE YET}
- **Confidence:** {canonical confidence label}

Calendar elapsed may open review. It is not sufficient evidence of exit.

### Extension and Early Exit

| Route | Condition | Opportunity cost / competition effect | Review scope | Confidence |
|---|---|---|---|---|
| EXTEND | {problem and hypothesis remain supported; progress remains plausible} | {cost of continuing} | {scope} | {confidence} |
| EARLY EXIT | {state reached early, priority changed, feasibility failed, or hypothesis weakened} | {effect of leaving now} | {scope} | {confidence} |

## EXPLAIN — Hypothesis and Decision Basis

Keep explanation behind the current action and exit logic. Use short,
traceable fields rather than a narrative essay.

### Adaptation Hypothesis

**Hypothesis:** {If the selected exposure produces the intended stimulus under
the required conditions, then the desired state may change in the stated
direction because of the proposed mechanism or athlete-specific history.}

**Competing explanations:** {material alternatives or None supported}

**What would weaken it:** {response, transfer, cost, or feasibility evidence}

**Confidence:** {canonical confidence label}

### Starting Athlete State Basis

- **State reference / version:** {authoritative current Athlete State}
- **Effective period / freshness:** {period and freshness status}
- **Relevant observation:** {fact or source record}
- **Interpretation:** {decision-relevant state claim}
- **Recent Actual Exposure / response:** {concise evidence}
- **Difference from Cycle assumption:** {None or explicit difference}

Only decision-relevant state dimensions belong here. Do not reduce the athlete
to one readiness score.

### Decision Logic

1. **Performance problem:** {observed problem}
2. **Candidate bottleneck or constraint:** {claim and alternatives}
3. **Desired state change:** {start -> exit state}
4. **Priority allocation:** {resource consequence}
5. **Exposure and dose direction:** {required direction}
6. **Expected response:** {what would support the hypothesis}
7. **Exit or review condition:** {what changes next}

### Constraints and Trade-offs

| Constraint or conflict | Class | Affected option | Feasible response | Displaced alternative | Confidence |
|---|---|---|---|---|---|
| {constraint} | {Hard, Soft, or Unresolved} | {option} | {response inside feasible space} | {trade-off} | {confidence} |

### Active Uncertainty

| Unknown or conflict | Decision affected | Consequence of error | Information needed | Next trigger | Current confidence |
|---|---|---|---|---|---|
| {uncertainty} | {decision} | {consequence} | {minimum useful observation} | {event} | {confidence} |

Preserve missing values as `Unknown`, `Not Assessed`, or `Missing`. Preserve
conflicting sources separately until an interpretation is supported.

### Change Trace and Higher-Level Review

- **Previous version:** {reference or None}
- **New evidence / constraint:** {source}
- **Changed fields:** {fields or None}
- **Reason:** {brief decision rationale}
- **Higher-level review flag:** {None or challenged Cycle assumption}
- **Flag consequence / confidence:** {effect and confidence}

### Week Handoff

- **Inherited Cycle intent:** {intent reference}
- **Current adaptation problem:** {problem}
- **Current Athlete State:** {state reference}
- **Priority allocation:** {allocation references}
- **Required exposure / dose direction:** {direction}
- **Feasible candidates:** {references or Candidate Intervention Required}
- **Stress requirements:** {requirements}
- **Competition constraints:** {constraints}
- **Monitoring and exit questions:** {decision interface}
- **Uncertainty to carry forward:** {open items}

## Renderer Projection Contract

- `COMPACT` retains identity, current problem, desired state change, PRIMARY,
  active exceptions, current Week, exit gate, and next decision.
- `STANDARD` renders SCAN and EXECUTE plus concise EXPLAIN fields.
- `EXPANDED` may reveal alternatives, provenance, and change history without
  changing semantic values.
- Narrow views stack tables or repeated blocks while retaining visible labels.
- Color or icon may reinforce a state but cannot replace its text label.

## View Invariants

1. The adaptation problem and desired state change define the Mesocycle.
2. PRIMARY, active warnings, conditional items, exit criteria, and next decision
   remain easy to scan.
3. Planned direction does not imply Actual Exposure or realized adaptation.
4. Lifecycle, priority, conditionality, athlete alert, confidence, and
   progression decision remain separate dimensions.
5. Weekly detail is rendered only from existing Week outputs or references.
6. No fixed phase name, duration, High / Low pattern, exercise library, or dose
   is introduced by the template.
7. Continue, progress, exit, extension, and invalidation depend on evidence,
   constraints, marginal value, and competition timing.
8. A renderer may change density and layout, but not source meaning.
9. Missing upstream data remains visible rather than being invented.
