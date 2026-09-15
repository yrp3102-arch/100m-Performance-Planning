# Evidence Record Schema

Version: 0.1
Status: Draft
Date: 2026-09-15
## Purpose
This schema defines the minimum structured representation for evidence that is
persisted in the project.

It supports scientific sources, coaching-practice records, athlete cases, and
project cases while preserving their different strengths and limitations.

It does not rank all evidence through one universal score or convert an
Evidence Record directly into a training prescription.

Use this schema only when persistence is justified by the
[Evidence Layer](./README.md).

## Record Header
```yaml
record_id:
schema_version: 0.1
record_status: draft | reviewed | superseded | deprecated
created_date:
last_reviewed:
review_owner:
```
`record_id` should be stable across updates.

`record_status` describes record governance, not evidence strength.

## Identification
```yaml
identification:
  title:
  source_name:
  authors_or_originator:
  publication_year:
  publication_date:
  source_version:
  url:
  doi_or_persistent_id:
  retrieval_date:
  last_verified:
  language:
```
For coaching practice or project cases, identify the originator, context,
record date, and whether the account is primary or second-hand.

Do not infer missing bibliographic fields.

## Evidence Type
```yaml
evidence_type:
  primary_type:
  secondary_tags: []
  peer_reviewed: true | false | unknown
  prospective_or_retrospective:
  controlled_or_uncontrolled:
```
Permitted `primary_type` values may include:

- systematic review;
- meta-analysis;
- intervention study;
- longitudinal study;
- observational study;
- biomechanical study;
- measurement study;
- case study;
- coaching practice;
- athlete case;
- project case;
- consensus or position statement;
- and other, with explanation.

Evidence type is descriptive.

It does not independently determine quality, relevance, or decision authority.

## Decision Question and Claim Link
```yaml
decision_link:
  decision_question:
  performance_problem:
  candidate_bottleneck:
  intervention_or_exposure:
  theory_claim_ids: []
  rule_or_model_links: []
  intended_decision_use:
```
The record should state why the evidence was retrieved or persisted.

If no decision, Theory, Rule, or model relationship can be stated, persistence
value may be low.

## Population
```yaml
population:
  age:
  sex:
  training_status:
  training_age:
  sprint_level:
  event_or_sport:
  sample_size:
  inclusion_criteria:
  exclusion_criteria:
  relevant_baseline_characteristics:
  injury_or_rehabilitation_context:
```
Training status should distinguish, where possible:

- untrained or recreational;
- generally trained;
- sprint-trained;
- competitive sprinter;
- elite or international sprinter;
- youth or developing athlete;
- and mixed or unclear population.

Do not infer applicability to trained adult or near-adult 100m athletes from
age or athletic status alone.

## Intervention or Exposure
```yaml
intervention_exposure:
  canonical_domain_term:
  task_or_method_label:
  intended_stimulus:
  actual_exposure_description:
  duration:
  dose_dimensions:
  intensity_or_quality:
  frequency_and_distribution:
  rest_and_density:
  execution_conditions:
  environment_and_equipment:
  cointerventions:
  comparator:
  adherence_or_exposure_fidelity:
```
Exercise or method label does not equal Training Stimulus.

Record actual exposure detail when the source provides it.

If exposure fidelity is missing, do not assume the prescribed intervention was
delivered as intended.

## Outcomes
```yaml
outcomes:
  terminal_100m_outcomes: []
  race_or_segment_outcomes: []
  sprint_test_outcomes: []
  mechanical_outcomes: []
  technical_outcomes: []
  strength_power_jump_proxies: []
  internal_response_outcomes: []
  tissue_adverse_recovery_outcomes: []
  competition_expression_outcomes: []
  measurement_protocols: []
  observation_windows: []
```
Keep terminal outcome, component outcome, determinant, capacity, indicator, and
proxy roles separate.

For each material outcome, record where possible:

- definition;
- unit;
- measurement protocol;
- comparison;
- direction and magnitude;
- uncertainty or interval;
- missingness;
- and practical interpretation boundary.

Proxy improvement does not establish 100m performance improvement.

## Main Finding
```yaml
main_finding:
  high_density_summary:
  result_direction:
  effect_or_pattern:
  statistical_context:
  practical_context:
  adverse_or_null_findings:
  author_conclusion:
  record_interpretation:
```
Separate the source's conclusion from the project's interpretation.

Do not infer superiority from the presence of significance in one group and
absence of significance in another without a valid between-group comparison.

Preserve null, adverse, and ambiguous findings.

