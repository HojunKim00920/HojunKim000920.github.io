# QATT: Controller for Quadrotor’s Aggressive Trajectory Tracking

This project was not just about building a controller; it was a journey that reshaped my understanding of control engineering's core challenges. It started as an attempt to solve a technical problem and evolved into the foundation of my research philosophy.

---

### What: The Initial Problem
The goal was to enhance the robustness of quadrotor trajectory tracking for aggressive maneuvers. The conventional approach suggested that combining the strengths of a model-based feedforward controller (Differential Flatness) and a robust feedback controller (Sliding Mode Control) would yield superior performance. The problem was how to best fuse these two control philosophies.

### How: A Journey Through Systematic Failure
My initial hypothesis was a straightforward fusion of the two controllers. However, rigorous SITL simulations in MATLAB/Simulink systematically proved that simple mechanical fusion or even more complex signal-blending architectures led to diminishing returns. This series of intellectual honest failures forced me to ask a more fundamental question: not "How do we best mix these signals?" but "Why are these signals different in the first place?".

This led to the critical discovery: a persistent 'Gap' always existed between the ideal prediction from the mathematical model (Θ_FF) and the robust correction from the feedback loop (Θ_FB), even in a perfect simulation.

My Contribution: I critically diagnosed the inherent limitations of the initial architecture, identifying that the root cause was not suboptimal signal fusion but a fundamental model-plant mismatch. I then redefined this 'Gap'—not as an error to be minimized, but as a rich information signal representing 'lumped uncertainty' in real-time.

### Why: A New Paradigm & Quantifiable Results
This re-framing elevated the project from a technical exercise to a new paradigm for uncertainty quantification. By treating the 'Gap' as a symptom to be analyzed, I pivoted my research towards developing a disturbance observer that directly estimates and compensates for this lumped uncertainty.

Quantifiable Impact: Even the initial hybrid architecture achieved up to an 11.6% reduction in maximum tracking error compared to a baseline SMC controller in simulations across 10 aggressive trajectories.
Lessons Learned: The most profound lesson was that the internal conflicts within a control architecture are not flaws, but can be exploited as a valuable source of information to build truly robust and provably safe autonomous systems. This project became the laboratory where this core principle was discovered and validated.

---
*[Back to Project List](projects.html)*
