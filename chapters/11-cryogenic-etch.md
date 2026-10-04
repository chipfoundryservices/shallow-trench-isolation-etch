# Chapter 11: Cryogenic Etch Mechanisms

## Overview

Cryogenic etch (−140°C) transforms selectivity via polymer passivation dynamics. This chapter quantifies the mechanisms making cold etch superior, models polymer formation/removal cycles, and addresses unique challenges like ice formation.

**Learning Objectives:**
- Understand polymer passivation layer dynamics
- Model temperature-dependent selectivity quantitatively
- Recognize polymer deposition and desorption cycles
- Design cryogenic etch recipes
- Manage ice formation at −140°C

---

## 11.1 Passivation Layer Formation & Role

### 11.1.1 Polymer Deposition Mechanism

```
Polymer source in fluorine plasma:

CF₄ dissociation:
  e⁻ + CF₄ → e⁻ + CF₃ + F·
  e⁻ + CF₄ → e⁻ + CF₂ + 2F·
  
CF_x fragment recombination:
  CF₃ + CF₃ → C₂F₆ (difluoroethane, gas)
  CF₂ + CF₂ → (CF₂)_n polymer (solid, redeposits)
  
Polymer composition:
  Primarily C-F based oligomers
  General formula: (CF_x)_n where x ≈ 1-2
  Soft, waxy polymer (not like hard carbon film)

Deposition sites:

On Si surface:
  F· radicals attack Si vigorously
  Si + 4F· → SiF₄ (escapes)
  Polymer cannot accumulate (radical etches Si faster than polymer can build)
  
On SiO₂ surface:
  F· radicals react slowly with SiO₂
  SiO₂ + 6F· → SiF₄ + 2OF₂ (slower reaction)
  Time window for polymer to deposit
  Polymer builds as C-F layer (~5-50 nm)
  
In trench interior (cool region):
  Further from plasma heating
  Temperature lower → polymer less likely to desorb
  Polymer accumulates on sidewalls and bottom

Temperature dependence of deposition:

At room temperature (20°C):
  Polymer formation rate: ~10 nm/minute
  Desorption rate: ~5 nm/minute
  Net accumulation: ~5 nm/minute
  
At cryogenic (−140°C):
  Polymer formation rate: ~10 nm/minute (unchanged, driven by radical flux)
  Desorption rate: ~0.5 nm/minute (100× slower, very cold!)
  Net accumulation: ~9.5 nm/minute (accelerated!)
  
Result: At −140°C, polymer accumulates 2× faster than room-T

Polymer thickness evolution:

Time 0−10 sec: 0−10 nm (rapid initial deposition)
Time 10−30 sec: 10−30 nm (accumulation continues)
Time 30−60 sec: 30−50 nm (may plateau as diffusion limits replenishment)
Time 60+ sec: 40−60 nm steady-state (equilibrium reached)

This thick polymer at low T provides excellent selectivity!
```

### 11.1.2 Selectivity Mechanism: Polymer Protection

```
How polymer creates selectivity:

SiO₂ protection:

Without polymer:
  F· radicals reach SiO₂
  Etch rate: ~5 nm/min
  
With 20 nm polymer layer:
  Polymer blocks F· access
  F· can't reach SiO₂ directly
  Etch rate: ~0.5 nm/min (10× reduction!)
  
Si etching unaffected:

Polymer cannot protect Si (Si beneath polymer still reacts)
  F· on Si surface: Attacks polymer first
  Polymer ablates (removed by F· + ion bombardment)
  Beneath: Si exposed and etches at normal rate
  
Cyclic mechanism:

1. Polymer deposits on SiO₂ (protecting it)
2. Polymer deposits on Si too (temporarily blocking)
3. Ion bombardment sputters polymer off Si (but not off SiO₂ as easily)
4. Si exposed, etches rapidly
5. SiO₂ still protected by polymer
6. Cycle repeats

Result:
  Si: Etches at high rate (polymer removed by ions)
  SiO₂: Etches slowly (polymer protection active)
  Selectivity: Si/SiO₂ = 10-20:1 (excellent!)
  
This is why cryogenic etch works!
```

### 11.1.3 Temperature-Dependent Selectivity Quantitative Model

