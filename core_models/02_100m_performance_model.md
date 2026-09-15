# 100m Performance Core Model

Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose

This document defines the performance object used by the
100m Performance Planning system.
It specifies:

- competitive 100m performance as the terminal criterion,
- the descriptive structure of a 100m race,
- the layers connecting race outcomes to performance determinants,
- the distinction between underlying capacity and competition expression,
- the role and limits of observable indicators,
- athlete-specific performance problems and bottlenecks,
- transfer relationships,
- uncertainty and identifiability,
- model invariants,
- and interfaces with adjacent Core Models.

This document answers:

> What is competitive 100m performance, what structures and determinants
> contribute to it, what can be observed, and how can performance outcomes
> constrain athlete-specific explanations?

It does not define:

- training methods,
- exercise selection,
- training dose,
- weekly organization,
- progression or readiness rules,
- monitoring workflows,
- or competition-preparation prescriptions.

Those functions belong to adjacent models, rules, and workflows.
The governing architecture is:

Constitution
→ Core Model
→ Rule
→ Workflow
→ Output.

This file defines stable objects and relationships at the Core Model layer.

---

## 1. Definition of 100m Performance

Competitive 100m performance is the athlete's realized result in a regulated
100m race under a specified competition context.
Its primary terminal outcome is elapsed race time from the start signal to the
finish, interpreted with the conditions required to establish what result was
actually achieved.
Relevant conditions include:

- legal and procedural status,
- timing method,
- wind,
- surface and lane,
- environmental conditions,
- competition round,
- and other context capable of changing performance or its interpretation.

The terminal result is produced through the athlete's time-varying interaction
with the race task.
It is not reducible to any single supporting capacity, test, or biomechanical
variable.

### 1.1 Core Performance Objects

The model distinguishes the following objects.

| Object | Definition | Logical role |
|---|---|---|
| Competitive 100m Performance | Realized performance in the target race under specified conditions | Terminal criterion |
| Race Outcome | Recorded result and direct race-level characteristics | Direct description of the target task |
| Segment Outcome | Performance over a defined non-overlapping or analytically selected portion of the race | Localization of where time was gained or lost |
| Performance Determinant | A factor that can contribute to race outcomes through one or more plausible paths | Explanatory component |
| Underlying Capacity | A relatively persistent capability or constraint available to support sprinting | Potential contribution, not realized performance |
| Competition Expression | The degree and organization with which available capabilities appear in the race | State-dependent realization |
| Observable Indicator | A measured or judged variable used to inform a claim about another object | Evidence-bearing observation |
| Proxy | An indirect indicator standing in for a target or determinant | Conditional substitute for observation, never for the terminal criterion |
| Diagnostic Variable | An observation selected to distinguish among candidate explanations | Information for inference |
| Performance Problem | A defined discrepancy between observed and relevant expected performance | Object requiring explanation |
| Candidate Bottleneck | A plausible limiting explanation consistent with available observations | Provisional causal hypothesis |
| Transfer Relationship | A proposed path by which change in one object alters sprint expression and race performance | Conditional bridge between adaptation and target |

These objects must not be treated as synonyms.
In particular:

Performance ≠ Capacity
Performance ≠ Indicator
Performance ≠ Proxy
Weak Indicator ≠ Bottleneck
Supporting Adaptation ≠ Transfer
Capacity ≠ Competition Expression.

### 1.2 Scope of the Performance Claim

A statement about performance is incomplete unless its target is clear.
Possible targets include:

- official or otherwise valid 100m race time,
- a standardized 100m trial,
- a race segment,
- a derived velocity characteristic,
- or a supporting test.

Only the first two are direct whole-task outcomes.
A change in a segment or supporting test may explain or predict the terminal
outcome, but it does not replace it.
The strength of a performance claim depends on both:

- the directness of the outcome,
- and the comparability of the conditions under which it was observed.

---

## 2. Terminal Performance Criterion

Competitive 100m performance is the terminal criterion of this system.
Every supporting object has value only through one or more of the following
relationships to the terminal criterion:

- describing it,
- explaining it,
- predicting it,
- constraining it,
- enabling its development,
- preserving it,
- or enabling its expression.

No supporting variable becomes a terminal objective merely because it is easy
to measure, trainable, correlated with sprinting, or common among elite
sprinters.

### 2.1 Terminal Outcome and Supporting Outcomes

The model distinguishes:

Terminal Performance
from
Supporting Outcome.
Examples of supporting outcomes include:

- 10m or 30m time,
- a flying sprint time,
- estimated maximum velocity,
- a velocity or acceleration profile,
- countermovement-jump performance,
- reactive strength index,
- one-repetition maximum,
- bar velocity,
- power output,
- a technical score,
- and an isolated biomechanical variable.

