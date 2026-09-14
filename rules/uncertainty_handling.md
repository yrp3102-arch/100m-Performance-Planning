# Uncertainty Handling Rules

Version: 0.1
Status: Draft
Date: 2026-09-14

## Purpose

This document defines the operational treatment of insufficient information and uncertainty. The core concepts and invariants are defined in [`../core_models/01_plan_model.md`](../core_models/01_plan_model.md).

---

A planning system must distinguish between:

Information that is missing

and

Information that is necessary for the current decision.

Not every unknown variable prevents action.

However, when missing information materially affects the expected benefit,
cost, risk, or feasibility of a decision,
the system must not silently replace that information with an assumption.

Insufficient information is therefore decision-dependent.

The relevant question is not:

"Do we know everything?"

The relevant question is:

"Do we know enough to make this decision at an acceptable level of
uncertainty?"

---

## 1. Information Sufficiency Is Decision-Specific

The amount of information required depends on the consequence of the decision.

A low-cost, reversible training choice may require less certainty.

A high-cost, high-speed, high-risk, or difficult-to-reverse decision may
require more.

For example:

A small modification to familiar supporting work

may require less information than

a major increase in high-speed sprint exposure after an interruption.

The system should therefore scale information requirements according to:

- decision consequence,
- reversibility,
- expected cost,
- uncertainty,
- and downside risk.

---

## 2. Unknown Does Not Mean Zero

Missing information must not be represented as:

- zero,
- normal,
- recovered,
- tolerated,
- or unchanged

unless that interpretation is explicitly justified.

Examples include:

- missing soreness data does not mean no soreness,
- missing sprint timing does not mean sprint performance was stable,
- missing training history does not mean the athlete is untrained,
- missing tissue information does not mean the tissue is fully tolerant,
- missing sleep data does not mean sleep was adequate.

The system must preserve unknown values as unknown when they matter.

---

## 3. Unknown Does Not Automatically Mean Unsafe

The opposite error must also be avoided.

Uncertainty does not automatically imply that all training is inappropriate.

The system should distinguish between:

Known Infeasible

Known Feasible

Uncertain but Low Consequence

Uncertain and Decision-Critical.

The response should depend on which category applies.

The purpose of uncertainty handling is not to stop planning.

It is to prevent unsupported confidence.

---

## 4. Decision-Critical Information

Information is decision-critical when a plausible alternative value would
meaningfully change the preferred action.

Examples may include:

- current tissue tolerance before high-speed sprinting,
- recent sprint exposure before increasing high-speed volume,
- competition timing before selecting a long adaptation block,
- actual available training days before designing weekly structure,
- timing protocol before interpreting a small sprint improvement,
- current symptoms before progressing plyometric demand,
- or recent training load before interpreting fatigue.

The system should prioritize collecting information that can change the
decision.

It should not collect data merely because the data are available.

---

## 5. Missing Context

A training prescription should not be evaluated independently from its context.

Important missing context may include:

- athlete identity,
- training age,
- current objective,
- current state,
- training history,
- competition timeline,
- recent exposure,
- recovery environment,
- tissue status,
- facilities,
- and lifestyle constraints.

If one or more of these variables materially affect the decision,
the system should state the limitation explicitly.

It should not create a highly individualized plan from generic information.

---

## 6. Measurement Uncertainty

Available data may still be insufficient if the measurement itself is not
interpretable.

The system should consider:

- protocol consistency,
- device reliability,
- environmental conditions,
- familiarization,
- measurement error,
- and normal within-athlete variation.

For example:

a faster Fly time measured with a different timing start

does not provide the same information as

a faster Fly time under the same protocol.

More data do not automatically reduce uncertainty if the measurement process
is inconsistent.

---

## 7. Conflicting Information

Information may be available but internally inconsistent.

Examples include:

- subjective fatigue is high while warm-up performance appears normal,
- CMJ is stable while sprinting produces local discomfort,
- strength improves while sprint performance declines,
- perceived readiness is high while repeated high-speed output deteriorates.

Conflicting information should trigger interpretation.

The system must not mechanically average conflicting signals into a single
readiness score.

The relevant question is:

Which signal is most specific to the current decision?

The system should also consider whether one signal has asymmetric
consequences.

For example:

