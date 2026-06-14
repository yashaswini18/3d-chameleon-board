# Original Testing Notes

> Raw notes from the board bring-up process. These were the reference during hardware testing and are preserved here for documentation accuracy.

---

## 3D CHAMELEON BOARD — MODIFICATIONS OR TESTING ISSUES

### Programming the ATtiny3226

To upload to the ATtiny3226 chip or program it, we can use an Arduino Nano board as a programmer.

**Step 1:** Download the zip file from GitHub — https://github.com/ElTangas/jtag2updi — then extract it. Inside the `source` folder you can see a `.ino` file. Click on it; it will open in a separate folder. Move all the `.h` and `.c` files — everything — into that folder, and even though the `jtag2updi` is empty, upload that to the Arduino Nano board.

**Step 2:** Now connect the 10 microfarad capacitor from the Reset pin to the GND of the Nano board. Then connect a resistor from Pin D6 of the Nano, and the other end of the resistor must be connected to Pin 16 of the ATtiny3226 chip. Then flash any simple `blink.ino` code to the chip by connecting an LED with a resistor.

**Step 3:** For I2C scanning, the pins of SDA and SCL are Pin 10 and Pin 11. Also, in order to read the scanned address in the Serial Monitor, we need to connect the default Pin 17 of ATtiny3226 (which is the TX pin) to the Arduino Nano D1 pin so that the address gets printed. Or else, connect Pin 9 of the ATtiny3226 chip as TX to the Arduino Nano D1 pin.

---

*Pinout of ATtiny3226 chip is referenced in the main README.*
