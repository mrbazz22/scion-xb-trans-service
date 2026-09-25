# JDM Transaxle — Solenoid Identification & Replacement Notes

**Context:** the installed transaxle is a **JDM U241E** (~50k mi). The original US-market U241E
(220k mi) is on the hoist, stripped for parts.

**Key finding (2026-09-25):** the two units do **not** share a solenoid set. A US-market donor
solenoid will not fit the JDM valve body. This was discovered with the pan off, mid-job.

⚠️ **Verify fitment before ordering anything.** See "What to capture" below.

---

## Measured condition of the installed (JDM) solenoids

Measured with the pan off, 2026-09-25. Meter had a **2.9 Ω lead offset**, but the offset was proven
stable (two solenoids read *identically* at 8 raw), so the corrected values are trustworthy.

| Solenoid | Raw | Corrected | Spec (5.0–5.6 Ω) | Verdict |
|---|---|---|---|---|
| 2-pin (good) | 8 | **5.1 Ω** | in spec | ✅ |
| 2-pin (good) | 8 | **5.1 Ω** | in spec | ✅ |
| **SL2** | 11 | **8.1 Ω** | out of spec (~50%) | ❌ **replace** |

- **Three 2-pin solenoids = SL1, SL2, SLT** (all share the 5.0–5.6 Ω spec)
- **Two 1-pin solenoids = DSL (11–13 Ω) and S4 (11–15 Ω)** — ground through the case body,
  so measure connector-to-body, not terminal-to-terminal

### What the bad SL2 does and doesn't explain

| Solenoid | Performance DTC | Electrical DTC |
|---|---|---|
| **SLT** | **P2714** | P2716 |
| **SL2** | **P0776** | **P0778** |

- The vehicle had **P2714**, which maps to **SLT — not SL2.**
- Neither P0776 nor P0778 was present.
- ⇒ **The out-of-spec SL2 does not explain P2714.** SL2 is an ON/OFF shift solenoid (works with
  SL1 + S4 for 1st–4th); it doesn't produce the slip signature P2714 monitors.
- **Watch item:** if SL2 degrades further it could eventually set P0776/P0778 and trigger
  **fail-safe (limp) mode** — typically stuck in one gear, no upshifts. That's the tell.

---

## Physical differences observed (US-market donor vs JDM installed)

- JDM solenoid **connectors are noticeably "beefier"** (larger) than the US-market parts
- JDM solenoid **bodies are larger** — SL2 confirmed visually larger
- A US-market donor SLT could **not** be matched to any equivalent position on the JDM valve body

**Unresolved:** whether this is a JDM-vs-US-market design difference, a running production change, or
a supersession. No public documentation found either way (see "Research tried" below).

---

## OE part numbers — U140E / U240E / U241E solenoid family

| Solenoid | Toyota OE # | Catalogue description |
|---|---|---|
| Shift #1 (SL1) | **35210-21010** | |
| **Shift #2 (SL2)** | **35220-21010** | "Clutch Control Solenoid Assy, NO.2" |
| Shift #3 | **35230-21010** | |
| EPC / SLT | **35290-32010** | "White Connector" |

**Connector descriptions in the catalogues** — worth noting because they differ:
- **35220-21010 (SL2)** = **"Neutral Connector"**
- **35290-32010 (EPC/SLT)** = **"White Connector"**

"Neutral" likely means unpigmented/natural plastic rather than literal white. Subtle enough that
three connectors could all read "whiteish" to the eye — which means **connector colour is not a
reliable field discriminator** on this transaxle.

**Sources:**
- Cobra Transmission — `cobratransmission.com`
- Sun Transmissions — SL2 listed ~$84.70
- ToyotaPartsDeal — `35220-21010`, listed fitment 2000–2007
- RockAuto — aftermarket equivalents
- Aftermarket 5-piece kit (Amazon, ~$173) lists `35210-21010 / 35220-21010 / 35230-21010`

---

