# Appendix B: Fluorine Chemistry Database

## B.1 Plasma Chemistry Reactions

### F₂ Dissociation & Radical Formation

```
Primary dissociation (electron impact):

e⁻ + F₂ → e⁻ + 2F·
  Threshold: ~3 eV
  Cross-section peak: ~5 eV (σ_max ≈ 1.2 × 10⁻¹⁵ cm²)
  Result: Atomic fluorine radical

e⁻ + F₂ → e⁻ + F⁺ + 2e⁻ + e⁻
  Ionization threshold: ~17 eV
  Cross-section: ~0.5 × 10⁻¹⁵ cm² (higher energy)
  Result: F⁺ ion + secondary electrons (ionization)

CF₄ dissociation pathways:

Path 1 (low energy):
  e⁻ + CF₄ → e⁻ + CF₃ + F·
  Threshold: ~1 eV
  Cross-section: ~2 × 10⁻¹⁵ cm² (high probability)
  Result: CF₃ radical + F radical

Path 2 (moderate energy):
  e⁻ + CF₄ → e⁻ + CF₂ + 2F·
  Threshold: ~2 eV
  Cross-section: ~1.5 × 10⁻¹⁵ cm²
  Result: CF₂ radical + 2F radicals

Path 3 (high energy):
  e⁻ + CF₄ → e⁻ + CF⁺ + ... (multiple fragments)
  Threshold: ~20 eV
  Result: Ionization, multiple products
```

### Radical Reaction Kinetics

```
Si etching by F· radicals:

Si + 4F· → SiF₄↑
  Rate equation: R = k × [F·]^n × [Si]
  n ≈ 1 (first-order in F radical)
  
Arrhenius temperature dependence:
  k(T) = A × exp(−E_a / kT)
  A ≈ 10¹³ cm³/mol/s (pre-exponential)
  E_a ≈ 12-15 kcal/mol (activation energy)
  
  Example:
    At T = 300 K (27°C):
      k(300) = k₀ × exp(−14 / (1.987×10⁻³ × 300))
             = k₀ × exp(−23.4) ≈ k₀ × 7.2×10⁻¹¹ (very small)
    
    At T = 373 K (100°C):
      k(373) ≈ k₀ × 2.8×10⁻¹⁰ (4× higher)
    
    At T = 500 K (227°C):
      k(500) ≈ k₀ × 1.1×10⁻⁸ (150× higher than 300 K!)

SiO₂ etching (slower, higher E_a):

SiO₂ + 6F· → SiF₄↑ + 2OF₂↑
  Rate equation: R = k × [F·]^m
  m ≈ 1.5-2 (higher order)
  E_a ≈ 25-30 kcal/mol (higher than Si)
  
  Selectivity temperature dependence:
    S(T) = R_Si / R_SiO₂ ∝ exp((E_a,SiO₂ − E_a,Si) / kT)
    
    At T = 200 K (−73°C):
      S ≈ exp(15 / (1.987×10⁻³ × 200)) ≈ exp(37.7) ≈ 2.4×10¹⁶
      (Mathematically huge, but limited by polymer protection ~10-20:1)
    
    At T = 130 K (−140°C, cryogenic):
      S ≈ exp(15 / (1.987×10⁻³ × 130)) ≈ exp(57.9) ≈ 10²⁵
      (Theoretical, but polymer protection factor limits to 25-30:1)
    
    At T = 300 K (+27°C):
      S ≈ exp(15 / (1.987×10⁻³ × 300)) ≈ exp(25.1) ≈ 9×10¹⁰
      (High but practical selectivity ~10-15:1 with polymer)
```

### Polymer Formation Chemistry

