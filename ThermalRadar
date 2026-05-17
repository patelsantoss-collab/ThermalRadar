# Thermistor Temperature Alarm System (ESP32)

## Sarav Patel Santosh  
CS-210 Computer Systems Fundamentals – Spring 2026 Final Project

---

# Project Overview

This project is a temperature alarm system using a thermistor and an ESP32 microcontroller. It reads temperature from a sensor and turns on an LED and buzzer when the temperature gets too high.

The goal of this project is to show how a computer system can:
- read input from a sensor
- process data
- make a decision
- control outputs

The user can set the temperature limit, so the alarm is adjustable instead of fixed.

---

# System Description

```text
Thermistor → ESP32 → Temperature Calculation → Comparison → LED + Buzzer
```

---

# How It Works

1. The thermistor reads temperature changes
2. The ESP32 reads the analog value
3. The program converts the value into temperature (Celsius)
4. The temperature is compared to a user-set limit
5. If temperature is too high:
   - LED turns ON
   - Buzzer turns ON
6. If temperature is safe:
   - Everything stays OFF

---

# Parts Used

- ESP32 microcontroller
- Thermistor (temperature sensor)
- 10kΩ resistor
- LED
- Buzzer
- Breadboard
- Jumper wires
- USB cable

---

# Circuit Setup

```text
Thermistor circuit:

3.3V → Thermistor → GPIO1
                    |
                 10kΩ
                    |
                   GND

Outputs:

GPIO2 → LED → GND
GPIO4 → Buzzer → GND
```

---

# Code Used

```cpp
#include <math.h>

#define PIN_ANALOG_IN 1
#define LED_PIN 2
#define BUZZER_PIN 4

const float BETA = 3950.0;
const float SERIES_RESISTOR = 10.0;
const float NOMINAL_TEMPERATURE = 25.0;

// User can change this value
float TEMP_LIMIT = 30.0;

double readTemperature();

void setup() {
    Serial.begin(115200);

    pinMode(LED_PIN, OUTPUT);
    pinMode(BUZZER_PIN, OUTPUT);
}

void loop() {

    double tempC = readTemperature();

    Serial.print("Temperature: ");
    Serial.println(tempC);

    if(tempC > TEMP_LIMIT) {

        digitalWrite(LED_PIN, HIGH);
        tone(BUZZER_PIN, 1000);

    } else {

        digitalWrite(LED_PIN, LOW);
        noTone(BUZZER_PIN);
    }

    delay(1000);
}

double readTemperature() {

    int adcValue = analogRead(PIN_ANALOG_IN);

    double voltage = (double)adcValue / 4095.0 * 3.3;

    double resistance = SERIES_RESISTOR * voltage / (3.3 - voltage);

    double tempK = 1.0 / (
        1.0 / (273.15 + NOMINAL_TEMPERATURE)
        + log(resistance / 10.0) / BETA
    );

    return tempK - 273.15;
}
```

---

# What the Code Does (Simple Explanation)

- `analogRead()` gets a number from the sensor
- That number is turned into voltage
- Voltage is used to calculate resistance
- Resistance is converted into temperature
- Temperature is compared to the limit
- If it is too high, the alarm turns on

---

# Testing

### Normal Temperature
- LED OFF
- Buzzer OFF
- Serial Monitor shows temperature

### High Temperature
- LED ON
- Buzzer ON
- Alarm activates

---

# What I Learned

- How sensors send data to a microcontroller
- How analog inputs work on the ESP32
- How to convert sensor values into temperature
- How a program can make decisions based on input

---

# Possible Improvements

- Add a display to show temperature
- Let user change temperature limit with buttons
- Add WiFi alerts
- Save temperature data over time

---

# Conclusion

This project shows a simple computer system that reads input, processes data, and produces output. The ESP32 reads temperature from a sensor and activates an alarm when needed. The system is adjustable and responds in real time.
