# Research Intervention Workflow

Version: 0.1
Status: Draft
Date: 2026-09-16

## Purpose

This Workflow converts a defined planning problem or required exposure into a
bounded set of intervention candidates that a planning Workflow can evaluate
and, when sufficiently specified, turn into an executable prescription.

It answers:

> Given the current problem, athlete context, and decision level, what
> intervention candidates are supportable, under what conditions, with what
> dose representation, cost, risk, evidence, and uncertainty?

Its primary chain is:

```text
Defined Problem or Exposure Need
→ Intervention Decision Question
→ Retrieval Vocabulary
→ Candidate Sources
→ Evidence Extraction
→ Normalized Candidate Intervention
→ Applicability Evaluation
→ Dose, Cost, Risk, and Uncertainty Representation
→ Conditional Candidate Comparison
→ Planning Handoff
```

The terminal product is decision input. It is not an automatic training
prescription.

---

## System Boundary

This Workflow is responsible for:

- defining the intervention information gap;
- deciding whether retrieval is necessary;
- building decision-relevant retrieval vocabulary;
- retrieving progressively rather than exhaustively;
- extracting source information under the
  [Evidence Record Schema](../evidence/evidence_record_schema.md);
- normalizing intervention candidates through the
  [Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md);
- evaluating population, protocol, athlete-state, constraint, and competition
  applicability;
- representing dose support, expected benefit, cost, risk, transfer, and
  uncertainty without false precision;
- comparing feasible candidates under current conditions; and
- returning a bounded handoff to the invoking planning Workflow.

This Workflow does not:

- define competitive 100m performance or its determinants;
- reconstruct Athlete State or identify the performance problem;
- allocate strategic priority;
- create a Mesocycle, Week, or Session;
- diagnose injury or any medical condition;
- establish a fixed exercise library;
- create permanent intervention rankings;
- treat search-engine ranking, popularity, or recency as evidence quality;
- convert one source directly into a prescription;
- automatically persist every retrieval result; or
- modify Evidence, Theory, Domain, Rules, Core Models, or the Constitution.

