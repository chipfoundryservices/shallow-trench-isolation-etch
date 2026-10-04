# Appendix F: Endpoint Detection & Tuning

## F.1 Optical Endpoint Monitoring

### Laser Reflectance Method

```
Principle:

Laser (wavelength 405-670 nm typical) shines on wafer surface
Light reflects from different materials with different intensities

Si reflectance: ~30-40% (moderate reflection)
SiO₂ reflectance: ~15-20% (less reflective, more absorptive)
Metal reflectance: >80% (very reflective, if exposed)

During STI etch:
  Wafer initially: Resist + Si + oxide (SiO₂ liner)
  Reflectance: ~30% (Si-dominated)
  
  As etch proceeds:
    Resist removed: Reflectance drops to ~25% (exposed Si)
    Si etched: Reflectance stable ~25%
    Near oxide: Reflectance drops ~20% (SiO₂ exposed)
    
  Oxide reached: Reflectance ~15-18% (SiO₂ dominant)
  
Endpoint detection:
  Algorithm monitors reflectance signal R(t)
  When dR/dt (slope) changes sign, oxide reached
  Endpoint trigger: R drops below threshold (e.g., 20%)
  
Signal profile:

Time (sec) | Material    | Reflectance (R) | dR/dt | Endpoint?
0-5        | Resist/Si   | 30%            | −0.5% | No
5-50       | Si bulk     | 28-25%         | −0.1% | No
50-100     | Si near ox  | 24-20%         | −0.2% | No
100-105    | SiO₂ layer  | 18%            | +2%   | YES! (transition)
105+       | Oxide       | 16-18%         | stable| Oxide layer
```

### Algorithm & Control Logic

```
Endpoint algorithm (pseudo-code):

```
while TRUE:
  R_now = read_laser_reflectance()
  
  if iteration == 0:
    R_baseline = R_now
    dR_threshold = −0.3% (threshold for change rate)
    t_debounce = 2 seconds
    
  dR = (R_now − R_prev) / dt
  
  if dR > dR_threshold:  // Reflectance increasing (oxide reached)
    counter_positive += 1
  else:
    counter_positive = 0  // Reset if trend changes
    
  if counter_positive > (t_debounce / dt):  // Sustained for >2 sec
    TRIGGER_ENDPOINT()
    STOP_PLASMA()
    break
    
  R_prev = R_now
  wait(dt = 0.5 sec)  // Update every 0.5 seconds
```

### Tuning Parameters

```
Endpoint threshold optimization:

Too aggressive (endpoint early):
  Oxide not fully exposed
  Selectivity poor, oxide over-etched
  Yield loss: Leakage high

Too conservative (endpoint late):
  Oxide over-exposed, SiO₂ sputtered
  Profile degraded
  Yield loss: Leakage higher

Calibration procedure:

1. Run 10 test wafers with fixed etch time (120 sec)
   Record endpoint detection times
   
2. Stop etch at various times for each wafer
   Measure oxide thickness remaining (XRR)
   
3. Plot:
   Etch time vs. Oxide remaining
   Endpoint time vs. Oxide remaining
   
4. Find sweet spot:
   Oxide remaining: 12-13 nm (good margin from initial 15 nm)
   = ~2 nm loss from sputtering during etch
   
5. Adjust algorithm threshold:
   If endpoint early: Decrease dR_threshold (less aggressive)
   If endpoint late: Increase dR_threshold (more aggressive)

Typical calibration data:

Etch Time (sec) | Endpoint Triggered? | Oxide Remaining (nm) | Status
90             | Yes                | 10                  | Early (oxide over-etched)
100            | Yes                | 12                  | Good
110            | Yes                | 14                  | Late (oxide not fully ready)
120            | No                 | 15                  | Very late (no endpoint trigger)

Decision: Use ~100 sec fixed etch time with endpoint detection
          Provides 2-4 sec margin for process variation
```

---

## F.2 In-Situ Mass Spectrometry (Diagnostic, not control)

### Real-Time Gas Phase Analysis

```
Quadrupole mass spectrometer (QMS) in plasma chamber:

Monitor plasma species during etch:
  Mass 19 (F+): Fluorine ion intensity
  Mass 20 (F2+): F2 ion
  Mass 28 (Si+): Silicon ion (indicates Si etch)
  Mass 44 (SiF2+): Etch byproduct (Si + 2F)
  Mass 64 (SiF4): Complete etch product (Si + 4F)
  
During Si etch:
  Signals M/Z = 28, 44, 64 increase (Si etching)
  Signal M/Z = 19 constant (F supply constant)
  
When approaching oxide:
  M/Z = 28 drops (less Si sputtered)
  M/Z = 44 drops (less SiF2 produced)
  M/Z = 64 drops (less SiF4 produced)
  New signals appear:
    M/Z = 16 (O from oxide)
    M/Z = 18 (H2O, environmental)
  
Endpoint detection:
  When M/Z 28 drops below threshold: Oxide reached
  More selective than optical (detects chemistry change)
  But slower response (mass spec has lag)
  
Typical detection time: 5-10 seconds after chemical change
Optical detection: 1-2 seconds (faster)

Advantage: Chemical confirmation
Disadvantage: Complex calibration, expensive instrument ($100K+)

Production use: Diagnostic/validation, not primary control
```

---

## F.3 Troubleshooting Endpoint Issues

### Problem: Endpoint Not Triggering (Etch Runs Too Long)

```
Cause 1: Optical window contaminated
  Symptom: Reflectance signal noisy, no clear trend
  Fix:
    □ Stop etch immediately
    □ Open chamber, inspect optical window
    □ Clean with soft cloth + isopropanol
    □ Reassemble, test with dummy wafer
    
  Time to fix: ~15 minutes (simple)
  Cost: Minimal (cleaning solution ~$20)

Cause 2: Algorithm threshold set too high
  Symptom: dR/dt always below threshold
  Fix:
    □ Reduce dR_threshold by 50% (e.g., −0.3% → −0.15%)
    □ Test on 3 dummy wafers
    □ Record endpoint times vs. standard recipe
    □ If endpoint now triggers: Recalibrate threshold
    
  Time to fix: ~30 minutes (tuning)
  Cost: $0 (software adjustment)

Cause 3: Laser wavelength mismatch
  Symptom: Reflectance signal too weak
  Fix:
    □ Check laser wavelength setting (usually 632 nm He-Ne)
    □ Verify laser power output (should be >1 mW)
    □ If weak: Clean laser optics (dust contamination)
    □ If still weak: Replace laser module (~$2K)
    
  Time to fix: 1-2 hours (optics work)
  Cost: ~$2K if laser replacement needed

Problem: Endpoint Triggers Too Early (Oxide Over-Etched)

Cause 1: Algorithm too aggressive
  Symptom: Triggers before expected endpoint time
  Fix:
    □ Increase dR_threshold (e.g., −0.3% → −0.5%)
    □ Measure oxide thickness after adjusted etch
    □ If margin good (12-13 nm remain): Calibration done
    
  Time to fix: ~30 minutes
  Cost: $0

Cause 2: Reflectance baseline shifted
  Symptom: R values lower than historical, dR appears high
  Fix:
    □ Check for window contamination (see above)
    □ Verify Si surface clean (no process residue)
    □ Run QMS trace to confirm chemistry (is Si still being etched?)
    
  Time to fix: 1-2 hours (diagnostic)
  Cost: $0-500 (inspection labor)
```

---

**Appendix F Version:** 1.0

