# Chapter 2: Trench Formation Physics

## Overview

Trench formation via plasma etching is fundamentally a balance of chemical and physical mechanisms. Fluorine radicals attack silicon and oxide chemically, while energetic ions provide directional bombardment. Understanding both mechanisms enables recipe optimization and ARDE compensation. This chapter quantifies the physics driving trench etch.

**Learning Objectives:**
- Master RIE vs. DRIE etch mechanisms
- Quantify ion bombardment and sputtering yields
- Understand fluorine radical chemistry and temperature dependence
- Model aspect-ratio-dependent etch (ARDE)
- Design recipes balancing etch rate and selectivity

---

## 2.1 RIE vs. DRIE Etch Modes

### 2.1.1 Isotropic Etch (RIE - Low Ion Energy)

```
Isotropic etch characteristics:

Recipe conditions:
  Bias power: Low (<100 W)
  Ion energy: ~20-50 eV
  Pressure: 10-50 mTorr (high, more collisions)
  
Etch mechanism:

  Primary: Neutral radical (F·) attacks Si from all directions
           Rate ∝ [F·] (neutral concentration)
           No directional dependence
           
  Secondary: Low-energy ions enhance radical reactions
             Ion energy insufficient for sputtering
             Mainly chemical assist (heating, bond activation)

Etch profile:

    Mask
     ↓
   ████████ ← No directional control
   ║ ╱╲ ║   ← Undercut beneath mask edge
   ║╱  ╲║   ← Lateral etch significant
   ╚════╝   ← Wide bottom
   
Undercut depth: ~0.2-0.5 × trench depth
(10-20% lateral etch)

Advantages:
  - Simple process (single RF power)
  - Less equipment complexity
  - Good etch uniformity (pressure-dominated)
  
Disadvantages:
  - Poor aspect ratio capability (<5:1 practical limit)
  - Lateral undercut ruins pattern fidelity
  - Not suitable for modern sub-100 nm nodes
  - Mask pattern distortion severe

Historical use:
  90 nm logic: acceptable (low AR ~2:1)
  Modern devices: RARELY used (DRIE preferred)
```

### 2.1.2 Anisotropic Etch (DRIE - High Ion Energy)

```
Anisotropic etch characteristics:

Recipe conditions:
  Bias power: High (300-500 W)
  Ion energy: ~80-150 eV
  Pressure: 5-30 mTorr (lower, less scattering)
  
Etch mechanism:

  Primary: Energetic ion bombardment
           Sputtering yield: ~0.5-1 atom/ion
           Directionality: downward only
           
  Secondary: Radical chemistry assists
             Fluorine radicals still important
             But selectivity set by ion energy (not chemistry alone)

Etch profile:

    Mask
     ↓
   ████████
   ║      ║  ← Nearly vertical walls
   ║      ║  ← Ion-driven directionality
   ║      ║
   ╚══════╝  ← Nearly flat bottom
   
Wall angle: 85-95° (excellent directionality)
Undercut: <5% (minimal lateral etch)
Scalloping: 5-20 nm (cyclic redeposition in pulsed mode)

Advantages:
  - Excellent aspect ratio capability (up to 20:1)
  - Minimal lateral undercut
  - Pattern fidelity preserved
  - Selectivity more predictable
  
Disadvantages:
  - More complex equipment (need ion acceleration)
  - Higher bias power → more thermal load
  - Surface roughness higher (ion bombardment)
  - Selectivity degradation at high ion energy

Modern preference:
  28 nm+: DRIE is standard
  Cryogenic DRIE: Industry standard for advanced nodes
  Enables aspect ratios 10:1 + (requirement for 7 nm+)
```

### 2.1.3 Hybrid CCP/ICP Modes

```
Capacitive vs. Inductive coupling:

CCP (Capacitive Coupling - STI Standard):
  
  Power delivery: Via electrode-to-ground capacitive plates
  Plasma generation: Direct ion acceleration
  Ion flux relationship: φ_ion ∝ √W_bias
  
  Characteristics:
    Higher pressure (5-30 mTorr) for good uniformity
    Lower plasma density (~10⁹-10¹⁰ /cm³)
    Good control of ion energy (via bias power)
    Lower etch rate (~0.5-2 µm/min)
    Better selectivity (chemical component significant)
  
  STI advantage: Selectivity tuning via ion energy

ICP (Inductive Coupling):
  
  Power delivery: Via RF coil around chamber
  Plasma generation: Inductive magnetic field coupling
  Plasma density: ~10¹⁰-10¹¹ /cm³ (10× higher)
  
  Characteristics:
    Lower pressure (1-10 mTorr) for good uniformity
    Higher plasma density (more radicals, more ions)
    Higher etch rate (~5-10 µm/min)
    Lower selectivity (mainly ion-driven)
    Less chemical selectivity tuning
  
  ICP advantage: Speed for deep etch (3D NAND specialty)

Hybrid CCP+ICP:
  
  Combined power delivery:
    Coil power W_coil: Generates plasma density
    Bias power W_bias: Accelerates ions
    Independent control: tune both parameters
  
  Benefit:
    Decouple plasma density from ion energy
    Better control of etch rate (coil) vs. selectivity (bias)
    More flexible process window
    Some advanced STI tools use hybrid approach
```

