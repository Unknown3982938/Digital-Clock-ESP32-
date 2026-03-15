# ESP32 Network Clock — Pin Layout

## Main Pin Assignment

| ESP32 Pin | Direction | Connected Component | Component Pin | Description |
|----------|-----------|---------------------|---------------|-------------|
| GPIO18 | Output | TM1637 Time Display | CLK | Clock line for main time display |
| GPIO19 | I/O | TM1637 Time Display | DIO | Data line for main time display |
| GPIO16 | Output | TM1637 Date Display | CLK | Clock line for date display |
| GPIO17 | I/O | TM1637 Date Display | DIO | Data line for date display |
| GPIO33 | Output | Buzzer | + | Active buzzer signal |
| GPIO32 | Output | AM/PM LED | Anode (via 220Ω) | Indicates AM/PM state |
| GPIO34 | Analog Input | LDR Sensor | Divider node | Auto brightness sensing |
| GPIO25 | Input | Mode Button | Button terminal | Mode control |
| GPIO26 | Input | Adjust Button | Button terminal | Enter adjustment mode |
| GPIO27 | Input | Set Button | Button terminal | Increment selected value |
| GPIO14 | Input | Left Button | Button terminal | Move selection left |
| GPIO12 | Input | Right Button | Button terminal | Move selection right |
| GPIO13 | Input | Source Button | Button terminal | Toggle SERVER / RTC mode |
| 3.3V | Power | LDR Divider | VCC | Sensor reference voltage |
| 5V (VIN) | Power | Displays + Buzzer | VCC | Main power rail |
| GND | Ground | All Components | GND | Common system ground |

---

## Time Display (TM1637)

| Display Pin | Connection |
|-------------|------------|
| VCC | 5V |
| GND | GND |
| CLK | GPIO18 |
| DIO | GPIO19 |

---

## Date Display (TM1637)

| Display Pin | Connection |
|-------------|------------|
| VCC | 5V |
| GND | GND |
| CLK | GPIO16 |
| DIO | GPIO17 |

---

## Button Wiring

All buttons use **internal pull-up resistors**.

### Configuration

| Button Pin | Connection |
|------------|------------|
| One terminal | ESP32 GPIO |
| Other terminal | GND |

### Logic

| State | GPIO Level |
|------|------------|
| Idle | HIGH |
| Pressed | LOW |

---

## LDR Brightness Sensor

Voltage divider configuration:

| Component | Connection |
|-----------|------------|
| LDR Top | 3.3V |
| LDR Bottom | GPIO34 |
| 10k Resistor | GPIO34 → GND |

This allows brightness to be read using: analogReadGPIO34

---

## AM/PM LED

| LED Pin | Connection |
|--------|------------|
| Anode | GPIO32 through 220Ω resistor |
| Cathode | GND |

### Behavior

| State | Meaning |
|------|---------|
| LED ON | AM |
| LED OFF | PM |

---

## Buzzer

| Buzzer Pin | Connection |
|-----------|------------|
| Positive (+) | GPIO33 |
| Negative (−) | GND |

Type: Active buzzer

---

## Power System

| Power Source | Connection |
|--------------|-----------|
| UPS Output 5V | ESP32 VIN |
| UPS Output 5V | Both TM1637 displays |
| UPS Output 5V | Buzzer |
| UPS GND | System Ground |

### Battery

| Type | Description |
|------|-------------|
| 18650 Li-ion | UPS backup battery |

---

## Optional RTC (Future Expansion)

| RTC Pin | ESP32 Pin |
|--------|-----------|
| VCC | 3.3V |
| GND | GND |
| SDA | GPIO21 |
| SCL | GPIO22 |

Module recommendation: DS3231 RTC

---

## Notes

| Item | Detail |
|------|-------|
| Wire gauge | 28 AWG |
| Construction | Dual perfboard |
| Power filtering | 1000µF + 470µF capacitors |
| Clock format | 12-hour |

---

##Visual Layout
Wokwi Project Link: https://wokwi.com/projects/458529261643797505
(I apologize for messy wiring layout, I haven't included some of the peripherals since Wokwi doesn't have them, and choosing alternative components might confuse people) 