```
Selectivity vs. temperature:

Three competing effects:

1. Polymer deposition rate T-dependent
   At lower T: More polymer accumulation
   At higher T: Less polymer (faster desorption)

2. Chemical etch rate (from Chapter 2)
   Si: E_a ~12-15 kcal/mol
   SiO₂: E_a ~25-30 kcal/mol
   At higher T: SiO₂ accelerates MORE than Si (higher E_a)
   
3. Ion sputtering contribution
   More effective at higher E_ion
   Higher T may increase E_ion slightly (sheath effects)

Combined model:

S(T) = [R_Si,chem(T) + Y_Si × φ_ion] / [R_SiO₂,chem(T) × P(T) + Y_SiO₂ × φ_ion]

where:
  P(T) = polymer protection factor
  P(T_room) ≈ 0.2 (polymer reduces SiO₂ etch 5×)
  P(T_cryo) ≈ 0.05 (polymer reduces SiO₂ etch 20×)
  P increases with T (thinner polymer at higher T)

Quantitative selectivity values:

T = −140°C: S ≈ 25-30:1 (excellent, thick polymer protection)
T = −100°C: S ≈ 20:1 (still good)
T = 0°C:    S ≈ 15:1 (acceptable)
T = +20°C:  S ≈ 10:1 (marginal)
T = +40°C:  S ≈ 6:1 (poor, thin polymer)

Production choice:

For Si/SiO₂ selectivity >15:1 needed:
  Must use T < 0°C (at least)
  Cryogenic (−140°C) provides margin (25:1 typical)
  
For Si/SiN selectivity (alternative liner):
  Polymer less effective on SiN (N changes chemistry)
  Selectivity Si/SiN: ~5:1 at −140°C (weaker protection)
  But still better than room-T (~2:1)
```

---

## 11.2 Ion-Assisted Polymer Removal

### 11.2.1 Ion Bombardment of Polymer Layer

```
Ion sputtering of polymer:

Polymer yield: Y_polymer ≈ 0.5-1 atom/ion (moderate sputtering)
Compared to: Y_Si ≈ 0.8, Y_SiO₂ ≈ 0.4

Example: 100 eV F⁺ ion

Flux: φ_ion = 10¹⁵ ions/cm²/s
Y_polymer ≈ 0.7 atoms/ion

Sputtering rate:
  R = Y × φ_ion × M / (ρ × N_A)
  R ≈ 0.7 × 10¹⁵ × 20 / (1.5×10²³) ≈ 10 nm/min

Polymer removal dynamics:

Polymer thickness: 20 nm
Ion sputtering rate: 10 nm/min
Removal time: ~2 minutes of ion bombardment

BUT: Polymer forming simultaneously!

Steady state:
  Polymer formation: ~5 nm/min (at −140°C)
  Polymer removal: ~10 nm/min (ion sputtering)
  Net: Formation < Removal
  Equilibrium: Polymer thickness ~10-15 nm (steady)
  
This prevents runaway polymer buildup!
```

### 11.2.2 Cyclic Formation-Removal at Low Temperature

```
Pulsed etch cycle (40% duty cycle):

ON phase (20 sec):
  Plasma active, radicals + ions
  Polymer forms + is sputtered simultaneously
  Thickness equilibrium: ~15 nm
  Net etching: Si fast (~2 µm/min - radicals)
              SiO₂ slow (~0.2 µm/min - polymer protection)
  Selectivity: ~10:1 maintained
  
OFF phase (30 sec):
  Plasma off, no ions, radicals decay
  No new polymer forming (no ions to prevent deposition)
  BUT: Existing polymer can desorb if warm enough
  At −140°C: Desorption extremely slow
  Most polymer remains
  
Next ON phase:
  Polymer still present (SiO₂ still protected)
  Selectivity maintained
  
Benefit:
  Pulsing doesn't degrade selectivity (polymer persists)
  But allows radical diffusion into deep trenches (fixes ARDE)
  
Cost: Process time increases ~40% (OFF time overhead)
Trade: ARDE compensation worth the time penalty
```

---

## 11.3 Ice Formation at Cryogenic Temperature

### 11.3.1 Condensation & Ice Layer

