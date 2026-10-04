# Chapter 14: STI Etch Profile Control

## Overview

Trench sidewall angle, scalloping, and corner rounding are critical to device performance and fill reliability. This chapter quantifies profile defects, their device impact, and design strategies for controlled vertical etching.

**Learning Objectives:**
- Understand sidewall angle physics and measurement
- Quantify scalloping mechanisms and effects
- Model corner rounding and its yield impact
- Design recipes for controlled profiles
- Verify profile quality via metrology

---

## 14.1 Sidewall Angle Control

### 14.1.1 Vertical Profile Physics

```
Ideal STI trench profile:

Perfectly vertical sidewalls:
  Angle: 90° (perpendicular to substrate)
  Undercut: <5% lateral vs. depth
  Profile: Rectangular

Actual achievable:

With good DRIE (energetic ions):
  Angle: 88-92° (nearly vertical)
  Undercut: 1-3% lateral
  
With marginal CCP (lower directivity):
  Angle: 80-95° (variable)
  Undercut: 5-10% lateral
  
With room-temperature isotropic RIE:
  Angle: 45-60° (very sloped)
  Undercut: 30-50% lateral
  
Modern STI (standard):
  Angle: 90 ± 2° (nearly perfect)
  Undercut: <2% typical
```

### 14.1.2 Ion Bombardment Directionality

```
How ions achieve vertical etching:

Ion energy and direction control:

High-energy ions (>50 eV):
  Travel mostly downward (from electrode below)
  Straight trajectory (few collisions)
  Impact normal to surface (90° incidence)
  Sputter Si effectively
  Sidewall ions mostly glancing blows (low sputtering)
  
Result: Bottom etches fast, sidewalls slow
         Vertical profile maintained!

Low-energy ions (<20 eV):
  More diffusive
  Hit sidewalls more easily
  Sputter sidewalls laterally
  Create undercut

Temperature effect:

Cold temperature (−140°C):
  Ion mobility lower
  Ions travel more straight
  Fewer lateral impacts
  Better verticality
  
Warm temperature (+20°C):
  Ion mobility higher
  More sidewall bombardment
  More undercut
  Worse verticality (80-85° instead of 90°)

Production specification:

Sidewall angle: 90 ± 3° (acceptable)
Process control: 90 ± 1° (target for consistency)
```

---

## 14.2 Scalloping Phenomena

### 14.2.1 Scalloping Mechanism

```
What is scalloping?

Periodic surface roughness on trench sidewalls:
  Wavelength: 10-50 nm (depends on ion energy, pressure)
  Amplitude: 5-20 nm (peak-to-valley)
  Pattern: Regular, repeating peaks and valleys
  
Cause: Ion-induced surface rippling

Physical mechanism:

Small surface irregularities form (random nucleation)
Ions preferentially sputter peaks (more exposed to ion beam)
Valleys become sheltered (less sputtering)
Ripples grow larger over time
Wavelength set by ion energy and mass
  Lower E_ion → longer wavelength (~50 nm)
  Higher E_ion → shorter wavelength (~10 nm)

Formation rate:

Time for scallops to grow:

Initial roughness: <1 nm (smooth surface)
After 50 nm Si etch: ~5-10 nm scallops (small)
After 200 nm Si etch: ~15-20 nm scallops (large)
After 500 nm Si etch: Plateau at ~20-25 nm (maximum)

Scallop formation is inevitable in DRIE!
```

### 14.2.2 Impact on Device Performance

```
Sidewall roughness effects:

Si/SiO₂ interface area increases:
  Smooth: A = depth × width (baseline)
  Scalloped: A = depth × width × (1 + roughness factor)
  
  For 20 nm scallops on 200 nm depth trench:
  Roughness factor ~0.2-0.3 (20-30% area increase)
  
Trap site increase:
  More interface → more traps
  Interface trap density: D_it ∝ Area
  Per-cell trap density increases ~20-30%
  
Leakage current increase:
  Trap-assisted tunneling: J_TAT ∝ D_it
  Leakage per cell increases ~20-30%
  
Yield impact:

Spec: Leakage <100 pA/cell
With smooth sidewalls: 50 pA/cell (good margin)
With 15 nm scallops: 70-80 pA/cell (still OK)
With 25+ nm scallops: 100-120 pA/cell (marginal, risk)

Production acceptance:
  Scallops <15 nm: Excellent (preferred)
  Scallops 15-20 nm: Acceptable (marginal)
  Scallops >20 nm: Problematic (rework required)
```

### 14.2.3 Scallop Reduction Strategies

