# Plan Comparison Rules

Version: 0.1
Status: Draft
Date: 2026-09-14

## Purpose

This document defines the operational comparison of feasible training options. The Plan Comparison Model is defined in [`../core_models/01_plan_model.md`](../core_models/01_plan_model.md).

---

Plan comparison refers to the process of deciding which among multiple
feasible training plans is more appropriate under the current conditions.

The purpose is not to identify a universally "best" training plan.

The relevant question is:

"Given this athlete, objective, state, time horizon, constraints, and
uncertainty, which available option is currently preferable?"

Comparison should occur only after:

- minimum information sufficiency has been checked,
- structural validity has been checked,
- hard constraints have been identified,
- and clearly infeasible options have been removed.

The system should not compare plans as if every possible option belongs to the
same feasible set.

---

## 1. Comparison Is Conditional

Plan A is not inherently better than Plan B.

A comparison is meaningful only relative to a defined condition set.

A comparison should therefore specify:

- the athlete,
- the current objective,
- the current state,
- the relevant time horizon,
- the competition context,
- the major constraints,
- and the important uncertainty.

The preferred plan may change when any of these conditions change.

Therefore:

Better Plan

means

Better Under the Current Decision Conditions.

It does not mean universally superior.

---

## 2. Necessary Conditions Come First

Before comparing expected benefits,
the system should exclude options that fail necessary conditions.

Examples include:

- the plan cannot be executed,
- the dose cannot be interpreted,
- the plan conflicts with a medical restriction,
- the required facility is unavailable,
- the training cannot fit the competition timeline,
- or the plan contains unresolved internal contradictions.

An infeasible plan should not remain in the comparison merely because its
theoretical upside appears large.

Comparison begins inside the feasible planning space.

---

## 3. Compare Expected 100m-Relevant Benefit

Among feasible options,
the system should compare expected contribution to the current 100m objective.

Relevant questions include:

- Which plan better addresses the current performance problem?
- Which plan has the more plausible transfer to competitive 100m performance?
- Which plan is more specific to the current priority?
- Which plan better preserves important existing capacities?
- Which plan is more likely to produce usable adaptation within the available
  time?

Expected benefit should be linked to the current objective.

A plan should not be preferred merely because it improves more variables.

A plan that improves several proxy measures may still be inferior to a simpler
plan that better improves the current sprint priority.

---

## 4. Compare Recovery Cost

Expected benefit must be compared with expected recovery cost.

Relevant recovery costs may include:

- residual fatigue,
- local tissue loading,
- muscle damage,
- high-speed exposure cost,
- metabolic stress,
- sleep disruption,
- and interference with the next important session.

The system should ask:

"What does this plan consume in order to produce its expected benefit?"

A method with slightly greater theoretical benefit may be inferior when its
additional recovery cost damages higher-priority training.

---

## 5. Compare Opportunity Cost

Training resources are finite.

Selecting one option means not selecting another.

Opportunity cost may include:

- time that could have been used for sprinting,
- recovery capacity consumed by supporting work,
- reduced technical practice,
- reduced sleep,
- reduced competition preparation,
- or loss of flexibility later in the cycle.

The system should therefore compare:

Benefit of the selected work

against

Value of the work it displaces.

A useful method may still have poor current value if it occupies resources
needed by a more important objective.

---

## 6. Compare Risk

Plans may differ in downside risk even when expected benefit is similar.

Relevant risks may include:

- tissue irritation,
- excessive fatigue,
- loss of key training quality,
- missed competition preparation,
- learning cost,
- technical disruption,
- and poor recovery from unfamiliar work.

Risk should not be treated as a reason to always choose the lowest-load option.

Instead, the system should ask whether the expected benefit justifies the
specific downside under the current conditions.

Risk tolerance may change with:

- time to competition,
- athlete history,
- tissue status,
- training age,
- and availability of alternative methods.

---

## 7. Compare Uncertainty

