# Chapter 8: Thermal Management Systems

## Overview

Cryogenic etch (−140°C) requires sophisticated cooling to maintain electrode temperature while managing plasma heating and thermal transients. This chapter covers cooling technologies, PID control, and cluster tool thermal coupling challenges.

**Learning Objectives:**
- Understand cryogenic cooling technologies (LN₂ vs. mechanical)
- Design thermal management for −140°C operation
- Model PID control and temperature stability
- Quantify thermal transients during wafer loading
- Optimize cluster tool thermal coupling

---

## 8.1 Cryogenic Cooling Technologies

### 8.1.1 Liquid Nitrogen (LN₂) Direct Injection

```
LN₂ cooling system:

Supply:
  Dewar (insulated tank) with LN₂ (~500-1000 L capacity)
  Pressure regulator: Maintains 50-60 psi
  Flow controller: Metered LN₂ delivery
  
Delivery to electrode:
  Stainless steel tubing (thermally insulated)
  LN₂ enters electrode cooling passages (~10-20 passages)
  LN₂ boils upon contact (phase change, absorbs heat)
  Nitrogen gas exits via return port (back to dewar or atmosphere)

Heat absorption via phase change:

Boiling point of N₂: 77 K (−196°C)
Latent heat of vaporization: 199 kJ/kg (enormous!)

Example: Absorb 1 kW of heat

  Q = ṁ × L_v
  1000 W = ṁ × 199,000 J/kg
  ṁ = 1000 / 199,000 ≈ 0.005 kg/s = 18 kg/hour
  
At 0.8 kg/L (LN₂ density): 18/0.8 = 22.5 L/hour consumption

Cost:
  LN₂ cost: ~$0.50-1.00 per liter
  Consumption: 22.5 L/hour
  Cost: ~$11-23 per hour of operation
  
For 8-hour shift: ~$90-180/day
For 30-day month: ~$2,700-5,400/month
Annual: ~$30,000-65,000/year

Advantages:
  Very cold (−196°C available, −140°C easily achievable)
  Reliable (proven technology, used for decades)
  Simple control (proportional valve)
  Gradual wear (no moving parts in chamber)
  
Disadvantages:
  Continuous consumption (no energy savings)
  Supply chain dependency (LN₂ availability)
  Safety (cryogenic hazard, must handle carefully)
  Dewar handling and maintenance
  Environmental (N₂ exhausted to atmosphere)
```

### 8.1.2 Mechanical Chiller Systems

```
Refrigerant cycle cooling:

Compressor:
  Compresses refrigerant gas (R410A typical, non-CFC)
  High-pressure liquid exits
  
Condenser:
  Liquid refrigerant cools in heat exchanger
  Rejects heat to environment (air or water cooled)
  
Expansion valve:
  Throttles high-pressure liquid
  Pressure drops
  
Evaporator (in electrode):
  Low-pressure refrigerant evaporates
  Absorbs heat from electrode
  Circulates back to compressor
  
Cycle efficiency:
  COP (Coefficient of Performance) ≈ 2-4
  For 1 kW cooling, compressor draws 250-500 W
  Much more efficient than LN₂!

Advantages:
  Energy efficient (electric only, no consumption)
  Predictable operating cost (~$0.20/kWh electricity)
  No supply chain (self-contained system)
  Safe (sealed refrigerant loop)
  Environmental (no emission)
  Reusable for decades
  
Disadvantages:
  High capital cost (~$50-100K equipment)
  Complex maintenance (compressor service every 3-5 years)
  Reliability concerns (mechanical failure possible)
  Space required (large compressor unit)
  Noise from compressor
  
Cost comparison (over 10 years):

LN₂ system:
  Equipment: ~$5K (valves, piping, controls)
  Consumables: ~$400K (30-year estimate)
  Total: ~$405K
  
Mechanical chiller:
  Equipment: ~$75K
  Electricity: ~$30K (10 years, ~$3/day)
  Maintenance: ~$20K
  Total: ~$125K
  
Payback: Chiller pays for itself in ~3-4 years at high volume
         Preferred for production (better economics long-term)
```

### 8.1.3 Passive Radiative Cooling

