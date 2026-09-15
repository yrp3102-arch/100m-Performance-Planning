# Visual System

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This document defines the visual semantics for every plan and review view in the 100m Performance Planning system.

It specifies how already-decided information is ordered, labeled, grouped, and reduced for different reading conditions.

It supports three outcomes:

- a coach can identify the current objective, priority, exception, and next action quickly;
- an athlete can execute a Session without reading the planning rationale;
- a reviewer can recover the interpretation, uncertainty, and decision trace.

This is a presentation contract. It does not allocate priorities, select training content, prescribe dose, interpret Athlete State, or make review decisions.

## System Boundary

The governing separation is:

Planning Logic → Output Schema → Visual Presentation → Renderer

Planning Logic ≠ Output Schema ≠ Visual Presentation ≠ Renderer.

- Models, Rules, and Workflows determine what a plan means.
- Workflows produce or reference the authoritative planning objects.
- Templates define which information a view must present.
- This Visual System defines how that information is prioritized visually.
- A renderer maps the contract to Markdown, Notion, HTML, PDF, Web UI, or Mobile UI.

Visual emphasis never creates planning authority. A renderer must not infer a status, priority, warning, confidence state, completed dose, or clinical meaning from layout.

Runtime athlete data remains outside this repository. Templates and this specification contain structure and minimal illustrative placeholders only.

## Information Hierarchy

Use this default order:

Identity / Status → Objective → Current State → Priority → Action / Exposure → Conditions / Warnings → Monitoring → Rationale → Next Decision

Adapt the order to the planning level while preserving these principles:

1. Important before detailed.
2. Action before explanation.
3. Current before historical.
4. Primary before supporting.
5. Exception before routine detail.
6. Warning before the action it can stop or modify.
7. Conditional work must look conditional at first encounter.
8. Planned and Actual information must remain visibly separate.
9. Uncertainty must remain attached to the claim it qualifies.
10. Visual complexity must earn its place.

When an exception changes immediate action, move the exception into the first visible block rather than preserving normal section order.

Do not solve hierarchy by repeating the same label in many locations. Use one canonical summary location and local references where needed.

## Reading Layers

Every view supports three reading layers in this order.

### Layer 1 — SCAN

SCAN answers within a few seconds:

- What object am I viewing?
- What is its lifecycle status?
- What is the objective?
- What is Primary?
- What must happen now or next?
- Is anything conditional, stopped, or under warning?
- Is a material claim provisional or unresolved?

SCAN content is short, current, and decision-relevant. It belongs at the top of the view.

Typical SCAN fields are:

- identity and effective date or horizon;
- status and version;
- objective or intent;
- current position;
- Primary allocation;
- active warning or review requirement;
- conditionality;
- next action or next decision.

### Layer 2 — EXECUTE

EXECUTE contains the information needed to act.

At Session level it includes:

- task or exposure;
- distance, duration, repetitions, and sets when relevant;
- load, contacts, or other task-specific dose dimensions;
- rest or recovery;
- intensity reference or execution intent;
- quality standard;
- stop or modification condition;
- conditional adjustment;
- recording fields for Actual Exposure.

At broader levels it includes the actionable roadmap, exposure strategy, weekly organization, monitoring question, exit condition, and review point appropriate to that level.

EXECUTE must not require the user to reconstruct instructions from rationale.

### Layer 3 — EXPLAIN

EXPLAIN supports review, audit, and deeper understanding.

It may include:

- decision rationale;
- Athlete State interpretation;
- Candidate Bottleneck or adaptation hypothesis;
- supporting and conflicting evidence;
- confidence and uncertainty;
- active constraints;
- expected response;
- why a plan changed;
- source and version references.

Keep explanations brief by default. Detailed theory appears only when explicitly requested or needed for audit. EXPLAIN never precedes SCAN or displaces execution-critical information.

### Layer Behavior by View

| View | SCAN | EXECUTE | EXPLAIN |
|---|---|---|---|
| Cycle | objective, horizon, Primary priorities, current position | strategic roadmap and review points | strategic problem, constraints, uncertainty |
| Mesocycle | current adaptation problem and desired State change | exposure strategy, weekly direction, exit criteria | hypothesis, monitoring logic, alternatives |
| Week | weekly intent, Primary exposure, exceptions | day grid, required exposures, adjustments | stress logic, constraints, carry-forward rationale |
| Session | today's objective, Primary Work, warning, stop | dose, rest, quality, adjustments | relation to Week, hypothesis, uncertainty |
| Review | reviewed object, key exception, decision, next action | update and handoff actions | observation, interpretation, confidence, decision trace |

