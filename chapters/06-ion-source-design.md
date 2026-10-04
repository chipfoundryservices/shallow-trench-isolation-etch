# Chapter 6: Ion Source & Energy Control

## Overview

Independent control of ion flux (via coil power) and ion energy (via bias power) is fundamental to STI recipe optimization. This chapter quantifies ion generation mechanisms, energy distribution, and spatial uniformity control.

**Learning Objectives:**
- Understand ion generation in capacitive discharge
- Model ion energy distribution (IED)
- Quantify independent tuning of flux vs. energy
- Design spatial uniformity compensation
- Achieve ±8-10% ion flux uniformity

---

## 6.1 Ion Energy Distribution (IED)

### 6.1.1 Sheath Physics & Ion Acceleration

```
Ion formation in CCP discharge:

Plasma bulk:
  Quasi-neutral region (n_e ≈ n_i, electrically neutral)
  Electron temperature T_e ~1-2 eV (very hot)
  Ion temperature T_i ~0.05 eV (room temperature)
  
Sheath region (near electrode):
  Thin layer (~10-100 µm) where ions are separated from electrons
  Electric field E ≈ V_bias / d_sheath (very strong)
  Ions accelerate in this field

Ion acceleration:

Energy gained by ion crossing sheath:
  E_ion = q × V_bias (full voltage acceleration)
  
But practical formula:
  E_ion ≈ 0.3 × V_bias (for CCP geometry)
  
Reason: Not all ions see full voltage
        Some ions lost to recombination in sheath
        Effective voltage lower than applied

Quantitative relationship:

V_bias = 200 V → E_ion ≈ 60 eV
V_bias = 300 V → E_ion ≈ 90 eV
V_bias = 400 V → E_ion ≈ 120 eV
V_bias = 500 V → E_ion ≈ 150 eV

Coefficient 0.3 typically 0.25-0.35 (depends on geometry)
Cryogenic temperature may shift to 0.32-0.35 (electron mobility changes)
```

### 6.1.2 Ion Energy Distribution Width

```
IED distribution shape:

In CCP discharge: Narrow distribution (FWHM 20-30% of peak)

Typical example:

V_bias = 300 V → E_peak ≈ 90 eV

Distribution:
  Peak: 90 eV (most ions)
  FWHM: ~20 eV (full width at half maximum)
  Range: 70-110 eV (main population)
  Low-energy tail: 50-70 eV (recombining ions)
  High-energy tail: 110-150 eV (secondary acceleration)

Sources of width:

1. Plasma potential variation
   Plasma not perfectly flat
   Some regions slightly different potential
   Ions see different accelerating voltages
   
2. Recombination in sheath
   Some ions created within sheath
   Start from non-zero energy
   See only partial voltage
   
3. Charge exchange collisions
   Ions collide with neutrals
   Exchange charge, change energy
   Creates low-energy tail

Practical impact:

Narrow IED good for:
  - Controlled selectivity (all ions roughly same energy)
  - Reproducible etch rates (less variation)
  
Narrow IED achieved by:
  - CCP geometry (produces naturally narrow IED)
  - Clean plasma (fewer collisions → less broadening)
  - Moderate pressure (50-80 mTorr optimal)
```

---

## 6.2 Independent Ion Flux & Energy Control

### 6.2.1 Flux Generation Mechanism

```
Ion flux relationship to coil power:

Flux generation:
  Coil power W_coil → generates electrons
  Electrons ionize gas (e⁻ + F₂ → F₂⁺ + 2e⁻)
  Ionization rate ∝ electron density
  Electron density ∝ coil power
  
Ionization rate scales:
  Rate ∝ √(W_coil) (square root scaling)
  
  Reason: Electron density increases with power
          But electron temperature also increases
          Combined effect is sublinear (√ scaling)

Quantitative:
  At W_coil = 2000 W: φ_ion ≈ φ₀ (baseline)
  At W_coil = 2500 W: φ_ion ≈ φ₀ × √(2500/2000) ≈ 1.12 × φ₀ (+12%)
  At W_coil = 3000 W: φ_ion ≈ φ₀ × √(3000/2000) ≈ 1.22 × φ₀ (+22%)
  At W_coil = 4000 W: φ_ion ≈ φ₀ × √(4000/2000) ≈ 1.41 × φ₀ (+41%)

Ion flux recipe tuning:

For higher etch rate, increase coil power
For lower etch rate (selectivity), decrease coil power
(But chemical etch rate also affected - not independent!)

Typical range: 1500-3000 W coil power
               φ_ion ranges 0.8-1.3 × baseline
```

