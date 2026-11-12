# BSPD changelog - changes from 2026

- **Sensor comparators:** Expanded from two LM339 quad comparators to three, with one chip each for current, front brake pressure and rear brake pressure.
- **Sensor fault detection:** Separated sensor faults from the braking and current logic, lowered the undervoltage threshold from 0.455 V to 0.243 V and added a 4.74 V overvoltage threshold.
- **Sensor fault timing:** Added a 100 kΩ resistor and 1 µF capacitor so any sensor outside its valid voltage range can independently request shutdown after about 159 ms.
- **Braking and current timing:** Reduced the timing resistor from 56 kΩ to 39 kΩ, shortening the nominal delay for high current and hard braking at either axle from 513 ms to 357 ms.
- **Fault latch:** Replaced the transistor-based timed recovery circuit with two cross-coupled NOR gates that hold a fault latched until the low-voltage master is power-cycled.
- **Startup reset:** Added a resistor-capacitor reset timer, clamp diode and Schmitt trigger to give the latch a clean reset at power-up.
- **Relay drive:** Replaced the comparator and pull-up resistor with a NOR gate that keeps the 2N7002 MOSFET off during reset or a latched fault.
- **Indicators and connectors:** Added a dedicated sensor-fault LED, bringing the total to six, and reassigned the power, sensor and shutdown connector numbers.

[Sensor calibration and checks](Sensor%20calibration.md)