---

## 2.2 Ion Bombardment & Sputtering Physics

### 2.2.1 Sputtering Yield

Physical removal of atoms by ion impact:

```
Sputtering yield Y (atoms/ion):

Y = Y_max × (E - E_th)ⁿ / (E_max)ⁿ

where:
  E = ion energy (eV)
  E_th = threshold energy (material-dependent)
  E_max = peak energy for yield
  n = exponent (~1.5-2 for most materials)

Material-dependent yields at 100 eV:

Silicon:           Y ≈ 0.8-1.2 atoms/ion
SiO₂ (oxide):      Y ≈ 0.3-0.5 atoms/ion
SiN (nitride):     Y ≈ 0.2-0.4 atoms/ion
Si₃N₄:             Y ≈ 0.4-0.6 atoms/ion

Yield increases with:
  - Higher ion energy (up to peak, then saturates)
  - Lighter ion mass (F⁺ sputter more than Ar⁺)
  - Lower material density (Si sputter more than SiO₂)
  - Elevated temperature (weakens bonds)

Selectivity from yield difference:

  At 100 eV F⁺ ion bombardment:
    Si etch rate: Y_Si × φ_ion ≈ 1.0 × 10¹⁵ ≈ 10¹⁵ atoms/s
    SiO₂ etch rate: Y_SiO₂ × φ_ion ≈ 0.4 × 10¹⁵ ≈ 4×10¹⁴ atoms/s
  
  Selectivity from sputtering alone: Si/SiO₂ ≈ 2.5:1
  
  BUT: Chemical contribution also present
       Actual selectivity Si/SiO₂ ≈ 5-10:1 (higher)
```

### 2.2.2 Ion-Induced Surface Damage

Ion bombardment creates surface roughness and defects:

```
Damage mechanisms:

1. Sputtering cascade
   - Ion creates collision cascade (10-100 nm deep)
   - Atoms knocked out sideways
   - Creates local defects, dislocations
   - Surface becomes rough

2. Ion reflection
   - Some ions reflect elastically (1-2% typical)
   - Reflected ions travel sideways
   - Can cause lateral undercut
   
3. Temperature rise (local)
   - Ion impact releases energy as heat
   - Local temperature rise: ~10-100 K per impact
   - Cumulative heating matters (high flux → warmer)

Surface roughness evolution:

Initial surface:     Ra ~0.5-1 nm (smooth Si)
After 50 nm etch:    Ra ~2-3 nm
After 200 nm etch:   Ra ~5-10 nm
After 500+ nm etch:  Ra ~15-20 nm (rough!)

Roughness scaling with ion energy:

Low E_ion (50 eV):  Ra ~3-5 nm (gentle)
High E_ion (150 eV): Ra ~10-15 nm (aggressive)

Device impact:
  Rough sidewalls → higher leakage (larger interface)
  Rough bottom → voids in CVD fill
  Ra > 10 nm → reliability concerns
```

### 2.2.3 Bias Power and Ion Energy Control

```
Ion energy relationship to bias power:

E_ion ≈ 0.3 × V_bias (eV)

Typical examples:

W_bias = 100 W → V_bias ~200 V → E_ion ~60 eV
W_bias = 300 W → V_bias ~300 V → E_ion ~90 eV
W_bias = 500 W → V_bias ~400 V → E_ion ~120 eV

Linear control:
  ΔV_bias / ΔW_bias ≈ constant
  Allows recipe tuning of E_ion via bias power
  
Practical range:
  Minimum: 50-60 eV (low selectivity but gentle)
  Standard: 80-100 eV (balance)
  Maximum: 150-200 eV (high rate but rough)
  
Temperature correction:

Cryogenic electrode (T = −140°C):
  Electron temperature affected (lower mobility)
  Sheath voltage may increase slightly
  E_ion ≈ 0.32 × V_bias (slightly higher coefficient)
  
Warm electrode (T = +40°C):
  Electron temperature higher (higher mobility)
  Sheath voltage may decrease
  E_ion ≈ 0.28 × V_bias (slightly lower coefficient)
  
Effect: 5-10% variation in E_ion with temperature
        Must account for in cryogenic etch recipes
```

---

## 2.3 Neutral Radical Chemistry

### 2.3.1 Fluorine Radical Generation & Reactions

