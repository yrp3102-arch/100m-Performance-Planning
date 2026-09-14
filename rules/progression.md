# Progression Rules

Version: 0.1
Status: Draft
Date: 2026-09-14

## Purpose

This document defines the operational decision states and escalation rules for progression. It implements the Adaptive Capacity interface in [`../core_models/01_plan_model.md`](../core_models/01_plan_model.md). Transition implementation is defined in [`stage_transition.md`](stage_transition.md).

---

## Decision States

After interpreting exposure and response,
the system should choose among a limited set of decision states.

---

## Maintain

Use when:

- the intended stimulus was achieved,
- the cost was acceptable,
- and there is not yet sufficient reason to increase or reduce the dose.

Maintain is an active decision.

It must not be treated as failure to progress.

---

---

## Progress

Use when:

- the intended stimulus has been repeatedly achieved,
- recovery cost remains acceptable,
- progression serves the current objective,
- and sufficient time remains for the expected adaptation.

Progression should preferably change one major variable at a time when
practical.

Progression may involve:

- higher velocity,
- greater distance,
- additional volume,
- increased frequency,
- greater external load,
- more demanding task conditions,
- or greater competition specificity.

---

---

## Reduce

Use when:

- the training objective remains relevant,
- but the current dose produces excessive cost,
- declining quality,
- or unacceptable recovery demand.

Reduction may involve:

- fewer repetitions,
- less high-speed distance,
- lower external load,
- fewer contacts,
- longer recovery,
- reduced supporting work,
- or lower session frequency.

---

---

## Modify

Use when:

- the target adaptation remains relevant,
- but the current method is not producing the desired stimulus,
- environmental constraints have changed,
- or the current method is unnecessarily costly.

Modification may involve changing:

- exercise,
- sprint format,
- distance,
- load,
- surface,
- sequencing,
- session placement,
- or supporting work.

The adaptation target should remain visible during modification.

---

---

## Temporarily Withdraw

Use when:

- tissue status,
- competition timing,
- repeated adverse response,
- or opportunity cost makes the current stimulus temporarily inappropriate.

Withdrawal should include:

- the reason for withdrawal,
- any suitable replacement,
- and conditions for reintroduction.

Temporary withdrawal is not equivalent to abandoning the capacity
permanently.

---

---

## Escalation Should Be Earned

The system should not assume that each new week requires additional load.

Progression should be supported by evidence that the athlete has tolerated and
benefited from the current exposure.

The system should reject automatic rules such as:

- increase volume every week,
- add a third High day in Week 3,
- increase load by a fixed percentage,
- or transition after a fixed number of weeks,

unless those rules are supported by the specific context.

Calendar time may trigger review.

It should not automatically trigger escalation.

---

---

## Decision Record

When the plan changes,
the system should record:

- what new information appeared,
- what previous assumption was affected,
- what element of the plan changed,
- why that change was selected,
- what response is now expected,
- when the decision will be reviewed,
- and what would cause the change to be reversed.

This allows the planning system to learn from its own decisions over time.

---