## Relevance to 100m Planning
```yaml
relevance_to_100m:
  target_performance_layer:
  determinant_or_capacity:
  planning_problem:
  intervention_family:
  stimulus_dose_cost_relation:
  transfer_path:
  decision_scope:
  possible_planning_implication:
  non_supported_inference:
```
`possible_planning_implication` describes how evidence may inform a decision.

It must not be written as an automatic prescription.

`non_supported_inference` should state tempting conclusions that the record
does not justify.

## External Validity
```yaml
external_validity:
  target_population_match:
  event_specificity:
  training_status_match:
  sex_and_age_applicability:
  protocol_match:
  dose_and_context_match:
  competition_relevance:
  ecological_relevance:
  applicability_summary:
```
Use qualitative applicability such as:

- High;
- Moderate;
- Limited;
- Indirect;
- Unknown;
- or Mixed.

High internal validity does not guarantee high external validity.

Athlete-specific relevance must remain separate from general source quality.

## Quality and Limitations
```yaml
quality_limitations:
  design_strengths: []
  design_limitations: []
  measurement_limitations: []
  exposure_reporting_limits: []
  confounding: []
  sample_and_power_limits: []
  analysis_limits: []
  reporting_limits: []
  conflicts_of_interest:
  replication_status:
  unresolved_questions: []
```
Do not force heterogeneous limitations into one numeric quality score.

State which inference each limitation weakens.

For practice or case evidence, preserve selection bias, attribution limits,
concurrent changes, and reporting uncertainty.

## Supporting or Contradictory Role
```yaml
claim_roles:
  - claim_id:
    role: Supports | Challenges | Bounds | Unresolved
    scope:
    rationale:
    conditions:
    contradictory_elements:
```
One Evidence Record may support one claim and challenge or bound another.

Do not assign a global `supportive` label that hides claim-specific conflict.

Contradictory evidence must remain discoverable.

## Confidence
```yaml
confidence:
  evidence_quality: Strong | Moderate | Limited | Weak | Mixed | Cannot Determine
  contextual_applicability: High | Moderate | Limited | Indirect | Unknown | Mixed
  decision_confidence_effect: Strengthens | Weakens | Narrows | No Material Change | Unresolved
  confidence_rationale:
  major_uncertainty: []
```
Confidence is qualitative and claim-specific.

Do not create unsupported probabilities or collapse quality and applicability
into one score.

## Decision Use
```yaml
decision_use:
  decisions_informed: []
  planning_level:
  conditions_required:
  constraints_or_risks:
  alternatives_affected: []
  monitoring_or_information_need:
  current_use: use | do_not_use | use_with_limits | unresolved
  rationale:
```
Evidence may alter:

- interpretation;
- Theory confidence;
- Candidate Bottleneck confidence;
- intervention comparison;
- dose or cost assumptions;
- transfer confidence;
- monitoring value;
- or a planning decision.

It does not bypass Core Models, Rules, constraints, or Athlete State.

## Freshness and Persistence
```yaml
freshness_persistence:
  publication_date:
  retrieval_date:
  last_reviewed:
  next_review_reason:
  likely_to_change: true | false | unknown
  persistence_reason:
  supersedes_record_ids: []
  superseded_by_record_ids: []
  source_access_notes:
```
Persistence reasons may include:

- repeated usefulness;
- high decision value;
- difficult rediscovery;
- Theory update relevance;
- recurring conflict;
- or frequent project reference.

Freshness does not substitute for validity or applicability.

## Review Candidate Interface
When evidence materially challenges a Warm or Cold Layer claim, attach:
```yaml
review_candidate:
  required: true | false
  challenged_layer:
  challenged_object:
  challenged_claim:
  reason:
  supporting_records: []
  contradictory_records: []
  affected_interfaces: []
  proposed_review_scope:
  urgency:
  uncertainty:
```
The record may create a `REVIEW CANDIDATE`.

It must not automatically rewrite Theory, Domain, Rules, Core Models, or the
Constitution.

## Minimum Completeness Gate
An Evidence Record is persistable when it contains enough information to
identify:

- the source;
- evidence type;
- decision question or claim relationship;
- population or practice context;
- intervention or exposure where relevant;
- outcome and measurement role;
- main finding;
- external-validity limits;
- material limitations;
- Supports, Challenges, Bounds, or Unresolved role;
- qualitative confidence;
- decision use;
- retrieval and review dates;
- and unresolved uncertainty.

If the source cannot support these fields, retain a retrieval note or reject
persistence rather than manufacturing context.

The precision of the record must not exceed the precision of the source.
