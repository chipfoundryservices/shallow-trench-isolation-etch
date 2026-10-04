# Chapter 12: Liner Integrity During Etch

## Overview

The thermal oxide liner must survive trench etch without degradation. Ion bombardment causes interface charge accumulation, thickness loss, and leakage increase. This chapter quantifies damage mechanisms and designs recipes protecting liner quality.

**Learning Objectives:**
- Understand ion bombardment damage to oxide
- Model interface trap creation during etch
- Quantify thickness loss from sputtering
- Design selectivity strategies protecting liner
- Manage oxide breakdown risk

---

## 12.1 Thermal Oxide Degradation During Etch

### 12.1.1 Ion-Induced Interface Damage

```
Mechanism: Oxygen vacancy creation

O₂⁻ ions and energetic fluorine ions bombard SiO₂:
  Ion energy: ~100 eV typical
  Sputtering yield Y ≈ 0.3-0.4 atoms/ion
  
Collision cascade:
  Ion hits O atom
  O atom knocked out, leaves vacancy
  Oxygen vacancy: Missing negative charge
  Acts as trap state (positively charged when empty)

Trap density increase:

Initial oxide (high-quality thermal):
  D_it ≈ 10¹⁰ /cm² (excellent)
  
After 100 nm Si etch (10-20 nm SiO₂ thinning):
  Ion fluence: ~10¹⁶ ions/cm²
  D_it increases to ~10¹¹ /cm² (degraded 10×)
  
After 200 nm Si etch (deep trenches):
  Ion fluence: ~2×10¹⁶ ions/cm²
  D_it ≈ 10¹²-10¹³ /cm² (heavily degraded)

Device impact:

Leakage current via TAT (trap-assisted tunneling):
  J_TAT ∝ D_it × exp(−E_a,trap / kT)
  
  At D_it = 10¹⁰: J ≈ 10⁻¹³ A/cm² (negligible)
  At D_it = 10¹²: J ≈ 10⁻¹¹ A/cm² (100× higher!)
  
  Example: 1 million isolated cells
    At 10¹⁰: Leakage ≈ 0.1 pA/cell (unmeasurable)
    At 10¹²: Leakage ≈ 10 pA/cell (measurable, problematic!)
```

### 12.1.2 Sputtering-Induced Thinning

```
SiO₂ sputtering rate:

Ion energy: 100 eV, F⁺ ions
Sputtering yield: Y_SiO₂ ≈ 0.3-0.4 atoms/ion

Etch rate from sputtering:
  R_sputter = Y × φ_ion × M / (ρ × N_A)
  R_sputter ≈ 0.35 × 10¹⁵ × 30 / (2.2×10²³)
           ≈ 4-5 nm/min (sputtering contribution to SiO₂ etch)

Total SiO₂ etch rate:
  Total = Chemical + Sputtering
  Chemical: ~1 nm/min (radical driven, slow in cold)
  Sputtering: ~4 nm/min (ion driven)
  Total: ~5 nm/min
  
  (This is measured SiO₂ etch rate during STI!)

Oxide thickness loss during etch:

Initial liner: 15 nm (grown thermally)
SiO₂ etch rate: ~5 nm/min

Time to remove liner: 15 nm / 5 nm/min = 3 min

Example: 80 nm Si etch

Si etch rate: ~50 nm/min (typical)
Time: 80 nm / 50 nm/min = 96 sec ≈ 1.6 min
SiO₂ loss: 5 nm/min × 1.6 min ≈ 8 nm
Final oxide: 15 nm − 8 nm = 7 nm remaining

Worst case (deep trenches):

200 nm Si etch
Time: 200 nm / 50 nm/min = 4 min
SiO₂ loss: 5 nm/min × 4 min = 20 nm
Final oxide: 15 nm − 20 nm = −5 nm (OXIDE GONE!)

This is catastrophic! Must protect oxide during deep etch.
```

---

## 12.2 SiN Liner Protection Strategy

