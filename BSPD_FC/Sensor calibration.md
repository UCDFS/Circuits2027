# BSPD sensor voltages and calibration checks

Values below are nominal. Record the installed sensors, measured voltages and calibration settings before accepting them for the car. Measure board voltages relative to GLV−.

## Current sensor

The project notes assume the Orion output wired to J2 pin 3 rises with battery discharge current, with 2.50 V at zero current and a slope of 10 mV/A. Orion supplies dual-range sensors. The installed part number and output channel still need identifying.

| Battery DC current | Expected voltage at TP1 under that assumption |
|---|---|
| −200 A (charging) | 0.50 V |
| 0 A | 2.50 V |
| +15.9 A | 2.66 V |
| +200 A (discharging) | 4.50 V |

The current potentiometer sets the operating threshold at **TP4**. For the documented 315 V maximum pack voltage, 5,000 W / 315 V = 15.9 A. With the assumed slope, set TP4 to the measured zero-current voltage at TP1 **plus 0.159 V**. Recalculate for the actual maximum pack voltage and measured channel slope.

The separate sensor-fault thresholds are **0.243 V and 4.737 V** at a nominal 5 V supply. The older 0.455 V lower limit is obsolete. On the assumed current scale these limits correspond to approximately −226 A and +224 A. They are calculated threshold crossings, not guaranteed sensor operating limits. A healthy sensor that crosses either threshold long enough can request shutdown independently of brake pressure.

## Brake pressure sensors

TP2 and TP3 measure the front and rear sensor signals. TP5 and TP6 measure their respective hard-braking thresholds. The two sets of figures below have different precision and assumptions. Neither is a measured calibration for the installed sensors.

| Pressure | Voltage in the pasted schematic note | Nominal voltage from the documented 0.5–4.5 V, 0–500 psi sensor span |
|---|---|---|
| 0 bar | — | 0.50 V |
| 20 bar | 2.80 V | 2.82 V |
| 25 bar | 3.36 V | 3.40 V |
| 30 bar | 3.93 V | 3.98 V |

## Checks to record

- [ ] Record the Orion part number, wired output pin and channel range. Trace it to J2 pin 3. Measure TP1 at zero and at a known discharge current to confirm offset, slope and direction.
- [ ] Confirm maximum pack voltage and record the calculated current threshold and measured TP4 setting. Compare peak battery DC discharge and regenerative current with the valid range of the wired channel. Check both signal extremes against the measured fault references, allowing for supply and sensor tolerances.
- [ ] Identify both brake sensor part numbers. Using a known pressure, record front and rear voltages at rest and at the chosen hard-braking pressure. Set TP5 and TP6 independently. Check peak normal braking pressure stays within the sensors’ rated range and their signals stay inside the fault window.
- [ ] On a low-voltage bench, check that each sensor input independently trips when disconnected, grounded or tied to its 5 V supply. Check the actual contact opening time at J3 and that the trip remains latched after the signal recovers.

## Two corrections to the older schematic notes

- An individual current or brake threshold LED can light during valid operation without a BSPD trip. LED5 indicates the latched trip. “All LEDs off” is not a general test for a healthy BSPD.
- High current together with hard braking at either axle has a nominal **357 ms** delay to the trip request. An out-of-range sensor has its own nominal **159 ms** delay. Startup reset also holds the relay open, and clearing a fault after it latches does not reclose the relay. The old “closed unless braking and high power for >500 ms” note leaves out these states.

Sources include the supplied schematic annotations, the [FC schematic](BSPD_FC.kicad_sch), the [project revision notes](https://github.com/UCDFS/Circuits/blob/bspd-latch-fix/BSPD_KR/README.md), the [Orion purchasing guide](https://www.orionbms.com/manuals/pdf/orionbms2_purchasing_guide.pdf) and the [Orion operation manual](https://www.orionbms.com/manuals/pdf/orionbms2_operational_manual.pdf).
