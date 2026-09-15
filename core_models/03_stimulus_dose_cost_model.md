# Stimulus-Dose-Cost Core Model
Version: 0.1
Status: Draft
Date: 2026-09-15

## Purpose
This document defines the representation of a training intervention before it enters the 100m Performance Planning system.
It specifies:

- training intervention objects,
- the distinction between task labels and training stimuli,
- prescribed tasks, intended stimuli, planned exposure, and actual exposure,
- multidimensional dose,
- expected adaptation,
- multidimensional cost,
- benefit-cost relationships,
- athlete-state and temporal dependence,
- interactions among stimuli,
- transfer potential,
- risk and uncertainty,
- model invariants,
- and interfaces with adjacent Core Models.

This document answers:

> Given a target performance problem or determinant, what is a training
> intervention, how should its dose and exposure be represented, what
> adaptation may be expected, what costs and risks may arise, and under what
> conditions is the intervention worth considering?

It defines the grammar of a training intervention.
It does not provide:

- an exercise library,
- a ranking of training methods,
- a sprint, strength, or plyometric menu,
- a weekly schedule,
- universal dose thresholds,
- progression or stop rules,
- readiness decisions,
- or an ordered feedback workflow.

The governing boundary is:

Model ≠ Rule ≠ Workflow.

---
## 1. Definition of a Training Intervention
A Training Intervention is a bounded, purposeful manipulation of training conditions intended to influence a defined performance determinant, underlying capacity, technical organization, competition expression, or constraint.
An intervention is not identified by an exercise name alone.
It is represented by the relationship among:

Target Problem
→ Target Determinant or Capacity
→ Training Task
→ Intended Stimulus
→ Planned Dose and Exposure
→ Expected Adaptation
→ Transfer Potential
→ Cost
→ Risk
→ Uncertainty.

This ordering identifies related objects.
It is not a fixed linear causal chain.
Each relationship can be conditional, reciprocal, delayed, incomplete, or unsupported.

### 1.1 Core Intervention Objects
| Object | Definition | Boundary |
|---|---|---|
| Target Problem | Performance discrepancy the intervention is intended to address | Defined by the Performance Model; not an exercise preference |
| Target Determinant | Candidate determinant, capacity, expression factor, or constraint expected to change | May remain provisional or uncertain |
| Training Intervention | Complete purpose-and-exposure hypothesis connecting a task to an expected target-relevant effect | More than the task label |
| Training Task | Executable activity performed under specified conditions | Describes what is done, not the full stimulus |
| Method Label | Conventional name used to identify a task family | Does not uniquely specify dose, exposure, or effect |
| Prescription | Planned instruction describing intended execution | Does not prove completion or stimulus delivery |
| Planned Exposure | External exposure expected if the prescription is executed as intended | Prospective representation |
| Actual Exposure | External work and conditions actually encountered by the athlete | Empirical execution record |
| Intended Stimulus | Functional demand the intervention is designed to create | Prospective hypothesis |
| Realized Stimulus | Functional demand inferred to have arisen from actual exposure in the current athlete state | Not directly observed in full |
| Internal Response | Immediate or delayed athlete response to exposure | Interpreted by the Feedback-Decision Model |
| Expected Adaptation | Direction and type of persistent change considered plausible after exposure and recovery | Not a guaranteed result |
| Transfer Potential | Plausibility that adaptation can alter target-relevant sprint expression | Distinct from realized transfer |
| Cost | Resource use or adverse burden expected or realized through the intervention | Multidimensional; not equivalent to risk |
| Risk | Possibility and consequence of an adverse result | Requires uncertainty about occurrence or magnitude |
| Uncertainty | Limited knowledge about objects, relationships, measurements, or outcomes | Must remain explicit |

These objects must remain distinguishable.

Task ≠ Stimulus

Prescription ≠ Actual Exposure

Exposure ≠ Internal Response

Expected Adaptation ≠ Guaranteed Adaptation

Transfer Potential ≠ Realized Transfer

Cost ≠ Risk

### 1.2 Exercise Label and Stimulus
An Exercise or Method Label identifies a recognizable task category.
Labels such as a flying sprint, acceleration sprint, squat, bound, sled sprint, or technical drill are useful for communication.
They do not uniquely define the stimulus.
The same label can produce different stimuli when any of the following differ:

- athlete state,
- execution intent,
- achieved velocity or load,
- range and duration,
- volume,
- density and rest,
- fatigue at task entry,
- technical organization,
- temporal placement,
- environment,
- equipment,
- or familiarity.

Conversely, different task labels can create overlapping functional demands.
Therefore:

Exercise / Method Label ≠ Training Stimulus.

Stimulus identity is relational.
It emerges from the implemented task, actual dose, achieved quality, environment, and athlete state.

### 1.3 Intervention Representation
A complete intervention object should be representable through:

- `target_problem`,
- `target_determinant_or_capacity`,
- `task_identity`,
- `intended_stimulus`,
- `planned_dose`,
- `planned_exposure`,
- `execution_constraints`,
- `athlete_state_assumptions`,
- `temporal_context`,
- `environment`,
- `expected_adaptation`,
- `transfer_hypothesis`,
- `cost_profile`,
- `risk_profile`,
- `uncertainty_profile`,
- and `observation_interface`.

