# Glossary: Shallow Trench Isolation Etch

## A

**Anisotropic Etch:** Directional etching producing vertical profiles with minimal lateral undercut; achieved via energetic ion bombardment; STI standard.

**ARDE** (Aspect-Ratio-Dependent Etching): Non-uniform etch rate across features of different aspect ratios; 5-10× rate variation typical without compensation.

**Arrhenius Kinetics:** Temperature-dependent reaction rate model R ∝ exp(−E_a/RT); fundamental to thermal oxidation and temperature-dependent selectivity.

**Aspect Ratio (AR):** Ratio of trench depth to width; 2:1 (logic) to 100+:1 (3D NAND); drives ARDE severity.

---

## B

**Band-to-Band Tunneling (BTBT):** Direct electron tunnel across semiconductor bandgap at high reverse bias; exponentially sensitive to electric field.

**Bird's Beak:** Lateral oxidation under photoresist mask during thermal oxidation; reduces active area definition; mitigated by recessed STI.

**Breakdown Voltage (V_BD):** Electric field strength at which dielectric catastrophically fails; SiO₂ ~5-10 MV/cm; oxide thickness determines voltage.

**BTBT** (Band-to-Band Tunneling): See Band-to-Band Tunneling.

---

## C

**CCP** (Capacitive Coupling Plasma): RF plasma generation via electrode-to-ground capacitive plates; standard for STI, allows independent ion energy control.

**Cryogenic Etch:** Plasma etch at ultra-low temperature (−140°C typical); electrode cooling critical for STI selectivity improvement.

**CTE** (Coefficient of Thermal Expansion): Material's fractional length change per degree temperature; Si ~2.6 ppm/°C, SiO₂ ~0.5 ppm/°C; mismatch creates thermal stress.

---

## D

**Deal-Grove Model:** Mathematical model of thermal oxide growth distinguishing linear (reaction-limited) and parabolic (diffusion-limited) phases.

**Defect Density (D_it):** Trap state concentration at Si/SiO₂ interface; high-quality oxide <10¹⁰ /cm², poor oxide ~10¹², affects leakage current.

**Diffusion Length (λ_diff):** Distance radical can travel while diffusing before reacting; ~1-2 µm effective in STI trenches.

**DRIE** (Deep Reactive Ion Etching): Anisotropic etch using energetic ions to achieve high aspect ratio capability; alternating etch/passivation cycles in Bosch process variant.

---

## E

**E-field** (Electric Field): Voltage per unit distance; critical in sheath region between electrode and plasma (~0.3×V_bias per electrode gap).

**Electrode Coating:** Protective layer (YSZ typical) on plasma-facing surfaces; prevents aluminum corrosion in fluorine plasma.

**Endpoint Detection:** Real-time monitoring to determine etch completion; optical (C₂ emission), electrical (reflected power), or timer-based.

---

## F

**Fringe Capacitance:** Parasitic capacitance between adjacent isolation trenches; ~8-15 pF/µm typical at 50 nm spacing; dominates parasitic capacitance at advanced nodes.

**F· (Fluorine Radical):** Highly reactive neutral atom with unpaired electron; primary etch species in F-based plasma; concentration ~10¹¹-10¹² /cm³.

---

## I

**ICP** (Inductive Coupling Plasma): RF plasma generation via coil-based inductive coupling; higher plasma density than CCP, less selectivity control; specialty application for STI.

**IED** (Ion Energy Distribution): Statistical distribution of ion kinetic energies; narrow distribution (~20-30% FWHM) in CCP discharge.

**Isolation Integrity:** Measure of isolation quality (leakage, breakdown risk); critical for device reliability and yield.

---

## J

**Junction Leakage:** Reverse-bias current at p-n junction; exponential temperature dependence (doubles every 5-7 K); dominated by diffusion at low bias, BTBT at high bias.

---

## L

**Liner (Oxide Liner):** Thin SiO₂ or SiN layer grown thermally on trench walls and bottom; 5-20 nm typical; isolates Si cells electrically.

---

## M

**Mean Free Path (λ_mfp):** Average distance gas molecule travels before collision; proportional to 1/P; affects ballistic vs. diffusive transport in trenches.

**Microloading:** Die-level etch uniformity variation; dense regions etch slower than isolated regions; typically ±10-15%.

---

## O

**Oxidation:** Chemical reaction of Si with O₂ to form SiO₂; thermal oxidation in furnace standard for STI liner formation.

---

## P

**Parasitic Capacitance:** Unwanted capacitance between circuit elements; fringe capacitance dominates at advanced nodes.

**Passivation Layer:** Thin polymer film (fluorocarbon) that deposits and removes cyclically during etch; provides selectivity via SiO₂ protection at low temperature.

**Photoresist (Resist):** Light-sensitive polymeric material used for pattern definition; removed after etch via O₂ plasma ashing.

**Pinhole:** Defect in oxide creating conducting path; defect density <10⁻³ /cm² required for acceptable yields.

**Plasma:** Ionized gas consisting of electrons, ions, and neutrals; sustained by RF power in STI tools.

---

## R

**Radical Concentration:** Abundance of F· radicals in bulk gas; ~10¹¹-10¹² /cm³ typical; temperature-dependent (Arrhenius).

**Radical Depletion:** Reduction of F· concentration in deep trenches due to consumption; primary ARDE mechanism.

**Radical Shadowing:** Geometric blocking of radical access to trench bottom by sidewalls; creates view factor <1.

**Recessed STI:** Process variant where trench etched deeper than final depth, then partially filled by oxidation; reduces bird's beak effect.

**Residue:** Partially oxidized carbon byproducts remaining after resist ashing; post-ashing cleanup required before next step.

---

## S

**Selectivity:** Ratio of etch rates between two materials; Si/SiO₂ ~5-15:1 in fluorine plasma; critical for liner protection.

**Showerhead:** Gas distribution structure at chamber inlet; packed-orifice design standard for STI.

**Sputtering:** Physical removal of atoms by ion impact; yield ~0.5-1 atom/ion for Si at 100 eV.

---

## T

**TAT** (Trap-Assisted Tunneling): Leakage mechanism using interface trap states as intermediate tunneling sites; highly dependent on trap density and temperature.

**TDDB** (Time-Dependent Dielectric Breakdown): Gradual oxide degradation over time under reverse bias; lifetime >10 years required at operating conditions.

**Thermal Budget:** Cumulative heating from all process steps; limits maximum temperature for device integrity.

**Thermal Oxide:** SiO₂ grown by heating Si in O₂ atmosphere; high-quality interface (D_it ~10¹⁰); standard for STI liner.

**Throttle Valve:** Upstream restriction controlling chamber pressure by restricting pump outlet flow.

**Trap-Assisted Tunneling:** See TAT.

---

## U

**Uniformity:** Wafer-level and die-level etch depth variation; ±8-10% target achieved with multi-step recipes.

---

## V

**View Factor (V_f):** Geometric parameter determining radical access to trench bottom; V_f = W/(W+D) for rectangular trench.

---

## Y

**YSZ** (Yttria-Stabilized Zirconia): Chamber and electrode coating material; corrosion-resistant in fluorine plasma; life ~20,000-30,000 wafers.

---

**End of Glossary: 50+ STI Etch Definitions**

