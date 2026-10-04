# Appendix C: Standard Operating Procedures (SOP)

## C.1 Pre-Etch Tool Startup (Daily)

```
Morning startup sequence (15 minutes):

1. Safety check (1 min)
   □ Check LN₂ dewar level (must be >50% full)
   □ Verify electrical panel power indicators (green lights)
   □ Check gas bottle regulators (CO₂ pressure dial 800-1000 psi)
   □ Inspect chamber cabinet for visible damage or leaks

2. Vacuum system pump-down (2 min)
   □ Rotary vane pump on, open vent valve
   □ Monitor backing pump oil level (must reach min line)
   □ Purge system with N₂ for 30 seconds (removes atmospheric moisture)
   
3. Temperature stabilization (5 min)
   □ Set cryogenic electrode to −140°C setpoint
   □ Monitor PID controller feedback
   □ Wait for amber standby light (ready to etch)
   □ Expected settling time: 3-5 minutes
   
4. RF system pre-check (3 min)
   □ Coil RF generator: Power ON, confirm green ready light
   □ Bias RF generator: Power ON, confirm green ready light
   □ Matching network: Automated tuning activated
   □ Reflected power should settle <10 W (good match)
   □ If P_reflected > 15 W: Run manual re-tune (see Section C.4)
   
5. Gas system check (2 min)
   □ CF₄ line: Verify 500 sccm setpoint on mass flow controller
   □ O₂ line (ashing): Verify 200 sccm setpoint
   □ N₂ purge (standby): Verify 50 sccm setpoint
   □ All regulators locked at operating pressure
   
6. Wafer handler check (2 min)
   □ Robot arm: Run home position, verify no obstructions
   □ Cassette loader: Test door open/close cycle
   □ Chamber vacuum doors: Test open/close smoothly
   
Status: READY TO ETCH
Time to first wafer: ~15 minutes total
```

## C.2 Standard Etch Recipe (STI at −140°C)

```
Recipe name: STI_100nm_SiO2liner_CRYO_v2.3
Target: Etch 100 nm Si + stop on 15 nm thermal SiO₂ liner

Step 1: Bulk etch (high rate)
  Duration: 60 seconds
  Power settings:
    Coil RF: 2000 W
    Bias RF: 800 V (→ ~70 eV E_ion via coefficient 0.30)
  Gas flow:
    CF₄: 500 sccm
    O₂: 50 sccm (oxygen additive for wall passivation)
    N₂: 0 sccm (no dilution)
  Pressure: 50 mTorr (moderate)
  Temperature: −140°C (maintained)
  
  Expected outcome:
    Si etched: 50-60 nm (deep etch, fast)
    SiO₂ attacked: Minimal (polymer protection active)
    Endpoint: Etch ~60% of total depth
    
Step 2: Transition etch (selectivity increase)
  Duration: 30 seconds
  Power settings:
    Coil RF: 1800 W (power reduced for selectivity)
    Bias RF: 600 V (→ ~50 eV E_ion, lower ion energy)
  Gas flow:
    CF₄: 400 sccm (reduced for polymer buildup)
    O₂: 30 sccm
    N₂: 0 sccm
  Pressure: 80 mTorr (higher pressure for selectivity)
  Temperature: −140°C
  
  Expected outcome:
    Si etched: 30-40 nm additional
    SiO₂ attacked: Minimal (polymer protection thicker now)
    Endpoint: Etch ~95% of total depth
    Profile: Sidewalls beginning to form

Step 3: Selective finish (oxide protection)
  Duration: Until endpoint signal (typically 20-40 sec)
  Power settings:
    Coil RF: 1500 W (low power for selectivity)
    Bias RF: 400 V (→ 30 eV E_ion, very low ion energy)
  Gas flow:
    CF₄: 300 sccm (minimal chemical etch)
    O₂: 20 sccm
    N₂: 100 sccm (dilution for reduced etch rate)
  Pressure: 100 mTorr (high pressure reduces ARDE)
  Temperature: −140°C
  
  Expected outcome:
    Si etched: Final 5-10 nm to reach oxide
    SiO₂ protected: Polymer ~30 nm thick, shields liner
    Endpoint: Optical detection of oxide exposure
    Profile quality: Excellent (minimal scalloping)

Total recipe time: 120 ± 20 seconds (2 minutes)

Endpoint detection:
  Optical monitoring: Laser reflectance drops when oxide reached
  Software endpoint: Reflects change in wafer surface properties
  Manual override: Operator can stop early if profile visible
```

