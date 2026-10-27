---
layout: page
title: Superconducting resonator for STM
description: Designing a superconducting λ/4 microwave resonator that is itself the sample of an ESR-STM, with Prof. Nacho Pascual's group. Work in progress.
img: assets/img/cards/resonator.png
importance: 5
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

Starting in October 2026, I am designing and simulating a superconducting microwave resonator for a low-temperature STM, in collaboration with Prof. Nacho Pascual's Quantum Probe Microscopy Group at [CIC nanoGUNE](https://www.nanogune.eu). It builds on the RF work from my [internship there](/projects/3_nanogune/).

## Motivation

In ESR-STM an RF voltage across the tunnel junction drives a single spin at $$h f = g \mu_B B$$, and the signal grows with the RF amplitude at the junction, typically a few to tens of mV. Getting that voltage there is the hard part: the RF travels down meters of cryogenic cabling to the tip, and the [transfer function](/projects/3_nanogune/) of that line is lossy and strongly frequency dependent. Most of the power never reaches the junction, and pushing more in heats the cryostat.

The idea of this project is to turn it around and make **the sample itself a superconducting resonator**.

## Concept: a λ/4 resonator as the sample

The chip carries a coplanar-waveguide (CPW) line, shorted to ground at one end and open at the other. It resonates when its length is a quarter wavelength: the voltage is zero at the short and maximum at the open end. At the open end sits a 100 × 100 µm pad, and **the tip tunnels onto that pad**. The tip is at RF ground through its own capacitance, so the full resonator voltage appears across the junction.

- **Voltage gain.** At resonance the stored energy builds the voltage up by roughly $$\sqrt{Q}$$. With a loaded quality factor $$Q_L = 1000$$, 10 mV at the junction needs about −67 dBm at the chip, around **30 dB less power** than a bare 50 Ω line ending in an open.
- **Target frequency.** 4.5 GHz, which puts the ESR of a $$g = 2$$ spin at $$B \approx 161$$ mT.
- **Material.** Nb covered by Au. The gold protects the surface for STM work and becomes superconducting through the proximity effect, the same Au/Nb platform as the nanoribbons in my internship.

## Why a low Q

Superconducting resonators easily reach $$Q \sim 10^5$$, but here a high Q would be a problem. The tip adds a small capacitance to the open end, and the mode's effective capacitance there is only $$C_\mathrm{eff} = 1/(8 f Z_0) \approx 560$$ fF. A change of just **1 fF shifts the resonance by about 4 MHz**, and the tip–pad capacitance changes whenever the tip moves.

With $$Q_L = 1000$$ the linewidth is 4.5 MHz, so the resonance stays usable as the tip moves; with $$Q = 10^5$$ it would be gone. The loaded Q is therefore set on purpose by the coupling ($$Q_c \approx 1090$$). Internal losses only have to be much smaller: the junction itself limits $$Q_i$$ to about $$1.6 \times 10^4$$ (for $$R_J = 1$$ MΩ), and Nb resonators measured on a test chip gave $$Q_i \geq 6 \times 10^4$$.

The coupling is a galvanic tap: the 50 Ω feedline connects directly to the resonator about 100 µm from the short, where the voltage is small. Moving the tap towards the open end strengthens the coupling, as $$Q_c = \frac{\pi}{4} \frac{R_\mathrm{feed}}{Z_0} \Big/ \sin^2\!\left(\frac{\pi x}{2l}\right)$$.

<div class="row mt-3">
  <div class="col-sm-12 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/resonator/design_results.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Analytical design at 4.5 GHz. Left: coupling Q versus tap position from the short. Centre: RF amplitude at the junction versus input power, compared with a line without resonator. Right: resonance frequency of a fixed-length resonator versus the kinetic-inductance fraction α, for several pad capacitances.
</div>

## The main unknown: kinetic inductance

In a superconductor the Cooper pairs carry momentum, which adds a **kinetic inductance** $$L_k$$ on top of the magnetic one. I parametrise it by $$\alpha = L_k / L_\mathrm{total}$$. It slows the wave down, so the line resonates below its geometric frequency, roughly as $$f \approx f_\mathrm{geo}\sqrt{1-\alpha}$$.

I re-analysed measurements of an earlier Nb test chip with four λ/4 resonators, measured at 50–100 mK. Three of them sit at 0.913–0.917 of their geometric frequency, which gives **α ≈ 0.16** if the substrate is Si. For the proximitised Au/Nb stack, though, α is not known: across α = 0.05–0.25, the same length lands anywhere between 4.2 and 4.8 GHz (right panel above).

## Chip layout

Because of that uncertainty, the first chip carries **four resonators, each designed for 4.5 GHz at a different α** (0.05, 0.12, 0.165 and 0.25). Whatever the real α turns out to be, at least one of them lands within about 120 MHz of the target. At 4.5 GHz that is only a few mT of extra field for the ESR.

<div class="row mt-3">
  <div class="col-sm-12 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/resonator/phase3_layout.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  7.2 × 5 mm chip with four meandered λ/4 CPW resonators (5 µm centre conductor, 2 µm gaps, Z₀ ≈ 50 Ω), 5.7 to 6.4 mm long. Bottom: the tap and short of resonator A, its pad with alignment markers and vortex-pinning holes, and the four pads at the chip centre.
</div>

- **One launcher per resonator.** Off resonance, a tap close to the short looks like a few ohms to ground. On a shared feedline the first tap would short the line for all the others, so each resonator gets its own input.
- **Pads at the centre.** The four pads sit 600–700 µm apart, all within a 1 mm square, so the tip can reach all of them without remounting the chip. L-shaped markers around each pad help find it with the STM.
- **Vortex pinning.** At 161 mT a field perpendicular to the film lets vortices into the superconductor, and moving vortices dissipate RF power. The ground plane is perforated with about 300 000 holes (5 µm, on a 10 µm pitch) that trap the vortices away from the CPW. Holes are kept out of the gaps and the pads.
- **Parametric.** The layout is generated in Python from the analytical model (gdstk to write it, KLayout to check it), so every length and tap position follows from the design parameters and the chip can be regenerated once α and the pad capacitance are known.

## Next steps

- **Electromagnetic simulation.** Finite-element simulations (COMSOL) of the pad capacitance, the tip–pad capacitance and the 3D modes of the chip inside the sample holder, to replace the assumed values in the model.
- **Practical constraints.** Fix the substrate and the Au/Nb thicknesses with fabrication, check how many RF lines the sample holder allows, and settle the field orientation (in-plane is much safer for the superconductor).

_To be continued._