Each may be useful.
None independently establishes improved competitive 100m performance.
Therefore:

Proxy Improvement ≠ 100m Performance Improvement.

The relationship may instead be:

Supporting Outcome Change
→ Evidence about a Determinant or Capacity
→ Possible Change in Sprint Expression
→ Possible Change in Race Performance.

Every arrow is conditional.

### 2.2 Directness Does Not Eliminate Measurement Conditions

A 100m result is the most direct outcome, but it is still an observation made
under conditions.
A faster recorded time may reflect some combination of:

- changed athlete capability,
- changed competition expression,
- different race execution,
- different environmental assistance or resistance,
- different competition context,
- and measurement variation.

Direct outcomes therefore receive priority without being treated as
context-free truth.

### 2.3 Segment Improvement and Whole-Race Performance

Segment outcomes are direct components of the race when segments are
non-overlapping and measured consistently.
Their sum can account for total race time.
Their interpretation remains relational.
A gain in one segment may:

- carry forward into later segments,
- be offset by a loss elsewhere,
- alter the conditions under which a later segment is entered,
- or reflect a different distribution of effort and execution.

Segment improvement is therefore evidence about the race, but it is not always
equivalent to whole-race improvement.

---

## 3. Race Performance Structure

The 100m can be represented through time, distance, velocity, acceleration,
and changes in movement organization across the race.
Race phases are descriptive structures imposed on a continuous performance.
They support communication and localization.
They are not automatically separate biological capacities, independent
training targets, or fixed distance zones.
The boundaries between phases may vary with:

- athlete characteristics,
- performance level,
- race execution,
- measurement method,
- and the analytic question.

Determinants can operate across several phases.
The same determinant can have different effects at different velocities and
task states.

### 3.1 Start and Block Clearance

This segment describes the interval from the start signal through initial
block exit and clearance.
Its direct outcomes may include:

- reaction time,
- block-exit timing,
- early displacement,
- and the initial conditions established for subsequent acceleration.

Reaction and movement execution contribute to the race result through related
but distinguishable processes.
Block clearance is not a self-contained capacity.
It reflects the interaction of start procedure, force application, movement
organization, anthropometric constraints, current state, and task execution.

### 3.2 Early Acceleration

Early acceleration describes the initial rise in running velocity after block
clearance.
Its direct feature is the rate and pattern by which velocity is established
over the selected interval.
It may be influenced by:

- effective impulse under the available contact conditions,
- force orientation,
- posture and step-to-step organization,
- available force-time capability,
- and the entry conditions created by the start.

No fixed distance is universally identical to early acceleration.
Early acceleration performance does not uniquely identify which underlying
factor limits it.

### 3.3 Late Acceleration / Transition

Late acceleration and transition describe the continuing increase in velocity
as posture, contact behavior, and step organization evolve toward upright
high-speed sprinting.
This structure is continuous with both earlier acceleration and maximum-
velocity running.
It should not be modeled as a sharply bounded capacity.
Performance in this region depends partly on:

- the velocity and organization carried into it,
- the ability to continue producing useful net acceleration as contact times
  shorten,
- and the coordination of changing task demands.

A problem observed here may originate earlier, emerge locally, or reflect a
constraint that also affects later high-speed running.

### 3.4 Maximum Velocity

Maximum velocity describes the highest velocity reached in the race or in a
defined sprint task.
It is a direct characteristic of the velocity profile.
It is not a single underlying capacity.
Its expression depends on interacting mechanical, neuromuscular, technical,
tissue, energetic, and state-related factors under very short contact times.
A flying split provides an interval-average performance under its specific
run-in and timing conditions.
It does not automatically equal instantaneous maximum velocity.

### 3.5 Speed Maintenance / Deceleration

This segment describes what happens after high velocity has been reached,
including the extent and timing of any decline.
Useful descriptions may include:

- absolute late-race velocity,
- absolute segment time,
- change from peak velocity,
- and the shape of the late-race velocity decline.

Relative deceleration must not be interpreted without entry velocity and
absolute performance.
A small percentage loss can coexist with a low peak velocity.
A larger percentage loss can coexist with a faster finish.
Late-race performance may reflect:

- the velocity brought into the segment,
- earlier race execution,
- fatigue-related loss of output,
- changing coordination under fatigue,
- energetic constraints,
- and tissue or protective limitations.

Speed maintenance in one 100m effort is distinct from the ability to repeat
multiple short sprints with limited recovery.

### 3.6 Segment Continuity

The race is a continuous task.
Segment labels partition its description, not the athlete.
Accordingly:

- a determinant may affect multiple segments,
- an earlier change can alter the initial conditions of a later segment,
- compensation in one segment can mask limitation in another,
- and the same segment outcome can arise from different internal solutions.