## C.3 Thermal Soak Protocol (Cryogenic Equilibration)

```
Required before etch step:

Wafer temperature must reach −140°C (electrode setpoint)

Test procedure:

1. Load wafer into chamber (room temperature, ~20°C)
2. Close chamber door (start thermal soak)
3. Monitor electrode temperature via IR sensor (if available)
   or rely on PID setpoint (−140°C assumed reached)
4. Wait for equilibration timer: 
   □ Shallow wafers (<50 nm depth): 3 minutes minimum
   □ Standard wafers (50-150 nm depth): 5 minutes minimum
   □ Deep trenches (>150 nm): 7 minutes minimum
   
Expected temperature evolution:
  t = 0 sec: Wafer at 20°C, electrode at −140°C
  t = 60 sec: Wafer at ~0°C (cooled ~20°C/min initially)
  t = 120 sec: Wafer at −60°C
  t = 180 sec: Wafer at −100°C (80% of target)
  t = 300 sec: Wafer at −130°C (95% of target)
  t = 360 sec: Wafer at −138°C (99% of target, equilibrated)

Verification (optional, for monitoring):
  If tool has type-K thermocouple insert on dummy wafer:
    Confirm temperature ≤ −138°C before starting etch
    If warmer: Wait additional 2 minutes, recheck
    If tool lacks sensor: Use timer defaults above
```

## C.4 Manual RF Impedance Tuning

```
When to manually tune:

- Reflected power > 15 W (auto-tuning failed)
- After electrode change (new impedance)
- After chamber maintenance (capacitor adjustment)
- Monthly preventive maintenance (re-baseline)

Procedure:

1. Initialization:
   □ Tool in standby (plasma off, vacuum maintained)
   □ Coil power: 1000 W test power
   □ Bias power: OFF
   □ Directional coupler measuring P_forward, P_reflected

2. Measure baseline:
   □ Note current P_reflected (reference)
   □ Record P_forward (usually 990-1000 W if matched)
   □ If P_reflected > 100 W: Auto-tuner circuit problem, skip manual

3. Manual capacitor tuning (L-match network):
   □ Identify variable capacitor C_series (left box on control panel)
   □ Note current position: ____ % (0-100% dial)
   □ Adjust by +5% (clockwise) → measure P_reflected
   □ If P_reflected decreased: Continue in same direction by +5% steps
   □ If P_reflected increased: Reverse direction by −10% from start
   □ Iterate: Adjust, measure, evaluate
   
   Target: Minimize P_reflected → <5 W optimal, <10 W acceptable
   
4. Convergence:
   □ When P_reflected changes <1 W per step: Fine-tuning zone
   □ Continue ±1% adjustments until minimum found
   □ Mark final position on dial (for reference)
   □ Expected total time: 3-5 minutes for convergence

5. Validation:
   □ Increase power to 2000 W (normal operating level)
   □ Re-measure P_reflected
   □ Should still be <15 W (tuning valid across power range)
   □ If >15 W: Tuning circuit drift, call service

6. Log results:
   □ Record: Before P_reflected: ___ W
   □ After P_reflected: ___ W
   □ Final capacitor position: ___ %
   □ Date/time: ___/___/____
```

## C.5 Post-Etch Tool Shutdown

