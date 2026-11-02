---
layout: page
title: Electric fields on the NV center
description: How a DC electric field acts on the NV⁻ center in diamond, from symmetry and finite-field DFT on diamond clusters to a predicted shift of the excited-state anticrossing.
img: assets/img/cards/nv_efield_en.png
importance: 4
category: research
---

<style>
  article p,
  article li,
  .caption {
    text-align: justify;
    hyphens: auto;
  }
</style>

A numerical project I started in September 2026, at the suggestion of Prof. Jorge Casanova (EHU), following the NV review by [Doherty _et al._, Phys. Rep. 528, 1 (2013)](https://doi.org/10.1016/j.physrep.2013.02.001). It is ongoing; the write-up is a working draft.

## The question

NV centers are used to sense electric fields through the Stark effect. In the standard room-temperature spin Hamiltonian of the optically excited state ³E, an electric field only multiplies the identity: it shifts the optical line but leaves the spin structure alone. I did not take that for granted. The project asks which field–spin couplings the symmetry of the defect allows, how large they are when computed from first principles, and which measurement could see them.

## Symmetry

Starting from the molecular-orbital picture of the defect (the a₁′, a₁, eₓ, e_y orbitals of the dangling bonds around the vacancy), I worked out which terms coupling the electric field to the spin are allowed by the C₃ᵥ point group and time reversal, in the ground state ³A₂ and in the excited state ³E, to first and second order in the field.

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    <div class="row">
      <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/nv-efield/orbitals_dft_en.png" class="img-fluid rounded z-depth-1" zoomable=true %}
      </div>
      <div class="col-sm mt-3 mt-md-0 d-flex align-items-center">
        {% include figure.liquid loading="eager" path="assets/img/nv-efield/levels_scheme_en.png" class="img-fluid rounded z-depth-1" zoomable=true %}
      </div>
    </div>
  </div>
</div>
<div class="caption">
  Left: defect orbitals a₁′, a₁, eₓ and e_y of the NV⁻ center from DFT (C₃₃NH₃₆⁻ cluster, B3LYP). Right: their occupation in the ground state ³A₂ and the excited state ³E.
</div>

## Finite-field DFT

I model the NV⁻ center in hydrogen-terminated diamond clusters of increasing size (C₃₃NH₃₆⁻, C₈₅NH₇₆⁻, C₁₆₃NH₁₀₀⁻) with spin-unrestricted DFT in PySCF (PBE and B3LYP). The electric field enters the electronic Hamiltonian as a dipole term, and the self-consistent field is solved with the field already included, so the orbital response is not perturbative. Coefficients come from symmetric finite differences at several field strengths, extrapolated to zero field. Because derivatives of Kohn–Sham levels at fields of ~10⁻⁴ a.u. are sensitive to SCF noise, every point is converged to an orbital gradient below 10⁻⁷, and the sign convention is checked with the Hellmann–Feynman theorem.

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nv-efield/clusters_en.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  The three diamond clusters around the NV center: nitrogen in amber, the vacancy dashed, its three carbon neighbors in dark gray.
</div>

A transverse field splits the e pair linearly, as the symmetry analysis predicts, and the induced charge density shows where the response comes from: the size of the coupling is controlled by the polarization between the a₁ and e orbitals inside the defect, which partly screens the applied field.

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nv-efield/stark_ks_en.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Shift of the defect Kohn–Sham levels under fields along x, y and z (C₃₃NH₃₆⁻, B3LYP): a transverse field splits the e pair linearly; an axial field shifts e relative to a₁.
</div>

<div class="row mt-3">
  <div class="col-sm-6 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nv-efield/induced_density_en.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Charge density induced by a field along z (top) and along x (bottom), in a symmetry plane and in the plane of the three carbon atoms.
</div>

## The excited state

For ³E, I build each orbital component with ΔSCF, keeping the excited configuration with the initial maximum overlap method (IMOM). The vertical excitation energy comes out at 1.88 eV, inside the range of earlier DFT calculations, and the excitation stays localized on the defect. On top of that I compute the spin–spin zero-field splitting from the spin density, the Jahn–Teller relaxation of the excited state, the ionic contribution to the field coupling, and the second-order terms in the field.

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nv-efield/stark_es_en.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  ΔSCF energies of the two ³E components under transverse and axial fields, and the ³E–³A₂ transition energy compared with the Hellmann–Feynman slope.
</div>

## From numbers to a measurement

The computed couplings feed a Lindblad model of the NV center at room temperature, including the excited-state level anticrossing (ESLAC) and nuclear spin polarization. The prediction: an axial electric field shifts the ESLAC by about 3.3 G per MV/cm. That is small but measurable with polarity modulation of the field and lock-in detection, using the ground-state Stark shift as an in-situ calibration and the GSLAC, which barely moves, as a control.

<div class="row mt-3">
  <div class="col-sm-8 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nv-efield/eslac_shift_en.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Predicted effect of an axial electric field on the ESLAC: (a) the photoluminescence dip, (b) the differential signal under polarity reversal, (c) the shift of the dip against the field, (d) an ensemble with both NV polarities, where the effect cancels.
</div>

## Tools

Python with PySCF (UKS, ΔSCF/IMOM, zero-field-splitting tensors), geomeTRIC for relaxations, QuTiP for the Lindblad dynamics, and pytest for the numerical checks. The report is written in LaTeX.
