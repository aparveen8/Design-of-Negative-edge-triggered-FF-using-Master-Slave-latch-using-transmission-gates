# Negative Edge-Triggered Master-Slave Flip-Flop Design

This repository contains the design, layout, and performance analysis of a **Negative Edge-Triggered D Flip-Flop** using a Master-Slave configuration with transmission gates.

## Schematic and Sizing
Transistors were sized to have delays under 200ps.
### Transistor Sizing Specifications

| Transistor Type | Width ($W$) | Transistor Names |
| :--- | :--- | :--- |
| **PMOS** | 0.6 µm | M4 |
| | 0.54 µm | XM16, XM3, XM2, XM1 |
| | 0.27 µm | XM0 |
| | 0.135 µm | XM7, XM6, XM5 |
| **NMOS** | 0.3 µm | M8 |
| | 0.27 µm | XM14, XM9, XM11, XM17 |
| | 0.135 µm | XM15, XM13, XM12, XM10 |

> **Note:** All lengths ($L$) are assumed to be at the technology node minimum (e.g., 0.06 µm) unless otherwise specified.
<p align="center">
  <img src="img/sch.png" />
</p>


## Layout & Physical Design
The layout was optimized through 5 iterations in order to reduce area consumed. It was designed as per standard cell design rules
* **Final Area:** $14.39\mu m^2$ ($5.535\mu m \times 2.6\mu m$)
* **Verification:** The layout passed **DRC** and **LVS** with a "CORRECT" status

### Verification Plan & Stimuli

To verify the design's performance and functionality, the following verification plan was implemented using specific pre-conditions and stimuli:

| Parameters | Pre-Conditions | Stimuli |
| :--- | :--- | :--- |
| **Clock to Q delay** | Data is stable ($D=1$), clock is high  | Apply Clock $= 0$  |
| **Setup Time** | Clock is high, about to transition low  | Change Data input before the clock edge; measured when Clk-to-Q delay varies by ~5%  |
| **Hold Time** | Clock has just transitioned from high to low  | Change Data input after the clock edge; measured when Clk-to-Q delay varies by ~5%  |

## 📊 Performance Analysis
Performance was evaluated under various PVT (Process, Voltage, Temperature) corners

| Parameter | worst Corner Case | Pre-Layout | Post-Layout |
| :--- | :--- | :--- | :--- |
| **Clock-to-Q Delay** | SS, 1.08V, 125°C | 178ps | 199ps |
| **Setup Time** | SS, 1.08V, 125°C | 34ps | 59ps |
| **Hold Time** | FF, 1.32V, -40°C | 14ps | 29ps |
| **Dynamic Power** | FF, 1.32V, -40°C | 3.192uW | 3.573uW |
| **Leakage Power** | FF, 1.32V, 125°C | 0.016uW | 0.037uW |

### Monte Carlo Simulations Analysis ( Pre vs Post-Layout)
To account for process variations, 1000-point Monte Carlo simulations were conducted
| Parameters | Mean (Pre) | Mean (Post) | Std. Deviation (Pre) | Std. Deviation (Post) |
| :--- | :--- | :--- | :--- | :--- |
| **Clock to Q delay** | 175ps | 189ps | 3.85ps | 6.96ps |
| **Setup Time** | 31ps | 49ps | 3.23ps | 9.56ps |
| **Hold Time** | 13ps | 25ps | 1.21ps | 4.45ps |



## 📂 Repository Structure
* `/schematic`: Circuit diagrams and transistor specifications.
* `/layout`: Layout GDSII files and iteration history.
* `/simulation`: Post-layout SPICE simulation results and waveforms.
* `/reports`: DRC/LVS check summaries.

---
Course Project of DVD(Digital VLSI Design) Course
* **Instructor:** Prof. Anuj Grover, Indraprastha Institute of Information Technology Delhi (IIIT-D)
