# Review {Review ID}

Version: 0.1
Status: Draft
Date: 2026-09-15

> **VIEW CONTRACT** - This view presents what happened, what can reasonably be
> inferred, and what changes now. It does not repeat the plan, implement Review
> logic, or create the revised prescription.

> **ILLUSTRATIVE ONLY** - Braced fields and repeated blocks describe
> presentation structure. They contain no athlete data or decision.

Source interfaces:

- [Review Training Workflow](../workflows/review_training.md)
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
- [Athlete State Schema](../schemas/athlete_state.md)
- [Context Summary Schema](../schemas/context_summary.md)
- [Visual System](./visual_system.md)
- [Session Template](./session_template.md)
- [Week Template](./week_template.md)

## Identity and Status

| Field | Value |
|---|---|
| Review | {review identifier} |
| Reviewed object | {Task / Session / Week / Mesocycle / Cycle} |
| Review window | {time span and evidence cutoff} |
| Lifecycle status | {authoritative status} |
| Parent intent | {higher-level reference} |
| Current priority | {PRIMARY / MAINTAIN / MINIMAL / TEMPORARILY WITHDRAWN} |
| Version | {review version} |
| Last update | {date and source} |

## SCAN - Decision and Next Action

This first layer should answer:

- What changed because of what happened?
- What remains stable?
- What is the next action?
- Is a Warning, unresolved conflict, or higher-level Review active?

### Decision

> **DECISION - {MAINTAIN / PROGRESS / REDUCE / MODIFY / TEMPORARILY WITHDRAW /
> TRANSITION}**
>
> - Target: {object affected}
> - Reason: {brief evidence-linked explanation}
> - Confidence: {canonical confidence label}
> - Effective scope: {Task / Session / Week / Mesocycle / Cycle}

The Decision must be more visible than routine observations.

### Next Action

- **Action:** {planning object to continue, revise, review, summarize, or close}
- **Destination:** {receiving workflow}
- **When:** {trigger or deadline}
- **Higher-level intent:** {preserved or requires review}

### Active Warning and Exception

> **WARNING - {warning or None}**
>
> - Affected decision: {scope}
> - Required response: {modify, stop, review, or external action}
> - Source and confidence: {reference and confidence}

> **REVIEW REQUIRED - {review flag or None}**
>
> - Scope: {level}
> - Challenged assumption: {assumption}
> - Destination: {workflow}

### Current State Change Snapshot

| State dimension | Before | Current estimate | Change | Confidence |
|---|---|---|---|---|
| Performance | {prior} | {current} | {changed / unchanged / unresolved} | {confidence} |
| Fatigue and recovery | {prior} | {current} | {change} | {confidence} |
| Tissue | {prior} | {current} | {change} | {confidence} |
| Technical stability | {prior} | {current} | {change} | {confidence} |
| Exposure tolerance | {prior} | {current} | {change} | {confidence} |

Do not collapse State into a single readiness score.

### Carry-Forward Items

| Item | Class | Current relevance | Owner | Review / exit trigger |
|---|---|---|---|---|
| {issue} | {constraint / tissue concern / uncertainty / bottleneck / benchmark / open question} | {next-decision consequence} | {Athlete State / Planning State} | {trigger} |

Unresolved information remains visible after the reviewed block closes.

## EVIDENCE - What Happened

### Intended

| Field | Intended value |
|---|---|
| Objective | {objective} |
| Priority | {allocation} |
| Prescribed task | {task or intervention} |
| Intended stimulus | {stimulus} |
| Planned Exposure | {task-specific dose and conditions} |
| Expected Response | {expected response profile} |

Keep this section compact. It provides the comparison reference.

### Actual

| Field | Actual value |
|---|---|
| Actual Exposure | {completed work and conditions} |
| Achieved Quality | {quality record} |
| Material deviation | {difference from plan} |
| Deviation context | {reason or condition} |
| Exposure agreement | {Aligned / Meaningfully Different / Cannot Determine} |

Planned and Actual remain visually separate. A deviation is not automatically a
failure.

### Key Observations

#### OBSERVATION {ID}

| Field | Value |
|---|---|
| Observation | {descriptive statement} |
| Timing | {immediate / delayed / repeated trend / longer-term signal} |
| Source | {measurement / athlete report / coach observation / record} |
| Context | {conditions and Actual Exposure relationship} |
| Quality | {reliability, validity, and comparability limits} |
| Alert | {STABLE / WATCH / WARNING / REVIEW REQUIRED, if authoritative} |

Observation contains no causal claim.

### Immediate Response

{decision-relevant immediate observations or None}

### Delayed Response

{decision-relevant delayed observations, open observation window, or Not Yet
Available}

### Recent Trend

- **Comparable evidence:** {references}
- **Descriptive pattern:** {trend without causal claim}
- **Comparability limits:** {limits}
- **Trend confidence:** {confidence}

A single observation must not look like a stable trend.

### Important Exceptions

| Exception | Why it matters | Scope | Confidence | Carry forward? |
|---|---|---|---|---|
| {event} | {State, constraint, competition, or risk consequence} | {level} | {confidence} | {Yes / No / Unresolved} |

A high-consequence exception may justify conservative action without being
labeled a repeated trend.

### Constraint Changes

