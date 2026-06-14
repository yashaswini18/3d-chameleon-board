# 3d-chameleon-board
Electronics bring-up, UPDI firmware flashing, and I2C bring-up for the 3D Chameleon Board using ATtiny3226
# 3D Chameleon Board — Electronics Bring-Up & Firmware Flashing Guide

> **Project Role:** I contributed to the **electronics side** of this project — board bring-up, firmware flashing, and validating all hardware commands using the original firmware.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Hardware Required](#hardware-required)
- [ATtiny3226 Pinout](#attiny3226-pinout)
- [Step 1 — Set Up Arduino Nano as UPDI Programmer](#step-1--set-up-arduino-nano-as-updi-programmer)
- [Step 2 — Flash Firmware to ATtiny3226](#step-2--flash-firmware-to-attiny3226)
- [Step 3 — I2C Scanning & Serial Monitor Setup](#step-3--i2c-scanning--serial-monitor-setup)
- [Known Issues & Notes](#known-issues--notes)
- [References](#references)

---

## Project Overview

The **3D Chameleon Board** is a hardware project where an **ATtiny3226 microcontroller** is the core chip. This repository documents the electronics bring-up process, including:

- Programming the ATtiny3226 using an Arduino Nano as a UPDI programmer
- Flashing and validating firmware
- I2C device scanning and serial output configuration

---

## Hardware Required

| Component | Purpose |
|---|---|
| Arduino Nano | Acts as UPDI programmer for ATtiny3226 |
| ATtiny3226 chip | Main microcontroller on the 3D Chameleon Board |
| 10µF Capacitor | Connected between Reset pin and GND of Arduino Nano |
| Resistor (470Ω recommended) | Between Arduino Nano D6 and ATtiny3226 Pin 16 |
| LED + Resistor | For blink test to verify flashing |

---

## ATtiny3226 Pinout

```
ATtiny3226 Key Pins:
  Pin 9  → TX (alternate UART output)
  Pin 10 → SDA (I2C)
  Pin 11 → SCL (I2C)
  Pin 16 → UPDI (programming pin)
  Pin 17 → TX (default UART output)
```

> Full official pinout available in the [ATtiny3226 datasheet](https://www.microchip.com/en-us/product/attiny3226).

---

## Step 1 — Set Up Arduino Nano as UPDI Programmer

The ATtiny3226 uses the **UPDI protocol** for programming. An Arduino Nano can be converted into a UPDI programmer using the `jtag2updi` firmware.

### Instructions

1. Download the `jtag2updi` zip file from:
   👉 [https://github.com/ElTangas/jtag2updi](https://github.com/ElTangas/jtag2updi)

2. Extract the zip file.

3. Inside the `source` folder, you will find a `.ino` file. Click on it — it will open in a **separate folder** in the Arduino IDE.

4. Move **all** `.h` and `.c` files from the `source` folder into that same folder where the `.ino` file opened.
   > Even though the `jtag2updi` sketch may appear empty, this is expected.

5. Upload the sketch to your **Arduino Nano** board via Arduino IDE.

Your Arduino Nano is now a UPDI programmer. ✅

---

## Step 2 — Flash Firmware to ATtiny3226

### Wiring

After uploading `jtag2updi` to the Arduino Nano, make the following connections:

| Arduino Nano | ATtiny3226 / Component |
|---|---|
| Reset pin | 10µF capacitor → GND (of Nano) |
| D6 | → Resistor → ATtiny3226 **Pin 16** (UPDI) |

### Verify with Blink Test

To confirm the flashing pipeline is working:

1. Write or open a simple `blink.ino` sketch.
2. Flash it to the ATtiny3226 via the UPDI connection.
3. Connect an LED (with a current-limiting resistor) to the target GPIO pin.
4. Confirm the LED blinks. ✅

> **In Arduino IDE**, select the target as **ATtiny3226** and programmer as **jtag2updi**.

---

## Step 3 — I2C Scanning & Serial Monitor Setup

The ATtiny3226 has I2C on the following pins:

| Function | ATtiny3226 Pin |
|---|---|
| SDA | Pin 10 |
| SCL | Pin 11 |

### Reading I2C Scan Results via Serial Monitor

Since the ATtiny3226 doesn't have a native USB-serial interface, you need to route its TX pin through the Arduino Nano to read output in the Serial Monitor.

**Option A — Default TX Pin:**
```
ATtiny3226 Pin 17 (TX)  →  Arduino Nano D1
```

**Option B — Alternate TX Pin:**
```
ATtiny3226 Pin 9 (TX)   →  Arduino Nano D1
```

Once wired, open the **Arduino IDE Serial Monitor** to read the I2C scanned addresses printed by the ATtiny3226.

---

## Known Issues & Notes

- The `jtag2updi` `.ino` sketch body may appear **empty** — this is normal. Do not add code to it; just ensure all `.h` and `.c` files are in the same folder before uploading.
- The **10µF capacitor** on the Nano's Reset pin is critical — it prevents the Nano from auto-resetting during UPDI programming.
- Make sure you select the correct **programmer (jtag2updi)** and **board (ATtiny3226)** in Arduino IDE before flashing.

---

## References

- [jtag2updi — GitHub](https://github.com/ElTangas/jtag2updi)
- [ATtiny3226 Product Page — Microchip](https://www.microchip.com/en-us/product/attiny3226)
- [Arduino IDE Download](https://www.arduino.cc/en/software)

---

*Electronics bring-up and firmware validation contributed as part of the 3D Chameleon Board project.*
