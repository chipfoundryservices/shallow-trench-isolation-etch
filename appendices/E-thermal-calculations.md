# Appendix E: Thermal Calculations & Modeling

## E.1 CTE Mismatch Stress Calculation

### Biaxial Stress in Constrained Oxide on Si

```
Given:
  Silicon substrate (constrained base)
  Thermal oxide layer (SiO₂) on top
  Temperature change: ΔT
  Both materials constrained (cannot expand freely)

Material properties:
  Si: E_Si ≈ 170 GPa, α_Si ≈ 2.6 ppm/°C, ν ≈ 0.28
  SiO₂: E_SiO₂ ≈ 70 GPa, α_SiO₂ ≈ 0.5 ppm/°C, ν ≈ 0.17

Composite biaxial modulus (plane-strain):
  E_eff = E × (1 − ν) / (1 + ν)(1 − 2ν)
  
  For Si: E_eff,Si ≈ 170 × 0.81 / (1.28 × 0.44) ≈ 210 GPa
  For SiO₂: E_eff,SiO₂ ≈ 70 × 0.83 / (1.17 × 0.66) ≈ 68 GPa

Effective thermal expansion mismatch:
  Δα = α_Si − α_SiO₂ = 2.6 − 0.5 = 2.1 ppm/°C

Stress in oxide layer (at interface):
  σ_ox = E_eff,SiO₂ × Δα × ΔT
  σ_ox = 68 × 10⁹ Pa × 2.1 × 10⁻⁶ /°C × ΔT
  
Example: ΔT = 940°C (from −140°C to 800°C anneal)
  σ_ox = 68 × 2.1 × 940 / 10⁶ ≈ 134 MPa (tensile in oxide)

Stress in Si substrate:
  σ_Si = −E_eff,Si × Δα × ΔT / (composite thickness ratio)
  
  For thin oxide (~15 nm) on Si:
  σ_Si ≈ −(170 × 2.1 × 940 × 0.015 / 1000) ≈ −5 MPa (compressive)
  
  Net: Oxide stretched (tensile), Si compressed

Shear stress at interface:
  τ ≈ σ_ox / 2 ≈ 67 MPa (delamination risk if interface weak)
```

### Allowable Stress & Fatigue

```
SiO₂ fracture strength:
  σ_fracture ≈ 1000-1500 MPa (very high, brittle)
  
  However, interface strength much lower!
  
SiO₂-Si interface strength (adhesion):
  σ_adhesive ≈ 100-300 MPa (typical chemical bond)
  
Fatigue limit (after N cycles):
  S_fat ≈ 50 MPa (after 1000 thermal cycles)
  
Stress cycle amplitude:
  For each heating (20°C → 800°C): Δσ ≈ 100 MPa
  For each cooling (800°C → −140°C): Δσ ≈ 150 MPa
  
After 500 cycles:
  Cumulative damage ≈ 500 × 150 / 50 ≈ 1500% (failure!)

Mitigation: Slow ramp rate
  At 20°C/min: Full stress ~150 MPa peak (fast, high peak)
  At 5°C/min: Stress distributed over time, lower peak (slower, safer)
  
  Peak stress at slow ramp ≈ 90 MPa
  After 500 cycles: 500 × 90 / 50 ≈ 900% (still risky)
  
Practical: Use slow ramp + in-situ annealing (lower ΔT) + occasional full anneals
```

---

## E.2 Heat Transfer to Electrode

### Conductive Heat Path (Frame)

```
Scenario: Deposition chamber @ 200°C, Etch chamber @ −140°C

Heat conduction equation:
  Q = k × A × ΔT / L
  
  where:
    k: Thermal conductivity of material (W/m·K)
    A: Cross-sectional area of conductor (m²)
    ΔT: Temperature difference (K)
    L: Conductor length (m)

Example heat path:

Deposition chamber wall (Al, 1 cm thick):
  k_Al ≈ 237 W/m·K
  T_dep = 473 K (200°C)
  
Connection to etch chamber:

Frame structural member (Al, 50 cm long, 50 mm² cross-section):
  k_Al ≈ 237 W/m·K
  A = 50 × 10⁻⁶ m²
  L = 0.5 m
  ΔT = 473 − 133 = 340 K
  
  Q_cond = 237 × 50×10⁻⁶ × 340 / 0.5
         ≈ 8 W (moderate heat leak)

Etch electrode cooling load:
  Q_cool,normal ≈ 5-10 kW (for large wafer throughput)
  
  Q_cond / Q_cool ≈ 8 / 7500 ≈ 0.1% (negligible)
  
BUT: Effective temperature swing on electrode:

Electrode temperature rise from 8 W heat leak:
  ΔT_elec = Q / (h × A_elec)
  
  h ≈ 100 W/m²K (radiation + conduction in cryogenic)
  A_elec ≈ 0.02 m² (200 mm electrode area)
  
  ΔT_elec ≈ 8 / (100 × 0.02) ≈ 4 K (modest rise)

However, in real clusters:
  Multiple chamber connections
  Cumulative heat leak: ~30-50 W
  Electrode temperature rise: 15-25 K
  
  Etch electrode setpoint: −140°C (133 K)
  Actual temperature: −125°C to −120°C (148-153 K)
  Error: ~20 K (SIGNIFICANT!)
  
  Effect on etch:
    Etch rate 15-20% higher
    Selectivity 10-15% worse
    Recipe invalid!

Radiation shielding mitigation:

Reflective shield (polished Al, ε ≈ 0.1) between deposition and etch:
  Q_rad_bare = ε × σ × A × (T_hot⁴ − T_cold⁴)
             = 0.8 × 5.67×10⁻⁸ × 0.1 × (473⁴ − 133⁴)
             ≈ 800 W (very large!)
  
  Q_rad_shield = 0.1 × 5.67×10⁻⁸ × 0.1 × (473⁴ − 133⁴)
               ≈ 100 W (still significant)
  
  Note: These are large area estimates; actual chamber areas ~0.5 m²
  
  Q_rad ≈ 0.8 × 5.67×10⁻⁸ × 0.5 × (473⁴ − 133⁴) ≈ 4000 W (with bare surface)
  Q_rad,shield ≈ 500 W (with polished shield, 87% reduction)
  
  Practical: Shielding reduces electrode temperature rise 20 K → 2-3 K (acceptable)
```