Plans may differ not only in expected benefit and cost,
but also in how uncertain those estimates are.

For each plan, the system should consider uncertainty about:

- expected adaptation,
- actual dose,
- athlete tolerance,
- transfer to sprint performance,
- recovery time,
- measurement validity,
- and available evidence.

A plan with slightly lower expected benefit but much lower uncertainty may be
preferable when:

- competition is near,
- recovery margin is small,
- tissue status is uncertain,
- or the downside of being wrong is large.

Greater uncertainty may be more acceptable when:

- the decision is reversible,
- the dose is exploratory,
- sufficient time remains,
- and the cost of failure is low.

---

## 8. Compare Reversibility

Plans differ in how easily they can be changed if the original assumption is
wrong.

A more reversible option may be preferable under uncertainty.

Reversible decisions may include:

- small dose changes,
- familiar exercise substitutions,
- limited exploratory exposures,
- or short-term changes in weekly organization.

Less reversible decisions may include:

- large increases in high-speed exposure,
- introducing multiple unfamiliar exercises,
- major restructuring close to competition,
- or training that produces long residual fatigue.

The system should value the ability to recover from decision error.

---

## 9. Compare Time to Benefit

Expected adaptation must arrive within the useful time window.

The system should ask:

- How long may the adaptation require?
- How long may familiarization require?
- How long may fatigue persist?
- Is there enough time for transfer to sprint performance?
- Is there enough time for the athlete to stabilize the new ability?

A method may be valuable in general but have poor current value because the
competition timeline is too short.

Time remaining changes the relative value of training options.

---

## 10. Compare Competition Availability

A training plan should be evaluated by whether the athlete can express the
desired ability when it matters.

A plan that produces adaptation but leaves excessive residual fatigue at the
target competition may be inferior to a plan with slightly less development
but better performance availability.

The system should therefore consider:

Development Value

and

Expression Value.

As competition approaches,
the second becomes increasingly important.

---

## 11. Compare Execution Reliability

Plans may differ in how reliably they can actually be implemented.

Relevant factors include:

- athlete familiarity,
- coaching requirements,
- equipment dependence,
- weather dependence,
- session complexity,
- measurement requirements,
- and lifestyle compatibility.

A theoretically superior plan that is frequently executed poorly may have
lower practical value than a slightly simpler plan that can be consistently
implemented.

The system should compare expected real-world execution,
not idealized execution.

---

## 12. Compare Monitoring Value

Some plans generate clearer information than others.

A plan may be preferable when it makes it easier to determine:

- whether the intended stimulus occurred,
- whether the athlete tolerated the dose,
- whether performance changed,
- and why the result may have occurred.

When two options have similar expected benefit and cost,
the option producing more interpretable feedback may have additional value.

This is especially relevant during exploratory or uncertain phases.

---

## 13. Simplicity Has Conditional Value

Complexity is not automatically a benefit.

When two plans have similar expected performance benefit,
similar cost,
and similar risk,
the simpler plan may be preferred.

Simplicity may improve:

- execution reliability,
- monitoring clarity,
- athlete understanding,
- traceability,
- and ability to identify cause and effect.

However, simplicity must not be preferred when it removes information or
structure necessary for the decision.

The goal is not minimum complexity.

The goal is minimum complexity sufficient for decision quality.

---

## 14. Pareto Comparison

The system may use Pareto logic when comparing feasible plans.

Plan A dominates Plan B when:

- A is no worse on the decision-relevant dimensions,
- and A is meaningfully better on at least one important dimension.

Relevant dimensions may include:

- expected 100m-relevant benefit,
- recovery cost,
- opportunity cost,
- risk,
- uncertainty,
- time to benefit,
- reversibility,
- competition availability,
- and execution reliability.

If Plan A provides similar or greater expected benefit
while requiring no greater cost and no greater risk,
the system should generally prefer Plan A.

A dominated plan should normally be removed from consideration unless an
important unmodeled condition exists.

---