```
Radiative cooling concept:

If electrode radiates heat to cold surroundings:
  Can passively cool without active system
  
Stefan-Boltzmann law:
  P_rad = ε × σ × A × (T_electrode^4 − T_environment^4)
  
  where σ = Stefan-Boltzmann constant
  
Example:

Electrode area: 0.1 m² (300 mm wafer area + margins)
T_electrode: 20°C (attempt passive cooling to room temp)
T_environment: 20°C

Heat radiated: P_rad = 0 (no difference!)

For cooling to actually happen:

T_electrode: 0°C
T_environment: 20°C (room)
ΔT = 20 K

P_rad = 0.95 × 5.67e-8 × 0.1 × (273^4 − 293^4)
      ≈ 50 W (very small!)

To achieve −140°C electrode:

T_electrode: 133 K
T_environment: 293 K
ΔT = 160 K

P_rad = 0.95 × 5.67e-8 × 0.1 × (133^4 − 293^4)
      ≈ 2000 W (significant!)

BUT: Chamber must be at ~133 K for this to work
     Entire lab needs to be cryogenic
     Impractical!

Conclusion: Passive cooling insufficient for −140°C
           Active cooling (LN₂ or chiller) required
           Passive may be sufficient for mild cooling (−20 to 0°C)
```

---

## 8.2 Temperature Control System

### 8.2.1 PID Feedback Control

```
Control objective:
  Maintain T_electrode = −140°C ±3°C
  
Measurement:
  Thermocouple (e.g., type K: −50 to +1000°C range)
  Placed in electrode (center preferred)
  Accuracy: ±1°C typical (depends on thermocouple calibration)
  
Setpoint:
  T_set = −140°C (configuration parameter)
  
Error signal:
  e(t) = T_set − T_measured
  
PID control:

u(t) = K_p × e(t) + K_i ∫e(t)dt + K_d × de/dt

where:
  K_p = Proportional gain (direct response to error)
  K_i = Integral gain (eliminates steady-state error)
  K_d = Derivative gain (prevents overshoot)

Control action:
  u(t) → Proportional valve (LN₂) or compressor speed (chiller)
  Larger u → more cooling
  
Typical gains (tuned empirically):

K_p ≈ 10 W/°C (for LN₂ system)
     (Each 1°C error → 10 W additional cooling request)
     
K_i ≈ 1 W/(°C·s)
     (Integral of error helps convergence)
     
K_d ≈ 50 W·s/°C
     (Derivative dampens oscillation)

Performance:

With good tuning:
  Settling time: ~10-20 seconds
  Temperature overshoot: <2°C
  Steady-state error: <0.5°C
  Oscillation: ±1-2°C around setpoint (normal)
  
With poor tuning:
  Overshoot: 10°C+ (electrode too cold initially, then oscillates)
  Settling time: >60 seconds
  Steady-state error: ±5°C (unacceptable)

Tuning procedure:

1. Set K_p only (K_i = K_d = 0)
   Increase K_p until system starts to oscillate (~50%)
   
2. Add K_d to dampen oscillation
   Increase K_d until oscillation minimal
   
3. Add K_i to eliminate steady-state error
   Increase K_i until error disappears
   
4. Fine-tune all three for balanced response
   Lab standard: K_p=10, K_i=1, K_d=50 (starting point)
```

### 8.2.2 Temperature Uniformity Across Electrode

```
Thermal gradient problem:

LN₂ injection point (one edge):
  Very cold locally (−196°C)
  
Opposite edge:
  Warmer (heat diffusion limited)
  
Temperature distribution:
  Edge near inlet: −150°C
  Center: −140°C
  Far edge: −130°C
  
Variation: 20°C across electrode!

This creates etch rate variation:
  Cooler area: Slower etch (higher selectivity)
  Warmer area: Faster etch (lower selectivity)
  Microloading effect amplified
  
Mitigation:

Multiple cooling passages:
  Instead of single inlet point
  Distribute LN₂ to 10-20 passages
  Crisscross pattern
  Result: More uniform temperature
  
Uniformity achievable: ±3-5°C (at −140°C setpoint)

Feedback thermocouple placement:

Single thermocouple (center):
  Measures only center
  May miss edge variations
  
Multiple thermocouples (3-5 positions):
  Measure edge, center, different radii
  Better indication of uniformity
  
Advanced systems: Thermal imaging
  IR camera views electrode surface
  Temperature map in real-time
  Can identify hot spots
  
Cost: Thermal camera system ~$50-100K extra
      Worth it for critical applications
```

---

## 8.3 Thermal Transients