These fields define what the planning system must be able to represent.
They do not require every output to display all fields in one table.

### 1.4 Intervention Identity
Two prescriptions with the same task label are different interventions when a material change occurs in their target, dose, execution conditions, athlete state assumptions, temporal context, expected adaptation, or cost profile.
Two differently labeled tasks may be comparable interventions when they pursue the same target through sufficiently similar stimuli and costs.
Intervention identity is therefore established by function and implementation, not naming convention.

---
## 2. Intended Stimulus and Actual Exposure
Training is prescribed prospectively and interpreted retrospectively.
The model separates five objects:

Prescribed Task
→ Intended Stimulus
→ Planned Exposure
→ Actual Exposure
→ Achieved Quality.

The first three express planning intent.
The final two describe execution.
The intended stimulus can only be evaluated against what actually occurred.

### 2.1 Prescribed Task
A Prescribed Task is the instruction given to the athlete.
It may contain:

- task or method,
- execution intent,
- target intensity or velocity,
- distance or duration,
- load,
- repetitions and sets where relevant,
- rest,
- environmental or equipment constraints,
- quality expectations,
- and placement within a larger session or plan.

The prescription defines intended action.
It is not evidence that the task was completed as written.

### 2.2 Intended Stimulus
The Intended Stimulus is the functional demand the prescription is designed to create for the current target and athlete.
It should identify:

- what is expected to be challenged,
- under what task conditions,
- in what direction,
- and through what plausible mechanism.

An intended stimulus is a hypothesis about the intervention.
Its existence on paper does not prove that it occurred.

### 2.3 Planned Exposure
Planned Exposure is the expected external work implied by the prescription.
It translates task instructions into exposure dimensions that can later be compared with execution.
Planned exposure may include target velocity, distance, load, contacts, duration, rest, density, frequency, and environmental conditions where those dimensions define the task.

### 2.4 Actual Exposure
Actual Exposure is what the athlete completed and encountered.
It may differ from planned exposure because of:

- changed execution,
- missed or added work,
- failure to reach target quality,
- altered rest or density,
- equipment or surface differences,
- environmental conditions,
- competition demands,
- or the athlete's state during execution.

The model treats competitions, tests, warm-up work, and unplanned additions as exposures when they contribute materially to the same demand or cost profile.

### 2.5 Achieved Quality
Achieved Quality describes the extent to which actual execution expressed the properties required by the intended stimulus.
Quality can include:

- achieved velocity or output,
- technical stability,
- range or task fidelity,
- timing and force-expression characteristics,
- consistency across repetitions,
- and maintenance of the intended task identity.

Quality is task-specific.
It cannot be reduced to effort, completion, or athlete motivation.
A high-effort performance can fail to create the intended high-velocity or high-quality exposure.

### 2.6 Exposure and Stimulus Relationship
Actual exposure provides the basis for inferring realized stimulus.
The relationship is:

Actual Task Conditions
× Actual Dose
× Achieved Quality
× Athlete State
× Environment
→ Realized Stimulus.

This is a conceptual relationship, not a directly calculable function.
The realized stimulus may remain partly unobservable.

### 2.7 Internal Response Boundary
External exposure and internal response are separate objects.
External Dose describes what was imposed and completed.
Internal Response describes what occurred within or was experienced by the athlete following that exposure.
The same external exposure can produce different responses across athletes or within the same athlete at different times.
03 defines this boundary and passes actual exposure to the Feedback-Decision Model.
It does not define how a response triggers maintenance, progression, reduction, modification, withdrawal, or transition.

---
## 3. Dose Model
Dose is the multidimensional specification of the amount, magnitude, quality, and temporal distribution of an exposure.
Dose is not a single universal quantity.
Its relevant dimensions depend on the task and intended stimulus.

### 3.1 Dose as a Multidimensional Object
A general dose representation is:

\[
D = \{M, I, V, R, T, \rho, P, F, W, Q, E\}
\]

where the dimensions may represent:

- \(M\): task mode and magnitude,
- \(I\): intensity relative to an explicit reference,
- \(V\): volume or amount,
- \(R\): repetitions, contacts, or discrete exposures,
- \(T\): duration or distance structure,
- \(\rho\): density and recovery intervals,
- \(P\): placement and sequence,
- \(F\): frequency and distribution,
- \(W\): external load or resistance where relevant,
- \(Q\): execution quality,
- and \(E\): environment and equipment.

This vector is a conceptual grammar.
It does not require every task to use every dimension.
No arithmetic operation on these symbols produces a universal training-load score.

### 3.2 External Dose
External Dose describes the observable work performed or imposed.
Depending on the task, it may include:

- distance,
- duration,
- achieved velocity,
- relative intensity,
- external load,
- repetitions,
- sets,
- contacts,
- work and rest intervals,
- movement range,
- surface or slope,
- and task-specific constraints.

External dose should distinguish planned values from actual values.
It should also identify the reference behind relative terms.
An intensity described as a percentage is uninterpretable unless the reference, task, protocol, and timing of that reference are known.