The [100m Performance Core Model](../core_models/02_100m_performance_model.md)
defines the target and transfer problem. The
[Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md)
defines intervention representation. The
[Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
defines how Actual Exposure and response later update the decision.

The following distinctions are invariant:

- Exercise Label does not equal Training Stimulus.
- Prescription does not equal Actual Exposure.
- Evidence does not equal Decision.
- Population Match does not establish athlete-specific transfer.
- Supporting Adaptation does not establish 100m Performance Improvement.
- Candidate Intervention does not equal Selected Intervention.
- Search Result does not equal Evidence Record.
- Recent does not mean better.
- Popular does not mean appropriate.
- Mechanistically plausible does not mean proven effective.
- No evidence found does not mean evidence of no effect.

---

## Entry Conditions

Enter this Workflow only when a defined planning decision contains an
intervention information gap.

Valid entry signals include:

- `Candidate Intervention Required` from
  [Create Mesocycle](./create_mesocycle.md),
  [Create Week](./create_week.md), or
  [Create Session](./create_session.md);
- `External Retrieval May Be Invoked` from a planning Workflow;
- inability to form a defensible `selected_intervention`;
- an existing intervention whose dose, applicability, evidence, cost, risk,
  stop condition, or monitoring interface is insufficient for the current
  decision;
- an explicit request for a method, dose, alternative, or evidence review; or
- a need for new external information to distinguish feasible candidates.

Retrieval is justified only when new information may materially change at
least one of:

- candidate inclusion or conditional preference;
- dose boundary or dose-status classification;
- confidence;
- constraint interpretation;
- cost or risk interpretation;
- stop or modification conditions; or
- monitoring requirements.

The ability to search is not an entry condition.

### Minimum Entry Packet

The invoking Workflow should provide:

| Field | Required meaning |
|---|---|
| `request_id` | Traceable identifier for this retrieval decision |
| `invoking_workflow` | Mesocycle, Week, Session, or explicit user request |
| `decision_level` | Planning level at which the answer will be used |
| `target_problem` | Defined performance or planning problem |
| `target_determinant_or_capacity` | Object the intervention is intended to influence |
| `required_exposure` | Exposure characteristics required by the plan |
| `priority_role` | Current strategic or supporting role, inherited rather than reassigned here |
| `athlete_state_assumptions` | Current decision-relevant state assumptions and their confidence |
| `constraints` | Hard and soft constraints already identified |
| `competition_context` | Time horizon, competition proximity, and freshness requirements |
| `current_uncertainty` | Unresolved facts relevant to intervention choice or dose |
| `missing_information` | Specific gap that retrieval may close |
| `decision_change` | What downstream decision could change if the gap is resolved |

If target, required exposure, or decision use is undefined, return
`MORE_INFORMATION_REQUIRED` to the invoking planning Workflow. Do not use
retrieval to manufacture the upstream planning problem.

---

## Required Interfaces

This Workflow reads the following authorities by reference:

- [Constitution](../CONSTITUTION.md) for system authority and layer boundaries;
- [100m Performance Core Model](../core_models/02_100m_performance_model.md)
  for determinant, indicator, bottleneck, transfer, and competition-expression
  meaning;
- [Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md)
  for intervention, exposure, dose, adaptation, cost, risk, and uncertainty;
- [Feedback-Decision Core Model](../core_models/04_feedback_decision_model.md)
  for Actual Exposure and monitoring handoff;
- [Domain Layer](../domain/README.md) and
  [100m Domain](../domain/100m_domain.md) for controlled vocabulary;
- [Evidence Layer](../evidence/README.md) and the
  [Evidence Record Schema](../evidence/evidence_record_schema.md) for extraction
  and persistence boundaries;
- [Theory Layer](../theory/README.md) and the
  [100m Training Framework](../theory/100m_training_framework.md) for explicit
  priors rather than assumed truth;
- [Conditional Appropriateness Rules](../rules/conditional_appropriateness.md),
  [Constraint Handling Rules](../rules/constraint_handling.md), and
  [Uncertainty Handling Rules](../rules/uncertainty_handling.md) for candidate
  boundaries;
- [Plan Comparison Rules](../rules/plan_comparison.md) for conditional
  comparison; and
- [Priority Allocation Rules](../rules/priority_allocation.md) for reading the
  inherited priority without reallocating it.

Source access may include project Evidence Records, primary literature,
systematic reviews, protocol or measurement sources, credible coaching-practice
sources, athlete history, and other structured sources. Source type changes
the supported inference; it does not automatically determine relevance.

---

## Workflow Overview

Each step uses the same routing form:

```text
Required Inputs
→ Action
→ Output
→ Stop, Return, or Escalation
```

The Workflow may end early with `RETRIEVAL_NOT_REQUIRED` when existing
information is sufficient. It may end without a candidate when the information
gap is athlete-side, medical, upstream, or not resolvable through additional
retrieval.

---

## Step 1. Define the Decision Question

### Required Inputs

- Minimum Entry Packet;
- current planning level;
- known candidate families, if any; and
- intended decision use.

### Action

Translate the entry signal into a specific intervention decision question.
Record:

- target performance problem;
- target determinant, capacity, or expression need;
- required exposure;
- inherited priority role;
- Athlete State assumptions and confidence;
- constraints and available resources;
- competition timing;
- current uncertainty;
- decision level;
- missing information; and
- the decision the answer could change.

The question must bind retrieval to an actionable planning distinction. A
generic request such as “find maximum-velocity training” is insufficient.

### Output

`intervention_decision_question`, including:

```yaml
intervention_decision_question:
  request_id:
  invoking_workflow:
  decision_level:
  target_problem:
  target_determinant_or_capacity:
  required_exposure:
  priority_role:
  athlete_state_assumptions:
  constraints:
  competition_context:
  current_uncertainty:
  missing_information:
  decision_change:
```

### Stop, Return, or Escalation

- Return `MORE_INFORMATION_REQUIRED` when the planning target, required
  exposure, or decision use is undefined.
- Return `EXTERNAL_ASSESSMENT_REQUIRED` when the missing information requires
  medical or other qualified external assessment.
- Continue only when retrieval can plausibly affect a bounded decision.

---

## Step 2. Test Existing Knowledge Sufficiency

### Required Inputs

- `intervention_decision_question`;
- relevant Domain and Theory entries;
- existing Evidence Records; and
- applicable athlete history and prior Actual Exposure records.

### Action

Determine whether the current decision can already be supported by:

- a sufficiently defined intervention family in Domain;
- an explicit Theory prior whose conditions match;
- existing Evidence Records with adequate protocol and applicability detail;
- a previously successful and still-applicable athlete-specific intervention;
  or
- a known, tolerated method whose current dose, cost, and constraints can be
  represented without additional claims.

Existing information is sufficient only when it can identify a feasible
candidate, represent the material dose dimensions at the required planning
level, state applicability limits, identify major cost and risk, preserve
uncertainty, and support bounded comparison or selection.

### Output

One of:

- `RETRIEVAL_NOT_REQUIRED`, with existing support and the downstream handoff;
- `RETRIEVAL_REQUIRED`, with a precise `retrieval_gap`; or
- `MORE_INFORMATION_REQUIRED`, when athlete-side or upstream information is
  missing.

### Stop, Return, or Escalation

Return immediately when existing information is sufficient. Do not repeat
retrieval solely to make the source list longer or newer.

---

## Step 3. Build Retrieval Vocabulary

### Required Inputs

- `intervention_decision_question`;
- `retrieval_gap`; and
- controlled terms from [100m Domain](../domain/100m_domain.md).

### Action

Build a vocabulary set across the dimensions that matter to the decision:

```text
Target
+ Intervention Family
+ Population and Training Status
+ Outcome
+ Dose or Protocol
+ Comparator
+ Risk or Recovery
+ Date or Freshness, when material
```

Preserve:

- canonical terms;
- aliases and common task labels;
- terms whose meaning is ambiguous;
- population and performance-level qualifiers;
- protocol and dose vocabulary;
- outcome and measurement vocabulary; and
- negative or contrast terms such as no effect, adverse effect, comparison,
  recovery, and transfer.

Use separate vocabulary branches when one label may describe materially
different tasks or stimuli. Do not let the initial hypothesis constrain the
search to supportive terms.

### Output

`retrieval_vocabulary`, containing canonical terms, aliases, ambiguity notes,
contrast terms, and query components linked to the decision question.

### Stop, Return, or Escalation

Return `MORE_INFORMATION_REQUIRED` if the target concept cannot be
disambiguated without upstream clarification. A vocabulary gap may create a
future Domain review candidate, but this Workflow does not update Domain.

---

## Step 4. Retrieve Progressively

### Required Inputs

- `intervention_decision_question`;
- `retrieval_vocabulary`;
- current source access; and
- a decision-specific stopping condition.

### Action

Retrieve from the smallest source set likely to resolve the current gap.
Possible source classes include:

1. existing persistent Evidence Records;
2. primary research or systematic review;
3. measurement or protocol evidence;
4. high-quality coaching-practice sources;
5. athlete-specific historical records; and
6. other relevant structured sources.

This order is adaptable. Source priority follows the decision, the missing
inference, and the consequence of error. It is not a permanent database
ranking.

For each retrieval round:

- state the unresolved question;
- retrieve sources capable of answering that question;
- include contradictory, null, and bounding evidence where available;
- record source access limits and missing full text;
- evaluate whether another round is likely to change the decision; and
- stop when the minimum sufficient evidence condition is met.

Search result ranking, snippets, citations without source inspection, author
reputation, and social popularity do not establish evidence strength.

### Output

`candidate_source_set`, with source identity, source type, retrieval date,
access status, relevance to the gap, and extraction status.

### Stop, Return, or Escalation

- Stop retrieval when Step 10 sufficiency is met.
- Return `INSUFFICIENT_EVIDENCE` when accessible sources cannot support the
  necessary inference.
- Return `MORE_INFORMATION_REQUIRED` when literature is adequate but the
  remaining limit is athlete-specific information.
- Return `EXTERNAL_ASSESSMENT_REQUIRED` when the remaining question lies
  outside training-planning authority.

---

## Step 5. Extract Evidence

### Required Inputs

- `candidate_source_set`; and
- [Evidence Record Schema](../evidence/evidence_record_schema.md).

### Action

For each material source, extract at least:

- source identity and evidence type;
- population, training status, and performance level;
- intervention or exposure and the actual reported protocol;
- dose dimensions, rest, density, duration, and frequency;
- execution conditions, environment, cointerventions, and comparator;
- outcome role and measurement protocol;
- main, null, adverse, and bounding findings;
- design, reporting, exposure-fidelity, and measurement limitations;
- external validity and 100m relevance;
- transfer boundary;
- risk and recovery information;
- uncertainty; and
- publication, retrieval, and review freshness.

Keep terminal 100m outcome, race or segment outcome, determinant, capacity,
indicator, and proxy roles separate. State the inference each source supports
and the inference it does not support.

Classify each extracted object as one of:

- `LIVE_RETRIEVAL_CANDIDATE`;
- `EXISTING_PERSISTENT_EVIDENCE_RECORD`; or
- `REJECTED_SOURCE`, with reason.

A live extraction does not need to become a complete persistent Evidence
Record during the current decision. Its precision must still not exceed the
source.

### Output

`evidence_extractions`, each linked to the decision question, candidate
relationship, supported inference, bounded inference, and unresolved limits.

### Stop, Return, or Escalation

Reject source-dependent claims that cannot be verified from the accessible
source. Missing reporting must remain missing; it must not be reconstructed
from common practice.

---

## Step 6. Normalize Candidate Intervention

### Required Inputs

- `evidence_extractions`;
- existing project knowledge;
- Athlete State assumptions; and
- the [Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md).

### Action

Convert task labels and source protocols into normalized Candidate
Interventions. One candidate represents a conditional intervention hypothesis,
not a universally defined exercise.

Candidates that share a label but differ materially in intended stimulus,
dose, execution conditions, temporal placement, or expected cost must remain
distinct.

### Candidate Intervention Output Contract

Each candidate must attempt to populate:

```yaml
candidate_intervention:
  candidate_id:
  request_id:
  candidate_status:
  target_problem:
  target_determinant_or_capacity:
  required_exposure:
  priority_role:
  intervention_family:
  task_or_method:
  intended_stimulus:
  expected_adaptation:
  transfer_hypothesis:
  transfer_boundary:
  athlete_population_match:
  athlete_state_assumptions:
  execution_conditions:
  environment_and_equipment:
  planned_dose_dimensions:
  dose_range_or_boundary:
  minimum_meaningful_exposure:
  upper_boundary:
  rest_and_density:
  frequency_and_distribution:
  quality_requirements:
  stop_or_modify_conditions:
  expected_time_to_useful_effect:
  cost_profile:
    acute_fatigue_cost:
    recovery_cost:
    local_tissue_cost:
    interference_cost:
    opportunity_cost:
    competition_expression_cost:
    execution_and_monitoring_cost:
  risk_profile:
  competition_proximity_effect:
  monitoring_interface:
  supporting_evidence: []
  contradictory_or_bounding_evidence: []
  evidence_roles:
  dose_support_status:
  applicability_summary:
  confidence:
  unresolved_uncertainty: []
  source_references: []
```

Use `not_applicable`, `not_reported`, `unknown`, or `cannot_determine` where
appropriate. Do not fabricate repetitions, distance, duration, load,
intensity, rest, frequency, velocity threshold, decrement threshold, or stop
threshold.

Qualitative bounds are valid outputs when they match source precision.
When the evidence cannot support a dose representation, emit
`CANNOT DETERMINE DOSE YET` rather than inferred numerical detail.

### Output

`normalized_candidate_set`, with traceable evidence and explicit missing
fields.

### Stop, Return, or Escalation

Reject `LABEL_ONLY_INTERVENTION` candidates that cannot be interpreted beyond
a task name. Retain partially specified candidates only when their limited
status is explicit and they can still inform a higher-level choice.

---

## Step 7. Evaluate Applicability

### Required Inputs

- `normalized_candidate_set`;
- Athlete State assumptions;
- constraints and resources;
- competition context; and
- relevant Rules.

### Action

Evaluate each candidate on:

- population match;
- training-status match;
- performance-level match;
- sex and age relevance when material;
- protocol match;
- current Athlete State match;
- hard- and soft-constraint compatibility;
- facility and equipment compatibility;
- competition timing;
- transfer plausibility;
- dose familiarity;
- tissue tolerance;
- recovery cost;
- opportunity cost; and
- measurement and monitoring feasibility.

Use qualitative states:

- `HIGH_MATCH`;
- `MODERATE_MATCH`;
- `LIMITED_MATCH`;
- `INDIRECT`;
- `UNKNOWN`; or
- `MIXED`.

Applicability is dimension-specific. A candidate may have a strong population
match and weak protocol match. Do not collapse the dimensions into a false
total score.

Separate:

- source quality;
- contextual applicability;
- athlete-specific feasibility; and
- transfer confidence.

### Output

`applicability_profile` for every candidate, including exclusions, conditional
requirements, and uncertainty.

### Stop, Return, or Escalation

- Exclude candidates that violate a hard constraint.
- Return `MORE_INFORMATION_REQUIRED` when feasibility depends on missing
  athlete data.
- Return `EXTERNAL_ASSESSMENT_REQUIRED` when safety or medical compatibility
  requires qualified assessment.

---

## Step 8. Represent Dose, Cost, Risk, and Uncertainty

### Required Inputs

- feasible Candidate Interventions;
- extracted protocol detail;
- applicability profiles;
- Athlete State assumptions; and
- decision level.

### Action

Represent dose as a task-specific, multidimensional object. Include only the
dimensions needed to distinguish meaningful exposure, execution quality, and
cost at the current planning level.

For each candidate, distinguish:

- the intervention family supported by evidence;
- the actual protocol studied or observed;
- the dose range or boundary that can be generalized, if any;
- source-specific conditions that limit generalization;
- the planning-level dose direction;
- the Session-level information still required; and
- athlete-side conditions that must be checked before execution.

Assign one dose-support status:

- `INTERVENTION_DIRECTION_SUPPORTED` together with
  `DOSE_NOT_YET_SUPPORTED`; or
- `EXECUTABLE_CANDIDATE_AVAILABLE`.

`EXECUTABLE_CANDIDATE_AVAILABLE` requires enough support to represent relevant
dose dimensions, rest or density, execution conditions, quality criteria,
stop or modification conditions, major cost, major risk, and uncertainty. It
does not guarantee that the planning Workflow will select the candidate or
that Actual Exposure will match the prescription.

Represent cost across relevant dimensions rather than one total score. Keep
risk separate from uncertainty:

- risk describes identified adverse possibilities or costs;
- uncertainty describes limits in knowing the relationship, response, or
  outcome.

Supporting adaptation requires an explicit transfer hypothesis to the current
100m target. Absence of direct 100m outcome evidence must remain visible.

### Output

Updated candidate records with `dose_support_status`, cost profile, risk
profile, transfer boundary, confidence, and unresolved uncertainty.

### Stop, Return, or Escalation

- Do not create an executable handoff from family-level support alone.
- Return `SESSION_INTERVENTION_HANDOFF_BLOCKED` when Session precision exceeds
  evidence precision.
- Identify whether missing precision is literature-side or athlete-side.

---

## Step 9. Compare Candidates

### Required Inputs

- feasible normalized candidates;
- current decision conditions; and
- [Plan Comparison Rules](../rules/plan_comparison.md).

### Action

Remove candidates that fail necessary feasibility conditions. Compare the
remaining candidates on:

- expected target relevance;
- transfer potential;
- execution reliability;
- dose interpretability;
- athlete familiarity;
- expected time to useful effect;
- recovery and opportunity cost;
- tissue demand and other risk;
- competition compatibility;
- monitoring feasibility;
- reversibility; and
- uncertainty.

Preserve Pareto trade-offs. Do not hide conflicting dimensions in a numeric
total score. Compare current marginal value rather than historical reputation.

The permitted conclusions are:

- best-supported candidate under current conditions;
- several conditionally viable candidates with explicit trade-offs; or
- cannot determine with the missing discriminating information stated.

### Output

One of:

- `CANDIDATE_SET_READY`;
- `SINGLE_CANDIDATE_PREFERRED_UNDER_CURRENT_CONDITIONS`;
- `INSUFFICIENT_EVIDENCE`;
- `MORE_INFORMATION_REQUIRED`; or
- `EXTERNAL_ASSESSMENT_REQUIRED`.

The output must include alternatives considered, exclusions, comparison
conditions, material trade-offs, and confidence.

### Stop, Return, or Escalation

This Workflow has no authority to declare a universal best exercise or to
select the final Session prescription. Conditional preference returns to the
invoking planning Workflow.

---

## Step 10. Determine Retrieval Sufficiency

### Required Inputs

- decision question;
- evidence extractions;
- normalized candidates;
- applicability profiles;
- comparison result; and
- remaining uncertainty.

### Action

Determine whether the current evidence is minimally sufficient for the
requested decision level.

Minimum sufficient evidence exists when the Workflow can:

- identify at least one feasible candidate or defensibly conclude that none is
  supportable;
- represent the dose dimensions material to the requested level;
- state applicability and transfer limits;
- identify major cost and risk;
- preserve contradictory or bounding evidence;
- define remaining uncertainty;
- support bounded comparison or selection; and
- state what the downstream Workflow may and may not infer.

Sufficiency is relative to the handoff level. Evidence may be sufficient for a
Mesocycle intervention direction while insufficient for an executable Session
dose.

### Output

```yaml
retrieval_sufficiency:
  status: sufficient | insufficient | athlete_information_limited | external_assessment_limited
  supported_decision_level:
  unsupported_precision:
  remaining_uncertainty:
  expected_value_of_further_retrieval:
  stop_reason:
```

### Stop, Return, or Escalation

Stop retrieval when any Stop Rule below applies. Continue only when another
bounded retrieval round is likely to change a material planning conclusion.

---

## Step 11. Produce Planning Handoff

### Required Inputs

- retrieval sufficiency result;
- candidate set or conditional preference;
- invoking Workflow; and
- supported decision level.

### Action

Return the smallest complete packet required by the invoking planning
Workflow. The handoff must preserve evidence limits and does not transfer final
selection authority.

### Mesocycle or Week Handoff

For Mesocycle or Week use, return:

- target problem and required exposure;
- feasible intervention families or candidates;
- intended stimulus and expected adaptation;
- dose direction and supported bounds;
- transfer hypothesis and boundary;
- cost, risk, and competition effects;
- applicability conditions;
- comparison result and alternatives;
- monitoring or information need;
- confidence and unresolved uncertainty; and
- source support.

### `SESSION_INTERVENTION_HANDOFF`

Produce this object only when at least one candidate is executable at Session
planning precision:

```yaml
SESSION_INTERVENTION_HANDOFF:
  request_id:
  candidate_id:
  target:
  intervention:
  purpose:
  intended_stimulus:
  transfer_hypothesis:
  dose_dimensions:
  dose_bounds_or_known_range:
  rest_and_density:
  execution_conditions:
  quality_criteria:
  stop_or_modify_conditions:
  expected_cost:
  major_risk:
  monitoring:
  confidence:
  uncertainty:
  source_support:
  what_remains_athlete_specific:
  alternatives_and_tradeoffs:
  planning_authority_note:
```

`planning_authority_note` must state that
[Create Session](./create_session.md) still confirms current Athlete State,
constraints, Session role, and final prescription.

### `SESSION_INTERVENTION_HANDOFF_BLOCKED`

When Session precision is unsupported, return:

```yaml
SESSION_INTERVENTION_HANDOFF_BLOCKED:
  request_id:
  supported_intervention_direction:
  missing_information:
  missing_information_side: literature | athlete | both | external_assessment
  unsupported_fields:
  why_execution_is_not_yet_justified:
  next_action:
  safe_downstream_use:
  confidence:
  unresolved_uncertainty:
```

`safe_downstream_use` may allow a Mesocycle or Week direction while blocking a
Session prescription.

### Output

Planning handoff plus one selection-boundary status:

- `CANDIDATE_SET_READY`;
- `SINGLE_CANDIDATE_PREFERRED_UNDER_CURRENT_CONDITIONS`;
- `INSUFFICIENT_EVIDENCE`;
- `MORE_INFORMATION_REQUIRED`; or
- `EXTERNAL_ASSESSMENT_REQUIRED`.

### Stop, Return, or Escalation

Return to the invoking planning Workflow. Do not create the Mesocycle, Week,
or Session inside this Workflow.

---

## Step 12. Evidence Persistence Decision

### Required Inputs

- live evidence extractions;
- decision value;
- rediscovery cost;
- project recurrence; and
- [Evidence Layer](../evidence/README.md) persistence policy.

### Action

Consider persistence only when at least one condition applies:

- recurring usefulness;
- high decision value;
- difficult rediscovery;
- Theory-update relevance;
- recurring conflict; or
- repeated project reference.

Check minimum completeness under the
[Evidence Record Schema](../evidence/evidence_record_schema.md). Preserve source
identity, population, protocol, outcomes, limitations, claim role, freshness,
and uncertainty.

### Output

One of:

- `PERSISTENCE_CANDIDATE`, with reason and proposed Evidence Record scope; or
- `NO_PERSISTENCE_RECOMMENDED`, with the live retrieval remaining task-local.

### Stop, Return, or Escalation

This Workflow does not write to Evidence or update Theory, Domain, Rules, Core
Models, or the Constitution. A material challenge to an existing claim may
create a `REVIEW CANDIDATE` under existing governance.

---

## Failure Modes

| Failure code | Why it matters | Required correction |
|---|---|---|
| `LABEL_ONLY_INTERVENTION` | A task name does not define stimulus, dose, execution, or cost | Normalize the candidate through the 03 model or reject it |
| `POPULARITY_AS_EVIDENCE` | Frequency of use does not establish effectiveness or suitability | Identify inspectable evidence and its supported inference |
| `PROXY_AS_TERMINAL_OUTCOME` | Improvement in a supporting measure may not transfer to competitive 100m performance | State the outcome role and explicit transfer boundary |
| `POPULATION_MISMATCH` | Effects in another population may not apply to the current athlete | Record the mismatch, reduce applicability, or find better-matched evidence |
| `PROTOCOL_MISSING` | An intervention label without exposure detail cannot support dose interpretation | Retrieve protocol detail or limit the output to family-level direction |
| `DOSE_PRECISION_UNSUPPORTED` | Fabricated precision can create an unjustified prescription | Use qualitative bounds or `CANNOT_DETERMINE_DOSE_YET` |
| `REST_PRECISION_UNSUPPORTED` | Rest changes stimulus and quality but is often incompletely reported | State that rest is unsupported and block executable handoff if material |
| `TRANSFER_ASSUMED` | Supporting adaptation is not automatically 100m improvement | Add a transfer hypothesis, limits, and verification need |
| `COST_IGNORED` | A useful candidate may displace higher-value work or impair quality | Represent recovery, tissue, interference, and opportunity cost |
| `RISK_IGNORED` | Expected benefit alone cannot justify avoidable downside | State candidate-specific risk and current tolerance uncertainty |
| `CONTRADICTORY_EVIDENCE_DROPPED` | Selective extraction inflates confidence | Preserve contradictory, null, and bounding findings |
| `CONFIRMATION_ONLY_SEARCH` | Query design can predetermine the answer | Add comparator, no-effect, adverse-effect, and boundary vocabulary |
| `SEARCH_WITHOUT_DECISION_VALUE` | Retrieval consumes time without changing planning | State the decision that could change or stop retrieval |
| `NO_STOP_CONDITION` | Open-ended search creates retrieval overload | Define minimum sufficiency and expected value of another round |
| `RETRIEVAL_OVERLOAD` | More sources can increase context cost without improving the decision | Keep only decision-relevant extractions and stop at sufficiency |
| `SOURCE_RECENCY_WORSHIP` | Newer sources are not automatically more valid or applicable | Evaluate quality, protocol, applicability, and freshness separately |
| `EVIDENCE_TO_PRESCRIPTION_JUMP` | Research conditions do not automatically define the athlete's Session | Route the candidate back through planning, constraints, and current state |
| `MEDICAL_INFERENCE_FROM_TRAINING_SOURCE` | Training evidence cannot establish diagnosis or medical clearance | Return `EXTERNAL_ASSESSMENT_REQUIRED` |

Failure correction should occur at the smallest affected step. A local
extraction error does not require restarting the full Workflow unless it
changes the decision question or candidate set.

---

## Stop Rules

Stop retrieval when any of the following is true:

1. Minimum Sufficient Evidence exists for the current decision level.
2. Additional sources are unlikely to change candidate inclusion, ordering,
   dose support, cost or risk interpretation, confidence, stop conditions, or
   monitoring need.
3. Precision is limited by athlete-specific unknowns rather than literature.
4. The next required information is Actual Exposure or athlete response.
5. The next required information needs qualified external assessment.
6. The opportunity cost of further retrieval exceeds its plausible decision
   value.
7. Accessible evidence cannot support the requested inference and the boundary
   has been documented.

Do not continue solely because a better paper may exist. Stop status must name
the reason and the next decision-relevant action.

---

## Output Contract

Every completed run outputs:

```yaml
research_intervention_output:
  request_id:
  workflow_version: 0.1
  retrieval_status: RETRIEVAL_NOT_REQUIRED | RETRIEVAL_REQUIRED
  decision_question:
  retrieval_gap:
  retrieval_scope:
  candidate_source_set:
  evidence_extractions:
  normalized_candidate_set:
  excluded_candidates:
  comparison_result:
  selection_boundary_status:
  supported_decision_level:
  dose_support_status:
  planning_handoff:
  persistence_decision:
  confidence:
  unresolved_uncertainty:
  stop_reason:
  provenance:
```

The output must be:

- problem-first;
- evidence-bounded;
- population-, dose-, cost-, risk-, transfer-, Athlete State-, and
  competition-aware;
- explicit about source and inference boundaries;
- precise only to the degree justified;
- retrieval-bounded; and
- consumable without repeating the intervention research.

No field in this contract grants final selection authority.

---

## Interfaces With Planning Workflows

### Create Mesocycle

[Create Mesocycle](./create_mesocycle.md) can invoke this Workflow when Step 5
emits `Candidate Intervention Required` or `External Retrieval May Be
Invoked`.

It can consume:

- intervention families and feasible candidates;
- intended stimulus and expected adaptation;
- transfer hypothesis;
- dose direction and supported bounds;
- cost, risk, applicability, and uncertainty; and
- conditional comparison.

The Mesocycle retains authority over adaptation direction, priority, temporal
organization, and exit conditions.

### Create Week

[Create Week](./create_week.md) can invoke this Workflow when a required
exposure lacks a candidate or when current dose, cost, and constraint support
is insufficient.

It can consume:

- target exposure mapping;
- feasible candidates;
- dose direction and bounds;
- execution and quality requirements;
- cost and recovery implications;
- timing and competition conditions;
- contingency-relevant limits; and
- remaining retrieval or athlete-information need.

The Week retains authority over exposure role, placement, stress organization,
and Session briefs.

### Create Session

[Create Session](./create_session.md) can consume
`SESSION_INTERVENTION_HANDOFF` as input to candidate selection, intended
stimulus, executable dose, quality criteria, stop conditions, monitoring, and
unresolved uncertainty.

It must still confirm current Athlete State, hard constraints, entry
conditions, Session role, and final prescription. Execution creates a separate
Actual Exposure record.

When the handoff is blocked, Create Session must not infer missing dose or rest
precision. It may return for athlete information, qualified assessment, or a
better-bounded candidate.

### Interface Review

The three planning Workflows contain compatible conceptual fields and already
emit retrieval need signals. A named invocation and return contract is not yet
declared in those files.

Record:

`WORKFLOW_INTERFACE_GAP`

- `create_mesocycle.md`, `create_week.md`, and `create_session.md` do not name
  `research_intervention.md` as the implementation behind their future
  external-retrieval interface;
- they do not declare `SESSION_INTERVENTION_HANDOFF` or
  `SESSION_INTERVENTION_HANDOFF_BLOCKED` as typed inputs; and
- they do not explicitly preserve retrieval status, source provenance, and
  dose-support status in their handoffs.

This gap does not prevent conceptual consumption: the current output fields
map to existing candidate, dose, cost, risk, quality, stop, monitoring, and
uncertainty fields. Future interface revision should add named routing without
changing planning authority.

### Schema Review Candidate

Record:

`SCHEMA_CANDIDATE`

The Candidate Intervention Output Contract is likely to recur across
Mesocycle, Week, Session, evidence retrieval, and audit traces. A future
`schemas/intervention_candidate.md` may improve validation, versioning, and
cross-Workflow compatibility if repeated use confirms the need. This Workflow
defines the contract locally and does not create a schema in this revision.

---

## Runtime Notes

- Read only the source sections needed to close the defined retrieval gap.
- Prefer a compact extraction table or structured record over long narrative
  source summaries.
- Preserve one traceable source reference for every material claim.
- Separate source fact, interpretation, and planning implication.
- Deduplicate sources and candidates before comparison.
- Use progressive retrieval rounds with an explicit unresolved question.
- Do not load a complete training-method literature when one bounded protocol
  question controls the decision.
- Do not repeat Core Model, Domain, Theory, Evidence, or comparison content;
  link to its authority and record only the current application.
- If source access is incomplete, state the access limit and lower the
  supported inference.
- Keep live retrieval task-local unless Step 12 returns
  `PERSISTENCE_CANDIDATE`.

### Dry-Run-Type Boundary Case

When the system knows that a high-velocity exposure direction is relevant but
recent exposure is limited, current tolerance is uncertain, direct recent
capacity measurement is absent, and no executable dose is justified, the
Workflow may:

```text
retrieve candidate approaches
→ identify a conservative feasible candidate structure
→ preserve dose uncertainty
→ identify Session-day tissue and preparation information needs
→ hand off a bounded candidate to Create Session
```

It must not convert prior familiarity or a traditional task label into a fixed
prescription. This is a boundary example, not a default rule.

---

## Workflow Completion Gate

The Workflow is complete only when:

- the decision question and changeable decision are explicit;
- retrieval necessity has been tested;
- vocabulary is controlled and not confirmation-only;
- material sources have been extracted with population, protocol, outcome,
  limitation, and freshness context;
- every retained candidate satisfies the Candidate Intervention Output
  Contract to the precision supported;
- applicability, transfer, dose, cost, risk, and uncertainty are visible;
- hard-constraint failures are excluded;
- comparison is conditional and preserves trade-offs;
- sufficiency and a Stop Rule are recorded;
- the correct planning handoff or blocked handoff is emitted;
- persistence is a recommendation rather than an automatic write; and
- no downstream planning authority has been assumed.

---

## Workflow Invariants

1. Retrieval begins with a decision gap, not with an exercise label.
2. Existing sufficient knowledge ends retrieval before external search.
3. Search vocabulary includes contradictory and boundary terms.
4. Search results require source inspection and structured extraction.
5. Population and protocol relevance are separate from source quality.
6. An intervention family may be supportable while its executable dose is not.
7. Dose precision, rest precision, and stop conditions cannot exceed source
   support.
8. Expected benefit is represented with cost, risk, opportunity cost, and
   uncertainty.
9. Transfer to competitive 100m performance remains an explicit hypothesis.
10. Candidate preference is conditional on current athlete, constraints,
    priority, competition context, and time.
11. Candidate comparison does not create a universal method ranking.
12. Planning Workflows retain final selection and prescription authority.
13. Retrieval stops when additional information has low decision value.
14. Live evidence does not automatically become persistent project knowledge.
15. New evidence may create a review candidate but cannot silently rewrite
    Theory, Domain, Rules, Core Models, or the Constitution.
16. Missing evidence, missing athlete information, and need for external
    assessment remain distinct outputs.
