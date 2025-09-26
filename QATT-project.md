---
layout: default
---
# QATT: From Naïve Fusion to a New Paradigm in Uncertainty Quantification

This project documents an intellectual odyssey. It began with a straightforward, albeit naïve, attempt to improve a quadrotor controller and culminated in the foundational principles of my research vision: a new paradigm for quantifying uncertainty by interpreting the internal conflicts within a control architecture.

---

### Phase 1: The Naïve Fusion Hypothesis
My research began upon receiving the QATT problem from my advisor, Prof. Rifat Sipahi. Inspired by the impressive results from literature on **Differential Flatness (DF)**, particularly **[Ezra Tal's INDI research](https://arxiv.org/abs/1809.04048)**, and the robustness of **Sliding Mode Control with a Disturbance Observer (SMC+DOB)** from **[Jing et al.](https://www.mdpi.com/2504-446X/6/9/261)**, I formed a simple hypothesis: combining the two would yield superior performance for aggressive maneuvers.

* **Baseline Controller (C1):** The robust SMC+DOB framework from Jing et al., which tracks up to the 2nd order derivatives (position, velocity, acceleration) of a given trajectory.
* **Experimental Controller (C5):** My initial modification. I replaced the reference attitude rates/accelerations (`ϕ_des`, `θ_des`) in the inner SMC loop with values derived from DF (`ϕ_DF`, `θ_DF`), which contain higher-order derivative information (jerk, snap). This was a direct, superficial application of Tal's structure to Jing's controller.
* **Blended Controller (C6):** A further attempt to salvage the idea by creating a linear combination of the two signals, `ϕ_ref = β∙ϕ_DF + (1-β)∙ϕ_des`.

I implemented these controllers in a high-fidelity SITL simulation environment (MATLAB/Simulink) and tested them against 10 mathematically defined, aggressive trajectories.

**The Result: Systematic Failure.**
Across all tests, neither C5 nor C6 demonstrated any clear, consistent performance improvement over the baseline C1. The approach was a failure. This series of intellectually honest failures forced me to confront a fundamental flaw in my reasoning: I lacked theoretical justification for why this fusion *should* work.

---

### The Pivotal Question: A Shift in Perspective
This systematic failure became the project's most valuable outcome. It forced me to abandon the superficial question of "How do we best mix these signals?" and ask a more profound one:

> **"Why are these signals different in the first place?"** 

This question shifted my entire research focus from signal fusion to signal analysis.

---

### The Breakthrough: The 'Gap' as a Rich Information Signal
Even in a pristine simulation environment with no external disturbances, I observed a persistent, non-zero discrepancy between the two command signals: the outer loop's demand (`ϕ_des`) and the DF-derived ideal (`ϕ_DF`). I named this phenomenon the **'Gap'**.

I redefined this 'Gap' not as a nuisance to be eliminated, but as the most information-rich signal within the architecture. It is a real-time, high-fidelity symptom of **'Lumped Uncertainty'**—the sum of all unmodeled dynamics, parameter uncertainties, and even simulation-based discrepancies that the ideal mathematical model fails to capture.

This re-framing elevated the project from a technical exercise to a new paradigm for real-time uncertainty quantification.

<p align="center">
    <img src="assets/img/helix_roll.jpg" alt="Fig 1: The observed 'Gap' between command signals" style="max-width: 100%; height: auto; border-radius: 5px;">
</p>

<div style="text-align: center; font-style: italic; color: #555;">
    Fig 1: A graph from simulation plotting `ϕ_des` and `ϕ_DF` over time, clearly showing the persistent 'Gap'.
</div>

---

### Future Directions: From a Special Case to a General Theory
My undergraduate work provided the first concrete evidence for this hypothesis. My doctoral research will be dedicated to transforming this fascinating symptom into a reliable engineering tool and building a rigorous theoretical foundation.

* **The 'Gap' as a Nonlinear Observer:** The 'Gap' is a modulated signal, influenced by the feedback controller's own dynamics. My first goal is to design a nonlinear observer framework to mathematically isolate the pure, uncorrupted uncertainty information from the observed 'Gap'.
* **Causal Inference:** The next step is to solve the nonlinear inverse problem: to infer the physical forces/torques (the cause) from the purified 'Gap' signal (the symptom).
* **Generalization of the Principle:** I believe this principle is universal, extending beyond the specific DF-SMC architecture where I discovered it. I plan to investigate how the 'Gap' manifests in other control architectures, such as the discrepancy between predicted and actual trajectories in Model Predictive Control (MPC), to develop a unified theory for uncertainty quantification.

---

### Connection to My Research Interests
This entire intellectual journey is the bedrock of my passion for **Robust Control, Optimization, and Nonlinear Dynamics**. It embodies my ultimate research goal: to design control architectures that can **provably guarantee** safety and performance under uncertainty. The 'Gap' philosophy is my first concrete step toward achieving **Provably Safe Autonomy**, moving beyond simply rejecting uncertainty and toward actively understanding and exploiting it.