```
Daily shutdown (10 minutes):

1. End-of-shift plasma off (1 min)
   □ Stop etch recipe if running
   □ RF generator OFF (coil power off first, then bias)
   □ Gas flow reduced to N₂ purge (50 sccm)
   □ Wait 30 seconds for plasma to extinguish
   
2. Temperature cool-down hold (2 min)
   □ Cryogenic electrode: Leave at −140°C setpoint
   □ Do NOT rapidly warm (prevents thermal shock to components)
   □ Expected cool-down time: 5-10 minutes passively
   □ Optional: If end of week, request controlled warm-up to −100°C
   
3. Vacuum system shutdown (2 min)
   □ Main pump: OFF
   □ Backing pump: OFF
   □ Vent valve: OPEN (to atmosphere for safe venting)
   □ Wait 30 seconds for pressure equilibration
   
4. Gas system shutdown (2 min)
   □ CF₄ flow: 0 sccm (MFC to zero)
   □ O₂ flow: 0 sccm
   □ N₂ purge: 0 sccm
   □ All gas bottle regulators: Verify closed
   
5. RF system shutdown (1 min)
   □ Coil RF: Power OFF
   □ Bias RF: Power OFF
   □ Matching network: Powered down (capacitor motors idle)
   
6. Facility shutdown (2 min)
   □ Facility chiller: Leave running (maintains chamber temperature)
   □ LN₂ dewar connection: Verify closed valve (no leak)
   □ Electrical panel: Leave on (standby power only)
   □ Close and lock control room if secure area

Status: STANDBY
Estimated time to restart next day: 15 minutes
```

## C.6 Weekly Maintenance Checklist

```
Every Monday morning (30 minutes):

Preventive maintenance to extend tool life:

1. Electrode inspection (5 min)
   □ Visual inspection via viewport: Color changes?
   □ Expected: Light tan/brown coating (normal corrosion)
   □ If black/charred: Call service (abnormal)
   □ Record coating color: _________
   
2. Chamber pressure test (5 min)
   □ Close all valves, pump chamber to <0.1 mTorr
   □ Stop pump, wait 5 minutes
   □ Record pressure: _______ mTorr
   □ Acceptable: <1 mTorr rise (good vacuum integrity)
   □ If >5 mTorr rise: Leak suspected, call service
   
3. Gas line purge (10 min)
   □ Plasma OFF, vacuum maintained
   □ Set CF₄ flow to 100 sccm for 60 seconds
   □ Set O₂ flow to 100 sccm for 60 seconds
   □ Purpose: Purges residual moisture from lines
   □ Reduces ice formation in electrode
   
4. RF matching baseline (5 min)
   □ Coil power: 1000 W
   □ Measure and record P_reflected: _____ W
   □ If >10 W: Perform manual tuning (see Section C.4)
   □ If <5 W: Tuning valid, no action needed
   
5. Cryogenic system check (5 min)
   □ LN₂ dewar level: Must be >50% full
   □ If <50%: Schedule refill (order before running out!)
   □ Cooling lines: No visible frost accumulation?
   □ Expected light frost, but ice >5mm indicates moisture issue
```

---

## C.7 Troubleshooting Quick Reference

```
Problem 1: Etch rate too slow (<30 nm/min when 50 nm/min expected)

Likely causes (check in order):
  1. Temperature too warm: Check PID setpoint, confirm −140°C
     → Solution: Verify LN₂ supply adequate, check electrode thermocouple
     
  2. Coil power low: Confirm 2000 W coil power
     → Solution: Check RF generator display, increase if needed
     
  3. Pressure too high: Check MFC setpoint, should be 50 mTorr bulk
     → Solution: Adjust pressure controller to lower setpoint
     
  4. Gas supply depleted: Check CF₄ bottle pressure
     → Solution: Replace gas bottle (below 20 psi, order new)
     
  5. Electrode corroded: Impedance changed, reduced coupling
     → Solution: Schedule electrode replacement (if >50K wafers)

Problem 2: Reflected power > 20 W (tuning network failing)

Causes:
  1. Impedance drift: Electrode condition changed
     → Immediate: Manual re-tune (Section C.4)
     → Long-term: Schedule electrode replacement
     
  2. Capacitor stuck: Motor drive may be jammed
     → Solution: Power cycle matching network, try auto-tune again
     
  3. Tuning limit reached: Impedance outside network range
     → Solution: Change to π-match network (if available)

Problem 3: Scallops visible in profile (>20 nm peak-to-valley)

Causes:
  1. Ion energy too high: E_ion creating large wavelength ripples
     → Solution: Reduce bias power 10-20%, decrease E_ion
     
  2. Pulsed recipe needed: Continuous plasma creates deep scallops
     → Solution: Switch to pulsed recipe (50% duty cycle)
     
  3. Etch time excessive: Long etch grows scallops larger
     → Solution: Reduce etch duration or use faster selectivity recipe
```

---

**Appendix C Version:** 1.0