### 6.2.2 Independent Ion Energy Control

```
Ion energy via bias power:

E_ion ∝ V_bias ∝ W_bias (linear relationship)

Example:
  W_bias = 300 W → V_bias ≈ 250 V → E_ion ≈ 75 eV
  W_bias = 400 W → V_bias ≈ 333 V → E_ion ≈ 100 eV
  W_bias = 500 W → V_bias ≈ 417 V → E_ion ≈ 125 eV

Linear tunability: Perfect for recipe optimization

Selectivity tuning via E_ion:

Low E_ion (50-70 eV):
  Sputtering yield low
  Chemical selectivity dominates
  Si/SiO₂ selectivity ~8-10:1 (good)
  
Medium E_ion (80-100 eV):
  Balanced (standard production)
  Si/SiO₂ selectivity ~6-8:1 (acceptable)
  
High E_ion (120-150 eV):
  Sputtering yield high
  Physical sputtering dominates
  Si/SiO₂ selectivity ~3-5:1 (poor)
  But faster etch rate (tradeoff)
```

### 6.2.3 Independent Tuning Example

```
Scenario: Current recipe produces poor uniformity
         Dense regions (high AR) etch 50% slower than open areas
         ARDE ratio: 2:1 (unacceptable)

Current conditions:
  W_coil = 2000 W, W_bias = 400 W
  φ_ion = φ₀, E_ion = E₀
  Rate: 1.0 µm/min
  ARDE: 2:1 (because deep features limited by ion flux)
  
Strategy: Increase ion flux to reach deep trenches faster

Modification 1: Increase coil power
  W_coil → 2800 W (40% increase)
  Effect: φ_ion ≈ 1.15 × φ₀ (+15% flux)
  Expected ARDE: 2:1 × (1/1.15) ≈ 1.74:1 (improved!)
  Rate: 1.15 µm/min (faster)
  
Modification 2: Reduce bias power (if selectivity acceptable)
  W_bias → 300 W (25% decrease)
  Effect: E_ion ≈ 0.75 × E₀ (lower energy)
  Expected ARDE: Slightly improved (less sputtering helps)
  Selectivity: Improved (lower E_ion)
  
Combined modifications:
  W_coil: 2000 → 2800 W
  W_bias: 400 → 300 W
  Result:
    ARDE: 2:1 → 1.5:1 (excellent improvement)
    Selectivity: Maintained or improved
    Rate: 1.0 → 1.25 µm/min (acceptable)
    
Implementation: Tune via recipe parameters
               No hardware changes needed
               Demonstrates power of independent control
```

---

## 6.3 Spatial Ion Uniformity

### 6.3.1 Center vs. Edge Ion Energy

```
Radial ion energy variation:

Plasma density non-uniform (higher at center):
  n_e(r) = n_0 × [1 − (r/R)²]
  
  Plasma potential varies with r
  Sheath voltage varies with position
  Ion energy becomes position-dependent

Energy variation:

Center (r = 0):  E_ion(0) = E₀ (maximum)
Mid-radius:      E_ion(r) = 0.95 × E₀ (slight reduction)
Edge (r = R):    E_ion(edge) ≈ 0.85 × E₀ (15% lower)

Impact on etch:

Higher E_ion (center): Slightly faster etch
Lower E_ion (edge): Slightly slower etch
Variation: ±8-10% typical

Microloading combined:

Center has wider trenches (open area) → faster etch
Edge has narrower trenches (high AR) → slower etch
Ion energy also varies → 15% reduction at edge
Combined effect: Center etch 20-30% faster than edge

This compounds uniformity challenge!
```

