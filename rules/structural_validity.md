# Structural Validity Rules

Version: 0.1
Status: Draft
Date: 2026-09-14

## Purpose

This document defines the operational rules used to determine whether a training plan is structurally coherent, interpretable, executable, and reviewable. It implements the Structural Validity component defined in [`../core_models/01_plan_model.md`](../core_models/01_plan_model.md).

---

Structural validity refers to whether a training plan is internally coherent,
interpretable, executable, and reviewable before considering whether it is
optimal for a specific athlete.

Structural validity is therefore different from conditional appropriateness.

A plan may be structurally valid but inappropriate for a specific athlete.

A plan may also produce a favorable result while still containing structural
defects.

The system should evaluate structural validity before comparing expected
training effectiveness.

---

## 1. Objective Clarity

The plan must identify what it is trying to achieve.

The objective should be specific enough to organize decisions.

Examples of insufficient objectives include:

- "get faster,"
- "improve athleticism,"
- "build power,"
- "increase fitness."

These may describe general intentions but do not yet define a usable planning
problem.

A structurally valid objective should clarify:

- the target performance outcome,
- the relevant time horizon,
- the current adaptation problem,
- and the priority of that problem.

---

## 2. Dose Interpretability

The prescribed training must be interpretable.

A plan should provide enough information to understand the actual stimulus.

For example:

"MaxV training"

is not a complete prescription.

Relevant information may include:

- approach distance,
- target distance,
- target velocity,
- repetitions,
- sets,
- recovery interval,
- timing method,
- actual achieved velocity,
- and stop conditions.

Likewise:

"strength training"

does not define:

- exercise,
- load,
- repetitions,
- sets,
- proximity to failure,
- movement range,
- or intended execution quality.

If the dose cannot be interpreted, it cannot be reliably executed,
compared, or revised.

---

## 3. Internal Consistency

The plan must not contain contradictions between its stated objective,
classification, and actual content.

Examples include:

- calling a session "Low" while prescribing substantial lower-limb loading,
- declaring MaxV the primary objective while allocating most recovery
  resources to unrelated work,
- labeling all capacities as Primary,
- prescribing recovery while simultaneously increasing total load,
- or describing a taper while replacing reduced sprint volume with additional
  strength, jumping, or testing.

Labels do not override actual content.

The system must evaluate what the plan actually requires.

---

## 4. Temporal Consistency

Training elements must be compatible across time.

A session may be reasonable in isolation but unreasonable in sequence.

The system should check:

- within-session ordering,
- spacing between demanding sessions,
- competition placement,
- travel,
- testing,
- recovery windows,
- and interactions between adjacent training days.

A plan is structurally defective if its own schedule prevents important
sessions from being executed as intended.

---

## 5. Resource Feasibility

The plan must fit the resources that actually exist.

Relevant resources may include:

- available training days,
- session duration,
- track access,
- sprinting distance,
- gym access,
- timing equipment,
- recovery time,
- travel conditions,
- coaching supervision,
- and athlete attention.

A plan that requires unavailable resources is not executable.

The system must not silently assume access to elite-level facilities,
medical support, recovery resources, or unlimited training time.

---

## 6. Priority Coherence

The plan must allocate limited resources according to declared priorities.

If multiple goals compete for the same time or recovery budget,
their relative importance must be visible.

A structurally valid plan should distinguish between:

- development priorities,
- maintenance priorities,
- supporting work,
- and temporarily reduced or withdrawn work.

If every training quality receives development-level volume,
the plan has not actually established priorities.

---

## 7. Recovery Coherence

The recovery structure must be compatible with the prescribed load.

The plan should not treat recovery as an empty label.

It should consider:

- the residual cost of previous sessions,
- the content of so-called Low days,
- expected tissue loading,
- competition load,
- travel,
- lifestyle stress,
- and the demands of the next key session.

A recovery structure is invalid if the plan repeatedly creates more residual
cost than the next important training task can tolerate.

---

## 8. Monitoring Coherence

Monitoring must correspond to the decisions the plan claims to make.

If the plan states that training will be adjusted according to performance,
recovery, or tissue response, then the relevant information must actually be
collected.

The system should ask:

- What is being monitored?
- Why is it being monitored?
- How is it measured?
- What decision can it change?
- How much noise is expected?
- When will it be reviewed?

Monitoring that cannot alter interpretation or action is informationally
redundant.

---

## 9. Correction Path

A structurally valid plan must define what happens when expectations are not
met.

The plan should contain paths for:

- maintaining the current dose,
- reducing the dose,
- changing the method,
- changing the sequence,
- temporarily withdrawing a stimulus,
- delaying progression,
- or transitioning to another phase.

A plan that defines only how to continue is structurally incomplete.

---

## 10. Traceability

Important planning decisions should be traceable.

The system should be able to reconstruct:

- what the original objective was,
- what was prescribed,
- what was actually completed,
- what response occurred,
- what information changed,
- and why the next decision was made.

Without traceability, later success or failure cannot be meaningfully audited.

---

## Structural Validity Check

Before evaluating whether a plan is optimal for a specific athlete,
the system should ask:

1. Is the objective clear?
2. Is the training dose interpretable?
3. Is the plan internally consistent?
4. Is the temporal sequence coherent?
5. Is the plan executable with available resources?
6. Are priorities explicit?
7. Is recovery compatible with the actual load?
8. Does monitoring correspond to decisions?
9. Is there a correction path?
10. Can important decisions be traced?

If a plan fails a necessary structural condition,
the system should first repair the structure before attempting fine-grained
optimization.
