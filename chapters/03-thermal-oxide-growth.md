# Chapter 3: Thermal Oxide Growth & Liner Materials

## Overview

After trench etch, a thin oxide liner is grown thermally to create the isolation dielectric. This chapter covers thermal oxidation physics (Deal-Grove model), liner material properties, and interface chemistry critical to isolation quality.

**Learning Objectives:**
- Understand Deal-Grove thermal oxidation model
- Quantify SiO₂ liner growth kinetics
- Recognize SiN liner properties and trade-offs
- Model interface charge accumulation
- Design liner specifications for target isolation performance

---

## 3.1 Deal-Grove Model of Thermal Oxidation

### 3.1.1 Linear and Parabolic Growth Phases

```
Deal-Grove oxidation model:

Assumption: Oxidation limited by diffusion of O₂ through oxide layer
           O₂ must travel through already-formed oxide to reach Si
           
Reaction sequence:
  1. O₂ arrives at oxide surface
  2. O₂ diffuses through SiO₂ layer (slow step!)
  3. O₂ reacts with Si at Si/SiO₂ interface: Si + O₂ → SiO₂
  4. New oxide layer forms
  5. Process repeats for next O₂ molecules

Growth rate equation:

d(X_ox)/dt = B / (2×X_ox + 2×C)

where:
  X_ox = oxide thickness (nm)
  B = parabolic rate constant
  C = linear rate constant
  
Solution with boundary condition X_ox = 0 at t = 0:

X_ox = (B/2) × [√(1 + 4Ct/B) − 1]

Limiting cases:

1. Short time (early oxidation):
   4Ct/B << 1 → X_ox ≈ C × t (LINEAR PHASE)
   Growth proportional to time
   
2. Long time (late oxidation):
   4Ct/B >> 1 → X_ox ≈ √(B × t) (PARABOLIC PHASE)
   Growth proportional to √t
   Diffusion is rate-limiting

Physical interpretation:

Linear phase (early):
  - Oxide thin (<10 nm)
  - O₂ diffusion fast (short path)
  - Reaction at Si/SiO₂ interface rate-limiting
  - Rate ∝ exp(-E_a,rx/RT) reaction kinetics
  
Parabolic phase (late):
  - Oxide thick (>50 nm)
  - O₂ diffusion slow (long path through oxide)
  - Diffusion is rate-limiting
  - Rate ∝ D × (C_O2_interface) diffusion constant
```

### 3.1.2 Temperature Dependence & Kinetics

```
Arrhenius temperature dependence:

B = B₀ × exp(-E_a,B / RT)
C = C₀ × exp(-E_a,C / RT)

where:
  E_a,B ≈ 1.3 eV (parabolic activation energy)
  E_a,C ≈ 0.5 eV (linear activation energy)

Practical growth rates:

Temperature: 800°C (standard for STI)

At t = 30 minutes oxidation:
  X_ox ≈ 8-12 nm (typical STI liner)
  
At t = 60 minutes:
  X_ox ≈ 12-18 nm (thicker liner)
  
Temperature: 900°C (faster oxidation)
At same times: X_ox ~1.5-2× thicker (faster kinetics)

Rate increase with temperature:

T = 800°C:  Rate ≈ R (baseline)
T = 850°C:  Rate ≈ 1.5-2× R (30% increase)
T = 900°C:  Rate ≈ 2-2.5× R (accelerated)

Typical STI choice: 850°C
  Good kinetics (not too slow)
  Good uniformity (diffusion controlled)
  Thermal budget manageable (device stress)
```

### 3.1.3 Oxide Thickness Control

