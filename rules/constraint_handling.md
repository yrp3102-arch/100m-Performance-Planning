# Constraint Handling Rules

Version: 0.1
Status: Draft
Date: 2026-09-14

## Purpose

This document defines the operational handling of hard constraints and the feasible planning space. The core concepts and invariants are defined in [`../core_models/01_plan_model.md`](../core_models/01_plan_model.md).

---

A hard constraint is a condition that defines the feasible planning space.

Hard constraints are not ordinary training variables to be optimized away.

They limit which plans are currently admissible.

The planning system must distinguish between:

Hard Constraints

and

Soft Constraints / Preferences.

A soft constraint may influence plan selection.

A hard constraint can make an otherwise attractive plan infeasible.

Therefore:

Best Expected Training Effect

does not override

Feasibility, Safety, Time, or Non-Negotiable Restrictions.

---

## 1. Competition Deadlines

Competition dates can function as hard temporal constraints.

The system cannot extend a development phase indefinitely when a fixed
competition date requires:

- tapering,
- travel,
- qualification,
- technical preparation,
- or performance expression.

The system should distinguish:

Flexible Review Date

from

Fixed Competition Deadline.

A mesocycle may be extended when useful,
but not without considering the opportunity cost imposed by the remaining
competition timeline.

When time becomes insufficient for the original objective,
the system must reconsider the objective rather than pretending that the
original adaptation can still be completed.

---

## 2. Medical and Rehabilitation Restrictions

Explicit medical or rehabilitation restrictions are hard constraints.

The planning system must not override:

- medical restrictions,
- rehabilitation-stage restrictions,
- return-to-sprint limitations,
- or other clearly defined clinical boundaries.

Training data such as:

- CMJ,
- RSI,
- sprint motivation,
- warm-up quality,
- or subjective readiness

must not independently cancel a relevant medical restriction.

The planning system may:

- identify conflicts,
- adjust training,
- record responses,
- and request reassessment.

It must not independently grant medical clearance.

---

## 3. Safety Constraints

A training method must be safely executable under the current conditions.

Relevant constraints may include:

- unsafe track surface,
- insufficient deceleration distance,
- severe weather,
- equipment failure,
- unsuitable footwear,
- dangerous training environment,
- or an acute loss of normal movement function.

If the intended stimulus cannot be delivered safely,
the system must:

- modify,
- postpone,
- substitute,
- or withdraw the session.

The existence of a scheduled training objective does not justify unsafe
execution.

Missed training caused by a safety constraint should not automatically be
"repaid" by compressing the same load into later sessions.

---

## 4. Tissue Constraints

Current tissue tolerance can define a hard local constraint.

Relevant information may include:

- acute pain,
- repeated localized symptoms,
- abnormal response to recent sprint exposure,
- reduced function,
- or known restrictions following injury.

A local tissue constraint may apply to one training method without prohibiting
all training.

For example:

Full-speed sprinting may be inappropriate

while

another lower-cost or non-provocative training option remains feasible.

The system should therefore avoid converting a local constraint into either:

"everything is safe"

or

"all training must stop"

without sufficient reason.

The feasible training space should be redefined around the actual limitation.

---

## 5. Facility and Environmental Constraints

The plan must respect the conditions required to produce the intended
stimulus.

Hard execution constraints may include:

- available track length,
- indoor space,
- safe acceleration and deceleration distance,
- surface quality,
- timing access,
- gym equipment,
- weather,
- temperature,
- and location access.

A training label must not substitute for the required task condition.

For example:

A session cannot meaningfully be treated as MaxV exposure if the available
space prevents the athlete from reaching the intended velocity.

When the environment changes,
the plan should preserve the adaptation objective where possible while
changing the method.

---

## 6. Time Availability

Available training time can function as a hard constraint.

The system must account for:

- school,
- work,
- travel,
- commuting,
- competition logistics,
- and realistic session duration.

A training plan that requires more time than the athlete can consistently
provide is not executable.

The system should not solve a time shortage by automatically:

- reducing rest below what the stimulus requires,
- adding excessive session density,
- sacrificing sleep,
- or removing the highest-priority training element.

When time is limited,
lower-priority work should normally be reconsidered before the primary
objective is compromised.

---

## 7. Recovery Ceiling

Recovery capacity places an upper boundary on usable training stress.

The system must not assume that all theoretically beneficial training can be
combined simultaneously.

Available recovery capacity may be constrained by:

- sleep opportunity,
- nutrition,
- life stress,
- previous training load,
- competition exposure,
- travel,
- and local tissue tolerance.

When the expected total cost exceeds plausible recovery capacity,
the system must reduce, reorganize, or remove training.

The solution must not simply be:

"recover better"

when the recovery environment itself is constrained.

Training design must adapt to the recovery resources that actually exist.

---

## 8. Information Constraints

Decision-critical uncertainty can itself limit admissible decisions.

When important information is missing,
the system should distinguish between:

Unknown but Low Consequence

and

Unknown with High Decision Consequence.

Examples of high-consequence uncertainty may include:

- unclear tissue tolerance before high-speed exposure,
- changed timing protocol before interpreting sprint improvement,
- uncertain competition date,
- unknown recent training load,
- or an unfamiliar high-cost training method.

When uncertainty is large and the downside of error is meaningful,
the system should avoid aggressive assumptions.

Feasible responses may include:

- using a previously tolerated option,
- reducing the exploratory dose,
- collecting more information,
- delaying an irreversible decision,
- or marking the decision as "cannot yet determine."

Missing information must not be converted into a convenient default when that
default materially changes the plan.

---

## 9. Constraint Conflicts

Multiple constraints may conflict.

For example:

- competition timing may favor continued sprint exposure,
- while tissue status limits the same exposure;

or:

- the current training objective may favor additional volume,
- while recovery capacity prevents it.

The system must not hide these conflicts.

It should identify:

1. which constraints are active,
2. which are hard,
3. which are soft,
4. which objectives are affected,
5. and what trade-off remains feasible.

When two requirements cannot both be satisfied,
the system must revise the feasible objective set.

---

## 10. Constraints Can Change

A hard constraint is not necessarily permanent.

Some constraints may change through:

- recovery,
- rehabilitation,
- improved facility access,
- calendar revision,
- reduced life stress,
- or new information.

The system should therefore distinguish:

Current Hard Constraint

from

Permanent Limitation.

When a constraint changes,
previously excluded training options may become feasible again.

Reintroduction should still be justified by the athlete's current state and
training objective.

---

## Constraint Invariants

Before optimizing a training plan,
the system must first define the feasible planning space.

The sequence is:

Objective

→ Identify Hard Constraints

→ Remove Infeasible Options

→ Identify Remaining Soft Constraints

→ Compare Feasible Training Options

→ Select and Monitor.

The system must not choose an infeasible plan merely because its theoretical
training benefit appears higher.

When a hard constraint changes,
the feasible planning space should be updated.

When a hard constraint cannot be satisfied,
the objective or method must change.
