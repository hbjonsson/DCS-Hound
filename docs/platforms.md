# Available ELINT Platforms

Complete list of units capable of ELINT operations in Hound.

---

## Platform Selection Guide

### Quick Recommendations:

**Best Overall:**

- 🥇 **TV Tower** (static) - Exceptional accuracy
- 🥇 **C-130** - Excellent airborne platform
- 🥇 **RC-135W** (SSS mod) - Real ELINT aircraft, very accurate

**Best By Role:**

- **Long-range picket:** RC-135W (mod), Tu-95
- **Medium range:** C-130, An-26B
- **Ground stations:** Comms Tower M, TV Tower, Command Center
- **Mobile ground:** SPK-11, Patriot CR
- **Low observable:** Smaller aircraft (worse accuracy trade-off)

---

## Understanding Platform Specs

### Accuracy Columns:

**C Band / H Band Resolution** - Angular accuracy in degrees against specific band.

- Lower = Better
- Most SAM radars operate in C/H bands
- Example: `0.65° / 0.07°` is excellent

**Minimum Band** - Lowest frequency band the platform can detect with some accuracy

- **A** = Can detect everything (best)
- **C** = Struggles with low-frequency radars
- **D** = Only effective against high-frequency radars

**Note:** Hound rejects datapoints with >10° error automatically.

---

## Airborne Platforms

### Large Aircraft (Best)

| Platform    | C Band / H Band Accuracy | Min. Band | Notes                                 |
| ----------- | ------------------------ | --------- | ------------------------------------- |
| **C-130**   | 0.65° / 0.07°            | A         | Excellent all-around, common          |
| **C-130J**  | 0.67° / 0.07°            | A         | DCS:C-130                             |
| **Tu-95**   | 0.50° / 0.05°            | A         | Excellent accuracy, large size        |
| **Tu-142**  | 0.46° / 0.05°            | A         | Maritime patrol version of Tu-95      |
| **An-26B**  | 0.96° / 0.10°            | A         | An-26RR/RT ELINT stand-in             |

### Medium Aircraft

| Platform        | C Band / H Band Accuracy | Min. Band | Notes                         |
| --------------- | ------------------------ | --------- | ----------------------------- |
| **S-3B Viking** | 1.10° / 0.12°            | A         | Carrier-based ASW, good ELINT |

### AEW / AWACS

| Platform         | C Band / H Band Accuracy | Min. Band | Notes                                 |
| ---------------- | ------------------------ | --------- | ------------------------------------- |
| **E-2D Hawkeye** | 0.93° / 0.10°            | A         | ALQ-217 ESM, four-quadrant            |
| **E-3A Sentry**  | 0.49° / 0.05°            | A         | Cheek-mounted ESM                     |
| **A-50**         | 0.45° / 0.05°            | A         | Russian AWACS                         |

### Tactical Aircraft (Fighter/Attack)

| Platform           | C Band / H Band Accuracy | Min. Band | Notes                     |
| ------------------ | ------------------------ | --------- | ------------------------- |
| **F-16C Block 50** | 15.79° / 1.69°           | D         | HTS pod, limited accuracy |
| **JF-17**          | 7.05° / 0.76°            | C         | KG-600 SPJ pod            |
| **Mirage F1**      | 6.19° / 0.66°            | C         | Cyril pod                 |
| **AJ-37 Viggen**   | 5.09° / 0.55°            | C         | U22 pod                   |
| **Su-25T**         | 6.54° / 0.70°            | C         | Fantasmagoria pod         |
| **Su-25TM**        | 6.54° / 0.70°            | C         | Fantasmagoria pod         |
| **Su-24M**         | 6.54° / 0.70°            | C         | Fantasmagoria             |
| **Su-24MR**        | 5.09° / 0.55°            | C         | Tangazh system            |
| **A-6E** (PlaceHolder for EA-6B) | 2.54° / 0.27°            | B         |  ALQ-167 ECM (ALQ-99 placeholder)           |
| **F/A-18C** (Placeholder for EF-18G)        | 1.68° / 0.18°            | A         | AN/ASQ-T50 TCTS Pod - ACMI Pod (AN/ALQ-218 placeholder)  |



**Note:** Tactical aircraft have smaller antennas = lower accuracy. Best used as gap-fillers or when precision platforms unavailable.