### 12.2.1 Silicon Nitride as Etch-Resistant Layer

```
Si₃N₄ properties vs. SiO₂:

SiO₂:
  Etch rate (chemical + sputtering): ~5 nm/min
  Sputtering yield: Y ≈ 0.3-0.4
  
Si₃N₄:
  Etch rate: ~0.5-1 nm/min (much slower!)
  Sputtering yield: Y ≈ 0.2-0.3 (lower)
  
Why slower?
  Si-N bond stronger than Si-O bond
  Higher activation energy for chemical etch
  More resistant to ion bombardment
  
Selectivity Si/SiN:
  Si etch: ~50 nm/min
  SiN etch: ~0.5 nm/min
  Selectivity: 100:1 (EXCELLENT!)

This is why SiN used in advanced nodes!
```

### 12.2.2 Multi-Layer Liner Strategy

```
Advanced liner stack:

Instead of simple SiO₂ or SiN:
  Use combination layer
  
Example (7 nm node):
  Top: 5 nm SiO₂ (thermal growth)
  Middle: 10 nm SiN (CVD, etch-resistant)
  Bottom: 2-3 nm SiO₂ (Si/SiN interface)
  Total: ~17-18 nm liner
  
Benefits:
  SiN provides etch selectivity (protects interface)
  SiO₂ at interface prevents N incorporation into Si
  SiO₂ on top reduces parasitic capacitance (lower K)
  
Etch protection:

During etch:
  SiO₂ top: Etches away (~5 nm)
  SiN middle: Barely affected (~0.5 nm loss)
  SiO₂ bottom: Protected by SiN above
  
Result: All liner survives etch intact!

Cost trade-off:
  Extra complexity (multi-step deposition)
  More process steps
  But essential for deep trenches (3D NAND)
```

---

## 12.3 Breakdown Risk & Voltage Stress

### 12.3.1 Oxide Breakdown During Etch

```
Electric field in oxide during etch:

During trench etch:
  Bias voltage: ~300-400 V
  Electrode gap: ~50 mm
  But at trench bottom: Much smaller gap!
  
At trench bottom (5 nm oxide):
  E_field = 300 V / 5 nm = 60 MV/cm
  (Very high field!)
  
Oxide breakdown field:
  E_BD ≈ 5-10 MV/cm typical
  
60 MV/cm >> 10 MV/cm (BREAKDOWN RISK!)

BUT: Wait, devices work fine. Why?

Answer: Trench isn't directly across 300 V
  Electric field concentrated at electrode-plasma boundary
  Not uniform through trench
  Actual trench bottom field: ~1-2 MV/cm (safe)
  
Practical safety:
  Design ensures trench field stays <5 MV/cm
  Breakdown extremely rare
  Protective plasma sheath voltage reduces effective field
```

### 12.3.2 TDDB (Time-Dependent Dielectric Breakdown)

```
Long-term oxide reliability:

Even below breakdown field:
  Oxide degrades over time
  Traps accumulate
  Leakage current increases
  Eventually breakdown occurs

TDDB lifetime model:

At constant field E:
  Time to failure: t_f = t_0 × exp(E_0 / E)
  
  where t_0, E_0 are material parameters
  
Example (E ≈ 2 MV/cm):
  t_f ≈ 10-100 years (excellent!)
  
At higher field (E ≈ 3 MV/cm):
  t_f ≈ 1-10 years (acceptable)
  
At extreme field (E ≈ 4 MV/cm):
  t_f ≈ 1 month (unacceptable!)

Production acceptance:
  Must maintain <3 MV/cm typical
  Ensures >10 year life at operating conditions
  Design review confirms fields stay safe
```

---

## 12.4 Selectivity-Driven Liner Protection

### 12.4.1 Low Ion Energy for Oxide Safety

