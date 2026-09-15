# Templates

## Purpose

The templates directory defines the View Layer for plans and reviews produced by the 100m Performance Planning system.

Templates make authoritative planning information scannable, executable, and reviewable. They do not decide what training means or what an athlete should do.

The governing flow is:

Planning Logic → View Model → Renderer

- Core Models, Rules, and Workflows provide Planning Logic.
- Templates provide the renderer-independent View Model.
- A future renderer controls the final Markdown, Notion, HTML, PDF, Web UI, or Mobile UI presentation.

## Boundary

Templates define:

- required visible information;
- reading order;
- grouping and comparison structure;
- controlled semantic labels;
- compact, standard, and expanded projections;
- interfaces for execution and review.

Templates do not:

- allocate priorities;
- select exercises or methods;
- prescribe a fixed dose;
- interpret Athlete State;
- replace a Workflow;
- invent missing values;
- infer completion from a prescription;
- store live athlete or plan data;
- define HTML, CSS, JavaScript, or vendor-specific properties.

Visual presentation must preserve the meaning supplied by the planning system. It must never become a second planning engine.

## Files

| File | View | Core question |
|---|---|---|
| [Visual System](./visual_system.md) | Shared presentation contract | How is meaning prioritized consistently? |
| [Cycle Template](./cycle_template.md) | Strategic Roadmap | Where are we trying to move the athlete across the competition horizon? |
| [Mesocycle Template](./mesocycle_template.md) | Adaptation Problem and State Transition | What State change are we trying to create now? |
| [Week Template](./week_template.md) | Exposure Organization | What must happen this Week, and how should exposures coexist? |
| [Session Template](./session_template.md) | Execution Interface | What exactly do I do now? |
| [Review Template](./review_template.md) | Observation → Interpretation → Decision | What happened, and what changes now? |

## Reading Contract

Every view follows three reading layers:

### SCAN

The first visible block answers:

- What is the objective?
- What is Primary?
- What happens now or next?
- Is anything conditional, under warning, or blocked?
- Is a material claim provisional or unresolved?

### EXECUTE

The action layer supplies the level-appropriate instruction:

- roadmap and review points at Cycle level;
- exposure strategy and exit criteria at Mesocycle level;
- exposure organization and adjustments at Week level;
- dose, rest, quality, stop, and adjustment at Session level;
- decision and handoff actions at Review level.

### EXPLAIN

The final layer preserves concise rationale, State interpretation, constraints, uncertainty, confidence, evidence, and change history.

Long explanation must not precede immediate action.

## Shared Semantics

All templates use the labels defined in the [Visual System](./visual_system.md).

The main axes remain separate:

- Priority: PRIMARY, MAINTAIN, MINIMAL, TEMPORARILY WITHDRAWN.
- Lifecycle: DRAFT, PLANNED, ACTIVE, MODIFIED, COMPLETED, CANCELLED, PAUSED, SUPERSEDED, INVALIDATED.
- Execution condition: FIXED, CONDITIONAL, OPTIONAL, REPLACEABLE.
- Athlete-State alert: STABLE, WATCH, WARNING, REVIEW REQUIRED.
- Confidence: STRONG SUPPORT, MODERATE SUPPORT, PROVISIONAL, WEAK SUPPORT, UNRESOLVED, CANNOT DETERMINE YET.
- Provenance: PLANNED, ACTUAL, OBSERVATION, INTERPRETATION.

A renderer may add color, icon, shape, card, callout, or timeline treatment. Visible text remains authoritative.

## Unified Information Order

Templates adapt this sequence to their planning level:

Identity / Status → Objective → Current State → Priority → Action / Exposure → Conditions / Warnings → Monitoring → Rationale → Next Decision

Exceptions move earlier when they change immediate action. Different planning levels do not mechanically repeat one layout.

## Density

Each template defines one information contract. A renderer may project it at:

- COMPACT for training-field and narrow mobile use;
- STANDARD for normal planning and review;
- EXPANDED for coaching analysis and audit.

STANDARD is the default. Density changes displayed resolution, not semantic meaning.

COMPACT must retain the objective, Primary action, active warning, conditionality, Stop condition, critical uncertainty, and next action.

## Renderer Targets

The canonical files are plain, readable Markdown. Their structures may map naturally to:

- Markdown headings, lists, tables, and blockquotes;
- Notion headings, callouts, statuses, selects, tables, and toggles;
- HTML or Web cards, grids, timelines, and disclosures;
- PDF page sections, tables, timelines, and execution cards;
- Mobile stacked blocks and Training Field View.

The templates do not depend on a specific renderer, storage product, database, front-end framework, or plugin.

## Data and Authority

Template fields must come from existing Workflow outputs, referenced schemas, or explicit user-supplied data.

When a field is unavailable:

- retain Missing, Unknown, Not Assessed, Not Recorded, or Not Applicable;
- do not manufacture training logic;
- do not copy Planned values into Actual fields;
- identify a VIEW_INTERFACE_GAP when the view requires an upstream value that no current interface supplies.

PLANNED, MODIFIED, and CANCELLED are supported view labels but are not yet normalized by the current Planning State lifecycle vocabulary. Render them only when an authoritative upstream value is supplied.

## Runtime and Storage

These files are reusable contracts. They do not contain real athlete records or live plan instances.

Runtime information belongs in a replaceable external persistence layer. References, version history, source provenance, and raw records remain available even when a compact view omits their detail.

Renderer independence and storage independence are separate requirements. Neither authorizes loss of status, conditions, uncertainty, or provenance.

## Authoring Rules

When producing a view:

1. load the authoritative planning object and relevant current State;
2. map only supported fields into the template;
3. preserve semantic labels and provenance;
4. place SCAN before EXECUTE and EXPLAIN;
5. promote active warnings and Stop conditions;
6. distinguish required, Conditional, Optional, and Replaceable work;
7. distinguish Planned Exposure from Actual Exposure;
8. keep rationale brief unless expanded detail is requested;
9. preserve source and version references where decisions require traceability;
10. validate the result against the Visual System invariants.

Synthetic examples must be minimal and marked ILLUSTRATIVE ONLY. They must not imply fixed sprint volumes, recovery intervals, intensities, phase lengths, exercise libraries, or weekly structures.

## Failure Boundary

Reject a rendered view when it:

- becomes a wall of text;
- gives everything equal visual priority;
- depends on color or icons alone;
- puts theory before action;
- hides Warning or Stop conditions;
- makes Conditional work look mandatory;
- makes Planned work look completed;
- presents unresolved information as certain;
- turns a Cycle into a detailed Session calendar;
- treats High / Low, phase names, or exercise choices as fixed template logic.

The [Visual System](./visual_system.md) defines the complete prohibited-pattern list and correction rules.
