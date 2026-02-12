# Two-Stage BJT 2N2222 Common-Emitter Amplifier (Audio Band)

This repository documents the design, simulation, and laboratory testing of a **two-stage common-emitter (CE) amplifier**
using **2N2222 NPN BJTs**, targeting the **audio frequency band (20 Hz–20 kHz)**. The project covers theoretical design,
NI Multisim simulation, PCB layout, and hardware verification using NI ELVIS instrumentation.

> Full report: see `https://github.com/izzudin01/Design-of-Two-Stage-BJT-Common-Emitter-Amplifier-2N2222-/blob/main/Final%20Project%20Report_Desain%20Two%20Stage%20BJT%202N2222%20Common%20Emitter%20Amplifier.pdf`.

---

## Overview
A two-stage CE amplifier can achieve higher total voltage gain than a single stage while maintaining stable biasing
and acceptable frequency response. This project implements a two-stage 2N2222 CE amplifier with voltage-divider bias,
emitter degeneration, and bypass capacitors to improve bias stability and linearity.

---
![](https://github.com/izzudin01/Design-of-Two-Stage-BJT-Common-Emitter-Amplifier-2N2222-/blob/main/Picture/Screenshot%202026-02-12%20224200.png)

## Background
Common-emitter BJT amplifiers are widely used in analog electronics due to their high voltage gain and practical biasing.
For many applications, a single stage may not provide sufficient amplification, so multi-stage amplification is used.
However, multi-stage designs require careful biasing, coupling, and frequency response control to avoid instability,
distortion, and undesired cutoffs.

---

## Design Targets
- Supply voltage: **5 V**
- Source resistance: **50 Ω**
- Load resistance: **1 kΩ**
- Target overall gain: **Av ≈ 20**
- Target stage gains: **|A1| ≈ 5** and **|A2| ≈ 4**
- Bandwidth target: **20 Hz – 20 kHz**

---

## Methodology (High-Level)
1) **Theoretical Design**
- Applied a systematic design approach (bias point selection near mid-load-line, small-signal model reasoning).
- Selected component values for both stages, including coupling capacitors and emitter bypass capacitors.

2) **Simulation (NI Multisim 14.1)**
- Verified DC operating point and frequency response (AC sweep).
- Evaluated gain stability across frequency and identified cutoff behaviors.

3) **PCB Layout**
- Produced 2D and 3D PCB layout design for documentation and manufacturability review.

4) **Hardware Testing**
- Built a breadboard prototype and tested using **NI ELVIS** (5 V supply, function generator, and oscilloscope).
- Due to instrument limitations, lab measurements were performed at **20 Hz, 100 Hz, and 1 kHz**.

---

![](https://github.com/izzudin01/Design-of-Two-Stage-BJT-Common-Emitter-Amplifier-2N2222-/blob/main/Picture/Screenshot%202026-02-12%20224253.png)
![](https://github.com/izzudin01/Design-of-Two-Stage-BJT-Common-Emitter-Amplifier-2N2222-/blob/main/Picture/Screenshot%202026-02-12%20224304.png)

## Results

### A) Simulation – Frequency Response & Gain Stability
- Midband performance (roughly **100 Hz to 8 kHz**) achieved stable overall gain around **Av ≈ 20.0–20.4**.
- Low-frequency cutoff was observed around **~50 Hz**, which is higher than the 20 Hz target.
- High-frequency behavior aligned with the intended roll-off; around **20 kHz**, the gain dropped to approximately **Av ≈ 14.6** (≈ -3 dB from peak), consistent with the design objective to limit high-frequency response.

![](https://github.com/izzudin01/Design-of-Two-Stage-BJT-Common-Emitter-Amplifier-2N2222-/blob/main/Picture/Screenshot%202026-02-12%20224322.png)
![](https://github.com/izzudin01/Design-of-Two-Stage-BJT-Common-Emitter-Amplifier-2N2222-/blob/main/Picture/Screenshot%202026-02-12%20224349.png)

### B) Simulation – DC Operating Point (vs Theory)
DC bias results showed small deviations between theory and simulation (notably in the second stage currents/voltages),
which is expected due to non-ideal transistor modeling and practical bias sensitivity.

### C) Lab Testing – NI ELVIS Measurements
Measured results show:
- **~20 Hz (≈19.9 Hz):** Av ≈ **4.56** (low-frequency gain lower than desired)
- **100 Hz:** Av ≈ **20.2** (excellent midband amplification)
- **1 kHz:** Av ≈ **20.4** (stable midband amplification)

Data is summarized in `data/lab_measurements.csv`.

### Discussion (Key Reasons for Deviations)
Differences between theory/simulation and real measurement are attributed to:
- Commercial component availability (value rounding) and tolerance
- Parasitic capacitance/inductance in breadboard wiring
- Variation in transistor parameters (β/hFE) across devices

---

## Conclusion
- The amplifier meets the **target midband gain (~20)** and behaves well in the primary audio midband range.
- The low-frequency performance did not fully meet the 20 Hz target due to cutoff shifting (observed ~50 Hz behavior).
- High-frequency cutoff behavior aligns with design intent around the 20 kHz region.
- Future improvements include tighter component selection/tolerance control, improved layout/prototyping approach,
and refined coupling/bypass capacitor sizing to push the low cutoff closer to 20 Hz.

---

