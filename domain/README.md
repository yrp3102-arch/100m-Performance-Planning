# Domain Layer

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

The Domain layer defines what concepts exist in 100m training discourse and
how those concepts can be named, related, interpreted, and retrieved.

It provides:

- canonical terminology;
- concept categories;
- aliases and ambiguous usages;
- relationships among domain objects;
- English retrieval vocabulary;
- and context needed to interpret search results or user language.

The Domain layer answers:

> What are we talking about, and how should we search for it?

It does not decide what should be trained.

It does not prescribe dose, select an intervention, rank evidence, validate a
theory, or generate a plan.

The current domain ontology is defined in
[100m Training Domain](./100m_domain.md).

---

## What Belongs Here

Domain files may define:

- sprint race and phase terminology;
- performance and competition terminology;
- intervention families;
- strength and power categories;
- plyometric and stretch-shortening-cycle terminology;
- speed-endurance terminology;
- technical and coordination concepts;
- monitoring and testing vocabulary;
- common abbreviations and aliases;
- and search terms used by future retrieval workflows.

A Domain entry should clarify, where useful:

- `canonical_term`;
- `concept_class`;
- `definition_or_scope`;
- `common_aliases`;
- `related_terms`;
- `common_ambiguities`;
- `retrieval_terms`;
- and `model_interface`.

Domain entries should remain lightweight.

They identify categories and language rather than attempting to contain all
available coaching or scientific knowledge about the category.

---

## What Does Not Belong Here

The Domain layer must not become:

- a giant exercise database;
- a training-method ranking;
- a fixed training menu;
- a universal dose table;
- a weekly template;
- a progression rulebook;
- a theory-validation system;
- an evidence hierarchy;
- or a repository of unreviewed web claims.

An intervention name does not establish its stimulus, dose, cost, transfer, or
conditional value.

Those relationships belong to the
[Stimulus-Dose-Cost Core Model](../core_models/03_stimulus_dose_cost_model.md),
Rules, Evidence, and current planning context.

Race-phase terms describe race structure.

They must not be converted into independent trainable capacities merely
because separate labels exist.

The [100m Performance Core Model](../core_models/02_100m_performance_model.md)
governs those performance relationships.

---

## Domain and Retrieval

Domain terminology supplies controlled language for future live retrieval.

The intended relationship is:

Decision Question

→ Domain Concept

→ Canonical Term and Aliases

→ English Search Vocabulary

→ Candidate Evidence or Intervention.

A user term may map to several English terms, and one English term may have
different meanings across coaching and research sources.

The Domain layer should preserve these mappings rather than forcing a false
one-to-one translation.

Search vocabulary should help future retrieval distinguish:

- performance outcome from proxy;
- intervention label from actual exposure;
- adaptation from test change;
- association from causal intervention evidence;
- and general athletic populations from trained 100m sprinters.

Future `workflows/research_intervention.md` may read Domain terms to form a
search strategy.

This task does not create that Workflow.

---

## Domain Relationships

Domain terms enter the system through the relationship:

Domain Vocabulary

→ Candidate Theory or Search Query

→ Evidence Record

→ Core-Model Interpretation

→ Rule-Governed Decision

→ Workflow.

Domain terminology has no independent decision authority.

A canonical label improves communication and retrieval.

It does not prove that the labeled object is appropriate, effective, or
currently important.

---

## Domain Update Policy

Domain is a Warm Layer.

It may be versioned when:

- terminology changes;
- a stable new intervention family appears;
- a new measurement concept becomes decision-relevant;
- an alias repeatedly causes retrieval error;
- or an existing category proves too broad or misleading.

Core definitions should not change merely because one source uses different
language.

An update should record:

- the term changed;
- the prior and revised scope;
- the reason for change;
- affected aliases and retrieval terms;
- downstream references;
- and review date.

New live evidence can propose a `REVIEW CANDIDATE`.

It must not automatically rewrite Domain definitions or any Cold Layer object.

---

## Layer Boundaries

The [Constitution](../CONSTITUTION.md) defines allowed forms of reasoning.

The [Theory Layer](../theory/README.md) supplies candidate explanatory and
organizational priors.

The [Evidence Layer](../evidence/README.md) records what current information
supports, challenges, bounds, or leaves unresolved.

Core Models define stable system objects and relationships.

Rules define conditions under which decisions are justified.

Workflows define ordered execution.

Domain defines the language these layers use and retrieve.

Constitution ≠ Theory ≠ Evidence ≠ Domain.

When a Domain entry conflicts with a Core Model or Constitution, the Domain
entry must be revised or narrowed.