```
Fluorine radical formation:

In CF₄ or F₂ plasma:
  e⁻ + CF₄ → e⁻ + CF₃ + F·
  e⁻ + F₂ → e⁻ + 2F·
  
  Dissociation requires ~3-5 eV electron energy
  
Radical concentration:
  [F·] ≈ 10¹¹-10¹² /cm³ in bulk plasma
  
Temperature dependence:
  Arrhenius-like: [F·] ∝ exp(-E_a/kT)
  E_a ~5-10 kcal/mol (for dissociation)
  Expected increase: ~5-10% per 5°C warmer
  
  Cryogenic etch (−140°C):
    F· concentration may be 30-50% LOWER than room-T
    Due to slower dissociation kinetics
    Requires higher plasma power to compensate
```

### 2.3.2 Chemical Etch Rates (Radical-Driven)

```
Reaction mechanisms:

Silicon etch:
  Si + 4F· → SiF₄ (volatile, exits chamber)
  
  Activation energy: E_a ~12-15 kcal/mol
  Arrhenius rate: R = A × exp(-E_a/RT)
  
  Measured rates:
    T = 0°C:   R ≈ 40 nm/min
    T = 20°C:  R ≈ 52 nm/min
    T = 40°C:  R ≈ 69 nm/min
    
  Temperature coefficient: ~7% per 5°C

SiO₂ etch:
  SiO₂ + 6F· → SiF₄ + 2OF₂ (both volatile)
  
  Activation energy: E_a ~25-30 kcal/mol (higher!)
  
  Measured rates:
    T = 0°C:   R ≈ 4 nm/min
    T = 20°C:  R ≈ 7 nm/min
    T = 40°C:  R ≈ 14 nm/min
    
  Temperature coefficient: ~12% per 5°C
  (Steeper than Si due to higher E_a!)

Selectivity from E_a difference:

At T = 0°C:   S_Si/SiO₂ = 40/4 = 10:1
At T = 20°C:  S_Si/SiO₂ = 52/7 = 7.4:1
At T = 40°C:  S_Si/SiO₂ = 69/14 = 4.9:1

Trend: Higher temperature → LOWER selectivity
(SiO₂ etch accelerates more due to higher E_a)

This explains cryogenic etch preference:
Cold temperature → higher selectivity
Cold temperature → more protection for SiO₂ layers
```

### 2.3.3 Polymer Formation (Fluorocarbon)

```
Polymer deposition mechanism:

In fluorine-rich plasma:
  CF₄ → CF₃· + F·
  CF₃· recombines at surface
  (CF_x)ₙ polymer builds up
  
Polymer composition:
  Primarily CFₓ with x = 0.5-2 depending on conditions
  Example: CF₀.₈ (intermediate fluorination)
  
Formation sites:
  Si: Little polymer (Si highly reactive to F·)
  SiO₂: More polymer (SiO₂ less reactive)
  SiN: Even more polymer (N creates different chemistry)
  Trench bottoms (cooler): Polymer accumulates
  Trench tops (warmer): Polymer desorbs faster

Polymer layer thickness:
  Transient: Forms and removes cyclically during etch
  Typical thickness: 5-50 nm (depends on recipe)
  Residence time: Milliseconds to seconds

Polymer role in selectivity:
  Acts as protective layer on SiO₂
  Blocks F· attack on oxide
  Removed rapidly by ion bombardment
  Creates cyclic protect-attack mechanism
  
  This is basis of cryogenic etch selectivity!
```

---

## 2.4 Aspect-Ratio-Dependent Etch (ARDE)

### 2.4.1 ARDE Mechanisms

```
Mechanism 1: Radical Depletion

  Deep trenches:
    F· radicals enter trench
    React with Si at trench bottom
    Radicals consumed locally
    Concentration [F·] decreases → bottom
    
  Etch rate ∝ [F·]
  
  Result: Bottom etch slower than top
          Trench fills up slower than widening
          (Aspect ratio increases dynamically!)

Mechanism 2: Radical Shadowing

  Ion/radical trajectories in trench:
    Top of trench: radicals approach from many angles
    Bottom of trench: radicals mostly vertical
                      Some miss (blocked by sidewalls)
                      
  Effective flux reduction:
    F¯_top ≈ F¯_bulk (full flux)
    F¯_bottom ≈ 0.3-0.5 × F¯_bulk (shadowed)
    
  Result: Bottom etches 2-3× slower than top

Mechanism 3: Polymer Redeposition

  Byproducts of Si etch: SiF₄ (gas, exits)
  Byproducts of SiO₂ etch: OF₂, CF_x (some stick to walls)
  
  In deep trenches:
    Byproducts accumulate locally
    Recombine into polymeric layer
    Polymer protects Si from further etch
    (Accidentally creates "mask" in trench!)
    
  Effect: Bottom protected by redeposited polymer
          Etch rate reduced 2-5×

Combined ARDE effect:

  Open area (low AR):     Etch rate = R (baseline)
  Dense 5:1 AR trench:    Etch rate = 0.2R (5× slower!)
  Dense 10:1 AR trench:   Etch rate = 0.1R (10× slower!)
  
  Uniformity impact:
    Wafer center: wide trenches (low AR) → fast etch
    Wafer edge: narrow trenches (high AR) → slow etch
    Result: ±30-50% depth variation without compensation!
```