---

## Helicopters

**Generally lower accuracy than fixed-wing due to smaller size.**

| Platform           | C Band / H Band Accuracy | Min. Band | Notes                             |
| ------------------ | ------------------------ | --------- | --------------------------------- |
| **UH-60A**         | 2.86° / 0.31°            | B         | Medium transport                  |
| **SH-60B**         | 2.86° / 0.31°            | B         | Naval variant                     |
| **Mi-8MT**         | 2.86° / 0.31°            | B         | Russian medium transport          |
| **Ka-27**          | 5.73° / 0.61°            | C         | Naval helicopter                  |

**Use Cases:**

- Mountain-top deployment
- Quick-reaction ELINT
- Transport + intelligence dual role
- Low-altitude operations

---

## Ground Units

| Platform           | C Band / H Band Accuracy | Min. Band | Notes                |
| ------------------ | ------------------------ | --------- | -------------------- |
| **SPK-11**         | 1.53° / 0.16°            | A         | Mobile ELINT vehicle |
| **SAM Patriot CR** | 1.53° / 0.16°            | A         | Control room, mobile |

**Advantages:**

- Can be positioned on high terrain
- No fuel/endurance limits
- Can accompany ground forces

**Disadvantages:**

- Fixed or slow-moving
- Limited by terrain line of sight
- Vulnerable to ground attack

---

## Static Objects (Best Ground-Based)

| Platform           | C Band / H Band Accuracy | Min. Band | Notes                     |
| ------------------ | ------------------------ | --------- | ------------------------- |
| **TV Tower**       | 0.10° / 0.01°            | A         | **Best overall accuracy** |
| **Comms Tower M**  | 0.21° / 0.02°            | A         | Excellent, very tall      |
| **Command Center** | 0.37° / 0.04°            | A         | Building, high accuracy   |

**Advantages:**

- Exceptional accuracy (largest "antennas")
- Unlimited endurance
- Can be on mountains/hills
- Cheap in terms of mission resources

**Disadvantages:**

- Completely fixed
- Single point of failure
- Can be destroyed
- Terrain dependent

**Best Practice:**

- Place on highest terrain available
- Provides excellent baseline for airborne platforms
- Acts as reference point for triangulation

---

## Community Mods

Supported third-party aircraft:

| Platform                | C Band / H Band Accuracy | Min. Band | Notes                          |
| ----------------------- | ------------------------ | --------- | ------------------------------ |
| **RC-135W** (SSS)       | 0.55° / 0.06°            | A         | Real ELINT aircraft, excellent |
| **EC-130H** (SSS)       | 0.77° / 0.08°            | A         | Compass Call variant           |
| **P-3C Orion** (MAM)    | 0.75° / 0.08°            | A         | Maritime patrol                |
| **P-8A Poseidon** (CLP) | 0.61° / 0.07°            | A         | Modern P-3 replacement         |
| **TU-214R** (CLP)       | 0.50° / 0.05°            | A         | Russian recon aircraft         |
| **Shavit** (IDF)        | 0.78° / 0.08°            | A         | Israeli ELINT                  |
| **EF-18G** (CJS)        | 1.68° / 0.18°            | A         | Growler equivalent, excellent  |
| **EA-6B Prowler** (VSN) | 2.54° / 0.27°            | B         | Electronic warfare             |
| **UH-60L**              | 2.86° / 0.31°            | B         | Modernized Blackhawk           |
| **Su-22M4**             | 6.54° / 0.70°            | C         | Wyuga pod                      |


**Note:** Requires respective mods installed. Hound will work without mods but won't detect these units.

---

## Realistic DF Data