No segment should be assigned an independent capacity merely because it has a
name.

---

## 4. Performance Determinant Layers

The model uses layers to prevent observations at different logical levels from
being treated as interchangeable.
The principal structure is:

Terminal Outcome
↓
Race / Segment Outcomes
↓
Performance Determinants
↓
Underlying Capacities / Constraints
↓
Observable Indicators.
The downward direction represents decomposition of the explanatory problem.
It is not a guaranteed causal chain.
Observation usually enters from the bottom or from race outcomes and supports
inference upward and downward with uncertainty.

### 4.1 Race Outcome Variables

Race outcome variables describe what occurred in the target task.
They include:

- total race time,
- reaction time where available,
- non-overlapping segment times,
- velocity over time or distance,
- acceleration over time or distance,
- maximum observed or estimated velocity,
- location and magnitude of velocity change,
- and race validity and context fields.

Total time is terminal.
The other variables describe the structure producing that total.
Derived profiles depend on measurement resolution, processing assumptions, and
protocol.
They should not be granted more certainty than the source data support.

### 4.2 Mechanical Determinants

Mechanical determinants describe how motion is produced under the constraints
of the sprint task.
Relevant constructs may include:

- force application,
- impulse,
- force orientation,
- braking and propulsive components,
- contact and flight behavior,
- force-time characteristics,
- velocity,
- acceleration,
- and the changing time available to apply force.

These constructs are coupled.
For example, a shorter contact time is not inherently superior if useful
impulse falls by more than the time reduction benefits performance.
Likewise, step length and step frequency jointly describe speed under
consistent definitions.
They are outcomes of the athlete-task interaction, not independent controls
that can be maximized separately.
No single mechanical metric is a universal master determinant.
The relevance of a mechanical variable depends on:

- the phase and velocity at which it is expressed,
- its direction and timing,
- the athlete's organization,
- the measurement method,
- and its relationship to the observed performance problem.

### 4.3 Neuromuscular and Physical Capacities

Neuromuscular and physical capacities provide resources and constraints that
may support sprint performance.
They may include:

- available force capacity,
- rapid force-expression capability,
- force capacity at relevant muscle lengths and joint configurations,
- power in defined tasks,
- stretch-shortening-cycle capability,
- muscle-tendon function,
- range of motion required by the task,
- and general work capacity relevant to training availability.

These capacities are task-dependent constructs.
Strength measured in one exercise is capacity for that exercise under that
protocol.
Power measured in a jump, barbell task, or modeled sprint profile represents
different objects.
Supporting capacity can enlarge the solution space available to the athlete.
It does not determine which solution will be used or whether it will improve
race performance.

### 4.4 Technical Organization

Technical organization is the athlete's coordination of movement and force
application to solve the sprint task under current constraints.
Technique is therefore relational.
It emerges from interaction among:

- task objective,
- race phase and velocity,
- athlete morphology,
- available capacities,
- learned coordination,
- fatigue and tissue state,
- and environmental constraints.

Technical quality cannot be defined by a universal pose, foot path, step
frequency, or single visual feature.
An observed movement feature can be:

- functional for the current athlete,
- compensatory but effective,
- compensatory and costly,
- a consequence rather than a cause of low velocity,
- or measurement artifact.

Technical analysis must therefore preserve the difference between movement
description and performance explanation.

### 4.5 Energetic and Fatigue Constraints

Energetic processes support the full race concurrently, with changing relative
contributions.
They must not be modeled as systems that switch on at fixed seconds.
Fatigue is a state-dependent constraint on performance expression.
It may appear through changes in:

- available output,
- force-time expression,
- coordination,
- perception and effort regulation,
- and the ability to preserve velocity late in the race.

Observed late-race decline does not uniquely identify an energetic limitation.
It may also reflect entry velocity, earlier execution, technical disruption,
or tissue-related inhibition.
Similarly, temporary suppression of a sprint test may reflect residual fatigue
rather than loss of underlying capacity.

### 4.6 Tissue and Robustness Constraints

Tissue and robustness constraints describe whether the athlete can express and
repeatedly expose performance-relevant capabilities under current demands.
Relevant objects include:

- current local tissue state,
- tolerance of task-specific loading,
- history of exposure and interruption,
- and the availability to train and compete consistently.

Tissue state can constrain:

- output,
- willingness or ability to apply force,
- movement organization,
- exposure tolerance,
- and training availability.

Robustness is not equivalent to the absence of reported pain.
It is also not a medical diagnosis or clearance decision.
This model identifies tissue state as a performance constraint while leaving
medical diagnosis, treatment, and return-to-sport authority outside its scope.