### 3.3 Dose Quality
Dose Quality describes whether the exposure retained the properties required to create the intended stimulus.
Relevant quality dimensions may include:

- actual rather than intended velocity,
- output stability,
- technical organization under the task constraint,
- task range and direction,
- consistency,
- and whether fatigue changed the nature of later repetitions.

Quality can change stimulus identity.
Additional work performed below the required task condition is not necessarily more of the same stimulus.
It may become a different exposure with a different adaptation and cost profile.

### 3.4 Frequency and Distribution
Dose has both event magnitude and temporal distribution.
The same total amount distributed differently can produce different:

- execution quality,
- acute fatigue,
- recovery demand,
- tissue stress concentration,
- learning conditions,
- interaction with other stimuli,
- and competition expression.

Temporal dose includes:

- within-session sequence,
- spacing among repetitions and sets,
- spacing among related exposures,
- distribution within a planning period,
- recent exposure history,
- and proximity to competition.

Frequency counts meaningful exposures, not labels on a calendar.
A session or competition contributes only the exposure that actually occurred.

### 3.5 Dose Is Task-Specific
Different tasks require different dose dimensions.
Distance may be central for one sprint exposure but inadequate for a strength or technical task.
Tonnage may describe part of a strength exposure while hiding velocity, range, proximity to failure, and exercise familiarity.
Contact count may describe part of a jump exposure while hiding direction, speed, height, surface, and landing strategy.
Duration may describe general conditioning while hiding mechanical and local tissue demand.
The model permits shared dimensions without forcing false equivalence.

### 3.6 Dose Comparability
Two doses are comparable only with respect to a defined question.
Comparability requires sufficient agreement in:

- construct,
- task,
- intensity reference,
- execution conditions,
- athlete state,
- measurement protocol,
- and temporal context.

Equal total meters, tonnage, contacts, duration, or session count do not by themselves establish equal dose or stimulus.

### 3.7 Composite Load Boundaries
A composite load score can summarize a specified aspect of exposure.
It cannot be assumed to preserve all mechanically, metabolically, technically, or tissue-relevant information.
Combining heterogeneous dose dimensions into one number creates information loss.
Such aggregation must not erase high-consequence local exposure or imply that different stressors are freely exchangeable.

---
## 4. Dose-Response Structure
Dose-response describes the conditional relationship between exposure and change in the athlete.
It is not assumed to be linear, monotonic, stable across time, or identical across athletes.
The same dose can occupy different response states depending on the target, athlete, history, and context.
The states below are relational classifications, not universal numerical zones.

### 4.1 Insufficient Exposure
Insufficient Exposure is an exposure that does not provide enough of the relevant stimulus to support the intended adaptation under the stated conditions.
Insufficiency is always relative to:

- a defined adaptation,
- an athlete state,
- a time horizon,
- and a confidence level.

Failure to observe adaptation does not uniquely prove insufficient dose.
The target, measurement, transfer path, recovery, or time assumption may also be wrong.

### 4.2 Effective Exposure
Effective Exposure is an exposure compatible with producing or preserving the defined adaptation at an acceptable cost under the stated conditions.
Effectiveness is endpoint-specific.
An exposure can be effective for a supporting capacity and ineffective for competitive 100m performance because transfer is absent or masked.
An effective exposure is not automatically the best available intervention.

### 4.3 Diminishing Returns
Diminishing Returns describe a state in which additional exposure is expected to produce progressively less marginal benefit relative to its added cost or risk.
This state can arise through:

- adaptation to the stimulus,
- reduced relevance of the target determinant,
- saturation within the available time,
- accumulating fatigue,
- or displacement of more valuable exposure.

The location of diminishing returns is athlete-specific and uncertain.

### 4.4 Maintenance Exposure
Maintenance Exposure is intended to preserve a defined adaptation or performance capability within an acceptable range over a stated time horizon.
Maintenance must specify:

- what is being preserved,
- for whom,
- under what concurrent training,
- across what period,
- and with what uncertainty.

Maintenance dose is not a universal fraction of development dose.
Minimum effective exposure for improvement and minimum exposure for retention are different objects.

### 4.5 Excessive Exposure
Excessive Exposure is exposure whose added cost, risk, or interference exceeds the value of its expected marginal benefit under the current conditions.
Excessive is not defined by a universal meter, repetition, contact, frequency, or duration threshold.
An exposure can be excessive because of magnitude, density, novelty, placement, interaction, tissue concentration, or competition proximity.

### 4.6 Maladaptive Exposure
Maladaptive Exposure is exposure associated with a persistent change that reduces the athlete's ability to develop, express, or sustain the target performance.
It is distinct from temporary fatigue that is compatible with later benefit.
The distinction depends on time course, target, and observed response.
03 defines the state concept.
04 defines how observations update the classification.

### 4.7 Nonlinearity and State Transitions
More Dose ≠ More Benefit.

Additional dose may:

- remain insufficient,
- enter an effective range,
- add useful adaptation,
- add little benefit,
- preserve rather than develop,
- increase cost without increasing benefit,
- or become maladaptive.

