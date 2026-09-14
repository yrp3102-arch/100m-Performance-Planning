# Conditional Appropriateness Rules

Version: 0.1
Status: Draft
Date: 2026-09-14

## Purpose

This document defines the conditions under which a structurally valid training plan is appropriate for the current athlete. It implements the Conditional Appropriateness component defined in [`../core_models/01_plan_model.md`](../core_models/01_plan_model.md).

---

Conditional appropriateness refers to whether a structurally valid training
plan is suitable for a particular athlete under a particular set of
conditions.

A plan can be structurally valid and still be inappropriate.

Appropriateness is therefore relational.

It depends on the interaction between:

Plan
→ Athlete
→ Goal
→ Current State
→ Training History
→ Time
→ Constraints
→ Uncertainty
→ Observed Response.

The system must not evaluate training content independently from these
conditions.

---

## 1. Athlete

The system must identify the athlete for whom the plan is intended.

Relevant information may include:

- training age,
- competitive level,
- technical proficiency,
- physical development,
- previous exposure to similar training,
- individual preferences,
- and known tolerance patterns.

Age or personal best alone is not sufficient to characterize an athlete.

Two athletes with similar 100m performance may require different training
because their training histories, strengths, limitations, and tolerance are
different.

---

## 2. Goal

The system must determine what outcome currently has the highest value.

The terminal objective is competitive 100m performance,
but the immediate planning problem may differ.

Examples may include:

- restoring trainability,
- improving acceleration,
- increasing maximum velocity exposure,
- improving late-race performance,
- maintaining strength,
- reducing residual fatigue,
- or preparing for competition.

A training method may be useful in general but inappropriate if it does not
serve the current priority.

---

## 3. Current State

The system must evaluate what the athlete can currently express and tolerate.

Current state may include:

- recent sprint performance,
- recent training exposure,
- fatigue,
- tissue response,
- technical stability,
- training motivation,
- and current ability to tolerate key tasks.

The system should distinguish where possible between:

Capacity Limitation

and

Performance Expression Limitation.

Poor performance does not automatically imply insufficient training.

It may reflect:

- accumulated fatigue,
- tissue irritation,
- environmental conditions,
- testing error,
- poor recovery,
- or an inappropriate recent load.

---

## 4. Training History

Training history provides information about what the athlete has already
adapted to and how the athlete has responded.

Relevant information may include:

- previously effective doses,
- previously ineffective doses,
- known intolerance,
- recent interruptions,
- previous injuries,
- previous taper responses,
- and long-term exposure to specific methods.

The system must not assume that a dose effective for another athlete is
appropriate for this athlete.

Individual history should be treated as prior information,
not as an irreversible rule.

---

## 5. Competition Calendar

Competition changes the value and cost of training.

The system must consider:

- competition importance,
- time remaining,
- competition density,
- qualifying rounds,
- travel,
- recovery between races,
- and whether competition itself provides a relevant sprint exposure.

A competition must not simply be added on top of a normal training week
without accounting for its training and recovery cost.

---

## 6. Time Horizon

The value of an adaptation depends partly on whether there is enough time for
it to occur, stabilize, transfer, and be expressed.

The system should ask:

- How much time remains?
- Is there enough time to develop this capacity?
- Is there enough time to learn the method?
- Is there enough time to recover from the intervention?
- Will this work interfere with competition preparation?

A training method with long adaptation or learning cost may be reasonable
early in a cycle and inappropriate immediately before an important race.

---

## 7. Recovery Capacity

The plan must match the athlete's actual recovery environment.

Relevant factors may include:

- sleep opportunity,
- nutrition,
- academic or occupational load,
- psychological stress,
- travel,
- total available recovery time,
- and recent accumulated training load.

The system must not assume full-time professional recovery conditions unless
they actually exist.

The same training dose may have different costs under different recovery
conditions.

---

## 8. Tissue Status

Local tissue response must influence planning when relevant.

The system should consider:

- pain,
- unusual tightness,
- localized soreness,
- repeated irritation,
- previous exposure tolerance,
- and applicable medical or rehabilitation restrictions.

General readiness indicators must not override a meaningful local tissue
warning.

A normal CMJ, motivation score, or subjective readiness value does not prove
that full-speed sprinting is appropriate for a symptomatic tissue.

---

## 9. Facilities and Environment

The training method must be executable under available conditions.

Relevant constraints may include:

- track length,
- surface,
- weather,
- temperature,
- indoor space,
- timing equipment,
- gym equipment,
- slope availability,
- and safe deceleration distance.

The system should modify the method when the environment prevents the intended
stimulus from being achieved.

For example, a short indoor space should not be labeled MaxV training if the
athlete cannot actually reach the required velocity.

---

## 10. Lifestyle Constraints

Training must fit the athlete's real life.

Relevant constraints may include:

- school,
- work,
- commuting,
- examination periods,
- training time,
- sleep schedule,
- and access to food or recovery resources.

A theoretically effective plan that cannot be consistently executed is not
conditionally appropriate.

Supporting work should not consume resources required for sleep, nutrition, or
key sprint sessions without sufficient reason.

---

## 11. Uncertainty

The system must explicitly identify important unknowns.

Examples include:

- missing recent sprint data,
- uncertain tissue tolerance,
- changed timing protocol,
- unfamiliar exercises,
- uncertain recovery capacity,
- or indirect evidence.

Greater uncertainty should generally reduce confidence in aggressive or
irreversible decisions.

When decision-critical information is missing, the system may prefer:

- a smaller exploratory dose,
- a previously tolerated option,
- additional observation,
- or a temporary "cannot determine" judgment.

Uncertainty must not be converted into false precision.

---

## 12. Observed Response

Appropriateness must be updated after implementation.

The system should compare:

Expected Response

with

Observed Response.

Relevant observations may include:

- whether the intended stimulus was actually achieved,
- immediate performance,
- technical quality,
- local tissue response,
- delayed recovery,
- and repeated performance trends.

A plan that was appropriate when prescribed may become inappropriate as the
athlete's state changes.

Appropriateness is therefore time-dependent.

---

## Conditional Appropriateness Rule

For a structurally valid plan, the system should ask:

1. Is this appropriate for this athlete?
2. Is it appropriate for the current goal?
3. Is it appropriate for the athlete's current state?
4. Does it account for training history?
5. Does it fit the competition calendar?
6. Is there enough time for the intended adaptation?
7. Can the athlete realistically recover from it?
8. Is it compatible with current tissue status?
9. Can the intended stimulus actually be produced with available facilities?
10. Can it be executed within lifestyle constraints?
11. How much important uncertainty remains?
12. Does the observed response continue to support the original decision?

Conditional appropriateness must be re-evaluated when relevant conditions
change.

The system must therefore distinguish:

"This method can work"

from

"This method is appropriate here, now, for this athlete."