### 2.4.2 ARDE Compensation Strategies

```
Strategy 1: Pressure Modulation

Higher pressure:
  Shorter mean free path λ = kT/(√2 × π × d² × n)
  More collisions → more mixing
  Radicals diffuse into deep trenches better
  Reduces radical depletion effect
  
  Effect: ARDE variation reduced from 5-10× to 2-3×
  
  Trade-off: Longer process time (slower rate overall)
             May require different ion energy tuning
             
Pressure optimization:
  Low pressure (10-20 mTorr): High ARDE (radical depletion severe)
  Medium pressure (50-80 mTorr): Moderate ARDE (acceptable)
  High pressure (100-150 mTorr): Low ARDE (minimal variation)
  
  Typical choice: 70-100 mTorr (balance)

Strategy 2: Pulsed Plasma

Duty cycle modulation:
  Plasma ON: 10-30 seconds → etch
  Plasma OFF: 10-30 seconds → no etch, wait
  Repeat N times
  
  During OFF time:
    Radicals diffuse into deep trenches (no consumption)
    Polymer inside trenches desorbs (no redeposition)
    Pressure equilibrates
    
  Result: Next etch pulse finds uniform radical distribution
          Deep trenches "catch up" in depth
          ARDE reduced 2-3×
  
  Cost: Process time increases (50%+ longer total)
        Cycle time rises
        Throughput impact: −30-40% wafers/hour

Strategy 3: Multi-Step Recipe

Different conditions per step:
  
  Step 1 (Fast bulk etch): 
    Low pressure, high power → fast rate
    ARDE moderate (acceptable, goal is speed)
    Time: until ~80% of Si removed
  
  Step 2 (Selective slow):
    High pressure, low power → slow rate
    ARDE minimal (selectivity optimized)
    Time: until target depth
    Rate: adjust pressure/power for final uniformity
  
  Combined:
    Total time: slightly longer than constant recipe
    But uniformity much better
    Selectivity controlled in final step
    
Typical result: ±8-10% uniformity (excellent)

ARDE Compensation Summary:

Without compensation:
  ARDE ratio: 5-10:1 (unacceptable)
  Uniformity: ±40-50% (fails)
  
With pressure tuning:
  ARDE ratio: 2-3:1 (marginal)
  Uniformity: ±15-20% (acceptable)
  
With pulsed plasma:
  ARDE ratio: 1.5-2:1 (good)
  Uniformity: ±8-10% (excellent)
  
With multi-step recipe:
  ARDE ratio: 1.5-2:1 (good)
  Uniformity: ±8-10% (excellent)
  Cost: Standard recipe complexity
```

---

## 2.5 Summary & Key Takeaways

1. **RIE vs. DRIE** — Low-energy RIE (isotropic) acceptable for wide trenches; DRIE (anisotropic) required for aspect ratios >5:1; modern nodes use DRIE standard.

2. **Ion Bombardment Dominant** — Bias power (ion energy) controls etch directionality and selectivity; sputtering yield ~0.8 for Si, ~0.4 for SiO₂, creating 2-3× selectivity.

3. **Fluorine Radical Chemistry** — Neutral F· radicals ~10×-100× more abundant than ions; radical concentration temperature-dependent (Arrhenius E_a ~5-10 kcal/mol).

4. **Selectivity from E_a Difference** — Si etch E_a ~12-15 kcal/mol, SiO₂ E_a ~25-30 kcal/mol; temperature-dependent selectivity peak at cryogenic (Si/SiO₂ ~10:1 at 0°C, drops to ~5:1 at 40°C).

5. **Polymer Passivation Critical** — Fluorocarbon polymers form and remove cyclically; protect SiO₂ from F· attack; basis of selectivity in cryogenic etch.

6. **ARDE Fundamental Challenge** — Radical depletion and shadowing cause 5-10× etch rate variation between wide and narrow trenches; pressure/pulsing/multi-step recipes reduce to 2-3× acceptable.

7. **Temperature Amplifies Effects** — Cold electrode reduces F· concentration (~30-50% lower) but increases selectivity dramatically; cryogenic etch trades speed for uniformity and selectivity.

---

**Next Chapter:** [Chapter 3 - Thermal Oxide Growth & Liner Materials](./03-thermal-oxide-growth.md)

**Chapter 2 Development Status:** Complete plasma physics framework  
**Version:** 1.0

