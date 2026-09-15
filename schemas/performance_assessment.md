# Performance Assessment Schema

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This schema defines how existing performance-assessment data and potential
future assessments are represented.

Assessment exists to reduce decision-relevant uncertainty. The ability to
measure something does not establish that it should be measured. More data does
not automatically produce a better decision.

This schema is not a fixed test battery, monitoring catalogue, interpretation
algorithm, or requirement that every athlete complete extensive testing.

## 1. Assessment Identity

An assessment record should identify:

- athlete identifier;
- assessment identifier;
- date or period;
- assessment question;
- decision or uncertainty it is intended to inform;
- information requirement;
- source;
- current record status;
- responsible observer when relevant.

A record may represent a completed assessment, an existing historical
measurement, a proposed assessment, or an explicitly missing assessment.

## 2. Information Requirement

Each assessment or measurement may be classified as:

| Class | Meaning |
|---|---|
| **Required** | Its absence materially distorts the current basic decision or prevents a minimally usable Athlete State. |
| **Decision-Dependent** | It is needed because a specific decision question or uncertainty depends on it. |
| **Optional / Additional** | It may add context, but its absence does not block the current decision. |

Requirement is decision-relative. It is not a permanent property of a test.

A flying sprint measure may be Optional during general intake and
Decision-Dependent when the question is whether maximum-velocity expression is
a plausible bottleneck. Detailed body-composition data may remain Optional when
it would not change the decision.

## 3. Assessment Question

Every assessment should state the question it is intended to inform before its
result is interpreted.

Examples of valid question forms include:

- Is maximum-velocity expression a plausible current bottleneck?
- Is acceleration exposure repeatable under the present conditions?
- Is a supporting strength capacity plausibly limiting the current task?
- Is current sprint quality stable across comparable exposures?
- Has the observed change persisted beyond normal variation?
- Would resolving this uncertainty change the next planning decision?

The question should identify:

- target decision;
- target performance problem, determinant, capacity, constraint, or exposure;
- current hypothesis;
- material alternative explanations;
- time horizon;
- consequence of error.

The schema records the question. It does not determine the assessment protocol
or operational decision rule.

## 4. Measurement Record

A completed measurement should support:

| Field | Meaning |
|---|---|
| Measure name | The variable or outcome recorded. |
| Date and time | When it was obtained. |
| Protocol | How the task and measurement were performed. |
| Conditions | Surface, environment, fatigue context, and other material conditions. |
| Equipment | Device or system used. |
| Result | Recorded value or description. |
| Unit | Unit attached to the result. |
| Timing method | Electronic, hand, video-derived, or other method when relevant. |
| Source | Athlete, coach, system, competition record, or other source. |
| Reliability or confidence | Qualitative judgment supported by known measurement properties and execution. |
| Notes | Limited context needed for interpretation. |

Repeated measurements should also preserve comparability with prior records.
A numeric value without unit, protocol, conditions, or source may remain usable
for limited purposes but receives lower interpretive authority.

## 5. Observation Record

Measurement is one source of observation. Other observations may include
athlete report, coach observation, video description, execution record, and
competition event.

An observation record may contain:

- raw description;
- source;
- date and temporal relation to exposure;
- context;
- affected task or phase;
- observation quality;
- whether it was expected;
- missing contextual information.

Observation remains descriptive. "30m time was slower" is an observation.
"Neural fatigue caused the decline" is an interpretation and belongs in the
Athlete State or Feedback-Decision layer.

## 6. Sprint Performance Measures

The schema can represent, without requiring:

- 10m, 20m, 30m, or 60m time;
- flying sprint time;
- segment or split time;
- velocity and acceleration profile;
- competition split;
- complete 100m result;
- repeatability across comparable sprint exposures.

Each record should distinguish training from competition, timing method,
distance definition, run-in when relevant, conditions, and achieved execution
quality.

Sprint measures are not logically interchangeable. A short acceleration time,
flying time, and complete 100m result occupy different performance layers and
answer different questions.

No universal sprint test set is defined here.

## 7. Strength and Power Measures

The schema can represent, without requiring:

- strength test result;
- load-velocity or bar-velocity result;
- jump outcome;
- reactive-strength measure;
- throw or other power proxy.

Each measure should identify its protocol, load or condition, equipment, result,
unit, comparability, and intended decision question.

Strength and power measures are supporting indicators or capacity proxies.
Their improvement does not by itself establish changed sprint expression or
competitive 100m performance. Transfer requires separate reasoning.

A low result relative to a norm is not automatically a bottleneck.

## 8. Technical Observation

Technical assessment may use video, direct observation, or task records.

Represent:

- observed feature in descriptive language;
- sprint phase or task context;
- speed and fatigue context;
- camera or observation conditions when relevant;
- repeatability;
- source;
- confidence;
- alternative explanations;
- relationship to the assessment question.

Technical observation should describe task organization rather than enforce a
single ideal posture, trajectory, or universal technical template.

An isolated biomechanical variable does not uniquely define technical quality
or causation.

## 9. Tissue and Recovery Observation

The assessment record may represent:

- athlete-reported local sensation;
- pain or discomfort report;
- change across or after exposure;
- relevant performance or execution observation;
- recovery report;
- supplied restriction;
- temporal context;
- source and confidence.

The record remains observational and non-diagnostic. Missing tissue information
does not imply normal tissue state or unrestricted exposure availability.