These states do not form a universally ordered numeric curve.
Different dose dimensions can move in different directions and change the stimulus itself.

---
## 5. Expected Adaptation
Expected Adaptation is a prospective claim about a persistent athlete change that may follow a realized stimulus and sufficient recovery.
It is conditional on:

- the target determinant,
- athlete state,
- prior exposure and adaptation history,
- actual dose,
- achieved quality,
- novelty and familiarity,
- recovery conditions,
- interactions with other exposures,
- time available,
- and individual responsiveness.

Expected Adaptation ≠ Guaranteed Adaptation.

### 5.1 Adaptation Object
An adaptation claim should specify:

- `adaptation_target`,
- `expected_direction`,
- `task_and_context_scope`,
- `expected_time_course`,
- `persistence_or_retention_scope`,
- `supporting_mechanism`,
- `observable_indicators`,
- `transfer_path`,
- `competing_adaptations_or_costs`,
- `evidence_basis`,
- and `uncertainty`.

This representation prevents a general phrase such as "improve power" from standing in for a defined adaptation claim.

### 5.2 Intended and Realized Adaptation
Intended Adaptation is the change the intervention is designed to produce.
Realized Adaptation is the persistent change supported by observations after the exposure and recovery process.
The two may differ in:

- direction,
- magnitude,
- timing,
- task specificity,
- persistence,
- and transfer.

Completion of the prescribed intervention establishes neither realized adaptation nor transfer.

### 5.3 Adaptation Specificity
Adaptation is specific to the demands actually experienced.
Specificity can include:

- movement and task,
- velocity,
- force and time constraints,
- range and direction,
- coordination,
- energetic demand,
- tissue loading,
- and psychological or contextual demand.

Specificity is multidimensional.
Superficial resemblance to sprinting does not guarantee useful transfer, and a less visually similar task may influence a relevant supporting capacity.

### 5.4 Adaptation Time
Adaptation has an uncertain time course.
Relevant distinctions include:

- immediate response,
- delayed response,
- accumulated adaptation,
- residual effect,
- retention,
- and loss after reduced exposure.

These are not fixed clocks.
Calendar duration alone does not establish adaptation or recovery.

### 5.5 Adaptation and Current Bottleneck
An adaptation has greater potential value when it changes a determinant that currently constrains performance.
The same adaptation may have low marginal value when:

- the determinant is already sufficient,
- another bottleneck dominates,
- the athlete compensates effectively,
- the time to benefit exceeds the available window,
- or the adaptation cannot be expressed in sprinting.

03 represents this dependence.
It does not diagnose the bottleneck or select the intervention operationally.

---
## 6. Cost Model
Cost is the resource use, burden, or negative consequence associated with an intervention or exposure.
Cost can be expected or realized.
It can be immediate, delayed, cumulative, local, systemic, or contextual.
Cost is multidimensional and need not be compressed into a single score.

### 6.1 Acute Fatigue Cost
Acute Fatigue Cost is the immediate reduction in capacity or execution quality associated with the exposure.
It can affect:

- later repetitions,
- later tasks in the session,
- technical organization,
- output quality,
- and the interpretation of subsequent tests.

Acute fatigue is task- and state-dependent.
It is not adequately represented by heart rate, effort, or session duration alone.

### 6.2 Recovery Cost
Recovery Cost is the time and resources required before relevant capabilities and tissues return to an acceptable state for the next target demand.
It can differ across:

- sprint output,
- local tissue response,
- strength or jump performance,
- subjective state,
- and competition expression.

Recovery cost has no universal 24-, 48-, or 72-hour value.
Its meaning depends on the next task and the athlete's history.

### 6.3 Tissue Stress
Tissue Stress is the local mechanical exposure imposed on tissues through the task, dose, execution, and environment.
It is distinct from general fatigue and from injury diagnosis.
Tissue stress can be concentrated despite low session duration, low heart rate, or low subjective effort.
The same nominal task can create different tissue stress through changes in velocity, surface, range, resistance, contact type, novelty, or technique.

### 6.4 Interference Cost
Interference Cost is the reduction in value of one adaptation or exposure caused by another exposure or by their organization.
The model distinguishes:

- acute sequencing interference,
- residual-fatigue interference,
- longer-term adaptation interference,
- and resource-mediated interference.

These mechanisms must not be treated as interchangeable.
A competing intervention can have meaningful interference through time and recovery use even when a specific biological interference mechanism is not established.

### 6.5 Opportunity Cost
Opportunity Cost is the value of the best relevant alternative displaced by the intervention.
An intervention consumes finite resources such as:

- training time,
- recovery capacity,
- high-quality exposure capacity,
- attention,
- technical learning capacity,
- facility access,
- and competition freshness.

The cost of inclusion includes what can no longer be performed, learned, recovered from, or expressed.
Opportunity cost can make a useful intervention unnecessary or inferior under current conditions.

### 6.6 Competition-Expression Cost
Competition-Expression Cost is the extent to which an intervention may reduce the athlete's ability to express performance at a target competition.
It can arise through:

- residual fatigue,
- local tissue disturbance,
- technical disruption,
- novelty,
- schedule conflict,
- or testing and training demands that compete with freshness.

Its relative importance generally changes as the competition window approaches.
This model represents the cost dimension.
It does not prescribe taper magnitude, duration, or final-session content.

### 6.7 Complexity and Monitoring Cost
Complexity Cost is the execution, learning, coordination, and communication burden introduced by an intervention.
Monitoring Cost is the time, fatigue, equipment, interpretation, and attention required to observe the intervention and its response.
More detailed prescription or measurement is justified only when it preserves enough decision value to warrant its burden.
A test can add cost and alter the exposure it is intended to measure.

### 6.8 Cost Profile
A cost profile should preserve separate dimensions such as:

- acute fatigue,
- delayed recovery,
- tissue stress,
- interference,
- opportunity cost,
- competition-expression cost,
- execution complexity,
- and monitoring burden.

The dimensions can differ in importance and time course.
They should not be averaged into a total score when aggregation would hide a material constraint.

---
## 7. Benefit-Cost Relationship
An intervention is worth considering only as a conditional relation among its expected marginal benefit, costs, risk, alternatives, and uncertainty.
The relevant question is not merely:

> Can this intervention produce an effect?

The model also asks:

> Is the expected target-relevant marginal benefit worth its recovery,
> opportunity, tissue, interference, complexity, competition-expression, and
> risk profile under the current conditions?

This is a comparison structure, not a universal scoring formula.

### 7.1 Expected Benefit
Expected Benefit is the target-relevant positive change considered plausible from the intervention.
It depends on:

- relevance to the current problem,
- likelihood of creating the intended stimulus,
- expected adaptation,
- transfer potential,
- time to benefit,
- persistence,
- and interaction with the rest of the plan.

Benefit should be expressed for a defined athlete, target, and time horizon.

### 7.2 Marginal Benefit
Marginal Benefit is the expected additional value of including or increasing an intervention from the athlete's current exposure state.
It differs from the intervention's historical or general usefulness.
A method that was previously valuable may now have lower marginal benefit because the target has adapted, another bottleneck has emerged, or time and competition conditions have changed.

### 7.3 Conditional Value
A conceptual value relation is:

\[
V(I \mid S,T,A) = g(B_m, C, R, U, O)
\]

where:

- \(I\) is the intervention,
- \(S\) is athlete state,
- \(T\) is temporal and competition context,
- \(A\) is the set of feasible alternatives,
- \(B_m\) is expected marginal benefit,
- \(C\) is the multidimensional cost profile,
- \(R\) is risk,
- \(U\) is uncertainty,
- and \(O\) is opportunity cost.

The relation is qualitative.
It does not imply that unlike dimensions can be measured or summed precisely.

### 7.4 Worth-Considering Conditions
For an intervention to remain a meaningful candidate, the model must be able to represent:

- a defined target problem or determinant,
- a plausible intended stimulus,
- an executable task and interpretable dose,
- a credible adaptation claim,
- a target-relevant transfer hypothesis,
- a visible cost and risk profile,
- feasible temporal placement,
- and material uncertainty.

Missing information can make comparative value indeterminate without proving the intervention useless.

### 7.5 Comparative Statements
Comparisons among interventions must state the dimensions on which they differ.
One intervention can have:

- greater expected benefit,
- lower recovery cost,
- higher tissue stress,
- lower opportunity cost,
- faster time to benefit,
- weaker transfer evidence,
- or greater reversibility.

There may be no single best option across all dimensions.

Useful ≠ Necessary.

Effective ≠ Optimal.

Effective ≠ Best Available Option.

The Plan Model represents comparison within the feasible planning space.
Operational selection rules do not belong in this file.

---
## 8. Athlete-State Dependence
Stimulus value is conditional on the athlete's current state.
The same prescribed task and external dose can create different realized stimuli, responses, costs, and adaptation probabilities.
Therefore:

Stimulus Value ≠ Fixed Property of Exercise.

### 8.1 Current Performance Problem
The intervention's value depends on whether its target remains relevant to the current performance problem and bottleneck hypothesis.
A broadly useful capacity may have little current value when it does not limit the athlete's performance.

### 8.2 Adaptation and Exposure History
Prior exposure affects:

- familiarity,
- learning cost,
- expected responsiveness,
- current capacity,
- retention,
- tolerance,
- and marginal benefit.

Novel exposure may create a new useful stimulus, additional uncertainty, or disproportionate cost.
Repeated exposure may improve execution while reducing novelty and marginal adaptation.

### 8.3 Current Fatigue and Recovery Capacity
Current fatigue can change achieved quality and the realized stimulus.
Recovery capacity changes the cost and timing of the same external exposure.
Relevant context can include recent training, competition, sleep, travel, lifestyle demand, and the next important task.
No single readiness score fully represents this state.

### 8.4 Tissue State
Current tissue state can constrain:

- acceptable exposure,
- force or velocity expression,
- technical organization,
- recovery cost,
- and risk.

A task tolerated previously is not automatically appropriate under a changed tissue state.
03 represents tissue state as a condition and cost modifier.
It does not provide medical diagnosis or return-to-sport rules.