## What to capture before ordering (do this with the pan off)

The catalogue can't settle JDM fitment. **The part in hand can.** Next pan-off:

1. **Photograph the failed solenoid** — side by side with a known US-market part for scale
2. **Measure:**
   - overall body length
   - body diameter at the widest point
   - connector width / height / pin depth
   - pin spacing
3. **Record every stamped number** on the body
   - Example already seen on this job: `000269` and `BJ26 2`
   - These read as **manufacturer lot/date codes, not service part numbers** — but they may help
     a parts counter confirm a revision
4. **Note the retaining method** — bolt vs lock plate, and which plate number if applicable
5. **Read the transaxle serial number** off the housing (see below)

With those numbers, a Toyota parts counter can look up the correct JDM supersession directly.

---

## Transaxle identification

**FSM, verbatim:** *"The engine serial number is stamped on the cylinder block of the engine and
**the transaxle serial number is stamped on the housing** as shown in the illustrations."*

- Also lists transaxle codes: **E351** and **U241E**
- **TSB S-SB-0040-08 Rev1** (Aug 7 2008; Rev1 Oct 13 2009 added 2010MY) — "Automatic Transmission
  Serial Number Location", applicability 2006–2010
- Diagrams: `diagrams/transaxle-serial-number-location.jpg`,
  `diagrams/engine-serial-number-location.jpg`, `diagrams/transaxle-id-location-tsb.jpg`
- ⚠️ The labels in those diagrams were **not** successfully OCR'd — read them directly

---

## Research tried (so it isn't repeated)

| Target | Result |
|---|---|
| TSB **TC005-04** "U240E/U241E Transaxle Solenoid Identification" — *the* answer document | ❌ charm.li timed out ×2 · dot.report 403 (Cloudflare) · direct PDF fetch returned 0 bytes · Scribd gated |
| Local FSM for solenoid part numbers | ❌ **None present.** FSM lists only consumables (filter, pump, gasket). Greps for `35210-`/`35220-`/`35290-`/`85420-` patterns: zero hits |
| Local FSM for solenoid wire colours | ❌ **No wire-colour data** for these solenoids. A brown/yellow observation could not be corroborated |
| `qwen3-vl:8b` / `deepseek-ocr` OCR of the FSM valve body diagrams | ❌ Hung repeatedly; labels never extracted |
| Sonnax U140E/F-U240E/U241E layout guide | ✅ Obtained → `diagrams/sonnax-u140e-u241e-layout.png`. **Valve-train exploded view, not a solenoid position map** — limited use |

**Still worth trying:** the TC005-04 bulletin via a paid manual service, or a Toyota parts counter
lookup by VIN/serial. Both beat further web searching.

---

## Valve body reference — U241E

- **5 solenoids** total (FSM: *"Disconnect the 5 shift solenoid valve connectors"*)
- **Valve body:** 17 bolts @ **11 Nm (8 ft-lbf)**. Positioning bolts marked (1) tighten first.
  Bolt lengths: **25 mm (A)**, **41 mm (B)**, **45 mm (C)**
- **Oil strainer:** 3 bolts @ **11 Nm (8 ft-lbf)** — one O-ring, coated in ATF
- **SLT retainer:** **6.6 Nm (58 in-lbf)** — the lightest fastener on the job
- **Oil pan:** 18 bolts @ **7.8 Nm (69 in-lbf)**
- **Drain plug:** 49 Nm (36 ft-lbf)
- ⚠️ **Do not skip the pan O-ring.** A **double O-ring** on the strainer (found on this job) stacks
  wrong and lets the pump draw air — aerated ATF is compressible, line pressure drops, clutches slip,
  and **P2714 is the clutch-slip monitor**. That is a plausible standalone root cause for a
  slip code with no electrical fault.

---

## Related

- `index.html` — the offline garage guide (see repo root)
- `diagrams/` — valve body components, B20 connector pinout, transaxle ID locations, Sonnax layout
