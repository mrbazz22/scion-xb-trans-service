# 2010 Scion xB — Transmission Service & SLT Solenoid Guide

Static HTML guide for servicing the **U241E** automatic transaxle in a 2010 Scion xB (2AZ-FE):
ATF drain & refill, ATF filter replacement, and SLT (shift solenoid valve SLT) replacement.

Built as an offline-first iOS home-screen app — add to Home Screen from Safari for full-screen,
offline use in the garage.

## Contents

| Tab | What's in it |
|---|---|
| Overview | Scope, order of operations, fault context |
| Parts | OEM numbers, donor/aftermarket equivalents, tools |
| Checks | SLT circuit pre-check + all U241E solenoid resistance specs |
| Bulb Test | The FSM 21 W bulb bench test, with wiring diagram |
| Teardown | Drain, pan off, filter |
| Install | Solenoid swap + full torque table |
| Refill | Fluid capacity and the HOT level-check procedure |
| Diagnose | P2714 vs P2716, FSM diagnostic path, expectations |
| Checklist | 32-item checklist with saved state |

## Field notes

Field notes from the actual job are kept in `notes/`:

| File | What's in it |
|---|---|
| [`notes/jdm-solenoid-replacement.md`](notes/jdm-solenoid-replacement.md) | **JDM vs US-market solenoid differences**, measured resistance values, OE part numbers (SL1/SL2/SLT/EPC), what to measure before ordering, transaxle ID location, and the research dead-ends so they aren't repeated |

**Headline finding:** the installed JDM U241E and the US-market U241E **do not share a solenoid set** —
a US-market donor solenoid will not fit the JDM valve body. Verify fitment by measuring the part in
hand before ordering.

Also documented there: a **double O-ring on the oil strainer** (stacked by a previous repair) is a
plausible standalone root cause for **P2714** — stacked O-rings leak air on the suction side, aerated
ATF is compressible, line pressure drops, clutches slip, and P2714 is the clutch-slip monitor.

## Key specs

**Torque**

| Fastener | Nm | ft-lbf / in-lbf |
|---|---|---|
| SLT to valve body | 6.6 | 58 in-lbf |
| SL1 / SL2 to valve body | 11 | 8 ft-lbf |
| DSL / S4 to valve body | 11 | 8 ft-lbf |
| Valve body to transaxle | 11 | 8 ft-lbf |
| Oil strainer to valve body | 11 | 8 ft-lbf |
| Oil pan to transaxle case | 7.8 | 69 in-lbf |
| Transmission wire to case | 5.4 | 48 in-lbf |
| ATF temp sensor to lock plate | 6.6 | 58 in-lbf |
| Drain plug | 49 | 36 ft-lbf |

**Solenoid resistance @ 20 °C (68 °F)**

| Solenoid | Test points | Spec |
|---|---|---|
| SL1 | terminal 1 – 2 | 5.0 – 5.6 Ω |
| SL2 | terminal 1 – 2 | 5.0 – 5.6 Ω |
| SLT | terminal 1 – 2 | 5.0 – 5.6 Ω |
| DSL | connector – body | 11 – 13 Ω |
| S4 | connector – body | 11 – 15 Ω |

**Fluids**

- ATF: **Toyota Genuine ATF WS only** — no substitutes. Drain & refill 3.7 qt (3.5 L); dry fill 8.6 qt.
- Engine oil: 5W-20 or 0W-20 ILSAC, 4.5 qt with filter.

## The 21 W bulb test

The FSM specifies a 21 W bulb in series with the solenoid for the actuation test. The bulb is a
**current limiter** — SLT is a linear PWM solenoid (~5.3 Ω), and straight across a 12.6 V battery
that's roughly 2.4 A / 30 W into a coil the ECM only ever drives at duty cycle.

A standard **1156** (or the bright filament of a **1157**) is ~27 W, which works out to ~6 Ω hot —
functionally the same as the resistor a bench supply would use. Don't jumper the solenoid directly
to a battery.

The bulb also doubles as an indicator: if it glows but the valve doesn't move, the circuit is good
and the fault is mechanical.

## Running it

Open `index.html`. No build step, no dependencies. For the home-screen app experience, serve it over
HTTP (GitHub Pages or any static host) and use Safari → Share → Add to Home Screen.

## Notes

- Specs sourced from the 2010 Scion xB L4-2.4L (2AZ-FE) service manual, U241E automatic transaxle sections.
- Part numbers are OEM Toyota unless noted; aftermarket equivalents are examples, verify fitment by VIN.
- Not affiliated with Toyota. Use at your own risk.
