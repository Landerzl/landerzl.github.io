---
layout: page
title: Superconducting resonator for STM
description: Designing a superconducting λ/4 microwave resonator that is itself the sample of an ESR-STM, with Prof. Nacho Pascual's group. Work in progress.
img: assets/img/cards/resonator.png
importance: 6
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

With $$Q_L = 1000$$ the linewidth is 4.5 MHz, so the resonance stays usable as the tip moves; with $$Q = 10^5$$ it would be gone. The loaded Q is therefore set on purpose by the coupling ($$Q_c \approx 1090$$). Internal losses only have to be much smaller: the junction itself limits $$Q_i$$ to about $$1.6 \times 10^4$$ (for $$R_J = 1$$ MΩ), and resonators on an earlier Al test chip gave $$Q_i \approx (4\text{–}10) \times 10^4$$.

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

α depends strongly on the film and on the line width: narrow lines concentrate the current in less metal. On the earlier 100 nm Al test chip, α is estimated at 5–22 % for the 5 µm lines, depending on the penetration depth, which has not been measured yet. For the proximitised Au/Nb stack, α is simply unknown: across α = 0.05–0.25, the same length lands anywhere between 4.2 and 4.8 GHz (right panel above).

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

## First electromagnetic simulations (COMSOL)

Before simulating my own chip, I checked the simulation method on two resonators from the group's next Al-on-Si test chip: one coupled capacitively to the feedline (open end next to it) and one coupled inductively (shorted end next to it). Both were designed with an analytical 2D model for $$Q_c = 2 \times 10^4$$, so the question was whether a full 3D simulation agrees.

**The model.** A 3D eigenfrequency study in COMSOL (RF Module). The metal is a 2D perfect-conductor sheet on silicon ($$\varepsilon_r = 11.45$$) with air above, inside a closed box, and the feedline ends in a 50 Ω lumped port. The meander is replaced by straight sections of the same length. With lossless metal and substrate, the only way energy can leave the resonator is through the port, so the quality factor of the complex eigenfrequency, $$Q = f'/(2f'')$$, is directly $$Q_c$$. Kinetic inductance is added afterwards as $$f = f_\mathrm{PEC}\sqrt{1-\alpha}$$.

**The mesh is the hard part.** The field sits in gaps a few µm wide along a line several mm long. My first run, with coarse layers above and below the metal, put the resonance 50 % too high: the mesh could not resolve the field in the gaps, so the line's capacitance came out too small. With thin layers at the metal plane (first layer about 1 µm) the resonance moved to the expected place. Refining further, from one to two elements across each gap, lowered $$f$$ by 2.5 % and changed $$Q_c$$ by only 2 %.

<div class="row mt-3">
  <div class="col-sm-12 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/resonator/comsol_geometry_ind.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Simplified geometry of the inductively coupled resonator. Left: the full model, with the 50 Ω port at x = 0. Right: the coupling region, where the resonator's shorted end runs parallel to the feedline for 262 µm.
</div>

| Coupling | $$f_\mathrm{PEC}$$, 3D | $$f_\mathrm{PEC}$$, analytical | $$Q_c$$, 3D | $$Q_c$$, design |
| --- | --- | --- | --- | --- |
| Capacitive | 5.434 GHz | 5.33 GHz | $$2.2 \times 10^4$$ | $$2.0 \times 10^4$$ (+10 %) |
| Inductive | 5.247 GHz | 5.15 GHz | $$1.37 \times 10^4$$ | $$2.0 \times 10^4$$ (−32 %) |

- **Frequency.** Both come out about 2 % above the analytical value, consistent with the remaining mesh error.
- **Capacitive coupling** agrees with the 2D model within its expected accuracy.
- **Inductive coupling** is stronger than designed, equivalent to a mutual inductance of about 12.5 pH instead of 10.3 pH. The likely reason is that the resonator's short sits right next to the feedline: its current returns through the 5 µm ground strip between the two lines and adds magnetic coupling that the 2D model leaves out. The simplified geometry matters most exactly there, so this is worth repeating with the real layout.

To make sure the right mode is the resonator, I looked at the field of each eigenmode. Only one has a high Q, and its field is concentrated along the resonator, strongest at the open end; the next mode up is the feedline itself resonating, damped in less than a cycle by the port.

<div class="row mt-3">
  <div class="col-sm-12 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/resonator/comsol_modes_ind.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Electric field (log scale) in the metal plane for two eigenmodes of the inductively coupled model. Left: the resonator mode, maximal at the open end and vanishing at the short. Right: a feedline mode, with the resonator dark.
</div>

For my own chip this matters directly: the galvanic tap near the short is closer to the inductive case, where the 2D model underestimated the coupling.

## Next steps

- **Simulate my chip.** Run the same eigenfrequency model on the Au/Nb layout to get $$f$$ and $$Q_c$$ of each tapped resonator, and electrostatic simulations of the pad and tip–pad capacitance, to replace the assumed values in the analytical model.
- **Practical constraints.** Fix the substrate and the Au/Nb thicknesses with fabrication, check how many RF lines the sample holder allows, and settle the field orientation (in-plane is much safer for the superconductor).

_To be continued._