meaningful local pain may override a normal general readiness indicator for a
high-speed sprint decision.

---

## 8. Evidence Uncertainty

The system must distinguish between:

Uncertainty about the athlete

and

Uncertainty about the training method.

A method may have:

- strong general evidence,
- weak evidence in trained 100m sprinters,
- indirect mechanistic support,
- coaching-practice support,
- or unresolved evidence.

Evidence strength does not remove the need for athlete-specific information.

Likewise, strong athlete-specific history does not transform weak scientific
evidence into universal truth.

The system should preserve both dimensions:

Evidence Confidence

and

Contextual Applicability.

---

## 9. Information Acquisition Has Cost

Obtaining more information may itself consume:

- time,
- recovery,
- attention,
- money,
- training opportunities,
- or athlete cooperation.

The system should therefore ask whether additional information is worth its
cost.

Examples include:

- repeated maximal sprint testing,
- repeated 1RM testing,
- complex monitoring batteries,
- or unnecessary daily questionnaires.

The purpose of information collection is improved decision quality.

If a test is unlikely to change the decision,
its value may be low even if the data are interesting.

---

## 10. Conservative Action Under Uncertainty

When decision-critical uncertainty remains,
the system should prefer actions that preserve future options.

Candidate responses may include:

- use a previously tolerated dose,
- reduce the size of the progression,
- choose a lower-cost method,
- increase observation,
- postpone a non-urgent change,
- retain the current dose,
- or perform a small exploratory exposure.

The system should avoid large irreversible changes when confidence is low and
the downside of error is meaningful.

Conservative does not mean passive.

It means limiting the cost of being wrong.

---

## 11. Exploratory Exposure

When information cannot be obtained directly,
training itself may be used as a controlled information-gathering exposure.

An exploratory exposure should:

- have a clear question,
- use a bounded dose,
- have interpretable monitoring,
- define acceptable response,
- define stop conditions,
- and specify when the result will be reviewed.

For example:

the system may use a small re-exposure to high-speed running to evaluate
tolerance rather than immediately restoring the previous full dose.

An exploratory exposure is not automatically a development session.

Its information value may be part of its purpose.

---

## 12. Cannot Determine Is a Valid Output

The system must be allowed to conclude:

"Cannot yet determine."

This is preferable to unsupported precision.

A "cannot determine" judgment should specify:

- what decision cannot yet be made,
- what information is missing or unreliable,
- why that information matters,
- what can still be done safely or usefully,
- and what information would reduce the uncertainty.

The system should avoid vague refusal when a narrower decision is still
possible.

For example:

It may be impossible to determine the optimal MaxV dose

while still being possible to choose a previously tolerated conservative
exposure.

---

## 13. Confidence Should Match Evidence

The system should not express confidence beyond the available information.

Possible language may include:

- high confidence,
- moderate confidence,
- low confidence,
- provisional,
- exploratory,
- unresolved,
- or cannot determine.

Confidence should reflect:

- data quality,
- measurement consistency,
- evidence relevance,
- athlete-specific history,
- and consequence of error.

Precision in wording should not exceed precision in knowledge.

---

## 14. Information Should Be Updated

Insufficient information is not necessarily permanent.

The system should update its information state as new evidence becomes
available.

New information may come from:

- training execution,
- monitoring,
- competition,
- standardized testing,
- medical or rehabilitation assessment,
- environmental change,
- or additional historical records.

The system should record which previous unknowns have become known and whether
the new information changes the preferred action.

---

## Information Sufficiency Invariants

The system should preserve the following principles:

1. Missing information is not automatically zero, normal, or favorable.
2. Not every unknown prevents action.
3. Information requirements depend on the consequence of the decision.
4. Decision-critical uncertainty must remain explicit.
5. Conflicting signals require interpretation rather than mechanical averaging.
6. Measurement quality matters as much as data availability.
7. More information is not automatically better if obtaining it has meaningful
   cost.
8. Under high uncertainty, reversible and bounded decisions are generally
   preferable to aggressive irreversible changes.
9. "Cannot yet determine" is a legitimate planning output.
10. Confidence must not exceed the quality and relevance of the available
    information.

The system should seek the minimum information necessary to support the next
meaningful decision rather than attempting to eliminate all uncertainty.
