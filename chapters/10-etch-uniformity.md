# Chapter 10: STI Etch Uniformity & ARDE

## Overview

Aspect-ratio-dependent etch (ARDE) is the fundamental challenge in STI uniformity. Deep narrow trenches etch slower than wide trenches, creating non-uniform depth. This chapter quantifies ARDE, models compensation strategies, and develops multi-step recipes for ±8-10% uniformity.

**Learning Objectives:**
- Understand ARDE mechanisms (radical depletion, shadowing, redeposition)
- Quantify etch rate variation vs. aspect ratio
- Design pressure-based ARDE compensation
- Develop pulsed plasma recipes for uniformity
- Model multi-step process windows

---

## 10.1 ARDE Mechanisms (Quantitative)

### 10.1.1 Radical Depletion Model

```
Radical depletion mechanism (primary ARDE driver):

In deep trench:

   Gas inlet ╬
             │
   Radical   │ ← F· from showerhead
   flux      │
             │  High [F·] at top
             │
             │  F· consumed at bottom
             │  [F·] decreases
        ╭────────╮
        │ SiO₂   │  ← Low [F·] here
        │ trench │  (depleted by etch)
        │        │
        └────────┘

Flux depletion model:

At top of trench:
  [F·] = [F·]_bulk (full concentration)
  R_top = k × [F·]_bulk
  
At depth z:
  [F·](z) = [F·]_bulk × exp(−z/λ_diff)
  
  λ_diff = diffusion length ≈ 100-200 µm (in gas)
  
  But at z = 200 nm (trench depth):
  exp(−200 nm / 150 µm) ≈ 1 (essentially no depletion!)
  
Wait... this model suggests no depletion for typical trench depths.
Why then does ARDE occur?

Answer: Radical generation rate < radical consumption rate in trench

  Radical generation: Limited by plasma density above trench
                     Can only enter from opening
                     
  Radical consumption: Every radical that reaches bottom reacts
                       R ∝ [F·]
                       
  Result: Net consumption faster than replenishment
         Depletion inevitable
         
Effective depletion length:

For realistic etch:
  λ_eff ≈ Diffusion length / (reaction rate / diffusion rate)
  
  Ratio ~100 (reaction faster than diffusion can replenish)
  
  λ_eff ≈ 100-200 µm / 100 ≈ 1-2 µm
  
  At 200 nm trench depth:
  [F·](200 nm) ≈ [F·]_bulk × (1 − 200 nm / 2 µm)
              ≈ [F·]_bulk × 0.9 (10% depletion)
  
  At deep 3D NAND trench (1 µm):
  [F·](1 µm) ≈ [F·]_bulk × (1 − 1 µm / 2 µm)
           ≈ [F·]_bulk × 0.5 (50% depletion!)

ARDE ratio from depletion:

R_top / R_bottom = [F·]_bulk / [F·](depth)
                 = 1 / (1 − depth/λ_eff)

Example: λ_eff = 1 µm, normal trench 200 nm

  R_ratio = 1 / (1 − 0.2) = 1.25 (25% slower at bottom)

Example: λ_eff = 1 µm, dense 3D NAND 1 µm

  R_ratio = 1 / (1 − 1) = infinite! (etch stops?)
  
Actually, R doesn't go to zero. Other mechanisms prevent.
```

### 10.1.2 Radical Shadowing & Ion Effects

