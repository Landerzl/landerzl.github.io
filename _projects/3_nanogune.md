---
layout: page
title: Molecular Architectonics
description: Nanographene spin chains and ESR-STM at CIC nanoGUNE. On-surface synthesis, STM spectroscopy, and spin-model numerics.
img: assets/img/nanogune/ribbons.png
importance: 2
category: research
github: https://github.com/Landerzl/Numerics-Nanogune
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
  <a href="https://github.com/Landerzl/Numerics-Nanogune" target="_blank" rel="noopener"><i class="fa-brands fa-github"></i> <b>Code</b></a>
</p>

Research internship in the Quantum Probe Microscopy Group at [CIC nanoGUNE](https://www.nanogune.eu) (San Sebastián, Jun. – Aug. 2026), supervised by Prof. Nacho Pascual.

Carbon-based systems are normally non-magnetic, so magnetism has to be engineered through molecular design. The internship had two parts: in the first month I grew and imaged graphene nanoribbons with magnetic end states and modeled nanographene spin chains; in the second I worked toward ESR-STM, driving and detecting a single spin with the STM.

I worked on two low-temperature STMs in ultra-high vacuum, Berlino (1.2 K) and Bilbo (300 mK). Keeping them running meant liquid helium and nitrogen refills several times a week, plus sputtering and annealing to keep the crystals atomically clean.

## Month 1: nanographenes

### Graphene nanoribbons on a superconductor

The platform is a 7-atom-wide armchair graphene nanoribbon (7-AGNR) on Au(111), on top of a Ag buffer layer and superconducting Nb. The gold inherits part of the superconducting gap through the proximity effect, and the tip probes the ribbon by scanning tunneling spectroscopy.

<div class="row mt-3">
  <div class="col-sm-6 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/agnr_platform.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  7-AGNR on Au(111)/Ag/Nb, probed by STS.
</div>

The ribbons are built on the surface from a small precursor molecule (DBBA) in two thermally activated reactions: Ullmann coupling at about 200 °C links the molecules into a polyphenylene chain, and cyclodehydrogenation at about 400 °C closes it into a flat ribbon.

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/synthesis.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  On-surface synthesis: DBBA precursor → polyphenylene oligomer → 7-AGNR.
</div>

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/ribbons.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  STM topographs of ribbons of increasing length, from L = 2 (1.8 nm) to L = 6 (4.75 nm) precursor units.
</div>

### End spins

A 7-AGNR has a non-trivial band topology (Zak phase γ = π), which guarantees a localized state at each open end. On the superconducting substrate, such an end spin shows up as Yu–Shiba–Rusinov (YSR) states: extra peaks inside the superconducting gap, absent on the bare gold.

<div class="row mt-3">
  <div class="col-sm-9 mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/ysr.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm-3 mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/zak_7agnr_bands.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Left: dI/dV on the bare proximitized gold (black) and at the ribbon end (blue); the in-gap YSR peaks at the end are the fingerprint of the end spin. Right: tight-binding bands of the periodic 7-AGNR, the origin of the topological end states.
</div>

The two end spins of a ribbon interact. I computed their exchange coupling $$J$$ as a function of ribbon length with a Hubbard-dimer model and with mean-field Hubbard calculations. $$J$$ falls off exponentially with length and drops below the superconducting gap and the thermal energy for the longer ribbons.

<div class="row mt-3">
  <div class="col-sm-8 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/J_vs_L.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  End-to-end exchange coupling J versus ribbon length: Hubbard dimer, mean-field Hubbard, and an exponential fit, compared with the Nb superconducting gap and the thermal energy at 1.2 K.
</div>

### A tunable spin chain

[3]Triangulene (spin 1) and phenalenyl (spin ½) are each magnetic on their own. Combining them into a phenalenyl–triangulene–phenalenyl (P–T–P) chain gives a mixed ½–1–½ antiferromagnetic spin chain. I modeled it with mean-field Hubbard spin densities and an effective Heisenberg Hamiltonian, solved by exact diagonalization.

<div class="row mt-3">
  <div class="col-sm-7 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/spin_chain_mix.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="row mt-3">
  <div class="col-sm-10 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/spin_chain_model.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Top: triangulene (S = 1) and phenalenyl (S = ½), and the mean-field Hubbard spin density of a P–T–P chain. Bottom: the effective spin model, in which each triangulene locks into a spin-1 unit.
</div>

The main result: the excitation gap of the chain can be set by design. It is about 22 meV for a single unit and decreases with chain length, extrapolating to Δ ≈ 5.8 meV for an infinite chain.

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/spin_gap_fss.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Spin gap from exact diagonalization: finite-size scaling against 1/N (left) and raw trend with the number of monomers N (right).
</div>

To connect the model to an experiment, I simulated STM spectroscopy (Tersoff–Hamann). For N = 3, the spin excitation localizes on the central triangulene and should appear as a step in dI/dV at ±11.04 meV, a concrete target for point spectroscopy.

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/iets_didv_map_N3.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Simulated dI/dV map of the spin excitation for the N = 3 chain.
</div>

## Month 2: toward ESR-STM

ESR-STM combines electron spin resonance with an STM: an RF voltage at the tip drives transitions of a single spin at $$h f_\mathrm{RF} = g \mu_B B$$, and a spin-polarized tip reads out the spin state through the tunneling current, which is higher for parallel than for antiparallel alignment.

The target platform was a naphthalocyanine (Nc) molecule on a bilayer MgO island on Ag(100). The roadmap: calibrate the RF line, grow Nc, grow MgO, prepare a spin-polarized tip, measure ESR.

<div class="row mt-3">
  <div class="col-sm-6 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/esr_platform.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  ESR-STM on Nc/MgO/Ag(100): spin-polarized tip, RF antenna and external magnetic field B.
</div>

- **RF line.** I measured the transfer function of the RF line, including the cryogenic antenna integrated into the STM junction, with a VNA. This is the calibration needed to know the RF amplitude that actually reaches the junction.
- **Nc deposition.** Thermal sublimation did not work, so I switched to flash evaporation from a silicon leaf, which gave intact Nc molecules on Ag(100).
- **MgO.** I grew MgO islands as the decoupling layer.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/rf_transfer_function.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm-3 mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/nc_on_ag100.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm-3 mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/nanogune/mgo_islands.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Left: RF transfer function of the line. Middle: Nc molecules on Ag(100) after flash evaporation. Right: MgO islands.
</div>

By the end of the internship the RF line was calibrated; single-spin resonance was still in progress.

## Methods and tools

- Experiment: LT-STM/STS in UHV at 1.2 K and 300 mK, cryogen handling, sputtering and annealing, on-surface synthesis, molecular evaporation, RF calibration with a VNA.
- Numerics (Python): tight-binding and Zak phase with `sisl`, mean-field Hubbard, exact diagonalization of spin chains with QuTiP, Tersoff–Hamann STM simulations. Code on [GitHub](https://github.com/Landerzl/Numerics-Nanogune).