### 4.7 Morphological, Historical, and Contextual Constraints

Some constraints change slowly or are not direct training targets.
They include:

- anthropometry and segment proportions,
- training age and learned history,
- prior exposure and interruption,
- age and maturation where relevant,
- competition experience,
- and stable environmental or resource constraints.

These factors shape how determinants operate and which solutions are available.
They do not define a universal ideal athlete profile.
Population associations involving elite performers must not be converted into
causal requirements for an individual athlete.

### 4.8 Layer Boundaries

The same label may refer to different objects unless its layer is stated.
For example:

- sprint force is a task-level mechanical variable,
- squat force is an exercise-specific capacity indicator,
- modeled force is an estimate conditional on model assumptions,
- and perceived forcefulness is a subjective observation.

The model requires the construct, task, protocol, and layer to remain explicit.
This prevents a measurement from silently becoming a determinant and a
determinant from silently becoming a training prescription.

---

## 5. Determinant Interactions

100m performance is an emergent result of interacting determinants under a
specific athlete state, race task, and context.
It is not a static sum of independent qualities.
A conceptual relationship is:

\[
P = f(S, R, D, I, E, C)
\]

where:

- \(P\) is competitive 100m performance,
- \(S\) is athlete state,
- \(R\) is race demand and execution,
- \(D\) is the set of performance determinants,
- \(I\) is interaction among determinants,
- \(E\) is competition expression,
- and \(C\) is context.

This is a relationship model.
It is not a fitted equation, scoring formula, or claim that the inputs can be
measured without error.

### 5.1 Interaction

Interaction exists when the effect of one determinant depends on the state of
another determinant or on the task conditions.
Examples at the model level include:

- force capacity whose relevance changes with available contact time,
- technical organization that changes with velocity,
- and late-race expression that depends on both peak velocity and fatigue.

### 5.2 Compensation

Compensation exists when one characteristic partly offsets another limitation.
Compensation can preserve performance while hiding a constraint.
It can also carry a cost that appears only at higher velocity, later in the
race, or under repeated exposure.
The presence of compensation does not prove dysfunction.

### 5.3 Redundancy

Redundancy exists when more than one combination of determinants can produce a
similar outcome.
Two athletes with the same race time may use different mechanical and
technical solutions.
The same athlete may also achieve a similar result through different states of
capacity and expression.
Redundancy limits inference from outcome to cause.

### 5.4 Bottleneck

A bottleneck exists when a constraint materially limits the best performance
currently attainable within the athlete's interacting system.
Its effect depends on the state of other determinants.
Removing one bottleneck may reveal another.
A low variable is not necessarily a bottleneck, and a bottleneck is not
necessarily the lowest standardized test score.

### 5.5 Trade-off

A trade-off exists when improving or emphasizing one expression changes the
conditions for another.
Trade-offs may occur within race execution, among mechanical solutions, or
between current expression and longer-term capacity.
The existence of a trade-off does not specify which option should be chosen.
That comparison belongs to the Plan and Stimulus-Dose-Cost interfaces.

### 5.6 Phase Dependence and Overlap

The contribution of a determinant can change across the race.
This phase dependence does not create independent determinant sets for every
segment.
One underlying capacity can support several segments, and one segment can be
limited by several interacting determinants.
The relationship is many-to-many.

---

## 6. Athlete-Specific Bottleneck Model

A performance bottleneck is an athlete-specific constraint that materially
limits competitive 100m performance under the conditions being modeled.
It is defined relative to:

- the athlete,
- the current performance state,
- the race problem,
- the relevant time horizon,
- and the interactions among determinants.

It is not defined solely by distance from a population norm.

### 6.1 Performance Problem

A Performance Problem is a specified discrepancy requiring explanation.
It contains:

- the outcome of interest,
- the observation conditions,
- the relevant comparison or expectation,
- the magnitude and direction of the discrepancy,
- and the uncertainty of that discrepancy.

Examples of problem form include:

- total race performance below the relevant expectation,
- a reproducible loss concentrated in a race segment,
- failure to express known performance under competition conditions,
- or a mismatch between supporting adaptation and sprint outcome.

The problem statement describes what requires explanation.
It does not contain the explanation itself.

### 6.2 Weakness, Candidate Bottleneck, and Causal Bottleneck

The model distinguishes four states.

| State | Meaning | Permitted claim |
|---|---|---|
| Observed Weakness | A measured variable is low relative to a relevant reference | The variable is low under the observed conditions |
| Candidate Bottleneck | A plausible constraint could explain the performance problem | The explanation deserves comparison with alternatives |
| Provisional Bottleneck | Multiple relevant observations support the constraint, while material alternatives remain | The constraint is the current working explanation |
| Causal Bottleneck | Change in the constraint is credibly linked to change in target performance with competing explanations sufficiently reduced | The constraint materially limited performance under the tested conditions |

