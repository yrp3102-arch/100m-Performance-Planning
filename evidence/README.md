# Evidence Layer

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

The Evidence layer records what current information supports, challenges,
bounds, or leaves unresolved about a decision, Theory claim, intervention, or
planning relationship.

Evidence answers:

> What does current information permit the system to believe, and with what
> limits?

Evidence may:

- support a claim;
- challenge a claim;
- narrow its applicable conditions;
- identify an exception;
- change confidence;
- expose missing information;
- or leave the issue unresolved.

Evidence is not selected only to confirm the current project framework.

The required persistent format is defined in
[Evidence Record Schema](./evidence_record_schema.md).

---

## Evidence Is Not Theory

Evidence describes support and limits.

Theory supplies a candidate explanatory or organizational prior.

Neither object independently determines what to do.

The decision relationship is:

Decision Question

→ Current Context and Athlete State

→ Candidate Evidence

→ Core-Model Interpretation

→ Rules and Constraints

→ Decision.

An association does not automatically establish a trainable cause.

A supporting adaptation does not automatically establish transfer to
competitive 100m performance.

A favorable athlete response does not automatically become universal evidence.

A single unfavorable outcome does not automatically falsify a theory or
intervention.

---

## Evidence Sources

Potential sources include:

- systematic reviews;
- meta-analyses;
- randomized or controlled intervention studies;
- longitudinal studies;
- observational studies;
- biomechanical studies;
- measurement and reliability studies;
- case studies;
- high-quality coaching practice;
- athlete case evidence;
- project case history;
- competition and training records;
- and structured expert reasoning.

Source type alone does not establish decision value.

Evidence evaluation must distinguish:

- internal validity;
- measurement validity;
- population and task applicability;
- ecological relevance;
- outcome directness;
- protocol comparability;
- temporal relevance;
- and practical decision consequence.

Evidence quality and practical relevance are separate dimensions.

A controlled study may have strong internal validity and weak applicability to
a trained 100m athlete.

A coaching case may have strong contextual relevance and weak causal control.

Both limits should remain visible.

---

## Evidence Roles

Each Evidence Record should state its role relative to a named claim:

| Role | Meaning |
|---|---|
| Supports | Increases support for the claim within stated conditions |
| Challenges | Provides material evidence against the claim or its current scope |
| Bounds | Defines limits, population differences, dose conditions, or exceptions |
| Unresolved | Is relevant but cannot determine the direction or distinguish explanations |

One record may have different roles for different claims.

For example, evidence can support improvement in a proxy while bounding claims
about race transfer.

Do not collapse conflicting roles into a single evidence score.

---

## Live Retrieval

The Evidence layer supports future live evidence retrieval.

The intended flow is:

Decision Question

→ Domain Vocabulary

→ Live Retrieval

→ Candidate Evidence

→ Population, Protocol, Exposure, Outcome, and Context Extraction

→ Relevance and Uncertainty Evaluation

→ Decision Use

→ Optional Persistence.

Future `workflows/research_intervention.md` may implement this sequence.

This task does not create that Workflow.

Live results enter the Hot Layer.

They may immediately inform a bounded current decision when source, context,
quality, and uncertainty are explicit.

They do not automatically modify Theory, Domain, Rules, Core Models, or the
Constitution.

---

## Persistence Policy

Not every search result should be stored.

Persistence is more valuable when evidence is:

- repeatedly useful;
- decision-relevant across cases;
- high-value or high-consequence;
- difficult to rediscover;
- theory-updating;
- important for a recurring disagreement;
- or frequently referenced by project decisions.

Before persistence, remove duplicates and preserve the original source.

Do not persist a claim without enough protocol, population, outcome, and
limitation context to interpret it later.

An Evidence Record is a structured representation of a source.

It is not a substitute for the source when precise verification is required.

---

## Contradictory Evidence

The Evidence layer must preserve evidence that:

- supports the current Theory;
- contradicts it;
- narrows it;
- identifies exceptions;
- or leaves it unresolved.

Search and persistence should not become confirmation-only processes.

When evidence conflicts, preserve differences in:

- population;
- training status;
- intervention and Actual Exposure;
- dose and duration;
- comparator;
- outcome definition;
- measurement protocol;
- context;
- analysis;
- and uncertainty.

Conflicting findings should not be mechanically averaged when they concern
different constructs or conditions.

The conflict may produce a Theory revision, a narrower condition, an
Exploratory decision, or `Cannot Determine`.

---

## Freshness

Every persistent record should contain:

- publication date or year;
- retrieval date;
- last-reviewed date;
- source version where relevant;
- and freshness notes for claims likely to change.

Older evidence is not automatically invalid.

Recent evidence is not automatically superior.

Freshness determines when rechecking may be needed; it does not replace quality
or applicability assessment.

Live retrieval should verify claims whose current status materially affects the
decision.

---

## Evidence and Athlete Response

Published or external evidence informs a prior about likely relationships.

Actual Exposure and athlete response update the contextual belief.

Athlete-specific evidence should retain:

- exposure fidelity;
- observation and measurement conditions;
- Expected versus Observed Response;
- repeated-trend status;
- competing explanations;
- and confidence.

Repeated individual response can justify a strong athlete-specific decision
without proving universal causality.

Group evidence can remain relevant without overriding a clear athlete-specific
constraint or response pattern.

---

## Knowledge Temperature and Review

Live Evidence, retrieval results, and current Athlete Data are Hot Layer
objects.

Persistent Evidence Records become reviewable project knowledge but retain
their date, scope, and uncertainty.

Theory, Domain, and Rules are Warm Layer objects.

Constitution and Core Models are Cold Layer objects.

Hot evidence may trigger a `REVIEW CANDIDATE` when it repeatedly or materially
challenges a Warm or Cold Layer claim.

It must not silently rewrite those layers.

---

## Evidence Boundaries

Evidence files must not become:

- training prescriptions;
- universal dose rules;
- decontextualized paper summaries;
- citation lists without decision relevance;
- author-reputation rankings;
- or repositories that retain only supportive findings.

Evidence informs decisions through Core Models, Rules, current context, and
Workflows.

Constitution ≠ Theory ≠ Evidence ≠ Domain.