### 8.3.1 Wafer Loading Thermal Shock

```
Scenario: Wafer at room temperature, electrode at −140°C

Transient timeline:

t = 0 sec:    Wafer inserted (fresh from cluster deposition step)
              Wafer temperature: +20°C
              Electrode temperature: −140°C
              Thermal gradient: 160°C!

t = 5 sec:    Wafer begins cooling
              Wafer surface: +15°C
              Electrode: still ~−140°C
              Wafer bulk: still warm (+20°C internally)
              
t = 30 sec:   Wafer half-cooled
              Wafer surface: −50°C
              Wafer interior: −20°C (temperature gradient inside wafer)
              Electrode: may warm slightly to −135°C
              
t = 60 sec:   Wafer nearly cooled
              Wafer surface: −120°C
              Wafer temperature mostly uniform: −100°C
              Electrode: warming to −130°C
              
t = 120 sec:  Thermal equilibrium approaching
              Wafer: −135°C
              Electrode: −135°C
              (Systems in equilibrium, can begin etch)

Thermal stress during cooling:

Wafer internal temperature gradient:
  Surface: −120°C
  Interior: −50°C (large gradient)
  
Differential contraction:
  Surface contracts more than interior
  Creates compressive stress at surface
  
Stress magnitude:
  σ = E × α × ΔT
  E ≈ 170 GPa (Si Young's modulus)
  α ≈ 2.6 ppm/°C (Si CTE)
  ΔT ≈ 70°C (internal gradient)
  
  σ ≈ 170×10⁹ × 2.6×10⁻⁶ × 70 ≈ 30 MPa
  (Significant stress, but below Si fracture strength ~1 GPa)
  
Risk: Wafer cracking if temperature ramps too fast
      Mitigated by slow cooling (natural diffusion)
      No active cooling ramp control needed
```

### 8.3.2 Thermal Stability During Etch

```
Electrode temperature during etch:

Baseline (before etch): T_e = −140°C

Plasma ignition:
  RF power applied (coil + bias)
  Plasma heating ~200 W dissipated as heat
  Heat conducted to electrode
  Temperature rises
  
During etch (2-3 min):
  Steady-state temperature: T_e ≈ −130 to −120°C
  Rise: ~10-20°C from baseline
  
PID compensates:
  Temperature rises slightly above −140°C
  Error signal triggers more cooling
  LN₂ flow increases
  Temperature stabilizes at new steady state
  
Temperature stability:
  Variation during etch: ±2-3°C (normal)
  Acceptable for most recipes
  
Etch rate impact:
  Temperature rise ~10°C during etch
  Rate increase: ~7-10% (from Arrhenius)
  
  Example:
    Baseline rate @ −140°C: 0.5 µm/min
    During etch @ −130°C: 0.54 µm/min
    Over 2.5 min etch: Rate drift ~8% (small, acceptable)
    
  Problem: Rate drifts over etch time
           Endpoint detection must account for this
```

---

## 8.4 Summary & Key Takeaways

1. **LN₂ Simplest, Chiller More Efficient** — LN₂ reliable but expensive ($30-65K/year); mechanical chiller higher capital but pays back in 3-4 years at production volume.

2. **−140°C Requires Active Cooling** — Passive radiative cooling insufficient; active system (LN₂ or chiller) mandatory for selectivity benefits.

3. **PID Control Standard** — Proportional-integral-derivative feedback maintains ±3-5°C uniformity; tuning empirical (K_p~10, K_i~1, K_d~50 starting point).

4. **Thermal Transient Significant** — Wafer loading creates 160°C shock; equilibration takes ~120 seconds; creates 30 MPa internal stress but below fracture risk.

5. **Electrode Temperature Drift During Etch** — Plasma heating raises T from −140°C to −130°C; causes ~7-10% etch rate increase over time; acceptable but must track.

6. **Uniformity Challenging** — Multiple cooling passages required (~10-20) for ±3-5°C wafer uniformity; single inlet creates 20°C variation (unacceptable).

7. **Cluster Tool Integration Complex** — Thermal coupling between deposition (200°C), ashing (room-T), and etch (−140°C) chambers creates huge transients; pre-cooling or in-situ stabilization needed.

---

**Next Chapter:** [Chapter 9 - RF Power Delivery & Matching Networks](./09-rf-networks.md)

**Chapter 8 Development Status:** Complete thermal management framework  
**Version:** 1.0

