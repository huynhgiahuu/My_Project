# 3-Phase Sensored BLDC Motor Driver Board Based on JY01 & IR2101

## 1. Project Overview
A robust, standalone 3-phase Brushless DC (BLDC) motor driver hardware design based on the dedicated **JY01 (JY01_HLLE)** motor controller IC. The board incorporates three **IR2101** high-and-low side gate driver ICs driving a 6-MOSFET N-channel inverter bridge, optimized for sensored BLDC motors equipped with $120^\circ / 60^\circ$ Hall-effect sensors.

This hardware-centric design delivers smooth closed-loop/open-loop commutation without requiring software development or complex microcontrollers. It features built-in soft-start, cycle-by-cycle over-current protection (OCP), linear analog/PWM speed regulation, and active directional control.

<!-- Drag and drop your 3D PCB layout render or assembled board photo below -->


---

## 2. Technical Specifications

| Parameter | Specification | Notes |
| :--- | :--- | :--- |
| **Primary Controller** | **JY01 / JY01_HLLE** | Dedicated hardware BLDC controller IC |
| **Gate Driver ICs** | **3 x IR2101** | Independent high & low-side bootstrap drivers |
| **Operating Bus Voltage (VCC)** | **12V – 36V DC** (48V max) | Filtered by $3 \times 100\,\mu\text{F} / 63\text{V}$ low-ESR capacitors |
| **Rated Continuous Current** | **10A – 15A** (20A peak) | Dependent on PCB copper weight and thermal sinking |
| **Power Stage Inverter** | 6 x N-Channel Power MOSFETs (6990) | Ultra-low $R_{DS(on)}$ for high conversion efficiency |
| **Position Feedback** | 3-Phase Hall Sensors (Ha, Hb, Hc) | Low-pass filtered inputs ($2.2\text{ k}\Omega + 10\text{ nF}$) |
| **Current Sense Resistor** | **$22\text{ m}\Omega$** (R022 / R20) | Low-side return path current monitoring |
| **Speed Control Interface (VR)** | **0 – 5V Analog** or PWM | Onboard pull-down and input clamp diode protection |
| **Auxiliary Power Supply** | LM317 (15V rail) & 78L05 (5V rail) | Derives driver and logic rails directly from bus voltage |

---

## 3. Circuit Architecture & Hardware Blocks

1. **Dedicated BLDC Core (JY01):**
   * Decodes incoming Hall transitions to deliver standard 6-step trapezoidal switching signals.
   * Internal ramp generator provides controlled soft-start acceleration, suppressing high current surges at stall.
   * Outputs a calibrated speed feedback pulse train via the **M pin (FG signal)** for closed-loop RPM tracking.
2. **Gate Drive & Bootstrap Stage (IR2101):**
   * Three dual-channel IR2101 driver ICs interface directly with the JY01 logic outputs (AT/AB, BT/BB, CT/CB).
   * Dedicated bootstrap diodes (1N4148) and bootstrap capacitors ($1\,\mu\text{F}$) supply sufficient gate charge for high-side N-channel MOSFET switching.
3. **Current Sensing & Protection:**
   * **Over-Current Protection (OCP):** Sensed across a $22\text{ m}\Omega$ precision shunt resistor in the return path. The signal is filtered through an RC low-pass filter ($10\text{ k}\Omega + 470\text{ nF}$) into pin `Is`, shutting down PWM instantly under stall or dead-short conditions.
4. **Master Control Interface Header (J2 / CON4):**
   * `5V`: Regulated 5V output for external potentiometers or MCU controllers.
   * `EL`: Enable / Emergency Electronic Brake control.
   * `M`: Speed pulse output (FG).
   * `Z/F`: Direction control (CW / CCW logic level).
   * `VRI`: Speed command input (0–5V analog or filtered PWM).
   * `GND`: Common power/signal return.

---

## 4. Schematic & PCB Implementation

<!-- Drag and drop your Schematic image below -->
<img width="1091" height="763" alt="image" src="https://github.com/user-attachments/assets/d4aad5ef-dab1-4ea2-b749-e88c1e2b54cb" />


| 3D PCB Layout | Assembled Board / Hardware Testing |
| :---: | :---: |
| <!-- Drop 3D layout render here --> | <!-- Drop actual PCBA photo or test clip here --> <img width="864" height="313" alt="image" src="https://github.com/user-attachments/assets/0c7ca722-09ac-46ff-bf16-446ddac9d9ca" />
<img width="861" height="316" alt="image" src="https://github.com/user-attachments/assets/8b48868a-2ef7-47f7-a495-e0c6a9b97353" />
|

---

## 5. Applications
* Small electric mobility drives (e-scooters, electric skateboards, AGVs).
* High-power brushless cooling fans, pumps, and blowers.
* Cordless power tools and light CNC spindle drivers.
