# Appendix A: Fluorine Chemistry Reference Data

## A.1 F₂ Dissociation & Plasma Species

```
F₂ dissociation pathways in plasma:

Direct impact dissociation:
  e⁻ + F₂ → e⁻ + 2F· (requires ~2.5 eV)
  
Ionization:
  e⁻ + F₂ → 2e⁻ + F₂⁺ (requires ~15.7 eV)
  e⁻ + F₂ → 2e⁻ + F⁺ + F· (requires ~24 eV)

Excitation:
  e⁻ + F₂ → e⁻ + F₂* (vibrational excitation, <0.5 eV)

Major plasma species:

Species          Concentration      Role in STI etch
─────────────────────────────────────────────────
e⁻               ~10⁹ /cm³         Drive dissociation
F· (radical)     ~10¹¹-10¹² /cm³   PRIMARY etch mechanism
F₂⁺ ions         ~10⁸-10⁹ /cm³     Ion bombardment
F⁺ ions          ~10⁷-10⁸ /cm³     Lower contribution
F₂* (excited)    ~10¹⁰ /cm³        Minor chemistry
```

## A.2 Radical Reaction Kinetics

```
F· radical oxidation of silicon:

Elementary reactions:

Si + F· → SiF (surface intermediate)
SiF + F· → SiF₂
SiF₂ + F· → SiF₃
SiF₃ + F· → SiF₄ (volatile, exits chamber)

Rate constants:

k₁(Si + F·): ~10⁻¹⁰ cm³/s (fast, diffusion-limited)
k₂-k₄: Similar magnitude

Net reaction:
  Si + 4F· → SiF₄ (g)
  Rate ∝ [F·]

Temperature dependence:

  Activation energy ~12-15 kcal/mol
  Arrhenius: R(T) = R₀ × exp(−E_a/RT)
  
  T = 0°C:   R ≈ 40 nm/min
  T = 20°C:  R ≈ 50 nm/min
  T = 40°C:  R ≈ 65 nm/min
  
  Temperature coefficient: ~6-8% per 5°C
```

## A.3 Ion Species Characteristics

```
Ion energy distribution in CCP STI etch:

F₂⁺ ions:
  Thermal energy: ~0.1 eV
  Sheath acceleration: ~0.3 × V_bias eV
  Total energy: E ≈ 0.3V_bias
  FWHM of distribution: ~20-30 eV (narrow)
  
  At V_bias = 200 V: E_peak ≈ 60 eV
  At V_bias = 300 V: E_peak ≈ 90 eV
  At V_bias = 400 V: E_peak ≈ 120 eV

F⁺ ions:
  Lower mass than F₂⁺
  Higher mobility
  Less abundant (~10% of F₂⁺)
  Similar energy distribution shape

Ion flux calculation:

φ_ion = (j_bias / e) / (1 + m_F₂/m_e)

where j_bias = bias current density

Typical: φ_ion ≈ 10¹⁴-10¹⁵ ions/cm²/s
         (comparable to radical flux)
```

## A.4 CF₄ Plasma Chemistry

```
CF₄ dissociation (alternative to F₂):

Dissociation pathways:
  e⁻ + CF₄ → e⁻ + CF₃ + F·
  e⁻ + CF₄ → e⁻ + CF₂ + 2F·
  
Products:
  F· radicals (same as F₂)
  CF₃· radicals (source of fluorocarbon polymer)
  CF₂ species (passivation layer precursor)

Comparison: CF₄ vs. F₂

CF₄ advantages:
  - More fluorine atoms per molecule (4 vs. 2)
  - Better polymer control (CF_x products)
  - Easier handling (non-toxic liquid at high pressure)
  
CF₄ disadvantages:
  - Less fluorine per ion energy per atom
  - Requires higher flow for same F· concentration
  - More polymer formation (can cause selectivity loss)

Industrial choice:
  F₂: Used when available (better efficiency)
  CF₄: More common in installed base (safer handling)
  Mix: Sometimes CF₄/O₂ blend (tuning polymer formation)
```

## A.5 Molecular Spectroscopy for Diagnostics

```
Optical emission lines useful for monitoring:

Species    λ (nm)    Transition              Application
─────────────────────────────────────────────────────────
F (I)      703       4p-4s (visible)        F· concentration
F (I)      777       3p-3s (near-IR)        Plasma diagnostic
F (II)     472       Ion line               Ion flux proxy
F₂         157       Lyman band (UV)        F₂ molecular state
CF (radical) 293     Swan band             Fluorocarbon indicator

OES use in STI:

Monitor F· line intensity:
  High intensity: Good dissociation, strong etch
  Low intensity: Poor dissociation, weak etch
  
Detect polymer buildup:
  Rise in CF band → excess polymer forming
  Indicates need for pressure/power adjustment
  
Endpoint detection:
  F· line sudden drop → substrate consumption
  But not used directly for STI (no endpoint marker)
```

## A.6 Temperature Effects on Dissociation

```
F₂ dissociation fraction vs. gas temperature:

Temperature    Dissociation %    Notes
───────────────────────────────────
300 K (27°C)     ~0.01%         Minimal thermal dissociation
400 K (127°C)    ~0.05%         Still low
600 K (327°C)    ~0.5%          Noticeable
800 K (527°C)    ~5%            Significant
1000 K (727°C)   ~20%           High

In plasma (electron-driven):
  T_electron ≈ 1-2 eV (equivalent ~10,000-20,000 K)
  Dissociation ~90%+ (very high, almost complete)
  T_gas (neutral temperature) much lower (~300-400 K)
  
Gas heating in F₂ discharge:
  RF power dissipation in plasma
  Ion-neutral collisions generate heat
  Temperature rise: ~100-200 K above electrode setpoint
  
  At electrode T = −140°C:
    Gas bulk ~−120 to −100°C (somewhat warmer)
  
  Effect: Bulk gas warmer than electrode
         Affects radical distribution (density gradients)
         More radicals near walls, fewer in center
```

## A.7 Plasma Stability & Frequency Effects

```
RF frequency for STI plasma:

Standard: 13.56 MHz (ISM frequency, FCC approved)

Frequency effects:

At 13.56 MHz:
  Electron drift velocity high
  Ion response: Slow (heavy), don't follow RF field
  Voltage across sheath can support
  Typical for CCP coupling
  
At higher frequencies (>100 MHz):
  Electron response faster
  Ions start to respond
  Sheath voltage becomes less well-defined
  Less common for STI (CCP optimized for 13.56 MHz)

Plasma stability:

Frequency stability critical:
  ±0.01% required (in practice ±0.001%)
  Frequency drift → impedance mismatch → reflected power
  Tuning network adjusts continuously
  
Power coupling efficiency:
  90% power transfer to plasma typical (10% reflected)
  Depends on impedance match
  Tuning network brings plasma load to 50 Ω
```

---

**End of Appendix A: Fluorine Chemistry Reference**

