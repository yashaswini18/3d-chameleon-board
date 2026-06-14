# Wiring Reference — ATtiny3226 Bring-Up

## UPDI Programming Wiring (Arduino Nano → ATtiny3226)

```
Arduino Nano                        ATtiny3226
─────────────                       ──────────
  RESET ──── [10µF Cap] ──── GND
  D6    ──── [Resistor] ──── Pin 16 (UPDI)
  GND   ────────────────────── GND
  5V    ────────────────────── VCC
```

> Use a 470Ω resistor between Nano D6 and ATtiny3226 Pin 16.

---

## Serial Monitor Wiring (ATtiny3226 → Arduino Nano)

### Option A: Default TX
```
ATtiny3226 Pin 17 (TX) ──── Arduino Nano D1 (RX)
```

### Option B: Alternate TX
```
ATtiny3226 Pin 9 (TX) ──── Arduino Nano D1 (RX)
```

---

## I2C Pins on ATtiny3226

```
SDA → Pin 10
SCL → Pin 11
```

---

## Blink Test Wiring

```
ATtiny3226 GPIO ──── [Resistor ~220Ω] ──── LED (+) ──── GND
```