An observed weakness can fail to be a bottleneck because it may be:

- irrelevant to the current race problem,
- adequately compensated,
- outside the athlete's effective solution,
- poorly measured,
- a consequence of another limitation,
- or unlikely to transfer if changed.

The system should use causal language only to the degree supported by the
design and observations.

### 6.3 Limiting Constraint

A Limiting Constraint is a broader object than a trainable deficit.
It may be:

- a modifiable capacity,
- current fatigue,
- technical organization,
- tissue tolerance,
- race execution,
- competition context,
- a hard constraint,
- or an unresolved interaction among factors.

A true performance limit is not necessarily trainable within the available
time or authority.
Trainability and time to effect are therefore properties relevant to planning,
not requirements for a constraint to exist.

### 6.4 Bottleneck Relationship

The model supports the following relationship:

Observed Performance
→ Performance Problem
→ Candidate Explanations
→ Candidate or Provisional Bottleneck.

This relationship is abductive rather than deductive.
The same observation may support several explanations.
A bottleneck claim is stronger when it has:

- direct relevance to the observed race problem,
- agreement across appropriately matched observations,
- a plausible mechanism at the required phase and velocity,
- evidence that the variable can change,
- a credible transfer path to race performance,
- consistency with the athlete's history,
- and reduced support for important alternatives.

Cost affects whether a bottleneck is worth addressing now.
It does not determine whether the bottleneck exists.

### 6.5 Bottleneck Representation

A bottleneck object should be representable through:

- `performance_problem`,
- `candidate_constraint`,
- `affected_outcome_or_segment`,
- `proposed_mechanism`,
- `supporting_observations`,
- `conflicting_observations`,
- `alternative_explanations`,
- `athlete_and_context_scope`,
- `trainability_status`,
- `transfer_hypothesis`,
- `confidence`,
- and `unresolved_information`.

This schema records the claim.
It does not specify the workflow for generating, ranking, or updating the claim.

### 6.6 Athlete Dependence

Population-level determinants define candidates, not individual priorities.
A variable associated with faster sprinters may reflect:

- selection,
- training history,
- morphology,
- correlated development,
- a true causal contribution,
- or several of these at once.

The current athlete's bottleneck depends on the relation among present level,
compensation, trainability, transfer potential, time, cost, and uncertainty.
No population correlation alone identifies what the athlete should train.

---

## 7. Observable Indicator and Proxy Model

Observation provides partial access to performance and its determinants.
The core relationship is:

Target
→ Determinant
→ Indicator.

Inference normally travels in the reverse direction:

Indicator
→ Evidence about Determinant
→ Evidence about Target.

Reverse inference is conditional and frequently many-to-many.

### 7.1 Indicator Classes

| Indicator class | Primary object observed | Main value | Main boundary |
|---|---|---|---|
| Race result | Whole-task competitive outcome | Most direct terminal evidence | Context and measurement still affect comparison |
| Segment time | Defined portion of the race or test | Localizes time gain or loss | Does not uniquely identify cause |
| Velocity / acceleration profile | Derived race or sprint structure | Describes how the result developed | Depends on sampling and processing assumptions |
| Sprint test | Performance in a standardized sprint task | Direct evidence for that task and conditional proxy for race components | Task, run-in, start, surface, and timing constrain transfer |
| Jump test | Output in a defined jump task | Indicator of task-specific neuromuscular behavior | Does not identify sprint mechanics or whole-body readiness by itself |
| Strength test | Output in a defined strength task | Indicator of exercise-specific force capacity | Does not establish high-speed force expression or sprint transfer |
| Technical observation | Description or rating of movement organization | Can identify patterns and candidate explanations | Observer, viewpoint, velocity, and model assumptions affect interpretation |
| Subjective information | Athlete-reported state or experience | Accesses fatigue, symptoms, confidence, and context not visible in performance data | Does not uniquely locate mechanism and depends on reporting conditions |

### 7.2 Conditional Validity

Indicator validity is conditional on the claim being made.
An indicator may be highly useful for one question and nearly irrelevant for
another.
Its decision value depends on:

- construct match,
- task match,
- phase and velocity match,
- protocol consistency,
- measurement reliability,
- sensitivity relative to expected change,
- environmental comparability,
- athlete-specific relevance,
- and the cost of obtaining the observation.

Reliability does not establish validity.
Validity for one construct does not establish validity for another.
Sensitivity to fatigue does not identify the source of fatigue.

### 7.3 Common Indicator Boundaries

#### Race and Split Times