```
Shadowing mechanism:

In narrow trench (width W < diffusion distance):

Radical approach angle distribution:
  Near opening: radicals approach from many angles
  Deeper in trench: radicals blocked by sidewalls
  
Effective flux reduction:

For cylindrical trench (width W, depth D):
  Geometric view factor V_f = (W / W + D)

Example:
  W = 50 nm, D = 200 nm
  V_f = 50 / 250 = 0.2 (only 20% of radicals reach bottom!)
  
  W = 100 nm, D = 200 nm
  V_f = 100 / 300 = 0.33 (33% reach bottom)

ARDE ratio from shadowing:

Wide opening (W >> D):  V_f → 1, R ≈ R_bulk
Narrow trench (W = D):  V_f = 0.5, R ≈ 0.5 × R_bulk
Deep narrow (D = 10W):  V_f = 0.1, R ≈ 0.1 × R_bulk (10× slower!)

Combined depletion + shadowing:

Effective ARDE:
  R_eff = R_bulk × [F·](D) / [F·]_bulk × V_f
  
For typical case (D = 200 nm, W = 50 nm):
  [F·] depletion: 0.9
  V_f shadowing: 0.2
  Combined: R_eff = R_bulk × 0.9 × 0.2 = 0.18 × R_bulk
  
  ARDE ratio: 1 / 0.18 ≈ 5.5:1
  
This matches experimental observation (5-10× ARDE typical)!

Ion contribution to ARDE:

Ions: Less affected by depletion/shadowing
      Higher directed velocity
      More likely to reach trench bottom
      
Ion contribution at trench bottom: ~80% of top
Chemical contribution: ~50% of top (from depletion + shadowing)

Total: 0.8 × I_ions + 0.5 × R_chem ≈ 0.65 × (I_ions + R_chem)

This is why biasing helps reduce ARDE:
Higher bias → more ion contribution (less affected by depletion)
Result: smaller ARDE ratio (better uniformity)
```

### 10.1.3 Polymer Redeposition

```
Polymer formation in trenches:

Source: Etch byproducts (SiF₄, OF₂) recombine
        Fluorocarbon polymers form from CF fragments
        
Deposition sites:
  Preferentially in trenches (cooler than open areas)
  Accumulates on sidewalls and bottom
  Thickness increases with etch time
  
Polymer protection mechanism:

At trench bottom:
  Polymer layer: 5-20 nm thick
  Blocks F· attack on Si
  Etch rate effectively zero where polymer thick
  
At trench opening:
  Warmer temperature
  Polymer desorbs faster
  Balance between formation and removal
  
Result: Bottom protected by polymer more than top
       ARDE effect amplified

Polymer thickness vs. aspect ratio:

Low AR (W = D):      Polymer ~5 nm (less accumulation)
                     ARDE from depletion: ~2-3×
                     
Medium AR (D = 4W):  Polymer ~15 nm (moderate)
                     ARDE from depletion + redeposition: ~5-8×
                     
High AR (D = 10W):   Polymer ~25+ nm (significant)
                     ARDE from all effects: ~10-20×

Cryogenic effect on polymer:

At −140°C:
  Polymer desorption rate extremely low
  Polymer accumulates heavily
  Can create ARDE inversion (bottom etches FASTER than expected!)
  Counterintuitive but experimentally observed
  
Solution: Temperature pulsing
          Periodically raise electrode T to 20°C
          Polymer desorbs
          Resume etch
          (Complicates recipe, but necessary for extreme AR)
```

---

## 10.2 ARDE Compensation Strategies

### 10.2.1 Pressure Modulation Approach

```
Pressure effect on mean free path:

λ_mfp = kT / (√2 × π × d² × n)

At low pressure (10 mTorr):
  λ_mfp ≈ 1-2 mm (large!)
  Ballistic transport dominates
  Radicals travel straight
  Shadowing severe
  ARDE: 8-10×
  
At medium pressure (50-80 mTorr):
  λ_mfp ≈ 100-200 µm (intermediate)
  Mixed ballistic-diffusive
  Some radical scattering
  Radicals reach deep trenches better
  ARDE: 3-5× (improved!)
  
At high pressure (100-150 mTorr):
  λ_mfp ≈ 10-50 µm (small)
  Diffusive transport dominates
  Radicals randomly scattered
  Access to deep trenches easier
  ARDE: 1.5-2× (excellent!)

Trade-off: Higher pressure → better uniformity BUT slower etch

Example recipe optimization:

Standard low-pressure etch:
  P = 30 mTorr, Rate = 1.5 µm/min
  ARDE ratio = 8:1 (terrible)
  Uniformity ±40% (fails)
  
High-pressure compensated:
  P = 100 mTorr, Rate = 0.8 µm/min (45% slower)
  ARDE ratio = 2:1 (good)
  Uniformity ±10% (acceptable)
  
Total time increase: (200 nm / 0.8 µm/min) / (200 nm / 1.5 µm/min)
                   = 2.5 min / 1.3 min ≈ 1.9× longer
                   
Cost of uniformity: Nearly 2× process time
                   Throughput: 20 wafers/hr → 10 wafers/hr
```