```
Process control for STI liner:

Target liner thickness: 5-20 nm (depends on device requirements)
Typical specification: ±1-2 nm (tight tolerance!)

Thickness vs. oxidation time:

Time: 5 min    → X_ox ≈ 3-4 nm
Time: 15 min   → X_ox ≈ 8-10 nm (standard STI)
Time: 30 min   → X_ox ≈ 12-15 nm
Time: 60 min   → X_ox ≈ 15-20 nm

Wafer-level uniformity:

Edge vs. center:
  Center: Access to furnace heat/gas good → faster oxidation
  Edge: Lower temperature (cooler zone) → slower oxidation
  Variation: 5-15% thickness variation typical (edge ~90% of center)
  
Management:
  Furnace design (radiant heaters around periphery)
  Boat/carrier optimization (ensure uniform temperature)
  Rotation during oxidation (averages local temperature variation)
  Target: ±5% uniformity (edge/center <10% difference)

Die-level uniformity:

Open area vs. dense trench area:
  Open area: Full oxidation exposure
  Dense trench area: Limited O₂ access (diffusion-limited)
  Typical: Dense areas ~5-10% thinner
  
Mitigation:
  Extended oxidation time (ensures dense areas saturated)
  Slightly higher temperature (increases diffusion rate)
  Alternative: Use post-oxidation anneal (time-temperature optimization)
```

---

## 3.2 SiO₂ Liner Properties

### 3.2.1 Oxide Physical & Chemical Properties

```
SiO₂ properties (thermally grown, high quality):

Crystal structure:
  Amorphous SiO₂ (no crystal order)
  Si-O bonding: Tetrahedral coordination (Si surrounded by 4 O)
  O-Si-O angles: ~109° (tetrahedral)
  Density: ~2.2 g/cm³ (less dense than Si ~2.33)

Refractive index:
  n ≈ 1.46 (visible light)
  Enables optical inspection (color change after oxidation visible!)
  
  Si: Shiny, metallic appearance
  5-10 nm SiO₂: Purple-ish (interference color)
  10-20 nm SiO₂: Cyan-ish (interference color)
  20-30 nm SiO₂: Brownish (interference color)
  
  Practical: Color under 405 nm lamp indicates oxidation thickness
  Used for rapid wafer inspection

Dielectric constant:
  κ = 3.9 (compared to Si₃N₄ κ = 7-8)
  Capacitance C = κ × ε₀ × A / t
  Thinner SiO₂ → higher capacitance (for same area)
  
  Example (28 nm node):
    SiO₂ 10 nm between adjacent trenches
    Area: 50 nm × 1 cm = 50 nm·cm
    C = 3.9 × 8.85e-12 × 50nm / 10nm ≈ 1.7 pF/cm

Thermal properties:
  Thermal conductivity: ~0.01 W/cm·K (very poor!)
  Specific heat: ~1 J/g·K
  Coefficient of thermal expansion (CTE): ~0.5 ppm/°C
  
  Implications:
    Poor heat dissipation (insulates electrode from cooling)
    Large CTE mismatch with Si (2.6 ppm/°C) → thermal stress
    Stress ~50-100 MPa at 100°C temperature swing
```

### 3.2.2 Oxide/Silicon Interface Quality

```
Si/SiO₂ interface formation:

Oxidation reaction:
  Si + O₂ → SiO₂
  
  Interface chemistry:
    Si-Si bonds break
    Si-O bonds form
    Oxygen atoms inserted
    
  Interface sharpness:
    Sub-monolayer resolution
    Abrupt transition (Si crystalline → SiO₂ amorphous)
    Interface width: <1 nm (extremely sharp)

Dangling bonds at interface:

  After oxidation:
    Some Si atoms still have dangling bonds (unsatisfied)
    Density: ~10¹² /cm² typical (one per ~100 nm²)
    
  These dangling bonds become trap states:
    Can trap electrons
    Can trap holes
    Can cause leakage current
    Can shift device threshold voltage

Interface trap density (D_it):

Quality measure: Density of states at Si/SiO₂ interface
Units: states/cm²/eV

High-quality furnace oxide (thermal growth):
  D_it ≈ 10¹⁰ /cm²/eV (excellent, low trap density)
  Reason: Slow thermal process allows interface reconstruction
  
Plasma-grown oxide (lower quality):
  D_it ≈ 10¹¹-10¹² /cm²/eV (higher, more traps)
  Reason: Fast deposition doesn't allow interface optimization
  
Device impact:
  Trap density affects subthreshold swing
  Trap density affects leakage current (trap-assisted tunneling)
  Thermal oxidation preferred for STI (best quality)
```

### 3.2.3 Post-Oxidation Annealing

