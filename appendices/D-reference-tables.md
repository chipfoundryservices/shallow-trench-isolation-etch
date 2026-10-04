# Appendix D: Quick-Reference Tables

## D.1 Etch Rate Lookup Table

```
STI Etch Rate vs. Key Parameters
(Si etch rate in nm/min, at −140°C, SiO₂ baseline 15 nm)

Temperature effect:

Temperature (°C) | Coil Pwr | Bias (V) | E_ion (eV) | Si Rate | SiO₂ Rate | Selectivity
−140            | 2000 W   | 800 V   | 70 eV     | 50      | 1.5       | 33:1
−120            | 2000 W   | 800 V   | 70 eV     | 55      | 1.8       | 30:1
−100            | 2000 W   | 800 V   | 70 eV     | 62      | 2.2       | 28:1
  0             | 2000 W   | 800 V   | 70 eV     | 75      | 5         | 15:1
+20             | 2000 W   | 800 V   | 70 eV     | 85      | 8         | 11:1

Power effect (at −140°C, 800 V bias):

Coil Power | Bias Power | Pressure | Si Rate | SiO₂ Rate | Notes
1500 W     | 600 V      | 50 mT    | 35      | 1.0       | Conservative (slow, selective)
2000 W     | 800 V      | 50 mT    | 50      | 1.5       | Standard recipe
2500 W     | 1000 V     | 50 mT    | 65      | 2.2       | Aggressive (fast, less selective)

Ion energy effect (at −140°C, 2000 W coil):

Bias Voltage | E_ion | Si Rate | SiO₂ Rate | Selectivity | Notes
300 V       | 20 eV | 25      | 0.8       | 31:1        | Very selective (slow)
600 V       | 50 eV | 38      | 1.2       | 32:1        | Good selectivity
800 V       | 70 eV | 50      | 1.5       | 33:1        | Balanced
1000 V      | 85 eV | 60      | 2.0       | 30:1        | Faster (less selective)

Pressure effect (at −140°C, 2000 W, 800 V):

Pressure | Si Rate | SiO₂ Rate | ARDE Factor | Notes
30 mT   | 52      | 2.5       | 8:1         | Low-P ARDE worse
50 mT   | 50      | 1.5       | 5:1         | Standard (good ARDE)
80 mT   | 42      | 0.9       | 3:1         | High-P ARDE better
100 mT  | 38      | 0.7       | 2:1         | Very high (slow, good uniformity)

Recipe time estimation:

Etch Depth | Standard Recipe | Fast Recipe | Selective Recipe | Notes
50 nm      | 60 sec         | 40 sec      | 100 sec          | Shallow trenches
100 nm     | 120 sec        | 70 sec      | 200 sec          | Typical STI
150 nm     | 180 sec        | 110 sec     | 300 sec          | Deep STI
200 nm     | 240 sec        | 150 sec     | 400 sec          | Very deep (3D NAND)
```

## D.2 Equipment Specifications

```
Typical CCP Etch Tool (STI-capable)

Tool vendor (example): Lam Research Kiyo or AMAT Endura class

Chamber specifications:
  Electrode diameter: 200 mm (wafer size)
  Electrode material: Anodized Al + YSZ coating
  Electrode gap: ~50 mm
  Chamber volume: ~10 liters
  
RF system (coil):
  Frequency: 13.56 MHz (industry standard)
  Power capacity: 3000 W (cryogenic STI tools)
  Impedance: 50 Ω (standard RF transmission line)
  Reflected power limit: <100 W (alarm threshold)
  
Bias system:
  Frequency: 13.56 MHz or 2 MHz (typically 13.56 for STI)
  Power capacity: 1500 W
  Voltage range: 100-1200 V
  Temperature coefficient: +0.3 V/°C at cryogenic
  
Cryogenic system (option):
  Cooling method: LN₂ liquid or mechanical chiller
  Minimum temperature: −145°C (achievable)
  Cooling capacity: ~20 kW (liquid) or ~10 kW (mechanical)
  PID control: ±3°C uniformity capability
  
Gas lines:
  CF₄ MFC (Mass Flow Controller):
    Range: 0-500 sccm
    Accuracy: ±2% of full scale
  O₂ MFC:
    Range: 0-200 sccm
  N₂ MFC:
    Range: 0-500 sccm
  
Vacuum pump:
  Type: Rotary vane + roots
  Pumping speed: ~200 L/min at chamber
  Ultimate pressure: <0.01 mTorr
  
Pressure controller:
  Range: 1-200 mTorr
  Accuracy: ±5% of setpoint
  Control valve: Automated mass flow balancer
```

## D.3 Material Properties

