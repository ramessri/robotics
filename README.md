# robotics

# Autonomous Dexterous Robotics

A research repository exploring autonomous humanoid robotics from first principles, with a focus on dexterous manipulation.

This work is an ongoing research effort into human-to-humanoid motion retargeting and dexterous grasping — building toward systems that can operate in unstructured environments with human-level manipulation capability.

---

## Core Question

**Does it generalise?**

Not: can it solve a task.  
But:
- can it adapt to new objects
- can it handle unseen dynamics
- can it infer latent states from partial observations

This is the question every design decision is evaluated against.

---

## System Overview

```
  → Perception (vision + touch + proprioception)
  → latent state estimation
  → intelligence policy (RL / IL)
  → control (IK + dynamics)
  → hardware
```

A human hand integrates perception, inference, and control seamlessly. Replicating this requires a system that combines multi-modal sensing, state estimation, and action under uncertainty — as a unified loop.

---

## Perception

Multi-modal by design. A policy that relies on vision alone will fail the moment contact matters.

**Vision**
- Semantic segmentation
- Depth estimation
- 3D reconstruction
- Gaussian Splatting

**Touch**
- Force: normal, shear, torsion
- Vibration and slip detection
- Temperature
- Contact geometry

**Proprioception**
- Joint positions and velocities
- Torques
- Internal state estimation

All signals fuse into a latent state representation used for estimation and control.

---

## Intelligence

### Imitation Learning
- Human-to-humanoid motion transfer
- Grasp-aware retargeting for dexterous manipulation
- Behaviour Cloning as initialisation before RL fine-tuning

Retargeting must account for multi-finger contact and object geometry — not just point interactions. This is the core limitation of most current retargeting pipelines.

### Reinforcement Learning
- Policy learning in simulation (IsaacLab / MuJoCo)
- PPO with BC-initialised policies
- World models for planning under uncertainty
- Sim-to-real transfer via domain randomisation

### Probabilistic Methods *(longer-term direction)*
- Latent state estimation and sensor fusion
- Active inference formulations
- Expected free energy minimisation

Generalisation is evaluated along three axes: visual, semantic, and behavioural.

---

## Action

Control is treated as a first-class component to the policy.

- Forward and inverse kinematics
- Jacobians and pseudo-inverse methods
- Constrained optimisation
- Safety-aware control

**Hardware focus**
- Tendon-driven dexterous hands
- Multi-finger manipulation
- NVIDIA Jetson for edge deployment
- CUDA / TensorRT for low-latency inference


### Manipulation

**Grasp types**
- Form closure
- Force closure
- Suction (out of scope)
- Semantic grasping (VLA-driven)

**Articulation**
- Rigid vs soft grippers
- Tendon-driven vs motor-driven actuation
- Articulated vs unarticulated objects

---

## Experiments

### Knot manipulation
Tying and untying knots. Evaluates whether vision alone is sufficient or whether tactile feedback is necessary for contact-rich manipulation.

### Object generalisation
Articulated vs unarticulated objects — from rigid boxes to plush toys. Tests whether the policy transfers across object classes without retraining.

### Vision vs tactile ablation
- Vision-only policy
- Vision + tactile fusion

Compare stability, robustness, and failure modes. 
Hypothesis: vision is sufficient for reaching, touch is necessary for stable grasping.

### Sim-to-real transfer
Train in simulation, deploy on hardware, measure performance degradation. Identify which failure modes are simulation artefacts and which are genuine generalisation failures.

---

## Simulation and Deployment

**Simulation**
- Isaac Sim / Isaac Lab — GPU-parallelised, PhysX backend
- MuJoCo — fast, accurate, standard in research

**Pipeline**
- Collect or retarget demonstrations
- Train policy in simulation
- Integrate perception and control
- Transfer to hardware

---

## Foundations

<details>
<summary>Prerequisites and background knowledge</summary>

**Mathematics**
- Calculus, linear algebra, probability and statistics

**Physics**
- Kinematics, nonlinear systems, linearisation, signals

**Machine Learning**
- Regression, classification, time series
- Neural networks, transformers, diffusion models

**Robotics**
- Control theory, motion planning, perception

**Systems**
- ROS2, embedded systems, edge AI

</details>

---

## Future Directions

- Vision-language-action models (VLA, Pi0)
- Differentiable grasp synthesis (GraspQP)
- Full humanoid whole-body manipulation
- Active inference for adaptive control
- World models for long-horizon planning

---

## Key References (TBA)

| Paper | Relevance |
|-------|-----------|
| [DexMachina (2025)](https://project-dexmachina.github.io/) | Human MoCap → robot hand retargeting pipeline |
| [OmniRetarget](https://omniretarget.github.io/) | Interaction-preserving whole-body retargeting |
| [DynaRetarget](https://arxiv.org/abs/2602.06827) | Dynamically-feasible trajectory retargeting |
| [GraspQP](https://arxiv.org/abs/2508.15002) | Differentiable force-closure grasp synthesis |
| [DeepMimic](https://xbpeng.github.io/projects/DeepMimic/index.html) | Physics-based character imitation learning |
| [InterAct](https://sirui-xu.github.io/InterAct/) | Human motion dataset for imitation learning |

---

## Status

**Early 2026**
- [ ] Simulation environment setup (IsaacLab)
- [ ] Behaviour cloning baseline
- [ ] Kinematics and retargeting pipeline
- [ ] Grasp synthesis integration
- [ ] RL fine-tuning
- [ ] Hardware deployment

This is an active research repository. Structure and scope will evolve with the work.

---

*If you are working on dexterous manipulation and want to connect, feel free to open an issue or reach out directly.*