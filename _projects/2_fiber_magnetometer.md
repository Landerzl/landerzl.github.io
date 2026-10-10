---
layout: page
title: NV-center magnetometry
description: A fiber-based NV-center magnetometer at Qubiz.team, and open-system and DFT simulations of NV centers.
img: assets/img/magnetometer/odmr.png
importance: 3
category: research
github: https://github.com/Landerzl/NV-Centers-Code
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
  <a href="https://github.com/Landerzl/NV-Centers-Code" target="_blank" rel="noopener"><i class="fa-brands fa-github"></i> <b>Simulation code</b></a>
</p>

## Fiber-based magnetometer

At [Qubiz.team](https://qubiz.team) (Bilbao, Sep. 2026 – present) I build and operate a fiber-based optical quantum sensing setup for magnetic field sensing, based on NV centers in diamond. A green laser excites the NV centers through an optical fiber and the photoluminescence returns through the same fiber. When a microwave field hits the spin resonance near 2.87 GHz, the photoluminescence drops: this is optically detected magnetic resonance (ODMR), and the position of the dip tracks the magnetic field.

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/magnetometer/odmr.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Zero-field CW-ODMR measured with the fiber setup, averaged over up and down frequency sweeps.
</div>

I also design and simulate microwave waveguides for hyperpolarization setups in Ansys HFSS and COMSOL RF.

## Simulations

Alongside the experiment, I wrote simulations of NV centers in two directions.

**Open-system dynamics (QuTiP).** A 7-level model of the NV center (ground and excited spin triplets plus the metastable singlet) under continuous laser driving, with Lindblad decay. It reproduces CW-ODMR spectra, Ramsey fringes, and the photoluminescence around the ground- and excited-state level anticrossings (GSLAC and ESLAC) as a function of magnetic and electric field, including the response to an oscillating electric field through the Stark effect.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/nv-sim/cw_odmr_sim.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/nv-sim/eslac_gslac_E.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Simulations with the 7-level model. Left: CW-ODMR spectrum under a bias magnetic field, with the two spin transitions split. Right: photoluminescence versus magnetic field across the ESLAC region for several axial electric fields; the GSLAC position (dashed) does not move.
</div>

**Quantum chemistry (PySCF).** DFT calculations on diamond clusters containing NV centers (with and without hydrogen passivation, single and pairs of NVs) to compute the zero-field splitting parameters D and E, their Stark shift under an applied electric field, the excited state, and the molecular orbitals.

Code: [github.com/Landerzl/NV-Centers-Code](https://github.com/Landerzl/NV-Centers-Code)