### 10.2.2 Pulsed Plasma ARDE Compensation

```
Pulsed plasma concept:

Plasma ON:  10-30 seconds (etch)
Plasma OFF: 10-30 seconds (wait/diffusion)
Repeat N times

Physics during OFF period:

While plasma off:
  No ion bombardment (ions recombine)
  No new radical generation
  But existing radicals diffuse into trenches
  Polymer inside trenches desorbs (no fresh formation)
  Pressure equilibrates (no consumption)
  
Trench filling effect:

Wide open area:
  Radical concentration rises to bulk value [F·]_bulk
  (Nothing consuming them)
  
Deep narrow trench:
  Was depleted to [F·]_deep
  During OFF, new radicals diffuse in
  Concentration rises toward [F·]_bulk
  After 10-20 sec OFF: [F·]_deep ≈ 0.7-0.8 × [F·]_bulk
  
Next etch pulse:

Start with better-filled deep trenches
Etch rate more uniform than continuous etch
ARDE effect reduced!

Pulsing efficiency:

Continuous etch: ARDE = 5:1
Pulsed (50% duty cycle): ARDE ≈ 2-3:1 (2-3× improvement!)

Cost: Process time increases

Time 1: Etch ON: 2 min
Wait: 2 min
Etch ON: 2 min
Wait: 2 min
Total: 8 min (vs. 2 min continuous)

Throughput penalty: 4× longer
But uniformity improves 2-3×

Trade-off acceptable for:
  - Critical devices (yield-sensitive)
  - 3D NAND (extreme AR)
  - High-reliability applications
```

### 10.2.3 Multi-Step Recipe (Industry Standard)

```
Three-step approach:

STEP 1: Fast bulk etch (aggressive)
  Power: High (W_coil = 2500 W, W_bias = 400 W)
  Pressure: Low-medium (50 mTorr)
  Time: Until ~70-80% of resist removed (60-100 nm consumed of ~200 nm total)
  
  Characteristics:
    Rate: ~1.5 µm/min (fast)
    ARDE ratio: ~3-5:1 (acceptable, goal is speed)
    Selectivity: Moderate (~5-10:1 Si/SiO₂)
    
  Goal: Remove most resist quickly, establish uniformity baseline

STEP 2: Transition (moderate conditions)
  Power: Medium (W_coil = 2000 W, W_bias = 350 W)
  Pressure: Medium-high (80 mTorr)
  Time: Until ~95% removed (additional 30-40 nm)
  
  Characteristics:
    Rate: ~0.8 µm/min (moderate)
    ARDE ratio: ~2:1 (good)
    Selectivity: Improved (~10-15:1)
    
  Goal: Fine-tune uniformity, reduce ARDE effect

STEP 3: Final trim (conservative)
  Power: Lower (W_coil = 1800 W, W_bias = 250 W)
  Pressure: High (100 mTorr)
  Time: Until complete removal (final <10 nm)
  
  Characteristics:
    Rate: ~0.4 µm/min (slow, selective)
    ARDE ratio: ~1.5:1 (minimal)
    Selectivity: Excellent (~15-20:1)
    
  Goal: Complete removal with maximum selectivity
         Ensure SiO₂ protection

Combined result:

Total time: ~3-4 min (reasonable throughput)
Effective ARDE: ~2:1 (weighted average, good)
Effective selectivity: ~10:1 (protected SiO₂)
Uniformity: ±8-10% (acceptable, excellent balance)

Throughput: ~15-20 wafers/hour (production-viable)
```

---

## 10.3 Pressure-Dependent Etch Kinetics

### 10.3.1 Quantitative Pressure Dependence

