# 220VAC Trailing-Edge Phase-Cut Dimmer for Flicker-Free LED Lighting

## 1. Project Overview
A custom hardware design of an AC mains **Trailing-Edge (Reverse Phase-Control) Dimmer** operating directly on **220VAC / 50Hz**. This project specifically targets and resolves the notorious **low-end flicker, strobing, and buzzing noise** inherent to legacy Triac (leading-edge) dimmers when paired with non-resistive solid-state lighting.

The board is dimensioned to drive a cluster of **three 220VAC Dimmable LED bulbs (5W to 10W each)**, delivering a clean, smooth, and linear dimming profile from 1% up to 100% across the full phase angle.

<!-- Drag and drop your demo video (.mp4) or animated GIF/hardware photo below -->
<img width="493" height="730" alt="image" src="https://github.com/user-attachments/assets/6a4092e5-6fdf-4a0c-841c-4303b8979f49" />


---

## 2. Technical Specifications

| Parameter | Specification | Notes |
| :--- | :--- | :--- |
| **Operating Input Voltage** | 220V – 240V AC (50Hz) | Standard single-phase AC mains |
| **Compatible Loads** | 220VAC Dimmable LEDs | Also compatible with Filament LEDs and incandescent bulbs |
| **Design Load Capacity** | **3 x LED Bulbs (5W – 10W each)** | Total rated load: 15W – 30W (Tested peak up to 50W) |
| **Dimming Topology** | **Trailing-Edge (Reverse Phase-Cut)** | Soft turn-on at zero-cross, hard cut-off via Power MOSFET |
| **Dimming Range** | **1% – 100%** | Zero strobing/flickering at ultra-low brightness levels (< 10%) |
| **Galvanic Isolation** | Optocoupler-isolated | Complete isolation between 220V high-voltage and logic MCU |
| **Zero-Crossing Detection** | Onboard ZCD circuit | Delivers crisp interrupt pulses for cycle-accurate phase tracking |

---

## 3. Why Trailing-Edge Over Leading-Edge (Triac)?

* **Inrush Current Suppression:** Conventional Triac dimmers chop the leading edge of the AC sine wave, causing sharp voltage rise times ($dV/dt$). This dumps excessive current into the input bridge and smoothing capacitors of LED drivers, causing violent flickering and premature driver failure.
* **Capacitive Load Optimization:** Modern LED power supplies behave as capacitive loads. Trailing-edge dimming turns on smoothly as the voltage crosses 0V and cuts off abruptly at the programmed phase angle, virtually eliminating peak current spikes and thermal stress.
* **Acoustic Noise Elimination:** Eradicates the audible 100Hz transformer/inductor hum often produced by lamp drivers under leading-edge control.

---

## 4. Hardware System Architecture
1. **Zero-Crossing Detector (ZCD):** Accurately samples the AC waveform and generates a clean hardware interrupt signal at every zero transition ($0^\circ$ and $180^\circ$).
2. **Galvanic Optoisolation:** High-speed optocouplers bridge gate drive signals and ZCD status back to the MCU, protecting low-voltage circuitry.
3. **Power Switching Output Stage:** Dual high-voltage Power MOSFETs configured for bidirectional AC blocking, offering ultra-low $R_{DS(on)}$ to ensure cool operation without requiring bulky heat sinks.

---

## 5. Experimental Verification
* Tested with a parallel bank of three 220VAC / 7W dimmable LED filament lamps:
  * Achieved stable deep-dimming down to 1% duty cycle without drop-out or visible modulation shimmer.
  * Linear transitions with zero audible coil whine.