```
CF_x oligomer formation:

Radical recombination:
  CF₃ + CF₃ → C₂F₆↑ (escapes as gas)
  CF₂ + CF₂ → (CF₂)₂ (dimer, can polymerize)
  CF · + CF · → C₂F₂ (reactive intermediate)

Polymer chain growth:
  (CF_x)_n + CF₂ → (CF_x)_{n+1} + CF₂
  
  Chain propagation: Adds 1-2 CF₂ units per collision
  Chain termination: ~50-100 nm polymer max thickness
                     (equilibrium when radical supply balances termination)

Temperature dependence:
  At higher T: Polymer more volatile (faster desorption)
              Equilibrium thickness smaller
  At lower T: Polymer less volatile (slower desorption)
             Equilibrium thickness larger
             
  At −140°C:  Equilibrium ~20-40 nm (thick)
  At +20°C:   Equilibrium ~5-10 nm (thin)
  At +100°C:  Equilibrium <1 nm (negligible)
```

---

## B.2 Gas Properties Reference

### F₂ and CF₄ Physical Properties

```
F₂ (Fluorine gas):

Molecular weight: 37.998 g/mol
Boiling point: −188°C (at 1 atm)
Critical temperature: −129°C
Critical pressure: 55 bar

At typical etch conditions (13.56 MHz, 50 mTorr, 20°C):
  State: Gas
  Mean free path λ ≈ 10 cm (very long at low pressure!)
  Molecular velocity: v ≈ 300 m/s
  Collision frequency: ~10⁶ collisions/s
  
Reactivity:
  One of most reactive elements
  Forms fluorides with nearly all elements
  Requires Teflon/Monel/Kel-F containers (not Al or Cu)

Safety:
  Toxic at high concentrations
  Etch tool cabinets purged with N₂ after run
  Exhaust scrubbed with alkaline solution (NaOH converts to NaF)

CF₄ (Carbon tetrafluoride):

Molecular weight: 87.996 g/mol
Boiling point: −128°C (slightly higher than F₂)
Density @ STP: 3.66 kg/m³

Plasma chemistry:
  CF₄ primary source in most commercial tools
  Easier to handle than F₂ (less reactive in bulk)
  Dissociation in plasma creates F·, CF_x radicals
  Preferred for tool safety

Greenhouse gas:
  GWP (Global Warming Potential) = 7,390 (100-year horizon)
  Extremely stable (atmospheric lifetime ~50,000 years)
  Increasingly restricted in EU and APAC
  
Cost:
  ~$20/kg bulk
  Purity 99.9% standard
```

### Ion Energy & Sputtering

```
Sputtering yield model:

Empirical fits (Yamamura):

Y(E) = Y_max × (E − E_th) / (E_0 − E_th) × exp(−0.3 × E / E_0)

where:
  Y_max: Maximum yield (material dependent)
  E_th: Threshold energy
  E_0: Energy at peak yield
  E: Ion kinetic energy

Example: Si sputtering by F⁺ ions

Y_max = 0.95 atoms/ion
E_th = 15 eV
E_0 = 100 eV

At E_ion = 50 eV:
  Y(50) = 0.95 × (50−15)/(100−15) × exp(−0.3×50/100)
        = 0.95 × 0.41 × 0.861 ≈ 0.33 atoms/ion

At E_ion = 100 eV:
  Y(100) = 0.95 × (100−15)/(100−15) × exp(−0.3)
         = 0.95 × 1.0 × 0.741 ≈ 0.70 atoms/ion

At E_ion = 200 eV:
  Y(200) = 0.95 × (200−15)/(100−15) × exp(−0.6)
         = 0.95 × 1.96 × 0.549 ≈ 1.02 atoms/ion
         
Trend: Yield increases then plateaus (peaks around 100-200 eV)
```

---

## B.3 Etch Rate Prediction

### Simple Etch Rate Model