### 8.5 Technical State
Technical stability and task familiarity influence whether the athlete can produce the intended stimulus.
The same external dose can function as:

- target-relevant practice,
- general exposure,
- a learning task,
- or a poorly organized high-cost exposure.

Technical state is athlete-, task-, and velocity-dependent.

### 8.6 Training Age and Competitive Level
Training age and competitive level modify expected adaptation, tolerable dose, novelty, and transfer.
They must not be inferred solely from chronological age or the label "athlete."
Evidence from youth, beginners, team-sport athletes, or world-class sprinters requires explicit applicability limits when used for trained adult or near- adult 100m athletes.

### 8.7 Competition Timing
As a target competition approaches, the time available to create, consolidate, recover from, and express a new adaptation changes.
Residual cost and uncertainty can gain importance while the value of slow or novel adaptation can decline.
This relationship does not prescribe a universal taper or forbid development near competition.

---
## 9. Temporal Context
An intervention exists within time, not as an isolated task.
Its stimulus, cost, and value depend on what precedes it, what follows it, and when the target performance must be expressed.

### 9.1 Within-Session Placement
Task order can change:

- entry fatigue,
- achieved velocity or force,
- technical quality,
- learning conditions,
- acute interference,
- and the cost imposed on later tasks.

Placement is therefore part of intervention identity when it materially alters exposure or stimulus.
This model does not prescribe a universal task order.

### 9.2 Within-Week Distribution
Distribution across days affects:

- concentration of stress,
- recovery opportunity,
- quality of repeated exposure,
- tissue-load overlap,
- and competition with other demands.

Labels such as High or Low do not establish actual cost.
A nominal Low day can contain meaningful local, mechanical, metabolic, time, or attention cost.
03 represents distribution and overlap.
It does not define a fixed number of demanding days or a weekly template.

### 9.3 Mesocycle Context
Mesocycle context changes whether an intervention is intended to:

- develop,
- maintain,
- provide minimal retention exposure,
- support another priority,
- or remain temporarily withdrawn.

These are resource and intent states.
They do not guarantee biological outcomes and do not contain their own progression rules.

### 9.4 Competition Proximity
Competition proximity changes the balance among:

- time to adaptation,
- residual fatigue,
- specificity,
- novelty,
- confidence in the intervention,
- and the need for performance expression.

Competition itself is an exposure and can contribute to dose, cost, and recovery requirements.
Competition proximity does not convert calendar time into a fixed biological readiness state.

### 9.5 Accumulated Fatigue and Recent Exposure
Current exposure cannot be interpreted without recent dose and response history.
Accumulated fatigue may change quality, cost, and apparent dose-response.
Recent exposure can also change familiarity, retention, or the marginal value of another repetition of the same stimulus.
Fixed recovery intervals cannot represent every athlete, tissue, task, and next-performance requirement.

### 9.6 Value Changes Over Time
Stimulus value is dynamic.
It can change because of:

- adaptation,
- exposure history,
- fatigue accumulation or dissipation,
- a changing bottleneck,
- changing constraints,
- altered transfer evidence,
- and competition proximity.

Past Effectiveness ≠ Current Marginal Value.

---
## 10. Interaction Between Stimuli
Training stimuli do not operate independently.
Their combined effect depends on overlap, sequence, timing, athlete state, and the finite resources available to absorb and express them.
The interaction structure is many-to-many.

### 10.1 Synergy
Synergy exists when one exposure increases the expected value or expression of another beyond what would be expected from treating them independently.
Synergy may arise through complementary capacities, learning, preparation, or shared adaptation.
A plausible synergy remains a hypothesis until supported in the relevant athlete and context.

### 10.2 Interference
Interference exists when one exposure reduces the quality, adaptation, recovery, or expression associated with another.
It may be:

- immediate,
- residual,
- adaptation-level,
- tissue-specific,
- or resource-mediated.

The model does not reduce every interference claim to a single mechanism.

### 10.3 Redundancy
Redundancy exists when multiple interventions create substantially overlapping stimuli or adaptations.
Redundancy can support robustness or repeated practice.
It can also add cost without enough marginal benefit.
The value of redundancy depends on target, alternatives, uncertainty, and execution reliability.

### 10.4 Sequencing Effect
A Sequencing Effect exists when the order of exposures changes their realized quality, stimulus, cost, or adaptation potential.
Order can matter within a session, across days, and across longer planning periods.
The existence of sequencing effects does not establish one universal sequence.

### 10.5 Competition for Recovery Resources
Interventions compete for finite recovery capacity even when their task labels differ.
Relevant overlap may include:

- high-velocity demand,
- rapid force-expression demand,
- local tissue loading,
- metabolic burden,
- technical attention,
- psychological demand,
- and time.

Category names and heart rate alone do not determine this overlap.

### 10.6 Overlapping Tissue and Neural Demand
Tasks can load the same tissues or force-expression processes through different movement forms.
Low global fatigue does not prove low local tissue stress.
Likewise, the label "neural" does not provide a sufficient mechanism or a common unit for all high-output training.
The model preserves the separate exposure dimensions instead of assigning an unsupported universal neural-load score.

