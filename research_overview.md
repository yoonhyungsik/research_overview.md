# Research Vision

## 1. Long-term Research Goal

My long-term research goal is to develop generative systems that can naturally incorporate external evaluative signals into the generation process itself, rather than using them only after generation is complete.

In particular, I am interested in text-to-image generative models based on diffusion and flow matching, which can be viewed as trajectory generation processes over latent or image space.
I want to study how external evaluators, especially non-differentiable vision-language models (VLMs), can be integrated into these trajectory dynamics in a principled way.

Ultimately, I aim to build self-corrective generative models that can:
1. inspect intermediate generation states,
2. identify what is wrong or missing,
3. infer how the trajectory should be adjusted,
4. and progressively revise the generation process toward more reliable, prompt-faithful, and perceptually strong outputs.

In this sense, my broader goal is to move from passive sampling to reflective and adaptive generation.

---

## 2. Motivation

Modern text-to-image models can generate highly realistic images, but they still often fail in subtle yet important ways, such as:
- missing attributes,
- incorrect object relations,
- counting errors,
- weak compositional binding,
- or mismatch between prompt intent and final appearance.

External evaluators such as VLMs can often detect these failures better than the generator itself.
However, in most current systems, such evaluators are used only at the end of generation for reranking, reward assignment, or best-of-N selection.

This is fundamentally limited.
If useful evaluative information is only used after the trajectory is already completed, the model loses the opportunity to correct errors while the generation is still evolving.
A more powerful paradigm would be to incorporate evaluator feedback during generation, so that the trajectory itself becomes adaptive.

This is especially important for diffusion and flow-based generative models, where generation is not a single-step prediction but a multi-step or continuous-time evolution process.
Such models provide a natural opportunity for intermediate monitoring, trajectory correction, and test-time adaptation.

---

## 3. Core Research Perspective

I view diffusion models and flow matching models through a unified trajectory-based perspective.

- In diffusion models, generation is a gradual denoising trajectory over discrete or continuous time.
- In flow matching, generation is modeled as continuous transport induced by a learned velocity field, often formulated as an ODE.

From this perspective, the key research question is:

**How can external evaluative signals be translated into trajectory-level corrective signals for generative dynamics?**

This question includes several subproblems:
- how to evaluate intermediate states,
- how to determine when evaluator signals are reliable,
- how to assign credit from final errors back to intermediate trajectory segments,
- how to convert sparse and non-differentiable judgments into useful control signals,
- and how to intervene in the trajectory without causing instability or collapse.

My research aims to address these problems in a unified framework spanning diffusion, flow matching, and ODE-based generation.

---

## 4. Current Starting Point

My current work focuses on training-free test-time methods for text-to-image diffusion, especially methods that combine:
- early-stage semantic refinement,
- late-stage reward-guided selection,
- and stage-aware integration of external evaluators.

The central insight is that different phases of generation support different types of control.
In noisy early stages, semantic structure, layout, and attribute binding remain malleable.
In later stages, perceptual quality and holistic visual preference become more reliably measurable by external evaluators.

This work serves as a first step toward a larger goal:
bringing external evaluation into the generative trajectory in a stage-aware and dynamics-aware manner.

---

## 5. Expanded Research Direction: From Diffusion to Flow/ODE-Based Generative Dynamics

My future research is not limited to diffusion in its standard discrete denoising form.
I want to generalize the problem to a broader class of trajectory-based generative models, including flow matching and related ODE-based frameworks.

This broader perspective is attractive for several reasons.

First, ODE-based generation offers a cleaner continuous-time interpretation of how a sample evolves.
This makes it easier to reason about trajectory correction, control, and intervention.

Second, flow-based or ODE-based formulations may provide more direct ways to connect evaluator feedback with vector field modification, trajectory steering, or local control.

Third, a continuous-time viewpoint may help bridge ideas from diffusion sampling, optimal control, feedback systems, and test-time scaling.

From this viewpoint, I am particularly interested in the following question:

**Can external evaluators shape not only which sample is selected, but also how the underlying trajectory field is modified during generation?**

For diffusion models, this may correspond to modifying denoising updates, guidance terms, or resampling rules.
For flow matching or ODE-based models, this may correspond to modifying the velocity field, introducing corrective control terms, or learning differentiable surrogate objectives that influence the continuous trajectory.

Thus, my long-term goal is to study evaluator-guided generative dynamics, rather than evaluator-based post hoc selection alone.

---

## 6. Key Research Questions

My research direction is organized around the following core questions:

### Q1. Evaluator Integration
How can non-differentiable external evaluators such as VLMs be incorporated into diffusion and flow-based generation more naturally?

### Q2. Intermediate-State Evaluation
How can intermediate latent or decoded states be evaluated meaningfully during generation, rather than only at the final step?