```
Approach 1: Pulsed plasma

ON/OFF duty cycle:

  Plasma ON: 5 sec (etch + create small scallops)
  Plasma OFF: 5 sec (wait, no sputtering)
  
During OFF:
  No new ions hitting surface
  Surface ripples partially relax (ion beam gone)
  Scallops don't grow continuously
  
Result: Smaller scallops (~50% reduction)

Cost: Process time increases (duty cycle overhead)
      ~2× longer for similar depth

Trade-off: Smoother sidewalls but slower

Approach 2: Higher pressure

Higher pressure → shorter mean free path
  Ions scattered more
  Less directed bombardment
  Sidewalls hit at wider angles
  Scalloping mechanism less effective
  
At 100+ mTorr:
  Scallops ~50% smaller
  But ARDE worse (must compensate)
  
Approach 3: Cryogenic temperature

At −140°C:
  Lower ion energy (coefficient 0.32 vs. 0.30 at room-T)
  Scallop wavelength longer (harder to form short wavelength)
  Overall reduction ~30-40%
  Plus: Better selectivity (bonus!)
```

---

## 14.3 Corner Rounding

### 14.3.1 Mask and Plasma Corner Effects

```
Mask corner rounding:

Photoresist mask pattern:
  Ideal: Sharp 90° corners (infinitely sharp)
  Real: Rounded corners (mask diffraction limit)
  
Corner radius from lithography:
  90 nm node: 50-100 nm corner radius (2.5D lithography)
  28 nm node: 30-50 nm corner radius
  7 nm node: 20-40 nm corner radius
  
Cause: Diffraction, resist exposure/development blur

Plasma corner rounding (over-etch):

At mask corner:
  Plasma slightly over-etches
  Rounds corner further
  Additional rounding: 50-100 nm typical
  
Total corner radius:
  Mask: 50 nm + Plasma: 50 nm = 100 nm total
  
Effect on final device:
  Trench nominally 50 nm wide
  With 100 nm corner radius: Effective width increased!
  Creates capacitive coupling between adjacent trenches
  
Yield impact:

Excess corner rounding →
  Higher parasitic capacitance
  Longer RC delays
  Noise coupling between cells
  Device performance degraded
  
Specification:
  Corner radius: <30 nm (preferred)
  <50 nm (acceptable)
  >70 nm (problematic, rework risk)
```

### 14.3.2 Profile Measurement

```
TEM cross-section (gold standard):

Procedure:
  Wafer cut perpendicular to trench
  Thin sample prepared (100 nm thick)
  Viewed in transmission electron microscope
  Direct observation of profile
  
Measurements possible:
  Sidewall angle: ±1° accuracy
  Scallop amplitude: ±2 nm accuracy
  Corner radius: ±5 nm accuracy
  Undercut depth: Direct visualization
  
Cost: ~$500-1000 per measurement (expensive)
Time: 1-2 days turnaround

SEM profile imaging (faster):

Scanning electron microscope (angled view):
  Sample cross-section at 45° angle
  Electron beam scans sidewall
  3D reconstruction of profile
  
Accuracy: ±3-5 nm (adequate for most spec)
Cost: ~$100-300 per measurement
Time: Few hours turnaround

CD-SEM (critical dimension metrology):

Automated measurement of trench width:
  Optical or e-beam based
  Non-destructive (no sample prep)
  Fast measurement
  
Measures: Top width, bottom width, depth
Accuracy: ±5 nm
Cost: ~$50-100 per measurement (cheapest)
Time: Minutes (fastest)

Production protocol:

Daily: CD-SEM check (width/depth)
Weekly: SEM profile imaging (scallops, angle)
Monthly: TEM cross-section (detailed inspection)
```

---

## 14.4 Summary & Key Takeaways

1. **Sidewall Angle Nearly Vertical** — Modern STI achieves 90 ± 2° via energetic ions; cryogenic etch better than warm (90° vs. 80-85°); critical for avoiding lateral undercut.

2. **Scalloping Inevitable in DRIE** — 15-20 nm scallops typical after full etch; caused by ion-induced surface rippling; longer wavelength at low E_ion.

3. **Scallops Increase Leakage** — 20 nm scallops increase interface area ~30%, trap density increases, leakage increases 20-30%; specification: <15 nm preferred, >20 nm problematic.

4. **Pulsed Plasma Reduces Scallops** — ON/OFF duty cycling reduces scallop amplitude ~50%; cost: process time increases 2×; trade-off acceptable for critical layers.

5. **Corner Rounding from Mask + Plasma** — Lithographic mask corner radius ~50 nm + plasma over-etch ~50 nm → total 100 nm; increases parasitic capacitance, affects device performance.

6. **Profile Metrology Multi-Level** — Daily CD-SEM (fast, destructive data only), weekly SEM (detailed scallops), monthly TEM (authoritative verification); cost-performance trade-off managed per node.

7. **Temperature Aids Profile** — Cryogenic (−140°C) achieves better sidewall angles and smaller scallops than warm (20°C); bonus selectivity improvement makes it preferred overall.

---

**End of Part III: Process Phenomena (Chapters 10-14) COMPLETE**

**Next:** [Part IV - Production Scale (Chapters 15-16)](./15-cluster-integration.md)

**Chapter 14 Development Status:** Complete STI profile control framework  
**Version:** 1.0