Race time directly observes the target outcome when the result is valid.
Split times directly observe defined segment outcomes.
They do not independently reveal whether a change arose from capacity,
execution, fatigue, context, or measurement.

#### Flying Sprint Time

A flying time observes average performance across a defined zone after a
specific run-in.
It can inform high-speed sprint expression.
It does not automatically equal instantaneous maximum velocity, and protocols
with different run-ins or zone locations are not interchangeable.

#### Short Acceleration Time

A 10m or 30m time represents integrated performance under its start and timing
protocol.
It cannot by itself separate reaction, block execution, early acceleration,
late acceleration, or the cause of any limitation.

#### Strength, Jump, and Power Tests

These tests observe performance in their own tasks.
They may indicate supporting capacities when the construct and protocol are
clear.
They do not directly measure competitive sprint performance.

#### Mechanical and Technical Variables

Contact time, step length, step frequency, impulse, force orientation, joint
motion, and visual technical features can describe parts of sprint execution.
No isolated value defines technical quality or a universal optimum.
Its meaning depends on velocity, body dimensions, neighboring variables, and
the performance outcome produced.

#### Subjective Information

Subjective information is an observation, not noise by definition.
It can reveal local symptoms, fatigue, confidence, sleep disruption, or race
context that external measures miss.
It remains partial and should not be converted into a complete athlete-state
estimate without interpretation.

### 7.4 Proxy Distance

Proxy distance describes how many uncertain conceptual links separate an
indicator from the terminal criterion.
In general:

Race Result
→ Segment Outcome
→ Sprint-Task Proxy
→ Supporting-Capacity Proxy
→ General or Remote Proxy.

This ordering describes directness, not automatic usefulness.
A remote proxy may be highly informative for a specific candidate constraint.
A direct race result may be insufficient to identify why performance changed.
The model therefore considers both outcome directness and diagnostic relevance.

---

## 8. Transfer Model

Transfer is the realized contribution of a change outside the terminal race
outcome to improved sprint expression and competitive 100m performance.
Transfer is not established by improvement in the source task alone.
The core transfer chain is:

Underlying Capacity Change
→ Changed Sprint-Relevant Capability
→ Changed Sprint Expression
→ Changed Race / Segment Outcome
→ Changed Competitive 100m Performance.

The chain may be:

- partial,
- athlete-dependent,
- phase-dependent,
- context-dependent,
- delayed,
- masked,
- offset elsewhere in the race,
- or absent.

### 8.1 Transfer Objects

A transfer claim contains:

- a source adaptation,
- the sprint-relevant capability it could change,
- a mechanism connecting that capability to sprint execution,
- the race outcome or segment expected to change,
- the athlete and context for which the claim applies,
- the expected time relation,
- possible masking factors,
- competing explanations,
- and evidence that would support or weaken the claim.

The transfer claim must name the bridge between source and target.
For example:

Strength Increase
→ greater available force under relevant constraints
→ improved force expression in the required sprint task
→ changed velocity profile
→ possible 100m improvement.

The first observation does not guarantee the later outcomes.

### 8.2 Transfer Conditions

Transfer can depend on:

- task specificity,
- velocity and force-time correspondence,
- athlete state,
- current bottleneck structure,
- technical organization,
- tissue tolerance,
- learning and familiarity,
- fatigue and residual cost,
- time available for expression,
- and competition context.

Dose and cost can alter transfer, but their representation belongs to the
Stimulus-Dose-Cost Model.
Feedback can change confidence in a transfer claim, but update rules belong to
the Feedback-Decision Model.

### 8.3 Transfer Failure and Masking

Absence of observed race improvement can be consistent with several states:

- the supporting capacity did not change,
- the capacity changed but was not sprint-relevant,
- the sprint-relevant capability changed but was not integrated into technique,
- the change transferred to one segment but was offset elsewhere,
- residual fatigue concealed expression,
- competition conditions concealed the change,
- the observation was too noisy,
- or insufficient time has passed to interpret the result.

Observed success is also non-unique.
A faster race does not prove that every intended supporting adaptation occurred
or caused the result.

### 8.4 Transfer Evidence

Transfer confidence is strongest when change is observed across the relevant
links with appropriate temporal order and competing explanations reduced.
Association alone supports candidate relevance.
Mechanistic plausibility supports a possible path.
Trainability supports the possibility of changing the source object.
Only target-relevant outcome change supports realized transfer.
These evidence roles must remain separate.

---

## 9. Competition Expression

Underlying capacity is what the athlete may be able to contribute under
relevant conditions.
Competition expression is what the athlete actually organizes and realizes in
the race at a particular time.
The relationship is:

Available Capacities and Constraints
× Current Athlete State
× Technical Organization
× Race Execution
× Competition Context
→ Competition Expression
→ Observed Race Performance.

