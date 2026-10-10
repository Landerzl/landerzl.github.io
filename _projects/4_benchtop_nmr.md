---
layout: page
title: Bench-top NMR
description: A home-built NMR spectrometer aimed at portable ¹⁹F detection of PFAS. RF hardware and ML-based signal enhancement.
img: assets/img/nmr/nmr_block_diagram.png
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

At [Qubiz.team](https://qubiz.team), a deep-tech start-up in Bilbao (Jun. – Dec. 2025).

## The problem

PFAS (per- and polyfluoroalkyl substances, the "forever chemicals") are persistent pollutants. Their carbon chains are covered in fluorine, and <sup>19</sup>F NMR gives them a distinctive spectroscopic fingerprint. The goal of the project was a portable, field-deployable NMR sensor that uses that fingerprint.

<div class="row mt-3">
  <div class="col-sm-6 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/nmr/perfluoroalkyl.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  A perfluoroalkyl chain. Every fluorine atom contributes to the <sup>19</sup>F NMR signal.
</div>

## The hardware

I built RF components of a home-built NMR spectrometer. The sample sits in a solenoid coil inside a C-shaped electromagnet, which provides the static field $$B_0$$; the coil applies the oscillating field $$B_1$$ and picks up the signal. A tuning and matching network connects the coil to a Tx/Rx duplexer, which routes the excitation pulses from the RF transceiver to the coil and the received signal to a low-noise preamplifier, followed by digitization and processing. The design also includes a microwave source and waveguide for hyperpolarization (DNP) of the sample.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/nmr/nmr_block_diagram.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Block diagram of the spectrometer: magnet and sample coil, tuning and matching network, Tx/Rx duplexer, low-noise preamplifier and RF transceiver, plus the microwave line for hyperpolarization.
</div>

## Signal processing

I tested classical machine-learning methods to improve the quality of the NMR signal.

## Related work at Qubiz.team

- Early-stage studies of quantum sensing devices for the biomedical, automotive and electrical industries.
- NV-centre pressure sensing, which became a follow-on project.