## Semantic Labels

Semantic labels are controlled text values, not decorative copy. Render them consistently in uppercase.

Every label must:

- remain visible as text;
- identify its semantic axis;
- retain the same meaning at Cycle, Mesocycle, Week, Session, and Review levels;
- remain understandable without color;
- come from an authoritative source or remain explicitly unassigned.

The main semantic axes are independent:

| Axis | Question answered |
|---|---|
| Priority | What receives scarce planning resources? |
| Lifecycle | Where is the planning object in its authoritative lifecycle? |
| Execution condition | Under what condition or scheduling protection does it apply? |
| Athlete-State alert | What current signal requires attention or review? |
| Confidence | How well supported is this specific claim? |
| Decision | What changes after review? |
| Provenance | Is this Planned, Actual, Observed, or Interpreted? |

Never collapse several axes into one badge. For example, ACTIVE · CONDITIONAL · PROVISIONAL communicates three distinct facts and must not become a single vague status.

## Priority Semantics

Use exactly these allocation labels:

| Label | Meaning | Presentation obligation |
|---|---|---|
| PRIMARY | Strongest current claim on development resources | Place first and show the protected object or exposure |
| MAINTAIN | Active retention allocation | Show the preservation target; do not present it as secondary development |
| MINIMAL | Smallest currently justified deliberate footprint | Show its bounded role and do not imply guaranteed maintenance |
| TEMPORARILY WITHDRAWN | No planned exposure in the current role | Show the reason and review or re-entry condition |

Priority labels describe allocation roles. They do not describe biological importance, expected outcome, lifecycle, feedback decision, or exercise category.

Presentation rules:

- name the object that holds the allocation;
- show at least one Primary item when supplied by the plan;
- never promote an item to Primary because it appears first;
- never use vague replacements such as important, very important, or more important;
- keep Primary scarce in visual emphasis;
- show Maintain, Minimal, and Temporarily Withdrawn as deliberate decisions;
- preserve confidence and review triggers when supplied;
- do not infer allocation from dose size or typography.

The same priority label means the same thing across all planning levels. Its scope must still be visible.

Recommended semantic tokens are:

- priority-primary;
- priority-maintain;
- priority-minimal;
- priority-temporarily-withdrawn.

Tokens are renderer hints and do not replace visible labels.

## Plan Status Semantics

### Lifecycle Status

Use lifecycle status only when supplied by an authoritative planning object.

| Label | Meaning |
|---|---|
| DRAFT | Defined but not authoritative for execution |
| PLANNED | Authoritatively prospective and not yet active |
| ACTIVE | Currently guides planning or execution |
| MODIFIED | Authoritative current presentation differs materially from its referenced prior version |
| COMPLETED | Reached its close under the applicable completion criteria |
| CANCELLED | Deliberately ended before completion without asserting foundational invalidity |
| PAUSED | Temporarily suspended without completion |
| SUPERSEDED | Replaced by a newer authoritative version and retained as history |
| INVALIDATED | Foundational assumptions no longer justify use |

MODIFIED is a lifecycle or version display state only when the source explicitly provides that state. The Review decision MODIFY does not automatically make a plan MODIFIED.

CANCELLED and INVALIDATED are distinct. Cancellation records a deliberate end. Invalidation records loss of the assumptions that justified use.

PLANNED, MODIFIED, and CANCELLED are required presentation semantics but are not yet normalized in the current Planning State lifecycle contract. Until an upstream contract supplies them, a renderer must not infer them. This is a VIEW_INTERFACE_GAP, not permission for template-side logic.

### Execution and Scheduling Status

Render execution condition beside lifecycle status while preserving it as a separate axis.

| Label | Meaning |
|---|---|
| FIXED | Time or role is constrained enough that moving it materially changes the Week |
| CONDITIONAL | Execute only when a stated condition is satisfied |
| OPTIONAL | May be omitted without compromising the current minimum intent |
| REPLACEABLE | Exposure role remains required while the selected method may change |