The multiplication signs indicate interaction.
They do not define a numerical equation.

### 9.1 Expression Modifiers

Competition expression may be altered by:

- current fatigue and freshness,
- local tissue state,
- technical stability at race velocity,
- start and race execution,
- arousal and attention,
- environmental conditions,
- competition rounds and recovery,
- travel and schedule,
- equipment and surface,
- and measurement conditions.

These modifiers can affect the observed outcome without representing a durable
change in underlying capacity.

### 9.2 Capacity Gain Without Performance Gain

An athlete can improve an underlying capacity while competitive performance
remains unchanged or worsens.
Possible explanations include:

- incomplete transfer,
- residual fatigue,
- technical disruption,
- offsetting loss in another determinant,
- poor race execution,
- adverse context,
- or measurement noise.

The capacity gain remains real only for the task in which it was validly
observed.
Its competitive value remains unresolved until the transfer chain is supported.

### 9.3 Performance Gain Without Broad Capacity Gain

Competitive performance can improve through:

- better expression of existing capacity,
- better race execution,
- more favorable conditions,
- reduced fatigue,
- improved technical organization,
- or change in one determinant without broad change elsewhere.

A favorable outcome does not prove that the entire underlying system improved.

### 9.4 Outcome Bias

Outcome bias occurs when the quality of a prior explanation or decision is
judged solely from the final result.
A good result can follow an incorrect model.
A poor result can follow a reasonable model under adverse or noisy conditions.
The performance model therefore separates:

- what was believed,
- what capacities were available,
- what was expressed,
- what context occurred,
- and what result was observed.

---

## 10. Uncertainty and Identifiability

Performance inference is incomplete because observations provide only partial,
noisy access to interacting determinants.
Uncertainty is a model property, not a defect to be hidden by additional
labels or numerical precision.

### 10.1 Sources of Uncertainty

Relevant sources include:

- incomplete information,
- measurement error,
- protocol inconsistency,
- environmental variation,
- biological and behavioral variability,
- multiple plausible explanations,
- confounding,
- compensation,
- interaction among determinants,
- model misspecification,
- population mismatch,
- and delayed or masked transfer.

### 10.2 Identifiability

A determinant is identifiable only to the extent that available observations
can distinguish it from plausible alternatives.
Non-identifiability occurs when different determinant states can produce the
same or sufficiently similar observations.
Examples include:

- the same 30m time arising from different start and acceleration profiles,
- the same late-race split arising from different peak velocities and rates of
  decline,
- the same jump height arising from different movement strategies,
- and the same race time arising from different combinations of capacity,
  fatigue, execution, and environment.
More data do not automatically solve non-identifiability.
The added observation must distinguish among the candidate explanations.

### 10.3 Permitted Inference States

The model permits the following outputs.

| Output | Meaning |
|---|---|
| Cannot Determine Yet | Available information does not support a useful distinction among material explanations |
| Candidate Explanation | A plausible relationship is consistent with some observations but remains weakly constrained |
| Provisional Bottleneck | The current evidence favors one limiting explanation while meaningful uncertainty remains |
| Supported Bottleneck | Converging athlete-specific evidence supports a limiting relationship within stated conditions |
| Contradicted Explanation | Relevant observations materially weaken the proposed relationship |

None of these labels converts an observational claim into a universal causal
law.

### 10.4 Evidence Roles

The model separates four questions.

| Evidence role | Question answered | What it does not establish |
|---|---|---|
| Association | Do the variables vary together in a defined population or athlete record? | Direction, causality, or benefit from intervention |
| Mechanistic Plausibility | Is there a credible path by which the determinant could affect performance? | That the determinant currently limits this athlete |
| Trainability | Can the source capacity or behavior change under relevant conditions? | That its change will transfer to the race |
| Transfer Evidence | Did source change correspond to target-relevant sprint and race change? | Universal effectiveness across athletes and contexts |

Evidence strength and contextual applicability are separate dimensions.
A methodologically strong finding in a mismatched population may be less useful
for a trained adult 100m sprinter than its design quality alone suggests.
Elite-athlete observation may be contextually relevant while providing weak
causal identification.

### 10.5 Population and Athlete Scope

The primary application of this model is the trained adult or near-adult
athlete seeking competitive 100m improvement.
Evidence from youth, beginners, team-sport athletes, other events, or world-
class sprinters can inform candidate relationships.
Its applicability depends on:

- biological and training age,
- competitive level,
- task and outcome match,
- prior exposure,
- sex representation,
- and the difference between the evidence context and the current athlete.

No population label removes the need for athlete-specific interpretation.

### 10.6 Confidence Boundaries

Confidence in a performance explanation must not exceed:

- the reliability of the observations,
- the validity of the indicators for the stated construct,
- the specificity of the evidence to the athlete and task,
- the degree to which alternatives have been reduced,
- and the directness of observed transfer.

Unknown values must remain unknown when they materially affect the claim.
"Cannot determine yet" is a valid and sometimes necessary output.

---

## 11. Performance Model Invariants

The following statements must remain true in every implementation of this
Core Model.

1. Competitive 100m performance is the terminal criterion.

2. A supporting test, proxy, technical variable, or isolated biomechanical
   measure cannot replace the terminal criterion.

3. Race segments describe the time-space structure of a continuous task; their
   labels do not establish independent capacities or universal distance
   boundaries.

4. Race outcomes, determinants, underlying capacities, indicators, and proxies
   occupy different logical layers and must remain distinguishable.

5. Performance emerges from interactions among determinants, athlete state,
   race execution, expression, and context; it is not a simple additive score.

6. No single mechanical, neuromuscular, energetic, technical, or tissue
   variable is a universal master determinant of 100m performance.

7. A population association identifies a candidate relationship; it does not
   establish an athlete-specific, causal, or trainable limitation.

8. An observed weakness is not automatically a performance bottleneck.

9. Bottlenecks are athlete-specific, state-dependent, and potentially
   non-identifiable from available observations.

10. Improvement in an underlying capacity requires an explicit and supported
    transfer path before it is credited as improved sprint performance.

11. Underlying capacity and competition expression are distinct objects; a
    change in one does not guarantee a corresponding change in the other.

12. Technical organization is an athlete-task solution and cannot be reduced
    to a universal movement template or isolated visual position.

13. Indicator validity is conditional on the construct, protocol, athlete,
    context, and decision question.

14. Measurement noise, competing explanations, compensation, and population
    mismatch must remain visible in the confidence assigned to any claim.

15. The model may output `Cannot Determine Yet`, `Candidate Explanation`, or
    `Provisional Bottleneck` without forcing false certainty.

16. This model defines performance relationships; it does not prescribe
    methods, doses, progression, readiness actions, or workflow order.

---

## 12. Model Interfaces

This Core Model supplies the target, explanatory objects, and uncertainty
structure used by adjacent models.
It does not duplicate their operational content.

### Plan Model

[Plan Core Model](./01_plan_model.md) defines how a training plan is
represented and evaluated.
This model supplies the Plan Model with:

- the terminal performance objective,
- race and segment outcomes,
- performance problems,
- candidate bottlenecks,
- transfer claims,
- and the distinction between capacity and competition expression.

The Plan Model determines how these objects constrain plan purpose, priority,
comparison, and reviewability.
This file does not evaluate complete plan quality.

### Stimulus-Dose-Cost Model

[Stimulus-Dose-Cost Model](./03_stimulus_dose_cost_model.md) defines how a
training stimulus is represented through its implementation, dose, expected
adaptation, and cost.
This model supplies 03 with:

- candidate determinants and capacities that may be targeted,
- the race problem to which a change must relate,
- the athlete-specific bottleneck hypothesis,
- and the transfer path requiring support.

03 must define:

- stimulus identity,
- multidimensional dose,
- actual exposure,
- recovery and opportunity cost,
- overlap among demands,
- and the distinction among development, maintenance, minimal, and withdrawn
  resource states.
This file does not specify exercises, sprint distances, volumes, intensities,
sets, repetitions, frequencies, rest intervals, or taper doses.

### Feedback-Decision Model

[Feedback-Decision Model](./04_feedback_decision_model.md) defines how actual
exposure and observed response update estimates of athlete state, determinant
status, transfer, and bottlenecks.
This model supplies 04 with:

- observable classes,
- indicator boundaries,
- uncertainty and identifiability constraints,
- candidate and provisional bottleneck states,
- and the distinction between capacity change and performance expression.

04 must define:

- how observations are combined over time,
- how noise and conflicting signals affect confidence,
- how candidate explanations are updated,
- how actual exposure is separated from prescription,
- and how updated beliefs connect to maintain, progress, reduce, modify,
  withdraw, or transition decisions.
This file does not define readiness thresholds, stop rules, review cadence,
progression criteria, or ordered decision workflows.

### Interface Summary

The cross-model relationship is:

100m Performance Model
→ defines the target, performance problem, determinants, observables,
bottlenecks, transfer, and uncertainty
→ Plan Model represents the strategy directed at that target
→ Stimulus-Dose-Cost Model represents how candidate adaptations are pursued
and what they cost
→ Feedback-Decision Model represents how actual exposure and response revise
the athlete-specific interpretation and future decision.
The boundary must remain:

Model ≠ Rule ≠ Workflow.
