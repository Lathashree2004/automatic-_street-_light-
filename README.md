# 🌃 Smart or automatic Street Light using Arduino

This project automates street lighting using **Arduino**, an **LDR** (Light Dependent Resistor), and **IR sensors**. LEDs turn on only when it's **dark** and **motion is detected**, helping to conserve electricity and simulate a real-world smart street lighting system.

---

## 📦 Components Used

| Component         | Quantity | Description                      |
|------------------|----------|----------------------------------|
| Arduino Uno       | 1        | Microcontroller board            |
| LDR Module        | 1        | Detects day/night                |
| IR Sensor Modules | 2        | Detect motion                    |
| White LEDs        | 2        | Acts as street lights            |
| 220Ω Resistors    | 2        | Current limiting for LEDs        |
| Breadboard & Wires| 1 set    | For circuit assembly             |

---

## ⚙️ Working Principle

- The **LDR** detects darkness (low light level).
- The system then checks both **IR sensors**.
- If motion is detected, the respective **LED** turns ON.
- If no motion is detected, the LED remains OFF even at night.
- Lights stay OFF during daytime, saving power.

---

## 🔌 Pin Connections

| Arduino Pin | Connected To     |
|-------------|------------------|
| A0          | LDR analog output|
| D2          | IR Sensor 1 OUT  |
| D3          | IR Sensor 2 OUT  |
| D8          | LED 1 Anode (+)  |
| D9          | LED 2 Anode (+)  |
| GND         | Common Ground    |
| 5V          | Power to sensors |

---

## 💻 Arduino Code Preview

```cpp
int ldrPin = A0;
int ir1Pin = 2;
int ir2Pin = 3;
int led1 = 8;
int led2 = 9;

void setup() {
  pinMode(ir1Pin, INPUT);
  pinMode(ir2Pin, INPUT);
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int ldrValue = analogRead(ldrPin);
  int ir1 = digitalRead(ir1Pin);
  int ir2 = digitalRead(ir2Pin);

  if (ldrValue > 500 && ir1 == LOW)
    digitalWrite(led1, HIGH);
  else
    digitalWrite(led1, LOW);

  if (ldrValue > 500 && ir2 == LOW)
    digitalWrite(led2, HIGH);
  else
    digitalWrite(led2, LOW);

  delay(200);
}