High-consequence warning information may have decision value without repeated
measurement. The operational response belongs to rules and feedback workflows.

## 10. Decision Relevance

Each assessment should answer:

- What decision could this inform?
- What relevant uncertainty could it reduce?
- Would a plausible result change interpretation?
- Would a plausible result change action?
- Would it change confidence?
- Could it detect an important risk?
- What are the time, fatigue, tissue, opportunity, and monitoring costs?
- When would the result arrive relative to the decision?

An assessment with no plausible effect on interpretation, action, confidence,
or important-risk detection has low monitoring value.

Can measure does not mean should measure. Information acquisition has cost.

## 11. Status of a Proposed Assessment

A proposed assessment may be marked:

- **Needed Now**;
- **Useful Later**;
- **Optional**;
- **Deferred**;
- **Not Justified**;
- **Not Feasible**;
- **Missing but Non-Blocking**;
- **Decision Blocking**.

These states describe the assessment's relationship to a decision. They are not
fixed test-selection rules.

## 12. Missing Assessment

If data do not exist, record **Missing** or **Not Assessed**. Preserve:

- the missing item;
- the question it might inform;
- whether the current decision depends on it;
- feasible alternative information;
- cost and timing of obtaining it;
- whether conservative action can proceed;
- next useful opportunity to assess.

Do not infer normality, zero, no deficit, or no problem.

Use **PARTIAL_STATE** or **PROVISIONAL_STATE** if a bounded decision remains
possible. Use **DECISION_BLOCKED_BY_MISSING_INFORMATION** only when the named
decision cannot reasonably proceed.

Missing assessment does not force a complete intake or test battery.

## 13. Data Quality and Comparability

Assessment quality should consider:

- reliability;
- construct and decision validity;
- protocol fidelity;
- equipment and resolution;
- achieved task quality;
- measurement conditions;
- source credibility;
- comparability with baseline or prior result;
- sample size and repeated trend;
- recency;
- missing context.

Quality is qualitative unless the measurement system supports a defensible
quantitative error estimate. Do not invent precision or probabilities.

A reliable measure can still have low decision relevance. A relevant measure
can still support only weak inference if conditions are poor.

## 14. Temporal Structure

Assessment records should preserve whether information reflects:

- immediate response;
- short-delay response;
- delayed response;
- repeated trend;
- longer-term adaptation signal;
- historical reference.

Observation opportunities are selected for the response in question. Fixed
universal biological deadlines are not implied.

A single observation usually supports weaker inference than a repeated,
contextually comparable trend. It may still justify conservative action when
the consequence of waiting is high.

## 15. Interpretation Boundary

The Assessment Record stores:

- assessment question;
- protocol and conditions;
- measurement or observation;
- quality and comparability;
- uncertainty;
- decision relevance.

Interpretation belongs in
[Athlete State](./athlete_state.md) and the
[Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md).

The following inference is invalid without additional reasoning:

> Slow flying sprint equals maximum-velocity deficit.

The measure may support a Candidate Interpretation. It does not uniquely
identify a causal bottleneck.

Competing explanations, context, Actual Exposure, prior state, and confidence
must remain visible.

## 16. Natural-Language Mapping

Natural-language assessment information may be mapped into structured meaning.

"I hand-timed 30m at about 4.1 on grass after lifting" maps to:

- 30m sprint measure;
- approximate and reported status;
- hand timing;
- grass condition;
- prior lifting context;
- limited comparability and confidence.

It does not become an electronic track result or proof of acceleration capacity.

"I look less stable upright late in the session" maps to a qualitative technical
observation with phase, fatigue context, source, and unresolved interpretation.

## 17. Minimum Complete Assessment Record

A record is minimally complete for decision use when it identifies:

- the assessment question;
- measure or observation;
- date;
- protocol sufficient to understand the result;
- material conditions;
- result and unit where applicable;
- source;
- quality or confidence;
- decision relevance;
- material uncertainty.

Historical data that fail this gate may still be retained with explicitly
limited use.

## 18. Interfaces and Boundaries

- [Athlete Profile Schema](./athlete_profile.md) stores durable performance and
  training history.
- [Athlete State Schema](./athlete_state.md) stores interpretations and current
  decision-relevant estimates.
- [Competition Context Schema](./competition_context.md) supplies race role and
  conditions for competition assessments.
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
  defines targets, determinants, indicators, proxies, and inference limits.
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
  governs contextualized interpretation and State Update.
- [Review Training Workflow](../workflows/review_training.md) governs the
  operational sequence after training.
- [Uncertainty Handling Rules](../rules/uncertainty_handling.md) govern
  information sufficiency and conservative action.

This schema does not create assessment schedules, universal thresholds, test
batteries, or decision trees.

## 19. Assessment Invariants

1. Assessment exists to reduce decision-relevant uncertainty.
2. Can Measure does not imply Should Measure.
3. More Data does not imply Better Decision.
4. Measurement and interpretation remain distinct.
5. Observation and conclusion remain distinct.
6. Requirement class depends on the current decision.
7. Missing and Not Assessed do not imply zero, normal, or no problem.
8. Proxy improvement does not establish 100m performance improvement.
9. No universal test battery is required.
10. Quality, comparability, context, and source constrain inference.
11. High-consequence warnings may matter before a repeated trend exists.
12. Natural-language information may enter without losing qualifiers.