```
Silicon (Si)

Density: 2.33 g/cm³ (23,300 kg/m³)
Molar mass: 28.085 g/mol
Melting point: 1414°C
Thermal conductivity: 149 W/m·K @ 20°C
CTE: 2.6 ppm/°C (20-100°C)
Sputtering yield (F⁺ at 70 eV): ~0.45 atoms/ion

Silicon dioxide (SiO₂)

Density: 2.20 g/cm³
Molar mass: 60.08 g/mol
Dielectric constant κ: 3.9
Bandgap: 9 eV (very wide, insulator)
Thermal conductivity: 0.01 W/m·K @ 25°C
CTE: 0.5 ppm/°C (very low)
Sputtering yield (F⁺ at 70 eV): ~0.25 atoms/ion
Interface trap density (high-quality thermal): 10¹⁰ cm⁻² eV⁻¹
                (plasma grown): 10¹² cm⁻² eV⁻¹

Silicon nitride (Si₃N₄)

Density: 3.1 g/cm³
Dielectric constant κ: 7.5 (higher than SiO₂)
Thermal conductivity: 0.02 W/m·K
CTE: 3 ppm/°C (matches Si closely)
Sputtering yield (F⁺ at 70 eV): ~0.15 atoms/ion (more resistant)
Etch selectivity vs. Si: ~100:1 (excellent protection)
```

## D.4 Thermal Properties

```
Temperature conversion reference:

Celsius to Kelvin: K = °C + 273.15

Common etch temperatures:
  Room temperature: 20°C = 293 K
  Warm etch: 0°C = 273 K
  Cryogenic: −100°C = 173 K
  STI standard: −140°C = 133 K
  Furnace anneal: 800°C = 1073 K
  
Thermal time constant (wafer cooling in chamber):

Wafer temperature evolution: T(t) = T_f + (T_0 − T_f) × exp(−t/τ)

Time to reach 95% of final temperature: t = 3τ

For STI etch chamber (LN₂ cooling):
  τ ≈ 60-120 seconds (per experimental measurement)
  Time to −133°C from 20°C: t_95% ≈ 300-360 seconds (5-6 minutes)
  
For warm chamber (mechanical cooling):
  τ ≈ 30-60 seconds (faster, less extreme ΔT)
  
Cryogenic cool-down power required:

Heat transfer rate: Q = h × A × ΔT

For wafer cooling from +20°C to −140°C:
  ΔT = 160°C
  Surface area A ≈ 35 cm² (200 mm wafer, both sides)
  Heat transfer coefficient h ≈ 100-200 W/m²K (electrode in vacuum)
  
  Q ≈ 150 × 0.0035 × 160 ≈ 84 W per wafer
  
  At 5 wafers/hour: 84 × 5/3600 ≈ 0.12 kW continuous
  (Plus chamber walls heat loss: ~1-2 kW total cooling needed)
  
LN₂ consumption:

Latent heat of vaporization (N₂): 198 kJ/kg
For 20 kW cooling load:
  Mass flow: 20,000 W / 198,000 J/kg ≈ 0.1 kg/s ≈ 6 kg/min
  
At 0.8 kg/liter (liquid N₂ density):
  Volume: 6 / 0.8 = 7.5 L/min ≈ 450 L/hour ≈ 500 L/day
  
Annual consumption (5 days/week): 
  500 L/day × 250 days = 125,000 L/year (typical for fab)
  
Cost @ $0.50/liter: $62,500/year (major operating expense!)
```

## D.5 Consumable Replacement Schedule

```
Predictive replacement guide (based on wafer count or time):

Component | Lifetime | Typical Interval | Cost | Priority
-----------|----------|-----------------|------|----------
Electrode (YSZ coating) | 50,000 wafers | 6-12 months | $20K | High (corrodes)
RF matching capacitor | 30,000 hrs | 2-3 years | $2K | Medium
O-rings (chamber seals) | 100,000 wafers | 1-2 years | $1K | High (leaks)
Pump oil (rotary vane) | 6 months | Every 6 mo | $500 | High (degradation)
Gas regulators | 50,000 hrs | 3-5 years | $2K | Medium
Cooling pump (mechanic) | 40,000 hrs | 4-5 years | $5K | High (fails catastrophically)
LN₂ supply line | 10 years | Check yearly | $1K | Low (monitoring)
Showerhead electrode | 100,000 wafers | 2-3 years | $5K | High (erosion)

Preventive maintenance intervals:

Daily (15 min):
  □ Visual inspection (electrode, connections)
  □ Gas pressure check
  □ LN₂ level check
  
Weekly (1 hour):
  □ Vacuum integrity test
  □ Gas line purge
  □ RF impedance verification
  
Monthly (2 hours):
  □ Chamber interior cleaning (tool off)
  □ Pump oil level check
  □ Thermal camera temperature scan
  
Quarterly (4 hours):
  □ O-ring replacement (preventive)
  □ Electrode inspection depth (profile SEM)
  □ Cooling system flow rate verification
  
Annually (8 hours):
  □ Complete equipment inspection by OEM
  □ Calibration of all sensors
  □ Documentation review & archival
```

---

**Appendix D Version:** 1.0