```
Cryogenic electrode at −140°C:

Surrounding gas:
  Electrode extremely cold
  Gas molecules that touch electrode: Stick (condense)
  H₂O vapor from air: Condenses first
  CF₄/F₂ gas: Some condenses at extreme cold
  
Ice/frost layer formation:

Thin ice forms on electrode surface:
  Thickness: 1-10 µm typical
  Grows over time (each day of operation)
  Composition: H₂O (primary) + trace CF₄/F₂
  
Physical properties:
  Hard, icy surface (not protective, but changes impedance)
  Different permittivity than Al
  May change RF coupling efficiency slightly
  
Practical impact:

First wafer loaded:
  Fresh ice layer
  RF impedance slightly different
  Tuning network needs small adjustment
  Not a problem, just different baseline
  
After 100 wafers:
  Ice layer thickens
  Impedance drifts
  May need retune
  
Weekly maintenance:
  Manual defrost cycle (warm electrode briefly)
  Ice sublimes away
  Reset to baseline state
  Or: Continuous dry N₂ purge (prevents ice formation)
```

### 11.3.2 Water Vapor Prevention Strategies

```
Moisture control strategies:

Strategy 1: Dry gas supply
  Use dry O₂ or dry CF₄ (dried via desiccant cartridge)
  Minimize water vapor in plasma
  Result: Less ice formation (~50% reduction)
  Cost: Gas drying system ~$5-10K
  
Strategy 2: Dry nitrogen purge
  When plasma off: Inject dry N₂
  Purges moisture from chamber
  Prevents ice between etch cycles
  Result: Minimal ice formation
  Cost: N₂ gas consumption (~$100/month)
  
Strategy 3: Periodic warm-up
  Heat electrode to 0°C for 5-10 minutes (weekly)
  Ice sublimes away
  Re-cool to −140°C
  Result: Controlled ice buildup
  Cost: Slight extra energy, time (~30 min/week downtime)
  
Combined (recommended):
  Dry gas supply + periodic warm-up
  Result: Minimal ice, stable operation
  Cost: ~$50/week
  Benefit: Consistent RF coupling, predictable tuning
```

---

## 11.4 Cryogenic Recipe Design

### 11.4.1 Selectivity-Optimized vs. Rate-Optimized

```
Two recipe approaches:

Selectivity-Optimized:
  Temperature: −140°C (coldest, thickest polymer)
  Selectivity: 25-30:1 (excellent)
  Rate: Slower (cold slows chemistry)
  Example:
    Si etch: 30 nm/min
    SiO₂ etch: 1 nm/min
    Time for 80 nm resist: 160 sec
  
Rate-Optimized:
  Temperature: 0°C (warmer, more etch)
  Selectivity: 15:1 (acceptable)
  Rate: Faster (warm accelerates chemistry)
  Example:
    Si etch: 50 nm/min
    SiO₂ etch: 3.5 nm/min
    Time for 80 nm resist: 96 sec
  
Difference: 64 sec per wafer = 40% slower with −140°C!

Production choice:

High-volume (throughput critical):
  Use 0°C, 15:1 selectivity
  Faster, acceptable margin
  
Advanced node (selectivity critical):
  Use −140°C, 25-30:1 selectivity
  Margin huge, safe
  Accept throughput penalty
```

---

## 11.5 Summary & Key Takeaways

1. **Polymer Passivation Core Mechanism** — CF_x polymer deposits 2× faster at −140°C vs. room-T (slower desorption); creates SiO₂ protection layer reducing etch rate 10-20×.

2. **Selectivity Temperature-Critical** — Si/SiO₂ selectivity 25-30:1 at −140°C, drops to 10:1 at 20°C; polymer protection increases by factor ~5 as temperature decreases 160°C.

3. **Ion Sputtering Cycle Maintains Equilibrium** — Polymer formation (~5 nm/min) balanced by ion sputtering (~10 nm/min) prevents runaway buildup; steady-state ~15 nm polymer thickness.

4. **Pulsed Etch Preserves Selectivity** — OFF-time radical decay doesn't desorb polymer at −140°C (too cold); selectivity maintained while allowing radical diffusion for ARDE compensation.

5. **Ice Formation Manageable** — H₂O condenses on −140°C electrode; 1-10 µm ice layer forms; mitigated by dry gas supply or periodic warm-up cycle.

6. **Selectivity-Rate Trade-off** — Coldest etch (−140°C) gives 25-30:1 selectivity but ~40% slower; warmest cryogenic (0°C) gives 15:1 selectivity but 40% faster; choose based on node requirements.

---

**Next Chapter:** [Chapter 12 - Liner Integrity During Etch](./12-liner-integrity.md)

**Chapter 11 Development Status:** Complete cryogenic mechanism framework  
**Version:** 1.0

