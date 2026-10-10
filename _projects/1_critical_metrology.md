---
layout: page
title: Critical Metrology
description: Quantum Fisher information across the superradiant transition of the quantum Rabi model. Bachelor's thesis, 10/10 with Honors.
img: assets/img/cards/critical_metrology.png
importance: 1
category: research
github: https://github.com/Landerzl/Critical-Metrology
---

<style>
  article p,
  article li,
  .caption {
    text-align: justify;
    hyphens: auto;
  }
</style>

<p style="font-size: 1.1rem">
  <a href="{{ '/assets/pdf/critical_metrology_zulueta.pdf' | relative_url }}" target="_blank" rel="noopener"><i class="fa-solid fa-file-pdf"></i> <b>Read the manuscript (PDF)</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Landerzl/Critical-Metrology" target="_blank" rel="noopener"><i class="fa-brands fa-github"></i> <b>Code</b></a>
</p>

**L. Zulueta, J. Apellaniz, I. Egusquiza.** _Critical quantum metrology with the quantum Rabi model: Fisher information across the superradiant transition._ Preprint, 2026.

Bachelor's thesis at the University of the Basque Country (EHU), Sep. 2025 – Jul. 2026, supervised by Iñigo Egusquiza and Jagoba Apellaniz, funded by an Ikasiker grant from the Basque Government. Graded 10/10 with Honors.

## The question

Near a quantum phase transition, the ground state becomes extremely sensitive to the parameters that drive it. Critical quantum metrology tries to use that sensitivity to estimate a parameter more precisely than classical limits allow. The catch is that true criticality usually needs the thermodynamic limit.

The quantum Rabi model, a single qubit coupled to a single bosonic mode, avoids that: it has a superradiant transition in the _classical oscillator limit_, where the ratio of qubit to mode frequency plays the role of the thermodynamic limit. I asked how much information about the coupling strength $$\gamma$$ the ground state carries as it approaches the critical point $$\gamma_c$$.

<div class="row mt-3">
  <div class="col-sm-8 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/critical-metrology/gs_energy_minima.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Variational ground-state energy f(x). Past the transition (γ² > 1/2) the single minimum splits in two: the superradiant phase.
</div>

## Normal phase: a −2 critical exponent

Using first- and second-order Schrieffer–Wolff effective Hamiltonians, I derived the quantum Fisher information (QFI) for estimating $$\gamma$$ analytically. It diverges at the critical point as $$F_Q \propto (1-\gamma/\gamma_c)^{-2}$$, and exact numerics of the full model (QuTiP) agree with the analytic result.

<div class="row mt-3">
  <div class="col-sm-6 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/critical-metrology/qfi_normal_combined.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Normal-phase QFI. (a) Numerics versus the first-order Schrieffer–Wolff result. (b) Log–log plot against the distance to the critical point, showing the slope −2.
</div>

## Superradiant phase: making the numerics converge

Past the transition the effective potential inverts and a plain Fock-basis diagonalization no longer converges. I introduced a displaced and squeezed Fock basis that restores convergence, and obtained the QFI of the physical ground state by accounting for how that basis transformation itself depends on $$\gamma$$.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/critical-metrology/qfi_heatmap_normal.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/critical-metrology/qfi_heatmap_superradiant.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  QFI (log scale) as a function of the coupling and the frequency ratio ω/Δ, in the normal phase (left) and the superradiant phase (right). The information peaks at γ = γ<sub>c</sub> and grows as ω/Δ → 0.
</div>

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/critical-metrology/fidelity_displaced_squeezed.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/critical-metrology/entanglement_entropy.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Left: convergence of the ground state with the Fock cutoff in the displaced and squeezed basis. Right: qubit–field entanglement entropy, which peaks at the critical point, an independent signature of the transition.
</div>

## Methods

- Analytics: Schrieffer–Wolff transformations to first and second order, bosonic Bogoliubov transformations.
- Numerics: dense diagonalization in truncated Fock bases (QuTiP), numerical differentiation for the QFI, convergence checks against the cutoff.
- All code and figure scripts are on [GitHub](https://github.com/Landerzl/Critical-Metrology).
