# Realistic DF (455 Fork)

Realistic direction-finding (DF) error model for Hound ELINT. Default on (`realisticDF = true`). ELINT produces search areas consistent with real-world DF constraints; multi-ship TDOA produces fixes.

Tracking issue: [hbjonsson/DCS-Hound#1](https://github.com/hbjonsson/DCS-Hound/issues/1)

---

## Problem Addressed

Legacy Hound accuracy, single standoff platform, 13 minutes: 95% ellipse minor axis 157–600 m, ratings "High". Monte Carlo of the legacy model (RC-135 racetrack, SA-6 at 150 km, 30 min): median error 92 m.

Causes in the legacy model:

| Cause | Effect |
|---|---|
| Independent random bearing error per 10 s sample | Errors average away; accuracy improves without limit |
| Accuracy = wavelength / antenna size, no floor | 40 m "antenna" at H band = 0.05° |
| No SNR or range dependence | 300 km as accurate as 30 km |
| Kalman filter assumes independent noise | Ellipse shrinks with every sample |
| No antenna field of view, attitude, masking | Every platform sees 360° in any bank |
| No receiver frequency coverage or sensitivity | Every platform hears every radar, main lobe or not |
| Platform nav error redrawn per sample | Nav error averages away |

---

## Model

Per sample (10 s), per platform, per emitting radar:

1. **Receiver coverage** (`rx`): emitter frequency outside platform coverage → no datapoint.
2. **Intercept link budget:** main-lobe intercept range from the radar's DCS detection range and the platform's receiver sensitivity; sidelobes −30 dB (EWR −20 dB). Scanning radars sweep the main lobe past every platform. Tracking radars point the main lobe at their target; other platforms outside a 2° beam hear sidelobes only. Out of range → no datapoint.
3. **Antenna apertures** (`ap`): line of sight rotated into the body frame (heading, pitch, roll). Outside every aperture or masked in a bank → no datapoint.
4. **Bearing error:**
   - Noise: DF-class floor or wavelength / antenna size (larger), × 1 / cos(off-boresight), growing with range within 10 dB of receiver sensitivity.
   - Persistent bias: drawn once per platform / emitter / 30° aspect sector.
   - Coning residual: azimuth-only arrays measure `sin(psi_m) = cos(el) · sin(psi)`; corrected with the elevation to the current estimate.
5. **Navigation error:** with `enablePlatformPosErrors()`, `ins_error` offset held per platform for 600 s.
6. **TDOA / FDOA:** two or more `tdoa` platforms (F-16C HTS) intercepting the same emitter in one scan add pairwise range-difference and Doppler-difference updates to the Kalman estimate.
7. **Uncertainty:** the Kalman filter tracks every bias as a Schmidt-Kalman consider parameter; the ellipse includes the position error the biases cause. Before the Kalman filter starts, the cluster ellipse adds the cross-bearing bias error.

### DF Classes

| Class | Bias (1σ) | Noise floor (1σ) | Receiver sensitivity | Sidelobe intercept of a 75 km SAM radar |
|---|---|---|---|---|
| PRECISION | 0.5° | 0.2° | −95 dBm | beyond radar horizon |
| TACTICAL | 1.0° | 0.5° | −80 dBm | ~160 km |
| COARSE | 2.5° | 1.0° | −70 dBm | ~50 km |
| AMPLITUDE | 6.0° | 3.0° | −60 dBm | ~16 km |

### Aperture Presets

| Preset | Coverage (body frame) |
|---|---|
| SIDE | port and starboard ±60°, ±45° elevation; blind ±30° about nose and tail |
| SIDE_NOSE | SIDE plus nose ±30° |
| QUAD | four 90° quadrants, 360° |
| FORWARD | nose ±70° |
| (none) | omnidirectional |

Per-platform class, coverage, aperture, antenna size and sources: [Platforms: Realistic DF Data](platforms.md#realistic-df-data).

---

## Platform Database

| Change | Platforms |
|---|---|
| Removed (no real radar-ELINT variant) | Cow, C-17A, CH-47D, CH-53E, Mi-26, UH-1H, IL-76MD, An-30M, C-47, H-6J, Hercules (mod) |
| RC-135 class | `RC135RJ` mod only; no stock stand-in |
| Antenna size from airframe | fuselage-side arrays: fuselage length; wingtip / quadrant systems: wingspan |
| TDOA capable | F-16C HTS |

---

## Results

### Monte Carlo (Hound UPLKF and DF code, LuaJIT, 200–300 runs per case)

| Case | Median error | 95% ellipse | Truth inside 95% ellipse |
|---|---|---|---|
| Legacy: RC-135 racetrack, SA-6 at 150 km, 30 min | 92 m | 1.5 km × 180 m | 100% |
| RC-135 racetrack, SA-6 at 150 km, 5 / 10 / 30 min | 2.7 / 2.9 / 3.4 km | ~20 × 5 km | 96 / 94 / 91% |
| F-16 HTS two-ship, AOA, SA-6 tracking elsewhere, 5 min | 1.0 km | 6.2 × 3.0 km | 96% |
| F-16 HTS two-ship + TDOA/FDOA | 0.8 km | 6.1 km × 100 m | 96% |
| F-16 HTS three-ship + TDOA/FDOA | 64 m | 364 × 73 m | 99% |

### Live Server (c2.455aew.com, single platform `ELINT1`, 14 min)

| | Legacy | Realistic DF |
|---|---|---|
| Minor axis | 157–600 m | 5–8 km |
| Major axis | 3–6.5 km | 8–31 km, shrinking with new aspects |
| Ratings | 2 of 7 "High" | 2 "Low", 5 "Unactionable" |
| Estimate behavior | converges to a point | moves 1–13 km as aspect changes |

---

## Tuning

| Setting | Default | Effect |
|---|---|---|
| `HOUND.DB.DfClass` | table above | bias, noise floor, receiver sensitivity per class |
| `HOUND.DF_SECTOR_DEG` | 30 | aspect sector width sharing one bias |
| `HOUND.DF_SNR_RANGE_FACTOR` | 0.316 | fraction of intercept range where noise starts growing (10 dB margin) |
| `HOUND.DF_SIDELOBE_DB` / `HOUND.DF_EWR_SIDELOBE_DB` | −30 / −20 | radar sidelobe level |
| `HOUND.DF_RADAR_GAIN_DBI`, `HOUND.DF_RADAR_SENS_DBM`, `HOUND.DF_REF_RCS` | 35, −110, 5 | link budget reference |
| `HOUND.DF_TRACK_BEAMWIDTH_DEG` | 2 | tracking radar main lobe width |
| `HOUND.DF_NAV_DRIFT_INTERVAL` | 600 | seconds a nav error offset is held |
| `HOUND.TDOA_SIGMA_NS` / `HOUND.FDOA_SIGMA_HZ` | 50 / 10 | TDOA / FDOA measurement error |
| `HOUND.DF_DEBUG` | false | logs `[Hound](DF) <unit> err= major= minor= withinMajor=` against truth each process cycle |

`disableRealisticDF()` restores the legacy model.

---

## Validation

- Unit tests (`demo_mission/hound_unit_test/extras/`): `TestDfError`, `TestDfErrorBandGate`, `TestInterceptRanges`, `TestIsInMainLobe`, `TestApertureGeometry`, `TestDfBias`, `TestEllipseFromCov`, `TestBiasCov`, `TestCovFromEllipse`, `TestKalmanBiasSens`, `TestKalmanTdoaFdoa`, `TestNavErr`, `Test_01_init_04_ConfigRealisticDF`. Pass in LuaJIT against source; DCS run pending.
- In-DCS calibration: `HOUND.DF_DEBUG = true`; `withinMajor=true` on ≥ 90% of lines indicates a consistent ellipse.

---

## Limitations

- Scanning radars are assumed to sweep the main lobe past each platform every scan; scan dwell and duty cycle are not modelled.
- Crossing flight paths (baseline collapsing mid-run) give over-confident ellipses (~75% coverage).
- TDOA/FDOA apply only after a contact has a Kalman estimate.
- Notional values: receiver sensitivities, TDOA/FDOA errors, `ins_error`, most aperture and coverage assignments (confidence per platform in [platforms.md](platforms.md#realistic-df-data)).

---

## Sources

- Torrieri, *Statistical Theory of Passive Location Systems*, US Army CM/CCM-83-1, DTIC [ADA128346](https://apps.dtic.mil/sti/pdfs/ADA128346.pdf); IEEE Trans. AES 20(2), 1984.
- Stansfield, "Statistical theory of d.f. fixing", J. IEE 94, 1947.
- Poisel, *Electronic Warfare Target Location Methods*, Artech House, 2012.
- Wiley, *ELINT: The Interception and Analysis of Radar Signals*, Artech House, 2006.
- [US 6,061,022](https://patents.google.com/patent/US6061022): amplitude vs phase DF accuracy; coning `sin(psi_m) = cos(el) · sin(psi)`.
- [US 5,457,466](https://patents.google.com/patent/US5457466), US 6,784,840: coning error growth with elevation and attitude.
- US 5,526,001: bias-dominated bearings-only geolocation.
- DTIC [ADB014135](https://apps.dtic.mil/sti/pdfs/ADB014135.pdf): ESM interferometer field of view; DTIC [ADP004113](https://apps.dtic.mil/sti/html/tr/ADP004113/index.html): installed antenna patterns.