Used when `enableRealisticDF()` is on ([How It Works: Realistic DF](how-it-works.md#realistic-df-opt-in)). Accuracy columns above are legacy-mode values (wavelength / antenna size only).

**Antenna size rule:** fuselage-side arrays: fuselage length; wingtip / quadrant systems: wingspan; pods: pod length; other entries notional.

**Confidence:** **H** placement in public sources, **M** inferred from predecessor or same family, **L** notional.

| Platform | DF class | Coverage (GHz) | Apertures | Size (m) | Conf. | Basis |
|---|---|---|---|---|---|---|
| RC-135 (`RC135RJ`) | PRECISION | 0.03-40 | SIDE_NOSE | 41.5 (length) | H sides / L nose | AEELS side-facing ELINT antennas in cheek fairings ([FAS](https://irp.fas.org/program/collect/rivet_joint.htm), [GlobalSecurity](https://www.globalsecurity.org/intell/systems/rivet_joint.htm)); thimble nose contents not public |
| Tu-214R (`CLP_TU214R`) | PRECISION | 0.03-40 | SIDE | 46.1 (length) | H | SIGINT antenna on side fuselage aft of wing ([GlobalSecurity](https://www.globalsecurity.org/military/world/russia/tu-214r.htm)) |
| Shavit (`Shavit`) | PRECISION | 0.03-40 | SIDE | 29.4 (G550 length) | M | ELINT arrays in radome beneath forward fuselage ([AIN](https://backend.ainonline.com/aviation-news/defense/2016-07-10/elta-offers-wide-variety-istar-solutions)) |
| E-3A | COARSE | 2-18 | SIDE | 46.6 (length) | M | AN/AYR-1 2-18 GHz ([Armada International](https://www.armadainternational.com/2019/09/best-supporting-actor)); cheek-mounted ESM |
| E-2C / E-2D | TACTICAL | 0.5-18 | QUAD | 24.6 (span) | H | ALQ-217: four antennas, 360 deg in low/mid/high bands ([Lockheed Martin](https://sustainability.lockheedmartin.com/content/dam/lockheed-martin/rms/documents/electronic-warfare/AN-ALQ-217-brochure.pdf)) |
| P-3C (`P3C_Orion`) | TACTICAL | 0.5-18 | QUAD | 30.4 (span) | H | ALR-77 wingtip interferometers, 360 deg ([Military Periscope](https://militaryperiscope.com/weapons/sensorselectronics/electronic-support-measureselectronic-warfare/analr-77/overview)) |
| P-8A (`CLP_P8`) | TACTICAL | 0.5-18 | QUAD | 37.6 (span) | L | ALQ-240 ESM; placement not public ([Aviation Today](https://www.aviationtoday.com/2012/10/04/northrop-grummans-p-8a-esm-receives-official-nomenclature/)) |
| S-3B | TACTICAL | 0.5-18 | QUAD | 20.9 (span) | M | ALR-76 form-fit replacement for wingtip ALR-47 ([avgeekery](https://avgeekery.com/war-hoover-the-fabulously-flexible-lockheed-s-3-viking/2/)) |
| A-50 | COARSE | 0.5-18 | QUAD | 50.5 (span) | L | No public ESM placement |
| EA-18G / FA-18C stand-in | TACTICAL | 0.5-18 | QUAD | 13.6 (span) | M | ALQ-218 wingtip pods with low-band receivers ([Wikipedia](https://en.wikipedia.org/wiki/AN/ALQ-218), [Military Aerospace](https://www.militaryaerospace.com/home/article/55382784/navy-awards-613-million-northrop-grumman-contract-for-ea-18g-alq-218-receiver-upgrades)) |
| EA-6B / A-6E stand-in | TACTICAL | 0.064-18 | QUAD | 9 | L | ALQ-99 receivers; notional |
| SH-60B | COARSE | 2-20 | QUAD | 8 | M | ALQ-142 is a repurposed SLQ-32 ([Military Periscope](https://www.militaryperiscope.com/weapons/sensorselectronics/electronic-support-measureselectronic-warfare/analq-142/)) |
| F-16C HTS | COARSE, TDOA/FDOA | 2-18 | FORWARD | 1.45 (pod) | L | Pod on intake side ([NMUSAF](https://www.nationalmuseum.af.mil/Visit/Museum-Exhibits/Fact-Sheets/Display/Article/196349)); forward sector from DCS testing only; multi-ship TDOA per owner input |
| Su-24M / Su-25T / Su-25TM | COARSE | 1.2-11 | FORWARD | 3.5 | L | Kh-58 seeker range as proxy ([DCS forum](https://forum.dcs.world/topic/289968-no-la-launch-authorization-kh-58-on-specific-search-radars)) |
| Su-24MR / Su-22M4 (KKR) | COARSE | 0.5-18 | SIDE | 4.5 / 3.5 | M | Tangazh antennas on pod sides ([16va.be](https://16va.be/page_su-17_kkr-1t.html)) |
| Mirage F1 (Syrel / ASTAC) | COARSE | 2-18 | SIDE | 3.7 / 4 | L | Notional |
| C-130 / C-130J / EC-130, An-26B, Tu-95MS | TACTICAL | 0.03-40 | SIDE | length | L | Notional stand-ins |
| Tu-142 | COARSE | 0.5-18 | SIDE | 50 | L | Notional |
| AJS37, JF-17 | AMPLITUDE | 2-18 | omni | pod | L | Jammer pods with cueing receivers |
| Helicopters (UH-60A/L, Mi-8MT, Ka-27) | AMPLITUDE | 2-18 | omni | - | L | Notional |
| Ground (towers, Command Center, Patriot AMG, SPK-11) | PRECISION / TACTICAL | 0.03-40 | omni | height | L | Notional fixed / mast stations |

`ins_error` values (platform navigation error, used with `enablePlatformPosErrors()`) are notional: 0 m for GPS-aided platforms, 50-100 m for INS-only types.

---

## Platform Selection Strategy

### For Maximum Accuracy:

1. **Primary:** 2-3 high-altitude large aircraft (C-130, RC-135W mod)
2. **Baseline:** 1-2 static towers on high ground
3. **Backup:** Additional platforms for redundancy

### For Wide Coverage:

1. **Pickets:** Aircraft at different cardinal directions
2. **Altitude separation:** Some high (30k ft), some medium (20k ft)
3. **Static anchors:** Ground stations at corners of AO

### For Survivability:

1. **Standoff distance:** Keep platforms outside threat range
2. **Redundancy:** More platforms = can afford losses
3. **Mix types:** Air + ground = harder to eliminate all

### Budget/Limited Resources:

1. **Minimum:** 2 x C-130 in racetracks
2. **Better:** 2 x C-130 + 1 x Comms Tower
3. **Optimal:** 3 x C-130 + 2 x Static objects

---

## Mission Planning Examples

### Large Theater (Syria/Caucasus):

```
- C-130 "ELINT North" - Racetrack north at 28,000 ft
- C-130 "ELINT South" - Racetrack south at 28,000 ft
- RC-135W (mod) "ELINT East" - Racetrack east at 32,000 ft
- TV Tower/Cooms Tower - On high terrain
```

### Small Theater (Persian Gulf):

```
- C-130 "ELINT Overwatch" - Figure-8 pattern at 25,000 ft
- SPK-11 "ELINT Ground" - High ground west side
- Comms Tower "ELINT Tower" - Fixed position east
```

### Low-Observable Mission:

```
- Viggen "ELINT 1" - Dash in, collect, dash out
- JF-17 "ELINT 2" - Different axis
- SPK-11 "ELINT Ground" - Maintain baseline when aircraft egress
```

### Ground Force Support:

```
- UH-60A "ELINT Helo 1" - Deployed to mountain-top
- UH-60A "ELINT Helo 2" - Deployed to different mountain
- SPK-11 "ELINT Mobile" - Travels with ground force
```

---

## Platform Positioning Tips

### Altitude Considerations:

**Fixed-Wing:**

- **Minimum:** 15,000 ft (survival vs detection trade-off)
- **Optimal:** 25,000-30,000 ft (range + safety)
- **Maximum:** 35,000+ ft if capable (best range)

**Helicopters:**

- **On ground:** Mountain-tops, hilltops
- **Hovering:** High terrain positions (fuel permitting)
- **Limited altitude ceiling:** Don't expect high-altitude performance

**Ground/Static:**

- **Elevation matters:** Every foot helps
- **Check line-of-sight:** Use DCS mission editor terrain view
- **Clear horizons:** Avoid valleys and depressions

### Spacing:

**Minimum Separation:** 20-30 nm for nearby targets
**Optimal Separation:** 50-100+ nm for long-range coverage
**Avoid:** Straight lines (poor geometry)

### Patterns:

**Racetracks:** Constant coverage, predictable
**Orbits:** Focused on area, changing geometry
**Figure-8:** Good aspect variation
**Static Grid:** Multiple fixed positions

---

## Adding Platforms in Code

### Automatic Platform Detection

**Default Behavior (Enabled):**

Hound automatically detects and adds units with ELINT payloads when they spawn:

```lua
-- No code needed! Hound automatically adds:
-- - F-16C with HTS pod
-- - Su-25T/TM with Fantasmagoria
-- - JF-17 with KG-600
-- - Viggen with U22
-- - Any other unit spawning with ELINT equipment
```

**How It Works:**

1. Unit spawns with ELINT payload (HTS, Fantasmagoria, etc.)
2. DCS triggers `S_EVENT_WEAPON_ADD` event
3. Hound validates unit type + weapon against internal database
4. If valid, unit is automatically added as ELINT platform

**DCS Limitation:** Only works for units **spawning** with pods. Adding pods to already-spawned units will NOT trigger detection.

**Player Aircraft:**

This enables player-based ELINT missions without manual configuration:

```lua
HoundBlue = HoundElint:create(coalition.side.BLUE)
HoundBlue:enableController({freq = "251.000", modulation = "AM"})
HoundBlue:systemOn()

-- Players spawn in F-16C with HTS → Automatically become ELINT platforms
-- Radio menu automatically updates when players spawn/leave
```

**Disable Automatic Detection:**

```lua
-- Set BEFORE creating Hound instance
HOUND.AUTO_ADD_PLATFORM_BY_PAYLOAD = false

HoundBlue = HoundElint:create(coalition.side.BLUE)
-- Now you must manually add all platforms
HoundBlue:addPlatform("ELINT_C130")
```

---

### Manual Platform Addition

### Basic:

```lua
HoundInstance:addPlatform("ELINT_C130")
```

### Multiple:

```lua
HoundInstance:addPlatform("ELINT_C130_1")
HoundInstance:addPlatform("ELINT_C130_2")
HoundInstance:addPlatform("ELINT_Tower")
```

### Dynamic (Add Later):

```lua
-- Add after system is already running
HoundInstance:addPlatform("Reinforcement_ELINT")
```

### Remove:

```lua
HoundInstance:removePlatform("ELINT_C130_1")
```

**Note:** Use exact unit/pilot name, NOT group name!

---

### Radio Menu Behavior

**Automatic Menu Updates:**

Hound automatically refreshes F10 radio menus when:

**Player Events:**

- Player spawns (`S_EVENT_BIRTH`)
- Player leaves aircraft (`S_EVENT_PLAYER_LEAVE_UNIT`)
- Pilot dies (`S_EVENT_PILOT_DEAD`)
- Pilot ejects (`S_EVENT_EJECTION`)

**Contact Events:**

- New SAM site created (`SITE_CREATED`)
- Site type classified (`SITE_CLASSIFIED`)

**BDA Events** (only when BDA enabled):

- Site destroyed (`SITE_REMOVED`)
- Radar destroyed (`RADAR_DESTROYED`)

**Why This Matters:**

- **Player Events:** Menus stay current as players join/leave
- **Contact Events:** New threats immediately appear in menu for reporting
- **BDA Events:** Destroyed contacts removed from menu to avoid clutter
- No stale menu items

**Performance Notes:**

- Player events only trigger for aircraft/helicopters (ground vehicles/ships ignored)
- Contact/BDA events update menu for all players simultaneously
- Menu updates are lightweight and don't impact performance

---

## Platform Limitations

### What Doesn't Work:

❌ Units without proper ELINT equipment (Hound checks unit type)
❌ Destroyed/dead units (removed automatically)
❌ Units with line-of-sight blocked by terrain
❌ Units > ~400nm from radar (even if LOS exists)

### Performance Notes:

Each platform scans every radar every cycle (5 seconds default):

- **10 platforms x 50 radars = 500 checks every 5 seconds**
- Usually not a problem
- For huge missions, see [Performance Tuning](performance.md)

---

## Summary

**Choosing Platforms:**

- **Accuracy matters:** Use best available
- **Geometry matters:** Wide separation, different angles
- **Redundancy matters:** Lose one, keep working
- **Height matters:** Higher = better range

**Best Bang for Buck:**

- 2 x C-130 (airborne)
- 1 x Comms Tower or TV Tower (ground reference)

**Next Steps:**

- **Configure in mission:** [Basic Configuration](basic-configuration.md)
- **Understand detection:** [How Hound Works](how-it-works.md)
- **Optimize setup:** [Advanced Configuration](advanced-configuration.md)
