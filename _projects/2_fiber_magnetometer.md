---
layout: page
title: Fiber-based NV magnetometer
description: Building and calibrating a fiber-coupled NV-center magnetometer at Qubiz.team. CW-ODMR with oscilloscope and lock-in detection.
img: assets/img/magnetometer/odmr_stability_1h.png
importance: 3
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

At [Qubiz.team](https://qubiz.team) (Bilbao, Sep. 2026 – present) I am building and calibrating a fiber-based optical quantum sensing setup for magnetic field sensing, based on NV centers in diamond read out through an optical fiber.

## The setup

A 520 nm laser (up to 120 mW) excites the NV centers through the fiber, and the returning photoluminescence (PL) goes to a photodetector and transimpedance amplifier. A microwave synthesizer sweeps the frequency across the NV resonance near 2.87 GHz, with an RF switch to modulate the microwaves. The signal is read either directly on an oscilloscope or with a lock-in amplifier (Moku). The laser is controlled from Python.

When the microwaves hit the resonance, the PL drops: that dip is the optically detected magnetic resonance (ODMR) signal, and its position shifts with the magnetic field.

## Phase 0: CW-ODMR at zero field

Before adding the coils for a controlled bias field, I characterized the system at zero field, aiming for the largest slope of the ODMR dip, since that sets the magnetic sensitivity.

- **Laser power.** Higher power gave more contrast; at 120 mW the dip reaches about 1.2%, against about 0.15% at 60 mW. Power also broadens the line, so the choice is a trade-off between contrast and linewidth.
- **Microwave power.** Swept from −25 to −5 dBm; −10 dBm became the working point.
- **Averaging.** Compared the number of frequency sweeps, from 5 to 20, and denser sampling around the resonance.
- **Background drift.** Checked whether the ferromagnetic optical table affected the measurement (the drift did not depend on position) and traced the slow background drift to laser stability.
- **Stability.** Ran continuous ODMR for an hour to check that the resonance stays put.

<div class="row mt-3">
  <div class="col-sm-9 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/magnetometer/odmr_laser_power.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  ODMR at zero field for decreasing laser power: the contrast drops from about 1.2% at 120 mW to about 0.15% at 60 mW.
</div>

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/magnetometer/odmr_lorentzian_fit.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/magnetometer/odmr_stability_1h.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Left: normalized ODMR signal with a Lorentzian fit and residuals. Right: consecutive ODMR spectra over one hour of continuous measurement (offset for clarity).
</div>

## Oscilloscope vs. lock-in detection

To reject noise, I set up lock-in detection: the microwaves are switched on and off at 1 kHz and the PL is demodulated at that frequency. Getting a clean signal took some troubleshooting:

- checked the RF modulation and the power after the RF switch;
- adjusted the demodulation phase to minimize the quadrature component, and later recorded both quadratures (X and Y) to correct the phase numerically;
- increased the low-pass filter slope from 12 to 24 dB/octave and raised the microwave power to −10 dBm, which reduced the noise and improved the contrast.

I then compared both detection schemes over the same frequency window (2820–2930 MHz, 1 MHz steps), varying the number of up and down sweeps.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/magnetometer/odmr_oscilloscope.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/magnetometer/odmr_lockin.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Zero-field ODMR around 2.87 GHz, averaged over up and down sweeps. Left: oscilloscope readout, voltage shift and contrast (about 1.5%). Right: lock-in readout, demodulated X signal and estimated PL contrast.
</div>

## Next: the coils

The next phase is characterizing the coils that will apply a controlled bias field: comparing the measured field per unit current with the Helmholtz value $$B = (4/5)^{3/2} \mu_0 n I / R$$, mapping homogeneity over the fiber volume with a Hall probe, and measuring resistance, inductance, heating, current-source stability and bandwidth (the $$L/R$$ time constant and eddy currents in the metal mounts).

## Also at Qubiz.team

I designed and simulated microwave waveguides for hyperpolarization setups in Ansys HFSS and COMSOL RF.