FIXED does not mean complete the full dose regardless of State. REPLACEABLE does not mean unimportant. CONDITIONAL and OPTIONAL are never synonyms.

Recommended tokens include status-active, status-paused, status-conditional, and status-optional. Visible text remains mandatory.

## Athlete-State Semantics

Athlete State is a current, decision-relevant estimate under uncertainty. The view must not reduce it to one readiness score.

Keep these source concepts distinct:

- completeness, such as CURRENT_STATE, PARTIAL_STATE, PROVISIONAL_STATE, or DECISION_BLOCKED_BY_MISSING_INFORMATION;
- value status, such as Known, Estimated, Uncertain, Not Assessed, Missing, or Not Applicable;
- trend, such as Improving, Stable, Declining, Mixed, Unresolved, or Cannot Determine;
- visual alert, defined below;
- claim-specific confidence.

Use the following alert labels for concise presentation:

| Label | Meaning | Required companion |
|---|---|---|
| STABLE | Relevant current evidence is sufficiently consistent for the named decision | scope and effective time |
| WATCH | A decision-relevant signal needs closer observation | what to watch and next trigger |
| WARNING | A consequential signal may require immediate modification or stopping | affected action and response |
| REVIEW REQUIRED | A named decision must be reviewed before the specified continuation or escalation | review scope and destination |

STABLE is not a declaration of perfect health, full recovery, or universal readiness. Missing information must not render as STABLE.

WATCH and WARNING are planning alerts, not medical diagnoses. Use wording such as Tissue State: WATCH. Do not invent diagnoses from symptoms, observations, or warning labels.

An alert must identify the state dimension and affected decision. A general badge without scope is insufficient.

Recommended tokens include state-stable, state-watch, state-warning, and state-review-required.

## Confidence Semantics

Use the qualitative states defined by the Feedback-Decision Core Model:

| Display label | Meaning |
|---|---|
| STRONG SUPPORT | Converging, relevant, sufficiently reliable evidence supports the claim and material alternatives are limited |
| MODERATE SUPPORT | Relevant evidence supports the claim while meaningful limitations or alternatives remain |
| PROVISIONAL | The claim is useful now but depends on limited or indirect evidence |
| WEAK SUPPORT | Some evidence is compatible with the claim but does not distinguish it well from alternatives |
| UNRESOLVED | Material competing interpretations remain without a justified leader |
| CANNOT DETERMINE YET | Available information cannot support the required distinction or decision |

Confidence is attached to a named claim. Do not display one global confidence badge for an entire athlete or plan when material claims differ.

Place confidence beside:

- a Candidate Bottleneck;
- a State interpretation;
- a priority rationale;
- an expected response;
- a review interpretation;
- a decision rationale;
- a material uncertainty.

PROVISIONAL and UNRESOLVED must be visible in SCAN when they materially condition the current plan. CANNOT DETERMINE YET must state what cannot be determined and what narrower action remains possible.

Do not translate qualitative confidence into unsupported percentages. Do not upgrade confidence through compression or visual polish.

Recommended tokens include confidence-strong-support, confidence-moderate-support, confidence-provisional, confidence-weak-support, confidence-unresolved, and confidence-cannot-determine-yet.

## Warning Semantics

A warning is an exception that can alter execution, feasibility, safety, review scope, or the validity of a current assumption.

Start every warning block with visible text:

WARNING — concise issue

A complete warning block contains:

- affected object or action;
- current signal or constraint;
- why it matters now;
- required action, modification, or stop;
- review or escalation destination;
- confidence or uncertainty when material;
- source or effective time when relevant.

Place an active warning:

- in the SCAN layer;
- immediately before affected execution content;
- again only where local action would otherwise be ambiguous.

Do not bury warnings in Notes, rationale, footnotes, hover states, or color. Do not dilute warnings by styling routine information identically.

REVIEW REQUIRED can accompany WARNING when a review is the required action. Neither label creates a diagnosis.

## Conditionality Semantics

Represent conditional work as an explicit decision structure:

IF → condition or observation THEN → action ELSE → fallback, omission, or review destination

Every Conditional item should identify:

- the condition being tested;
- when and how it is checked;
- the action if satisfied;
- the action if not satisfied;
- the objective that remains protected;
- the level to review if the condition fails.

Do not use may adjust, as needed, or if necessary without an interpretable trigger and destination.

