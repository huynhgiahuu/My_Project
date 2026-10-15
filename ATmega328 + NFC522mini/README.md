# Standalone 13.56MHz RFID/NFC Access Control System Using ATmega328P & RC522-Mini

## 1. Project Overview
A compact, highly reliable contactless RFID/NFC reader/writer embedded system based on the **Microchip ATmega328P** 8-bit AVR microcontroller and the ultra-small **MFRC522-Mini** transceiver module. Operating at the **13.56 MHz** ISM frequency band, this design provides a modular solution for physical access control, smart locker mechanisms, and user authentication.

The system communicates over high-speed SPI, featuring rapid UID acquisition, sector-level authentication via Crypto1 coprocessor, and non-volatile UID whitelist storage.

<!-- Drag and drop your Schematic, 3D PCB render, or demonstration clip below -->
<img width="700" height="594" alt="image" src="https://github.com/user-attachments/assets/d0651dcf-db73-432f-adc7-a21f7f5e95d9" />


---

## 2. Technical Specifications

| Parameter | Specification | Notes |
| :--- | :--- | :--- |
| **Microcontroller (MCU)** | Microchip ATmega328P (8-bit AVR) | 32KB Flash, 2KB SRAM, 1KB EEPROM |
| **System Clock Frequency** | 16 MHz (External XTAL) / 8 MHz Internal | Compatible with 5V or 3.3V core voltages |
| **Transceiver Module** | MFRC522-Mini | Compact footprint, based on NXP MFRC522 |
| **Carrier Frequency** | **13.56 MHz** (High Frequency RFID / NFC) | Onboard tuned PCB loop antenna |
| **Supported Protocols** | ISO/IEC 14443 Type A | MIFARE Classic 1K/4K, Ultralight, NTAG21x |
| **Host Interface** | **4-wire SPI Bus** (Up to 10 Mbps) | SCK, MOSI, MISO, SS/SDA, and HW Reset |
| **Module Operating Voltage** | **3.3V DC** | Requires logic-level adaptation when MCU runs at 5V |
| **Effective Reading Range** | $20\text{ mm} - 45\text{ mm}$ | Depends on tag antenna geometry |
| **Standby Power Consumption** | $< 15\text{ mA}$ | Supports hardware/software power-down states |

---

## 3. Hardware Pin Mapping

SPI bus interconnection between ATmega328P and the RC522-Mini module:

| RC522-Mini Pin | ATmega328P Pin (Arduino Pin) | Signal Function | Remarks |
| :---: | :---: | :--- | :--- |
| **3.3V** | 3.3V Rail | RF Transceiver Power Supply | *Do not connect directly to 5V* |
| **GND** | GND | Ground Reference | Common ground plane |
| **RST** | D9 (PB1) | Hardware Reset / Power Down | Active-low hard reset |
| **SDA (SS)** | D10 (PB2) | SPI Slave Select | Active-low chip select |
| **MOSI** | D11 (PB3) | SPI Master Out Slave In | Data transmitted from MCU to RC522 |
| **MISO** | D12 (PB4) | SPI Master In Slave Out | 3.3V CMOS output back to MCU |
| **SCK** | D13 (PB5) | SPI Serial Clock | Master clock synchronization |

*Hardware Note:* Since the MFRC522 I/O lines are 3.3V-rated, passive resistor dividers ($1\text{ k}\Omega / 2\text{ k}\Omega$) or dedicated bidirectional logic level shifter ICs are implemented on MOSI, SCK, SDA, and RST when operating the ATmega328P at 5V to prevent RF frontend degradation.

---

## 4. Firmware Architecture & Features
* **Rapid Card Detection:** Polling cycle detects tag arrival (PICC_IsNewCardPresent) and reads serial UID in under $50\text{ ms}$.
* **On-Chip Whitelist Storage:** Authorized card UIDs are committed directly to the internal **1KB EEPROM**, preserving access permissions through power-cycling events.
* **Sector Authentication:** Leverages standard Key A/Key B authentication sequences prior to accessing secure MIFARE memory blocks.
* **User Feedback:** Output drivers for dual-color status LEDs (Green = Granted, Red = Denied) and audible feedback buzzer.

---

## 5. Applications
* Secure electronic door locks and entry gate controllers.
* Standalone time-and-attendance logging terminals.
* Equipment activation interlocks via authorized technician badges.
