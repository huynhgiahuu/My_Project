# Single-Phase AC Mains EMI Filter (220VAC / 3A)

## 1. Project Overview
A compact, standalone dual-mode Electromagnetic Interference (EMI) mains filter designed for single-phase AC lines (110V – 250VAC, up to 3A). The board features a two-stage $\Pi$-type network utilizing a dual-winding common-mode choke paired with safety X and Y suppression capacitors. 

Engineered primarily to improve power purity for **high-fidelity audio electronics (DACs, Preamplifiers, Headphone Amps)** and sensitive measurement equipment by mitigating grid switching spikes, RFI, and electromagnetic noise before reaching downstream power supplies.

<!-- Drag and drop your Schematic or 3D PCB layout render below -->
<img width="1002" height="408" alt="image" src="https://github.com/user-attachments/assets/f4a24f22-d42e-4765-9d76-27f1f95418e7" />
<img width="833" height="709" alt="image" src="https://github.com/user-attachments/assets/28f470ab-775e-4dfd-ad2c-19e85d2ad21f" />


---

## 2. Technical Specifications

| Parameter | Specification | Notes |
| :--- | :--- | :--- |
| **Input Voltage Range** | 110V – 250V AC (50/60 Hz) | Single-phase mains |
| **Rated Current** | **3.0 A** continuous | Governed by UU9.8 wire gauge and PCB trace geometry |
| **Filter Topology** | Dual-mode $\Pi$-Network | Common-Mode (CM) & Differential-Mode (DM) suppression |
| **Common Mode Choke (L1)** | UU9.8 Core – **$10\text{ mH}$** | High-permeability ferrite core for low/mid frequency RFI |
| **Differential Capacitors (X-Cap)** | $0.1\,\mu\text{F}$ (100nF) / 275VAC (C2, C3) | Line-to-Neutral high-frequency shunt |
| **Common-Mode Capacitors (Y-Cap)** | $1\text{ nF} / 1\text{ kV}$ (C1, C4) | Line/Neutral-to-Earth low-impedance ground path |
| **AC Input Terminal (P1)** | KF128-3P Screw Terminal | Pin 1: Line (L) \| Pin 2: Earth (PE) \| Pin 3: Neutral (N) |
| **AC Output Terminal (P2)** | KF128-2P Screw Terminal | Filtered Line (L) and Neutral (N) output |

---

## 3. Circuit Analysis & Topology

1. **Common-Mode Noise Suppression:**
   * **UU9.8 Dual Choke ($L_1 = 10\text{ mH}$):** Built with two symmetrically wound coils. While differential load currents cancel their magnetic flux, common-mode in-phase noise encounters high inductive impedance, effectively blocking line-borne interference.
   * **Safety Y-Capacitors ($C_1, C_4 = 1\text{ nF} / 1\text{ kV}$):** Channel high-frequency leakage currents and transient common-mode noise directly to Protective Earth (PE).
2. **Differential-Mode Noise Suppression:**
   * **Safety X-Capacitors ($C_2, C_3 = 0.1\,\mu\text{F}$):** Placed across L and N on both input and load sides of the choke, providing low impedance for high-frequency differential spikes caused by switching events in surrounding appliances (motors, relays, SMPS).

---

## 4. Bill of Materials (BOM)

| Designator | Value / Part Number | Footprint | Qty | Description |
| :---: | :---: | :---: | :---: | :--- |
| **P1** | KF128-3P | Screw Terminal Block (5.0/5.08mm) | 1 | AC Mains Input (L, PE, N) |
| **P2** | KF128-2P | Screw Terminal Block (5.0/5.08mm) | 1 | Filtered AC Output (L, N) |
| **L1** | UU9.8 10mH | Through-Hole | 1 | Common Mode Choke |
| **C2, C3** | $0.1\,\mu\text{F}$ (104) / 275VAC | X2 Film Safety Capacitor | 2 | Differential Line-to-Line Filter |
| **C1, C4** | $1\text{ nF}$ (102) / 1kV | High-Voltage Ceramic / Y-Cap | 2 | Common-Mode Line-to-Earth Filter |

---

## 5. Applications
* Front-end AC filtering for **linear transformer power supplies, DACs, and discrete audio amplifiers**.
* Noise isolation for precision measurement setups and sensitive embedded controllers.
* Line cleaner for small SMPS units to prevent EMI back-propagation into mains wiring.