```
Combined Si etch rate:

R_Si = R_chemical + R_sputtering

R_chemical = A × exp(−E_a / kT) × f_radical
  where:
    A: Pre-exponential factor (~10¹² m/s at reference)
    E_a: Activation energy (14 kcal/mol)
    T: Temperature (K)
    f_radical: Radical flux fraction of total plasma species

R_sputtering = Y(E_ion) × φ_ion × M / (ρ_Si × N_A × 100)
  where:
    Y(E_ion): Sputtering yield (from model above)
    φ_ion: Ion flux (m⁻²s⁻¹)
    M: Si molar mass (28 g/mol)
    ρ_Si: Si density (2.33 g/cm³ = 2.33×10³ kg/m³)
    N_A: Avogadro's number

Example calculation (typical STI conditions):

Pressure: 50 mTorr
Temperature: −140°C = 133 K
Coil power: 2000 W (typical CCP)
Bias power: 800 V / 0.3 coeff = 240 eV → ~70 eV E_ion typical

Radical flux estimation:
  Plasma density: n_e ≈ 10¹⁶ m⁻³ (cryogenic, moderate)
  Radical fraction: ~30% of ions (typical for F plasma)
  Flux: f_radical ≈ 10¹⁵ m⁻²s⁻¹

Chemical etch rate @ 133 K:
  k(133) = k₀ × exp(−14 / (1.987×10⁻³ × 133)) 
         ≈ k₀ × 1.5×10⁻¹¹
  R_chem ≈ 5-10 m/hour = 1.4-2.8 nm/s

Sputtering etch rate @ 70 eV:
  Y(70) ≈ 0.45 atoms/ion (from Yamamura model)
  φ_ion ≈ 5×10¹⁵ m⁻²s⁻¹ (rough estimate)
  R_sputter ≈ 0.45 × 5×10¹⁵ × 28 / (2.33×10³ × 6.022×10²³ × 100)
            ≈ 9 nm/s = 32 µm/hour
  
Total Si etch rate:
  R_Si ≈ (1.4 + 9) nm/s ≈ 10 nm/s ≈ 36-50 µm/hour
  
Experimental typical: 50-60 nm/min ≈ 50-60 µm/hour ✓
(Order of magnitude match!)
```

---

## B.4 Ion Energy Distribution

### IED Model (13.56 MHz RF)

```
Sheath voltage relationship:

For self-biasing CCP electrode:
  V_bias ≈ 0.3 × P_bias (in watts) / A (electrode area, cm²)
  
  Typical: P_bias = 800 W, A = 200 cm²
  V_bias ≈ 0.3 × 800 / 200 = 1.2 V (NO!)
  
  Correct formula:
  V_bias ≈ √(2 × E_rf × m_e / q_e) ≈ 0.30 × P_bias^{0.5}
  
  For P_bias = 800 W:
  V_bias ≈ 0.30 × √800 ≈ 0.30 × 28.3 ≈ 8.5 V
  
  E_ion ≈ 0.3 × V_bias = 2.5 eV (typical cold etch)

Ion energy distribution FWHM:

Experimental observation:
  At E_ion = 70 eV: FWHM ≈ 20-30 eV
  At E_ion = 100 eV: FWHM ≈ 30-40 eV
  Broader at higher energy (ion multiplication effects)
  
Gaussian approximation:
  I(E) ∝ exp(−(E − E_ion)² / (2σ²))
  
  σ = FWHM / (2√(2 ln 2)) ≈ FWHM / 2.36
  
  For E_ion = 70 eV, FWHM = 25 eV:
  σ ≈ 10.6 eV
  
  I(E=50 eV) / I(E=70 eV) = exp(−(50−70)²/(2×10.6²))
                           = exp(−3.55) ≈ 0.03 (3% of peak)

Temperature coefficient (cryogenic effect):

At 20°C vs −140°C:
  Coefficient ratio: 0.32 vs 0.30
  E_ion increases ~3% when cold
  FWHM increases slightly (~5-10% wider)
  Enables use of slightly higher bias (maintains E_ion control)
```

---

## B.5 Further Reading

- Chapter 2: Trench Formation (detailed reaction kinetics)
- Chapter 11: Cryogenic Etch Mechanisms (polymer chemistry in detail)
- Appendix A: Fluorine Chemistry (foundational equations)
- References: Lieberman & Lichtenberg (2005) Principles of Plasma Discharges

**Appendix B Version:** 1.0