---

## E.3 Wafer Cool-Down Transient

### Exponential Cool-Down Model

```
Wafer temperature transient (first-order approximation):

T(t) = T_ambient + (T_initial − T_ambient) × exp(−t / τ)

where τ is the thermal time constant.

For wafer in vacuum chamber:
  Heat loss mechanism: Radiation from wafer to electrode
  
  Heat transfer coefficient (radiation-dominated):
    h_rad ≈ ε × σ × (T_wafer² + T_electrode²) × (T_wafer + T_electrode)
    
    Typically: h_rad ≈ 10-20 W/m²K at cryogenic (much lower than room-T convection)

Thermal time constant:
  τ = (ρ × c × V) / (h × A)
  
  For 200 mm Si wafer (~125 g, c ≈ 700 J/kg·K):
    V/A ≈ t/6 (thickness ~0.7 mm, diameter 200 mm)
    V/A ≈ 0.0001 m³ / 0.03 m² ≈ 3 mm
    
    τ ≈ (2330 × 700 × 0.0001) / (15 × 0.03)
      ≈ 163 / 0.45 ≈ 360 seconds (typical)

Wafer cool-down timeline:

t = 0 min: T_wafer = 20°C, T_electrode = −140°C, ΔT = 160°C
t = 1 min: T(60) = −140 + 160 × exp(−60/360) ≈ −140 + 145 ≈ 5°C
t = 2 min: T(120) = −140 + 160 × exp(−120/360) ≈ −140 + 106 ≈ −34°C
t = 3 min: T(180) = −140 + 160 × exp(−180/360) ≈ −140 + 68 ≈ −72°C
t = 4 min: T(240) = −140 + 160 × exp(−240/360) ≈ −140 + 44 ≈ −96°C
t = 5 min: T(300) = −140 + 160 × exp(−300/360) ≈ −140 + 28 ≈ −112°C
t = 6 min: T(360) = −140 + 160 × exp(−360/360) ≈ −140 + 18 ≈ −122°C
t = 8 min: T(480) = −140 + 160 × exp(−480/360) ≈ −140 + 5 ≈ −135°C
t = 10 min: T(600) = −140 + 160 × exp(−600/360) ≈ −140 + 1 ≈ −139°C

Time to 95% equilibration (ΔT < 8°C):
  t_95% = 3τ ≈ 3 × 360 ≈ 1080 seconds ≈ 18 minutes (!)
  
Practical tolerance (within 3°C of setpoint):
  ΔT = 3°C requires (160 − 3) / 160 = 0.98 = exp(−t/τ)
  ln(0.98) = −t/360
  t ≈ 7 seconds × 360 ≈ 2520 seconds ≈ 42 minutes (extreme!)

More realistic: 5-6 minutes for 95% cool-down (practical in 360s time constant)
```

---

## E.4 Thermal Budget Calculation

### Cumulative Temperature Change During Process

```
Complete STI process thermal budget:

Step 1: SiO₂ deposition @ 200°C
  Time: 10 minutes
  Temperature: +200°C (stays constant)
  Cumulative thermal: +200 × 10 = +2000 °C·min

Step 2: Cool to ashing chamber @ 20°C
  Transfer time: 1 minute
  Temperature change: 200°C → 50°C (mid-transfer, non-linear)
  Cumulative thermal: +100 × 1 = +100 °C·min

Step 3: Ashing @ 20°C
  Time: 15 minutes
  Temperature: +20°C (stable)
  Cumulative thermal: +20 × 15 = +300 °C·min

Step 4: Cool to etch @ −140°C
  Transfer time: 1 minute
  Temperature change: 20°C → −70°C (mid-transfer)
  Cumulative thermal: −50 × 1 = −50 °C·min

Step 5: Thermal soak to −140°C (in etch chamber)
  Time: 6 minutes
  Temperature drops from −70°C → −140°C
  Cumulative thermal: −105 × 6 = −630 °C·min

Step 6: Etch @ −140°C
  Time: 2 minutes
  Temperature: −140°C (stable)
  Cumulative thermal: −140 × 2 = −280 °C·min

Step 7: Cool-down in cluster & transfer to furnace
  Time: 5 minutes
  Temperature: −140°C → +20°C (gradual, ambient exposure)
  Cumulative thermal: −60 × 5 = −300 °C·min

Step 8: Anneal @ 800°C
  Time: 30 minutes
  Temperature: +800°C (high T for interface healing)
  Cumulative thermal: +800 × 30 = +24,000 °C·min

Total cumulative temperature exposure:
  Sum = 2000 + 100 + 300 − 50 − 630 − 280 − 300 + 24000
      = 25,140 °C·min
  
Average temperature: 25,140 / (10+1+15+1+6+2+5+30) = 25,140 / 70 ≈ 359°C
(Very high average due to anneal dominating!)

Annealing thermal contribution: 96% of total
Non-anneal thermal budget: 4% (deposition + etch + transfers)

Implication:
  Most thermal stress from furnace cycle (−140°C → 800°C)
  In-situ annealing (limited to 0-400°C) would reduce stress significantly
  But may compromise interface healing (lower anneal temperature)
```

---

**Appendix E Version:** 1.0