Optional work may still have an inclusion condition, but satisfying that condition does not make execution mandatory.

Conditional work must carry the CONDITIONAL label in the SCAN and EXECUTE layers. Its typography, border, shape, or icon may differ from routine work, but text must carry the meaning.

Unknown decision-critical conditions must remain Unknown, Unresolved, or CANNOT DETERMINE YET. They must not default to satisfied.

## Dose Presentation

Dose is multidimensional and task-specific. Show only dimensions relevant to interpreting and executing the exposure.

Possible dimensions include:

- task or mode;
- distance or duration;
- repetitions and sets;
- frequency or distribution;
- rest interval and density;
- target or actual velocity;
- intensity reference;
- external load;
- contacts;
- surface or slope;
- technical or quality criterion;
- stop and modification rule.

Use a compact labeled block for one task. Use a table when several tasks share comparable dimensions. Do not force every training type into one universal field set.

Keep these objects visibly distinct:

- PRESCRIPTION;
- PLANNED EXPOSURE;
- ACTUAL EXPOSURE;
- ACHIEVED QUALITY;
- INTERNAL RESPONSE.

Every recorded dose must state whether it is PLANNED or ACTUAL. If Actual Exposure has not been recorded, show NOT RECORDED or leave an explicitly labeled field empty. Never copy Planned values into Actual fields.

Do not create unsupported composite load scores. Labels such as sprint, strength, plyometric, or recovery do not establish actual demand.

Stop conditions must have visibility equal to or greater than dose.

## Time Presentation

Time establishes sequence, horizon, and review context. It does not predict adaptation by itself.

Show, as applicable:

- effective date or date range;
- competition horizon;
- current position;
- sequence relationship;
- review point;
- deadline;
- condition-based exit;
- last verified or updated time.

Use explicit dates when known. Use relative labels such as next review only when anchored to an event or condition.

Do not imply that:

- a Mesocycle ends because a fixed number of weeks elapsed;
- progression occurs because the next calendar cell arrived;
- an unverified historical State is current;
- a provisional future Session is guaranteed.

For planned future items, retain status and uncertainty. For completed items, distinguish planned timing from actual timing when they differ.

## Card and Section Structure

A card is a semantic grouping, not a required UI component. In plain Markdown, a heading plus a short structured block may represent it.

Supported semantic card roles include:

- OBJECTIVE CARD;
- PRIORITY CARD;
- CURRENT STATE CARD;
- SESSION CARD;
- WARNING CARD;
- CONDITIONAL CARD;
- REVIEW CARD;
- NEXT DECISION CARD.

A card should contain:

1. a role label or heading;
2. one main statement;
3. only the fields required to act or interpret;
4. local status, condition, or confidence when relevant;
5. a clear next action when the card requests one.

Default limits are one or two lines for an Objective and one short paragraph each for priority rationale, Session rationale, and decision explanation.

Do not make every paragraph a card. Do not split one decision across many decorative blocks. Do not use a card boundary to hide semantic relationships.

Keep Objective, Primary Work, Warning, Stop, Decision, and Next Action easy to locate across every template.

## Table Usage

Use a table when users must compare repeated objects across the same dimensions.

Good uses include:

- priority allocation;
- Cycle roadmap entries;
- weekly exposure organization;
- repeated task doses;
- Planned versus Actual comparison;
- observation and interpretation separation;
- carry-forward items.

Avoid a table when:

- content needs multi-paragraph rationale;
- uncertainty or competing interpretations require context;
- cells contain several nested lists;
- one object has no meaningful peers;
- narrow-screen reading would destroy the relationship.

Table rules:

- use explicit column headings;
- keep one semantic object per row;
- include units in the value or heading;
- do not use blank cells to mean zero, normal, or completed;
- write Not Applicable, Missing, Unknown, or Not Recorded when material;
- retain status labels as text;
- provide a stacked structured-block alternative for narrow screens;
- do not make a table the only accessible representation of critical action.

## Timeline Usage

Use a timeline only when sequence or current position matters.

Recommended mappings are:

- Cycle: strategic Mesocycle roadmap;
- Mesocycle: Week-level direction and expected State evolution;
- Week: calendar or exposure grid;
- Session: ordered execution sequence;
- Review: Observation → Interpretation → Decision → Next Action.

Every timeline item should identify:

- object or event;
- purpose or intent;
- status;
- time relationship;
- condition or exit point when relevant.

Highlight current position with text such as YOU ARE HERE or CURRENT. Do not rely on position or color alone.

Timeline entries at Cycle level must not contain invented Session detail. Expected evolution is directional and must not become false future precision. Phase names come from the actual plan; the Visual System defines no fixed phase vocabulary.

## Mobile and Training-Field Scanability

On a narrow screen, preserve this order:

1. Objective;
2. Status and conditionality;
3. Primary Work or Primary Exposure;
4. Active Warning;
5. Dose and Rest;
6. Quality;
7. Stop or Modify condition;
8. Actual record fields;
9. explanation.

TRAINING FIELD VIEW is the COMPACT projection of a Session. It shows only:

- Objective;
- Main Work;
- Dose;
- Rest;
- Quality;
- Stop;
- Warning;
- conditional adjustment.

Training Field View must be usable without sideways scrolling. Convert wide tables into stacked task blocks. Repeat column headers or task identity when content crosses pages.

Keep labels short, values close to their labels, and one action per line when rapid scanning matters. Do not hide Stop, Warning, or Conditional meaning behind expansion controls.

## Accessibility

Every semantic state must be perceivable without color.

Use:

Color
+
Text label
+
optional icon or shape

Rules:

- never use color as the only carrier of meaning;
- never use an icon as the only carrier of meaning;
- keep visible text for status, warning, priority, and confidence;
- use heading order that reflects reading order;
- use descriptive link text;
- preserve sufficient contrast in any renderer;
- do not encode order through spatial position alone;
- repeat table headers across pages when supported;
- provide stacked alternatives to complex tables;
- avoid all-caps paragraphs even though controlled labels are uppercase;
- keep units, dates, and conditions explicit;
- make empty, Missing, Not Applicable, and Not Recorded distinguishable.

Icons are optional. If used, they reinforce a label and never replace it.

## Renderer Independence

Plain Markdown is the canonical readable form. The templates may use:

- headings;
- short paragraphs;
- lists;
- compact tables;
- bold labels;
- blockquotes for visible exceptions;
- semantic text tokens.

The templates must not depend on:

- HTML-only layout;
- CSS;
- JavaScript;
- a specific component library;
- a special Markdown plugin;
- a Notion database or property name;
- a particular PDF engine;
- a specific storage adapter.

A renderer may map:

- a section to a card;
- a WARNING block to a callout;
- a controlled label to a status or select field;
- a roadmap to a horizontal timeline or stacked phase cards;
- a Mesocycle to problem and State-transition cards;
- a Week table to a calendar or exposure grid;
- a Session task block to a vertical execution card;
- EXPLAIN content to an accessible disclosure region.

The mapping must preserve order, labels, content, conditions, provenance, and uncertainty.

Semantic tokens may include:

- priority-primary;
- state-watch;
- state-warning;
- confidence-provisional;
- status-conditional;
- provenance-planned;
- provenance-actual.

Tokens do not define colors, CSS classes, database fields, or storage keys.

## Visual Density

Every template has one information contract and three potential projections:

| Density | Use | Required behavior |
|---|---|---|
| COMPACT | Training field, narrow mobile, quick handoff | Preserve immediate action, conditions, warning, stop, and critical uncertainty |
| STANDARD | Default planning and review | Present SCAN, EXECUTE, and concise EXPLAIN |
| EXPANDED | Coach analysis, audit, detailed review | Add evidence, alternatives, provenance, and fuller decision trace |

STANDARD is the default. Do not create three independent template schemas.

Density changes visible resolution. It does not change truth, status, priority, or the source object.

COMPACT may omit routine explanation and secondary historical detail. It must not omit:

- the current objective;
- Primary work or exposure;
- active warning;
- stop or modification condition;
- conditionality;
- critical provisional or unresolved status;
- the next required action.

EXPANDED adds traceability and context. It must not repeat the same prose merely to appear complete.

## Visual Invariants