```
Annealing process:

After forming oxide layer, wafer annealed:
  Temperature: 850-950°C
  Atmosphere: N₂ or N₂/O₂ blend
  Time: 5-30 minutes
  
Purpose: Improve interface quality

Mechanisms:

1. Interface reconstruction:
   Dangling bonds at Si/SiO₂ interface reorient
   Some bonds satisfy (Si-Si distances adjust)
   Interface trap density improves: 10¹² → 10¹⁰ /cm²/eV
   
2. Hydrogen passivation:
   If anneal in N₂/H₂ blend: H atoms arrive at interface
   H passivates dangling bonds: Si-H stable, low energy
   Further reduces trap density
   (However, STI typically uses N₂ only, not H₂)

3. Residual stress relief:
   Oxidation introduces Si-O compressive stress
   Annealing allows atomic rearrangement
   Stress partially relieved
   Reduces cracking risk at interface
```

---

## 3.3 SiN Liner Alternative

### 3.3.1 Silicon Nitride Properties

```
Si₃N₄ (Silicon Nitride) characteristics:

Stoichiometry:
  Si₃N₄: 3 Si atoms per 4 N atoms
  Actually SiₓNᵧ where x/y varies 0.7-1.3 (non-stoichiometric)
  
Crystal structure:
  Hexagonal or cubic forms possible
  CVD-grown typically amorphous or mixed phases
  
Dielectric constant:
  κ ≈ 6-8 (higher than SiO₂ κ = 3.9)
  Higher κ → higher capacitance for same thickness
  Effect: Increased parasitic capacitance (but sometimes desired for stress tuning)

Refractive index:
  n ≈ 1.9-2.0 (higher than SiO₂, more visible color difference)
  Colors after deposition very distinctive

Thermal properties:
  Thermal conductivity: ~0.02-0.04 W/cm·K (still poor, ~2-3× SiO₂)
  CTE: ~2-3 ppm/°C (closer to Si 2.6 ppm/°C than SiO₂)
  
  Implication: Lower CTE mismatch stress than SiO₂
             Better for thermal cycling stability

Hardness & Mechanical:
  Very hard (similar to SiO₂)
  Good mechanical strength
  Lower wet-etch rate than SiO₂ (more stable in wet processing)
```

### 3.3.2 SiN vs. SiO₂ Trade-offs

```
Comparison in STI context:

Etch selectivity challenge:

SiO₂ liner:
  Si etch rate: ~2 µm/min
  SiO₂ etch rate: ~0.2-0.4 µm/min (during trench etch)
  Selectivity Si/SiO₂: ~5-10:1
  Protection: Good (oxide erodes slowly)

SiN liner:
  Si etch rate: ~2 µm/min (unchanged)
  SiN etch rate: ~0.05-0.1 µm/min (MUCH slower!)
  Selectivity Si/SiN: ~20-30:1 (EXCELLENT!)
  Protection: Superior (nitride almost not attacked)

Advantage of SiN: Much better selectivity during etch

Disadvantage of SiN:

1. Etch selectivity becomes TOO good
   → May need special recipe for SiN removal later
   → Additional process step
   
2. Stress issues:
   SiN has compressive stress (thin film property)
   Creates stress layer on wafer surface
   Can cause device threshold voltage shift (intentional in some cases)
   
3. Interface quality:
   Si/SiN interface has more defects than Si/SiO₂
   D_it ≈ 10¹¹-10¹² /cm²/eV (worse than SiO₂)
   More leakage current possible

4. Cost:
   SiN deposition more complex (CVD process)
   More expensive than thermal oxidation

Decision: When to use SiN vs. SiO₂

Use SiO₂ (standard):
  - Most planar logic (90-28 nm)
  - When device doesn't require stress tuning
  - Standard process (easier control)

Use SiN:
  - Advanced nodes (7 nm FinFET) — want stress tuning
  - High-density 3D NAND — need selectivity
  - When selective etch of SiN later is acceptable
  - Advanced device requires specific dielectric constant
```

---

## 3.4 Interface Chemistry & Contamination

### 3.4.1 Oxide Trapping & Charge Accumulation

