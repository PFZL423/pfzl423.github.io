# Roadmap

A living document tracking what I am learning, building, and reading.
Updated periodically.

---

## Research Roadmap

### Stage 1 — Motivation *(current)*

Establish that current latent world models under-perform when
representation learning and planning costs are treated as independent
problems. Empirical study on dynamic-obstacle environments.

### Stage 2 — Method

Develop **CILD** — a latent world model that couples representation
learning with planner-aware cost heads (risk, progress, occupancy),
trained jointly through the latent dynamics chain.

### Stage 3 — Planner

Build a cost-informed planner on top of CILD:

- gradient-informed sampling
- safety-constrained trajectory pruning
- OOD-aware horizon adaptation

---

## Learning Roadmap

A non-linear study plan. Priority decreases top-down within each group.

### Latent Dynamics & Model-Based RL *(core)*

- TD-MPC, TD-MPC2
- PlaNet
- DreamerV1, V2, V3
- RSSM

### Transformer in Decision-Making

- Decision Transformer
- Trajectory Transformer
- IRIS
- Gato

### Diffusion in Decision-Making

- Diffuser
- Decision Diffuser
- DIAMOND
- Diffusion Policy

### World Models for Embodied AI

- UniSim
- DreamerV3 robotics applications
- SWIM

### Representation Learning *(auxiliary)*

- SPR
- BYOL
- SimCLR

### Foundation Models for Robotics *(survey-level)*

- RT-2
- π0
- OpenVLA

---

## Engineering Roadmap

Side projects that build the toolkit underneath the research.

- **TD-MPC2 deep-read** — line-by-line walkthrough, possible PR
- **Diffusion Policy reproduction** — small-scale, self-contained
- **MPPI utilities** — clean GPU-batched implementation
- **Technical writing** — periodic notes on world models and planning

---

## Reading Standard

- For most papers: understand the main idea, run the code if available.
- For core papers (DreamerV3, IRIS, SPR, TD-MPC2): read the code in
  detail; be able to explain the method to someone unfamiliar.
- Always ask: *can this be grafted onto the latent-dynamics framework
  to address a problem it currently cannot solve?*

---

*Last updated: 2026-05*