| Constraint | Prior status | Current status | Source | Planning consequence |
|---|---|---|---|---|
| {constraint} | {prior} | {active / changed / resolved / unresolved} | {reference} | {affected action or scope} |

Missing is not resolved.

## INTERPRETATION - What the Evidence May Mean

This section follows the observation record.

### Expected vs Observed Response

| Field | Value |
|---|---|
| Expected Response | {conditional on intended exposure} |
| Actual Exposure basis | {what actually occurred} |
| Observed Response | {response} |
| Consistency | {consistent / mixed / inconsistent / cannot determine} |
| Benefit-cost implication | {brief} |
| Assumptions challenged | {dose / exposure / recovery / transfer / model / None} |

### Candidate Interpretations

#### INTERPRETATION {ID}

| Field | Value |
|---|---|
| Claim | {candidate explanation} |
| Supporting evidence | {references} |
| Conflicting evidence | {references} |
| Plausible alternatives | {alternatives} |
| Claim scope | {what the interpretation does and does not explain} |
| Confidence | {canonical confidence label} |

Do not present Interpretation as Observation.

Several interpretations may remain active. **CANNOT DETERMINE YET** is valid.

### Failure Classification

| Possible failure class | Support | Competing class | Confidence |
|---|---|---|---|
| {Prescription / Execution / Exposure / Measurement / Recovery / Constraint Change / Transfer / Model-Hypothesis / Unresolved} | {evidence} | {alternative} | {confidence} |

An unfavorable outcome does not automatically equal method failure.

### Updated Athlete State

- **Prior State reference:** {reference}
- **Updated State reference:** {reference or update required}
- **Changed dimensions:** {evidence-weighted changes}
- **Unchanged relevant dimensions:** {when useful}
- **Current uncertainty:** {unresolved state}

The Review output may supply an Athlete State update interface. The
authoritative construction remains with the Athlete State workflow when needed.

### Confidence and Uncertainty

> **{PROVISIONAL / UNRESOLVED / CANNOT DETERMINE YET / other canonical label}**
>
> Claim: {claim}
> Evidence limitation: {limitation}
> Competing explanation: {alternative}
> Narrower conclusion supported: {bounded conclusion}
> Next information trigger: {observation or assessment}

Low confidence must not be hidden in Notes.

## DECISION TRACE - Why This Changes Now

### Decision Basis

- **Observation basis:** {references}
- **Interpretation basis:** {references}
- **Rule interface:** {Progression or Stage Transition Rule reference}
- **Consequence of error:** {brief}
- **Smallest-justified-level rationale:** {why this scope is sufficient}

### Decision Scope

| Scope | Status |
|---|---|
| Task | {affected / preserved / not applicable} |
| Session | {affected / preserved / not applicable} |
| Week | {affected / preserved / review required} |
| Mesocycle | {affected / preserved / review required} |
| Cycle | {affected / preserved / review required} |

A local problem does not automatically rewrite the Cycle.

### Decision Quality Boundary

- **Ex Ante decision quality:** {assessment using information available then}
- **Ex Post outcome:** {observed result}
- **Learning update:** {how the outcome changes future belief}

Outcome does not retroactively determine whether the earlier decision was
reasonable.

## Handoff

### Next Planning Action

- planning object: {object};
- requested action: {maintain, revise, create next, pause, or close};
- receiving workflow: {reference};
- handoff packet: {reference};
- higher-level intent to preserve or review: {statement}.

### Unresolved Questions

- {open decision-relevant question};
- {plausible alternatives};
- {consequence};
- {residual uncertainty}.

### Next Observation Needs

- minimum information capable of changing the next decision;
- source and context;
- expected decision value;
- collection cost;
- observation window.

### Summary Update Required?

**Status:** {No / WEEK_CLOSE / MESOCYCLE_CLOSE / CYCLE_CLOSE /
SUMMARY_REVISION}

**Reason:** {State change, repeated trend, important exception, constraint,
decision implication, or Archive Only}

- **Destination:**
[Update Context Summary Workflow](../workflows/update_context_summary.md)

### Continuity Update

- **Planning State update required:** {Yes / No}
- **Carry-Forward update:** {items}
- **Destination:**
[Update Planning State Workflow](../workflows/update_planning_state.md)

## Renderer Projection Contract

### COMPACT

Retain Decision, Next Action, active Warning, State Change Snapshot, and
Carry-Forward Items.

### STANDARD

Render SCAN, Evidence, Interpretation, Decision Trace, and Handoff.

### EXPANDED

Add fuller source detail, competing interpretations, provenance, and historical
comparison without repeating the original plan.

On narrow screens, render tables as labeled cards. OBSERVATION and
INTERPRETATION labels remain explicit.

## Review View Invariants

1. Decision and Next Action are immediately visible.
2. Intended and Actual remain distinct.
3. Observation and Interpretation remain distinct.
4. Single observations do not look like stable trends.
5. Conflicts and uncertainty remain visible.
6. State changes are evidence-weighted.
7. Decision uses the smallest justified scope.
8. Review decision state and plan priority remain distinct.
9. Warning labels do not create medical diagnoses.
10. Carry-Forward Items survive block closure.
11. Summary and Planning State update needs are explicit.
12. The Review view presents workflow output; it does not perform the workflow.
13. The Review does not generate the revised plan.
