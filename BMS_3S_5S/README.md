# 3S–5S Configurable Battery Management System (BMS) Based on TI BQ77914 / BQ77915

## 1. Project Overview
A standalone, highly reliable Battery Management System (BMS) hardware design supporting **3S to 5S** battery pack configurations. The design is built around the **Texas Instruments BQ77914 / BQ77915** family, offering autonomous cell protection and balancing without requiring an external microcontroller (MCU).

This board is engineered specifically for **Mini-UPS backup power supplies dedicated to audio equipment** (DACs, Preamps, Network Streamers), focusing on clean DC power rails, low impedance, and zero audible switching artifacts.

<!-- Drag and drop your main 3D rendering or assembled board image below -->
<img width="574" height="722" alt="image" src="https://github.com/user-attachments/assets/2d3963ba-0efa-4fec-9c3a-335ca3ec601c" />
<img width="792" height="847" alt="image" src="https://github.com/user-attachments/assets/559c2166-91a4-40df-b6f3-717390142a1a" />


---

## 2. Technical Specifications

| Parameter | Specification | Notes |
| :--- | :--- | :--- |
| **Primary Controller** | TI BQ77914 / BQ7791500PWR | Ultra-low quiescent current standalone protector |
| **Cell Configuration** | **3S, 4S, or 5S** | Configurable via strapping resistor network on CCFG (J6) |
| **Operating Voltage Range** | 3.0V – 22.0V DC | Suitable for Li-ion, Li-Po, and LiFePO4 chemistries |
| **Continuous Current Rating** | **4.0 A** | Footprints reserved for parallel FETs (Q3, Q4) for expansion |
| **Current Sense Resistor** | $15\text{ m}\Omega$ / 1% (R33) | Filtered via differential RC network (SRP / SRN) |
| **Switching Topology** | Low-side Common-Drain N-Channel | Q1 (Discharge) & Q2 (Charge) independently driven |
| **Cell Balancing** | Integrated Autonomous Balancing | 5 onboard LED indicators (D5–D9) for cell status |
| **Thermal Monitoring** | External $10\text{ k}\Omega$ NTC Thermistor (RT1) | Monitored via TS and VTB pins |
| **Cascading Capability** | Stackable for >5S packs | Expansion headers J4 & J5 (CBI, CBO, LPWR, PRES) |

---

## 3. Hardware Protection Features
* **Cell-Level Over-Voltage (OVP) & Under-Voltage (UVP):** Individual cell monitoring on lines VC0–VC5 equipped with low-pass RC filtering ($43\,\Omega$ + $1\,\mu\text{F}$).
* **Over-Current Discharge (OCD) & Short-Circuit (SCD):** Fast hardware cut-off via low-side discharge MOSFET during overload or dead-short events.
* **Over-Current Charge (OCC):** Prevents degradation from excessive charging currents.
* **Over-Temperature Protection (OTP):** Dedicated NTC probe placed directly on battery cells.
* **Autonomous Cell Balancing:** Mitigates cell voltage imbalance during charge cycles, extending pack longevity.

---

## 4. Hardware Prototype

| Assembled Board (PCBA) |
| :---: |
| <!-- Drop assembled board photo here -->
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/9e0f4788-a8a5-4a20-b011-92cf853a77a8" />
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/946b13d5-0e02-4802-953f-df67c758ef80" />
<img width="984" height="2144" alt="image" src="https://github.com/user-attachments/assets/ad841811-c1ec-4453-bfce-60e2f3f90847" />
|

---

## 5. Applications
* Low-noise **Mini-UPS units** for high-fidelity audio equipment (DACs, Phono stages, Streamers).
* Uninterruptible power source for critical network switches and small routers.
* Standalone battery packs requiring zero software overhead and high fault tolerance.