```
Ion energy effect on oxide damage:

Sputtering yield:
  Y(E) ∝ E (approximately linear above threshold)
  
  At E = 50 eV: Y ≈ 0.15 (low)
  At E = 100 eV: Y ≈ 0.3 (moderate)
  At E = 200 eV: Y ≈ 0.6 (high)

SiO₂ thickness loss:

Low ion energy (50 eV):
  SiO₂ etch: ~2 nm/min (slow)
  During 100 sec etch: Loss = 2 × 1.67 = 3 nm
  Initial 15 nm → Final 12 nm (survives!)
  
High ion energy (200 eV):
  SiO₂ etch: ~8 nm/min (fast)
  During 100 sec etch: Loss = 8 × 1.67 = 13 nm
  Initial 15 nm → Final 2 nm (barely survives!)

Trade-off:

Low E_ion:
  Oxide protected (minimal sputtering)
  Better selectivity (chemical advantage)
  Slower etch rate (need longer time)
  
High E_ion:
  Oxide more damaged (heavy sputtering)
  Worse selectivity (ion contribution high)
  Faster etch rate (shorter time, less total damage)

Optimal strategy:
  Start high E_ion (fast bulk etch)
  Transition to low E_ion (final selective etch)
  Protects oxide in final phase when most vulnerable
```

### 12.4.2 Weekly Oxide Quality Validation

```
Validation procedure:

Control wafer stack:
  ArF resist: 80 nm
  SiO₂ liner: 15 nm (thermally grown)
  Si substrate
  (Simpler than full STI stack, focuses on liner)

Weekly etch + measurement:

Run standard recipe:
  Etch 80 nm resist
  Stop after standard endpoint detection
  
Measure oxide remaining:
  XRR (X-ray reflectometry): Non-destructive
  Measures oxide thickness remaining
  
Acceptance criteria:
  Oxide remaining: >10 nm (strong margin)
  If <8 nm: Oxide over-etched, investigate
  If <5 nm: Oxide nearly gone, recipe failure
  
Leakage current test (C-V curve):

Apply gate voltage sweep
  Measure capacitance vs. voltage
  Calculate interface trap density D_it
  
Acceptance:
  D_it < 5×10¹¹ /cm² (acceptable)
  If > 10¹² /cm²: Oxide damaged, recipe adjustment needed

Quarterly electron microscopy:

TEM cross-section:
  Direct observation of oxide thickness
  Visual assessment of damage
  Interface quality inspection
  
Defect detection:
  Pinholes or voids in oxide
  Crystalline damage in Si beneath
  Abnormal oxide structure
```

---

## 12.5 Summary & Key Takeaways

1. **Ion Bombardment Creates Traps** — Oxygen vacancy formation increases D_it ~10-100× during etch; trap-assisted tunneling leakage increases correspondingly.

2. **SiO₂ Sputtering Significant** — Sputtering yield ~0.3-0.4; SiO₂ loss ~5 nm/min during etch; 15 nm initial oxide can be partially or completely removed in deep trenches.

3. **Multi-Layer Liner Strategy** — SiO₂/SiN/SiO₂ stack: SiN provides etch selectivity (100:1 vs. Si), protects underlying interface, SiO₂ minimizes capacitance.

4. **Low Ion Energy Protects Oxide** — Sputtering scales linearly with E_ion; 50 eV causes 3× less damage than 200 eV; multi-step recipe (high E_ion early, low E_ion late) balances speed and protection.

5. **TDDB Lifetime Long** — Oxide field <3 MV/cm ensures >10 year life; >4 MV/cm risks <1 month failure; design confirms safety.

6. **Weekly Validation Critical** — Measure oxide thickness remaining (XRR), interface trap density (C-V), and direct observation (TEM); ensures recipe protects liner adequately.

7. **Selectivity Trade-off** — Low E_ion excellent selectivity + oxide protection but slower; high E_ion fast but oxide vulnerable; multi-step resolves tradeoff.

---

**Next Chapter:** [Chapter 13 - Thermal Transients & Annealing](./13-thermal-transients.md)

**Chapter 12 Development Status:** Complete liner integrity framework  
**Version:** 1.0