```
Etch rate vs. pressure model:

R(P) = R_0 × (P_ref / P)^n

where n ≈ 0.5-0.8 (exponent for radical-limited etch)

Physical interpretation:
  Low n (~0.5): Radical-limited (depletion dominant)
  High n (~0.8): Transport-limited (diffusion important)

Practical examples (Si etch rate):

At baseline (P = 70 mTorr): R_0 = 1.0 µm/min

P = 50 mTorr:  R ≈ 1.0 × (70/50)^0.6 ≈ 1.21 µm/min (+21%)
P = 100 mTorr: R ≈ 1.0 × (70/100)^0.6 ≈ 0.83 µm/min (−17%)
P = 150 mTorr: R ≈ 1.0 × (70/150)^0.6 ≈ 0.64 µm/min (−36%)

Selectivity vs. pressure:

Si/SiO₂ selectivity increases with pressure:

P = 50 mTorr:  Si/SiO₂ ≈ 4:1 (lower selectivity)
P = 70 mTorr:  Si/SiO₂ ≈ 6:1 (baseline)
P = 100 mTorr: Si/SiO₂ ≈ 8:1 (good selectivity)
P = 150 mTorr: Si/SiO₂ ≈ 10-12:1 (excellent)

Reason: SiO₂ etch more pressure-sensitive than Si
       Higher P → higher diffusion to SiO₂ surface
       But SiO₂ also gets better polymer protection
       Net: Selectivity improves at high P
```

### 10.3.2 Microloading Effects

```
Microloading at different length scales:

Die-level microloading:
  Isolated region (wide trenches): Fast etch
  Dense region (narrow trenches): Slow etch
  Variation: 5-10% typical
  
Wafer-level microloading:
  Center (more open area): Faster etch
  Edge (higher trench density): Slower etch
  Variation: 10-15% typical
  
Combined: Center etch 20-30% faster than edge
         Recipe must compensate

Compensation via process design:

Approach 1: Power variation
  Center: Lower power (slow etch)
  Edge: Higher power (fast etch)
  
  Limitation: Power non-uniform in chamber
             Hard to implement precisely
             
Approach 2: Pressure tuning
  Microloading less sensitive to pressure
  High-pressure etch reduces microloading difference
  
Approach 3: Multi-step with different microloading optimum
  Step 1: Conditions optimize for overall uniformity
  Step 2: Conditions optimize for edge compensation
  
  Result: Die-level and wafer-level uniformity balanced

Microloading specification:

Acceptable: ±10-15% microloading
           (die-level <10%, wafer-level <15%)
           
Excellent: ±5-8% microloading
          (requires careful recipe optimization)
```

---

## 10.4 Summary & Key Takeaways

1. **ARDE Root Causes** — Radical depletion (~30-50% concentration drop), shadowing (view factor ~0.1-0.3), polymer redeposition (~5-20 nm accumulation); combined effects create 5-10× rate variation.

2. **Pressure Modulation Effective** — Higher pressure (100+ mTorr) reduces ARDE 2-3×; cost: ~50% slower etch rate; trade-off between uniformity and throughput.

3. **Pulsed Plasma Powerful** — ON/OFF cycling allows radical diffusion into trenches; 50% duty cycle reduces ARDE 2-3×; cost: 4× longer process time; used for critical applications.

4. **Multi-Step Standard Practice** — Step 1 (fast bulk), Step 2 (transition), Step 3 (selective finish); achieves ±8-10% uniformity and 10-15:1 selectivity; ~3-4 min/wafer typical.

5. **Selectivity Improves at High Pressure** — Si/SiO₂ selectivity increases from ~4:1 at 50 mTorr to ~10:1 at 150 mTorr; enables SiO₂ protection without extra plasma chemistry tricks.

6. **Microloading Inevitable** — Die-level and wafer-level microloading combined creates 20-30% etch rate variation; multi-step recipes and pressure tuning mitigate but don't eliminate.

7. **Cryogenic Adds Complexity** — At −140°C, polymer accumulation extreme; may require temperature pulsing to avoid inversion; adds recipe complexity for advanced nodes.

---

**Next Chapter:** [Chapter 11 - Cryogenic Etch Mechanisms](./11-cryogenic-etch.md)

**Chapter 10 Development Status:** Complete ARDE framework with quantitative models  
**Version:** 1.0