```
Oxide traps vs. interface traps:

Interface traps (at Si/SiO₂ boundary):
  Discussed above: dangling bonds, ~10¹⁰-10¹² /cm²
  
Oxide traps (within SiO₂ volume):
  Defects inside oxide layer
  Can store charges
  Density: ~10¹⁶-10¹⁷ /cm³ typical
  
Charge accumulation mechanisms:

1. Electron trapping:
   Electrons from Si conduction band may enter oxide
   Trapped by oxide defect sites
   Becomes stuck (charge remains)
   
2. Hole trapping:
   Holes from Si valence band may enter oxide
   Trapped in oxide defects
   Becomes stuck
   
3. Ion contamination:
   Mobile ions (Na⁺, K⁺, H⁺) in oxide
   Can drift under electric field
   Accumulate at Si/SiO₂ interface
   Create ionic charge layer

Device impact:

Charge accumulation → changes electric field in oxide
→ Threshold voltage shift
→ Leakage current variation
→ Device mismatch (adjacent cells have different Vt)
```

### 3.4.2 Contamination Sensitivity

```
Common contaminants in STI:

After etch:
  - Resist residue (carbon, polymers)
  - Etch byproducts (SiF₄, OF₂ deposits)
  - Photoresist remnants

Cleaning (RCA clean) removes most of these

But some contamination can survive:

Metal contamination:
  - Cu, Fe, Ni from tool surfaces
  - Typically <10¹² atoms/cm² acceptable
  - Above 10¹³ /cm²: causes leakage increase
  
Organic residue:
  - Photoresist polymers (C,H,O)
  - Typically removed by O₂ plasma ashing
  - Traces may remain (<1% coverage acceptable)
  
Oxide contaminants:
  - Native oxide on Si surface (before oxidation)
  - Should be <0.5 nm (cleaned off before oxidation)
  - Thicker oxide: interferes with quality oxidation
  - RCA clean SC1 specifically removes native oxide

Impact on oxidation:

Native oxide pre-existing:
  → May create defects at Si/SiO₂ boundary
  → Lower oxide quality
  → Higher trap density (worse device performance)

Metal contamination in oxide:
  → Creates deep traps in oxide
  → Trap-assisted tunneling leakage
  → Device leakage increases significantly

Organic residue:
  → Voids/gaps in oxide
  → Reduced oxide thickness locally
  → Leakage paths
  → Yield loss

Prevention: Clean Before Oxidation

RCA sequence:
  Step 1: SC1 (Piranha: H₂SO₄ + H₂O₂)
          Oxidizes and removes organics
          Removes native oxide
  
  Step 2: Water rinse (dilute, remove contaminants)
  
  Step 3: SC2 (Weak HCl + H₂O₂)
          Removes metallic contamination
  
  Step 4: Water rinse
  
  Result: Pristine Si surface, ready for oxidation
          Device-quality oxide produced
```

---

## 3.5 Summary & Key Takeaways

1. **Deal-Grove Model Predicts Kinetics** — Linear phase (thin oxide, reaction-limited) transitions to parabolic phase (thick oxide, diffusion-limited); accurate to ~±20% for STI range.

2. **Temperature Tightly Controls Thickness** — E_a ≈ 0.5-1.3 eV means ±50°C furnace variation → ±30-40% thickness change; thermal control critical for ±1 nm specifications.

3. **Interface Quality Crucial** — High-quality thermal oxide (D_it ~10¹⁰) required; plasma-grown oxide (D_it ~10¹²) inferior; annealing improves interface trap density.

4. **SiO₂ Preferred Standard** — Lower CTE mismatch, better interface quality, lower cost; SiN used in advanced nodes for stress tuning and superior selectivity.

5. **Contamination Fatal** — Native oxide >0.5 nm, metal >10¹³ /cm², organics >1%: all degrade oxide quality and increase leakage; RCA clean mandatory.

6. **CTE Mismatch Creates Stress** — SiO₂ CTE 0.5 ppm/°C vs. Si 2.6 ppm/°C → 50-100 MPa stress at 100°C swing; SiN (2-3 ppm/°C) lower stress.

---

**Next Chapter:** [Chapter 4 - Isolation Performance & Electrical Properties](./04-isolation-performance.md)

**Chapter 3 Development Status:** Complete thermal oxidation and liner framework  
**Version:** 1.0