### 10.7 Interaction Representation
An interaction claim should identify:

- the interventions involved,
- the shared or competing demand,
- the relevant sequence and time window,
- the athlete state,
- the expected direction of interaction,
- the outcome affected,
- the evidence basis,
- and uncertainty.

03 represents the interaction.
Rules and workflows determine how the plan changes because of it.

---
## 11. Transfer Potential
[100m Performance Core Model](./02_100m_performance_model.md) defines the performance determinants, bottlenecks, and transfer structure to which an intervention must connect.
Training adaptation has 100m-specific value only when it can alter a relevant determinant or capability and be expressed in sprint and race performance.
The relationship is:

Training Intervention
→ Realized Stimulus
→ Realized Adaptation
→ Sprint-Relevant Capability
→ Sprint Expression
→ Race / Segment Outcome
→ Competitive 100m Performance.

Each arrow is conditional.

### 11.1 Expected Adaptation and Transfer Potential
Expected Adaptation describes what may change in the source capacity or task.
Transfer Potential describes the plausibility that this change can influence the target performance system.
The two must not be collapsed.
A strong adaptation claim can coexist with weak transfer potential.

### 11.2 Transfer Conditions
Transfer potential may depend on:

- relevance to the current bottleneck,
- task and velocity specificity,
- force-time and coordination demands,
- athlete state,
- technical integration,
- tissue tolerance,
- time available,
- residual fatigue,
- and competition context.

The model does not require visual similarity as the sole test of specificity.
It requires an explicit bridge from adaptation to target expression.

### 11.3 Realized Transfer
Realized Transfer requires target-relevant change, not source-task improvement alone.

Supporting Adaptation ≠ Guaranteed 100m Improvement.

A strength, jump, drill, resisted task, or other supporting result can improve while race performance remains unchanged.
A race result can also improve without proving that the intended supporting adaptation caused it.
The Feedback-Decision Model interprets observations across this chain.

### 11.4 Transfer Uncertainty
Transfer can be:

- partial,
- delayed,
- athlete-dependent,
- context-dependent,
- masked by fatigue,
- offset by another determinant,
- or absent.

Transfer confidence must not exceed the directness, quality, and applicability of the evidence.

---
## 12. Risk and Uncertainty
Risk and Uncertainty are related but distinct.
Risk concerns possible adverse outcomes and their consequences.
Uncertainty concerns the limits of knowledge about exposure, response, adaptation, cost, transfer, or risk itself.

### 12.1 Risk Object
A risk object should be representable through:

- the adverse outcome,
- the pathway by which it may occur,
- the exposure conditions,
- the athlete and tissue context,
- estimated likelihood where supportable,
- consequence severity,
- time horizon,
- reversibility,
- and uncertainty around each element.

Risk is not equivalent to expected fatigue or known resource use.
Those belong to cost.
Risk also does not provide medical diagnosis or permission.

### 12.2 Uncertainty Object
An uncertainty profile may include:

- individual-response uncertainty,
- measurement uncertainty,
- dose-response uncertainty,
- adaptation uncertainty,
- transfer uncertainty,
- interaction uncertainty,
- cost uncertainty,
- risk uncertainty,
- temporal uncertainty,
- and population-applicability uncertainty.

These dimensions may differ in direction and consequence.
They should not be averaged into a single confidence score when that would hide decision-relevant uncertainty.

### 12.3 Evidence and Applicability
Evidence strength and contextual applicability are separate properties.
A well-controlled study can support a dose-response claim while remaining indirect for trained adult 100m athletes, the current task, or the target race outcome.
Elite practice can be highly relevant to context while providing weak causal identification.
Mechanistic plausibility does not establish trainability, dose sufficiency, or transfer.

### 12.4 Uncertain Dose-Response
The model does not assume a known precise dose-response curve.
Observed non-response may reflect:

- insufficient exposure,
- inappropriate stimulus identity,
- inadequate time,
- poor recovery,
- measurement noise,
- low trainability,
- absent transfer,
- or interaction with other exposures.

Observed improvement may also have multiple explanations.

### 12.5 Permitted Uncertainty States
The model permits outputs such as:

- `Cannot Determine Yet`,
- `Plausible Stimulus`,
- `Provisional Dose Range`,
- `Uncertain Adaptation`,
- `Uncertain Transfer`,
- `Cost Not Yet Characterized`,
- and `Risk Requires Separate Assessment`.

These states preserve uncertainty without silently replacing unknown values with defaults.
03 defines the uncertainty that accompanies an intervention claim.
04 defines how observed response changes that uncertainty over time.

---
## 13. Stimulus-Dose-Cost Invariants
The following statements must remain true in every implementation of this Core Model.

1. A task or exercise label does not uniquely identify a training stimulus.

2. Intervention identity depends on target, implementation, dose, execution,
   athlete state, temporal context, environment, and expected effect.

3. A prescription records intent; it does not prove that planned exposure,
   intended stimulus, or adaptation occurred.

4. Actual exposure and achieved quality provide the primary external basis for
   interpreting the realized stimulus.