### 6.3.2 Compensation via Bias Power Tuning

```
Edge power ring concept:

Electrode design with secondary bias:
  Center electrode: Main bias power
  Outer ring electrode: Secondary bias power
  
Ring at different voltage:

If ring voltage higher:
  Edge ions accelerated more
  E_ion(edge) increases
  Compensates for natural decrease
  Result: Uniform E_ion across wafer

Practical implementation:

Main electrode: 400 W bias (E_ion ≈ 100 eV center)
Edge ring: 500 W bias (E_ion ≈ 125 eV edge)

Result:
  Center: 100 eV (baseline)
  Edge: Could be 85 eV (without ring) → adjusted to 95-105 eV (with ring)
  Uniformity: ±5% (excellent!)

Trade-offs:

Advantage:
  Excellent ion energy uniformity
  Improved etch depth uniformity
  
Disadvantage:
  More complex electrode design (cost)
  More power supplies (complexity)
  Tuning more parameters (recipe complexity)
  Maintenance more involved

Most advanced STI tools include edge ring capability
```

---

## 6.4 Cryogenic Ion Behavior

### 6.4.1 Electrode Temperature Effects on Sheath

```
Sheath voltage vs. temperature:

At room temperature (T = 20°C):
  Electron mobility high
  Sheath voltage stable: V_sheath ≈ 0.3 × V_bias
  IED narrow: FWHM ~20 eV
  
At cryogenic (T = −140°C):
  Electrode temperature very cold
  But electrode cooling doesn't cool gas immediately
  Gas still room temperature at first
  Plasma-sheath boundary modified

Effects:

Electron mobility at low T:
  Electrons slower → different drift behavior
  Sheath width may change slightly
  Effective voltage ratio: 0.3 → 0.32-0.35 (±5% increase)
  
Ion temperature:
  Already room temperature (ions heavy, can't be cooled easily)
  Cryogenic electrode doesn't cool ions below sheath
  Ion distribution similar to room-T case

Ice layer on electrode:

At −140°C, water/gas may condense (frost/ice)
  Thin ice layer (~nm-µm) forms on electrode
  Ice layer affects:
    - Sheath formation (different permittivity)
    - Ion reflection (some ions bounce off ice)
    - Effective ion energy (slight reduction)

Practical impact:
  First few wafers at start: Ice building
  Ion energy may drift ±5-10%
  Recipe compensates with first-wafer adjustment
  Stabilizes after electrode is "seasoned"
```

---

## 6.5 Summary & Key Takeaways

1. **Ion Energy ∝ Bias Power** — E_ion ≈ 0.3 × V_bias; linear tunability enables independent selectivity control separate from flux.

2. **Ion Flux ∝ √(Coil Power)** — φ_ion ∝ √W_coil (sublinear); doubling coil power increases flux ~40%; controls ARDE compensation.

3. **Narrow IED Standard** — FWHM ~20-30% of peak typical; CCP geometry naturally produces narrow distribution; preferred for controlled etch.

4. **Spatial Uniformity Challenging** — Center ion energy ~15% higher than edge; combined with microloading creates 20-30% etch variation; edge ring compensation available.

5. **Cryogenic Shifts Ion Energy** — Coefficient 0.3→0.32-0.35 at −140°C; ~5-10% increase in effective ion energy; ice formation adds complexity.

6. **Independent Control Powerful** — Decouple flux (coil) from energy (bias) enables recipe flexibility; adjust for ARDE, selectivity, uniformity without tradeoffs.

7. **Recipe Optimization Path Clear** — High coil for flux (ARDE reduction), variable bias for selectivity (E_ion tuning), edge ring for spatial uniformity.

---

**Next Chapter:** [Chapter 7 - Chamber Materials & Corrosion](./07-chamber-corrosion.md)

**Chapter 6 Development Status:** Complete ion source framework  
**Version:** 1.0