### Q3. Reliability Across Time
At which stages of the generative trajectory are evaluator signals reliable, and how does this depend on the model family, timestep, or representation?

### Q4. Credit Assignment
If an evaluator judges an image as flawed, how can we determine which part of the trajectory caused the problem and where intervention should occur?

### Q5. Corrective Control
How can evaluator feedback be transformed into practical corrective signals such as guidance adjustment, latent refinement, trajectory branching, resampling, or vector-field control?

### Q6. Differentiable Approximation
Can VLM judgments be approximated by differentiable surrogate models that provide smoother and cheaper optimization signals for trajectory-level correction?

### Q7. Self-Corrective Generation
Can generative models evolve from passive samplers into systems that diagnose, revise, and improve their own intermediate predictions at test time?

---

## 7. Conceptual Progression of the Research Program

I see this research program as a progression through four increasingly ambitious stages.

### Stage 1: External evaluation for final selection
At the first stage, external evaluators such as VLMs are used after or near the end of generation.
Their role is to rank, resample, or select among candidate trajectories or samples.
This includes reward-guided selection, reranking, and particle-based filtering.

This stage is useful, but it remains fundamentally post hoc.

### Stage 2: Stage-aware evaluative guidance
At the second stage, evaluator signals are introduced during generation in a stage-aware way.
The goal is not yet full trajectory correction, but selective intervention when evaluator signals become sufficiently reliable.

This includes:
- delayed reward activation,
- timestep-dependent evaluator usage,
- reliability-aware resampling,
- and adaptive control based on trajectory phase.

### Stage 3: Trajectory-level correction in diffusion and flow dynamics
At the third stage, evaluator feedback begins to affect the trajectory more directly.
Instead of only scoring samples, the system identifies likely failure modes and adjusts the trajectory accordingly.

For diffusion, this may involve:
- adaptive guidance,
- correction of latent direction,
- step-wise prompt adjustment,
- or branch-and-select strategies.

For flow matching / ODE-based models, this may involve:
- modifying the velocity field,
- injecting corrective control terms,
- or applying evaluator-conditioned steering along continuous trajectories.

### Stage 4: Self-corrective generative systems
At the final stage, the model becomes self-corrective.
It does not simply generate and receive a score.
Instead, it monitors its own intermediate outputs, diagnoses problems, infers what kind of correction is needed, and revises its trajectory iteratively.

At this stage, generation becomes closer to reasoning-driven test-time scaling:
the model improves outputs not only through scale or training, but through evaluation, diagnosis, and revision during inference.

---

## 8. Near-, Mid-, and Long-Term Plan

### Near-term
My near-term goal is to establish stable and practical mechanisms for incorporating external evaluator signals into diffusion sampling under a training-free setting.

Key directions include:
- late-stage reward-guided selection,
- reliability-aware evaluator activation,
- particle-based or branch-based selection,
- and analysis of when evaluator signals become trustworthy across denoising steps.

At this stage, the main focus is on understanding how evaluator signals interact with the trajectory and how to prevent instability such as premature collapse or noisy selection.

### Mid-term
My mid-term goal is to move from final-step scoring to intermediate trajectory correction.

This includes:
- diagnosing specific generation errors such as missing attributes, wrong relations, count errors, or compositional failures,
- converting evaluator outputs into step-wise corrective signals,
- and studying how such signals can steer or revise generation trajectories.

At this stage, I also want to extend the framework beyond standard diffusion to flow matching and continuous-time ODE-based generation, where evaluator feedback may be interpreted as a trajectory control signal.

### Long-term
My long-term goal is to develop self-reflective and self-corrective generative systems.

This includes:
- differentiable surrogate models for VLM-based judgment,
- evaluator-informed control of generative dynamics,
- step-wise diagnosis-and-revision loops,
- and a unified framework for test-time scaling in trajectory-based generative models.

Ultimately, I want to build generative systems that can progressively improve their own outputs by evaluating intermediate states, identifying mistakes, and revising the trajectory before the final sample is produced.

---

## 9. Long-term Vision

My long-term vision is to make generative models more reflective, adaptive, and controllable at test time.

Rather than treating generation as a fixed sampling procedure, I want to study generation as a dynamic process that can be monitored, evaluated, and corrected while it unfolds.
This perspective naturally connects diffusion, flow matching, ODE-based generation, external verifier integration, and test-time scaling.

I believe that a major future direction in generative AI lies not only in larger models or more training data, but also in better inference-time intelligence:
the ability to evaluate partial outputs, reason about what is wrong, and revise the generative trajectory accordingly.

In this sense, my ultimate goal is to develop trajectory-aware generative systems that do not merely sample images, but iteratively improve them through evaluator-guided self-correction.