## 15. Trade-Offs Prevent a Universal Winner

Many comparisons will not produce Pareto dominance.

For example:

Plan A may offer:

- greater expected adaptation,
- but greater recovery cost.

Plan B may offer:

- smaller expected adaptation,
- but lower risk and greater competition availability.

Neither plan is universally better.

The preferred option depends on:

- current priority,
- remaining time,
- athlete tolerance,
- competition importance,
- uncertainty,
- and acceptable risk.

The system must not hide a trade-off by producing an arbitrary total score.

---

## 16. Avoid False Precision

The system should not assign precise numerical weights to dimensions unless
those weights have a defensible basis.

For example:

Benefit = 8.4

Risk = 5.7

Recovery Cost = 6.2

may create an appearance of objectivity without valid measurement.

Qualitative comparison may be more accurate when uncertainty is high.

Useful comparison language may include:

- clearly preferable,
- preferable under current conditions,
- approximately equivalent,
- different trade-off,
- insufficient information,
- or currently cannot determine.

The precision of the comparison should match the precision of the evidence.

---

## 17. Athlete Preference Can Matter

When multiple plans are similarly defensible,
athlete preference may be a legitimate decision variable.

Preference may affect:

- adherence,
- motivation,
- perceived control,
- consistency,
- and execution quality.

Athlete preference should not override:

- safety constraints,
- major competition requirements,
- or clearly superior evidence.

But when the expected performance difference is small,
preference can help choose between otherwise reasonable options.

---

## 18. Compare Marginal Value, Not Historical Reputation

A training method should be evaluated by its current marginal value.

The relevant question is not:

"Has this method ever worked?"

The relevant question is:

"What additional value is this method likely to provide now?"

A method may have been highly valuable earlier in the cycle
and now be worth only a maintenance dose.

Likewise,
a previously unnecessary method may become valuable after the athlete's state
or competition context changes.

Historical usefulness does not guarantee current priority.

---

## 19. Plan Comparison Can Change Over Time

The result of a comparison is provisional.

After implementation,
the system should update the comparison using actual information.

Relevant questions include:

- Was the intended stimulus achieved?
- Was the recovery cost as expected?
- Did the athlete tolerate the plan?
- Did sprint performance move as expected?
- Did another explanation become more plausible?
- Has competition timing changed?
- Has another option become relatively more valuable?

A plan that was preferred at time T1 may no longer be preferred at time T2.

---

## 20. Outcome Does Not Retroactively Define Decision Quality

A good decision can produce an unfavorable outcome.

A poor decision can occasionally produce a favorable outcome.

Therefore the system should distinguish:

Decision Quality

from

Observed Outcome.

Plan comparison should be evaluated according to the information available at
the time of the decision.

After implementation,
the outcome should update future decisions,
but it should not automatically rewrite the quality of the original reasoning.

This protects the system from outcome bias.

---

## Plan Comparison Invariants

The system should preserve the following principles:

1. Compare only plans that satisfy necessary feasibility conditions.
2. Plan superiority is conditional, not universal.
3. Competitive 100m relevance has priority over improvement in proxy metrics.
4. Expected benefit must be evaluated together with recovery cost.
5. Opportunity cost matters because training resources are finite.
6. Risk and uncertainty are separate dimensions.
7. Time to benefit and competition availability change plan value.
8. Reversibility has value when uncertainty is high.
9. Execution reliability matters more than idealized theoretical execution.
10. A plan dominated on relevant dimensions should normally be rejected.
11. When benefits and costs trade off, there may be no unique best plan.
12. False numerical precision should be avoided.
13. Simplicity is preferred only when it preserves required decision quality.
14. Current marginal value matters more than historical reputation.
15. Plan comparison must be updated when conditions or observed responses
    change.
16. Decision quality must be distinguished from eventual outcome.

The system should therefore compare plans as conditional,
multi-objective decisions under constraints and uncertainty,
rather than searching for a universally optimal training template.