5. External dose and internal response are different objects and must not be
   combined by definition.

6. Dose is multidimensional and task-specific; sets, repetitions, meters,
   tonnage, contacts, duration, or frequency alone cannot describe every
   exposure.

7. Relative intensity requires an explicit reference, task, and protocol.

8. Equal totals do not establish equivalent doses, stimuli, costs, or expected
   adaptations.

9. Dose-response is conditional and potentially nonlinear; additional dose
   does not guarantee additional benefit.

10. Insufficient, effective, maintenance, diminishing-return, excessive, and
    maladaptive exposures are relational states rather than universal numeric
    zones.

11. Expected adaptation is not guaranteed adaptation, and source-task change
    does not establish target-task transfer.

12. Supporting adaptation requires an explicit transfer path to a determinant
    and expression defined by the 100m Performance Model.

13. Cost is multidimensional and includes acute fatigue, recovery, tissue,
    interference, opportunity, competition-expression, complexity, and
    monitoring costs where relevant.

14. A useful or effective intervention is not automatically necessary, optimal,
    or superior to the feasible alternatives.

15. Opportunity cost must remain explicit because training time, recovery,
    attention, and high-quality exposure capacity are finite.

16. Stimulus value and marginal benefit depend on athlete state, exposure
    history, current bottleneck, and temporal context.

17. Past effectiveness does not establish current marginal value.

18. Stimuli can interact through synergy, interference, redundancy, sequence,
    and overlapping demands; they must not be modeled as independent additions.

19. Cost and risk are distinct, and uncertainty can apply to either.

20. Confidence in a stimulus-dose-adaptation-transfer claim must not exceed the
    evidence quality, contextual applicability, and measurement support.

21. This model may preserve an intervention as indeterminate rather than invent
    a precise threshold, response curve, or effect estimate.

22. This model defines intervention relationships; it does not prescribe a
    method, dose, weekly structure, progression action, or feedback decision.

---
## 14. Model Interfaces
This Core Model converts a target-relevant problem into a representable intervention hypothesis.
It supplies objects to adjacent models without duplicating their functions.

### Performance Model
[100m Performance Core Model](./02_100m_performance_model.md) defines:

- competitive 100m performance,
- race and segment outcomes,
- performance determinants and underlying capacities,
- athlete-specific bottlenecks,
- competition expression,
- and transfer relationships.

02 answers what may need to change.
03 answers how a candidate intervention can be represented as a possible influence on that target, with dose, adaptation, cost, risk, and uncertainty.
03 does not redefine the performance determinant hierarchy or diagnose the bottleneck.

### Plan Model
[Plan Core Model](./01_plan_model.md) defines how interventions are organized inside a time-constrained, updateable training plan.
03 supplies the Plan Model with:

- intervention identity,
- planned exposure,
- dose dimensions,
- expected adaptation,
- transfer potential,
- cost and risk profiles,
- temporal dependencies,
- interactions,
- and uncertainty.

01 defines their priority, feasibility, time organization, and plan-level comparison.
03 does not create a week, mesocycle, season structure, or training plan.

### Domain Knowledge
Future `domain/` files define candidate training content and its commonly observed task-specific properties.
They may describe sprint, strength, plyometric, speed-endurance, technical, and other training domains.
Domain files answer what candidate tasks exist and what characteristics they may have.
03 defines the common grammar through which any candidate task enters the planning system.
It does not reproduce method catalogs, exercise variations, coaching cues, or session examples.

### Rules
Rules implement operational decisions using objects defined here.
They may define:

- admissibility checks,
- dose boundaries,
- quality thresholds,
- progression or regression conditions,
- stop conditions,
- conflict handling,
- and comparison logic.

03 identifies the variables that rules must consider.
It does not state universal thresholds or encode `if X, choose Y` procedures.

### Feedback-Decision Model
[Feedback-Decision Model](./04_feedback_decision_model.md) defines the update relationship:

Actual Exposure
→ Observed Response
→ Updated Athlete State
→ Updated Interpretation
→ Decision Update.

03 supplies 04 with:

- the prescribed task,
- intended stimulus,
- planned and actual exposure,
- achieved quality,
- expected adaptation,
- expected cost and risk,
- transfer hypothesis,
- and uncertainty profile.

04 must define:

- how internal and observed response are interpreted,
- how noise and conflicting signals affect confidence,
- how expected and realized outcomes are compared,
- how athlete state and intervention value are updated,
- and how the system reaches maintain, progress, reduce, modify, withdraw, or
  transition decisions.
03 does not implement readiness thresholds, response-triggered actions, review cadence, or ordered feedback workflows.

### Interface Summary
The cross-model relationship is:

100m Performance Model
→ defines the target problem, determinant, bottleneck, and transfer endpoint
→ Stimulus-Dose-Cost Model represents a candidate intervention, its exposure,
adaptation, cost, risk, and uncertainty
→ Plan Model organizes feasible interventions across time and constraints
→ Feedback-Decision Model compares expected and observed states and updates
future decisions.
The stable boundary remains:

Performance Object ≠ Intervention Object ≠ Decision Rule ≠ Workflow.