1. Planning Logic, output structure, visual presentation, and rendering remain separate.
2. The view never creates or revises a planning decision.
3. SCAN precedes EXECUTE, and EXECUTE precedes EXPLAIN.
4. Identity, scope, status, and version remain visible.
5. Current information precedes historical context.
6. Primary content precedes supporting content.
7. Priority labels retain one meaning across levels.
8. Lifecycle and execution condition remain separate.
9. CONDITIONAL never looks mandatory.
10. OPTIONAL never looks required.
11. Planned Exposure never looks like Actual Exposure.
12. Missing Actual data never inherit Planned values.
13. Observation and interpretation remain visually distinct.
14. Warning and Stop conditions remain highly visible.
15. Uncertainty and confidence stay attached to the qualified claim.
16. Missing does not look like normal, zero, or resolved.
17. A proxy never looks like the terminal 100m target.
18. Dose remains task-specific and interpretable.
19. Timeline placement does not claim biological adaptation.
20. Fixed High / Low structures are never implied.
21. Fixed phase names and exercise libraries are never implied.
22. Color, icon, or position never carries meaning alone.
23. STANDARD is the default density.
24. Narrow-screen reduction preserves action-critical semantics.
25. Plain Markdown remains understandable without a specialized renderer.

## Failure Modes

The following patterns are prohibited:

| Code | Failure | Required correction |
|---|---|---|
| WALL_OF_TEXT | Long prose prevents scanning | Split into SCAN, EXECUTE, and concise EXPLAIN blocks |
| EVERYTHING_SAME_PRIORITY | Routine and Primary content receive equal emphasis | Restore allocation labels and order |
| COLOR_ONLY_MEANING | State is carried only by color | Add visible text and another cue |
| THEORY_BEFORE_ACTION | Rationale precedes the instruction | Move explanation after execution content |
| HIDDEN_STOP_CONDITION | Stop rule is buried or collapsed | Place Stop beside dose and quality |
| HIDDEN_WARNING | Warning appears only in Notes or detail | Promote it to SCAN and affected action |
| PLAN_AS_STATIC_CALENDAR_ONLY | Dates replace update logic | Add conditions, review points, and next decisions |
| CONDITIONAL_AS_MANDATORY | Conditional work resembles required work | Add CONDITIONAL and explicit IF / THEN / ELSE |
| PLANNED_AS_ACTUAL | Prescription appears as completed exposure | Separate provenance and leave Actual unrecorded |
| PROXY_AS_TERMINAL_TARGET | Supporting metric appears to be the final objective | Restore competitive 100m target hierarchy |
| UNRESOLVED_AS_CERTAIN | Uncertainty disappears through wording or polish | Restore confidence, alternatives, and unknowns |
| HIGH_LOW_AS_FIXED_WEEK_TEMPLATE | A possible organization becomes a universal week | Render only the organization produced by the plan |
| FIXED_PHASE_NAMES | Template supplies predetermined training stages | Use plan-generated names and conditions |
| FIXED_EXERCISE_LIBRARY | Template supplies preferred exercises | Render workflow-selected tasks only |
| UI_LOGIC_INSIDE_CORE_MODEL | Presentation rules alter model meaning | Move display behavior back to this layer |
| STATUS_AXIS_COLLAPSE | Lifecycle, conditionality, or confidence become one badge | Render separate labeled axes |
| UNSOURCED_STATUS_INFERENCE | Renderer invents PLANNED, MODIFIED, or CANCELLED | Preserve Unknown or request authoritative normalization |
| DENSITY_AS_DATA_LOSS | Compact view removes a warning, condition, or stop | Restore all action-critical semantics |
| TABLE_FOR_EVERYTHING | Rationale and uncertainty become unreadable cells | Use structured prose or cards |

## Interface Review

The current presentation contract exposes known interface gaps:

- VIEW_INTERFACE_GAP — Planning State defines DRAFT, ACTIVE, COMPLETED, PAUSED, SUPERSEDED, and INVALIDATED, while the required view vocabulary also includes PLANNED, MODIFIED, and CANCELLED.
- VIEW_INTERFACE_GAP — current Workflows expose warning and review flags, but do not normalize authoritative STABLE and WATCH alert values.
- VIEW_INTERFACE_GAP — `create_mesocycle` does not expose first-class per-Week roadmap objects; the template can only project existing child Week outputs or render `NOT YET DEFINED`.

Templates may reserve positions for unavailable upstream values or objects. Upstream interfaces must provide authoritative data before a renderer uses them.

No visual rule requires a change to Core Models, Rules, or current planning logic. No ARCHITECTURE_REVIEW_NEEDED condition is identified by this specification.
