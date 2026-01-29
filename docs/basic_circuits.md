# วงจรพื้นฐานที่ควรรู้จัก

วงจรที่ใช้บ่อยในโปรเจกต์อิเล็กทรอนิกส์

---

## **1. วงจร Seven Segment Display**

### **หลักการทำงาน**

Seven Segment Display เป็นจอแสดงผลตัวเลข 0-9 ประกอบด้วย LED 7 ดวง (a-g) และจุดทศนิยม

### **ประเภท**

- **Common Cathode:** ขั้วลบรวมกัน ส่ง HIGH เพื่อให้ LED ติด
- **Common Anode:** ขั้วบวกรวมกัน ส่ง LOW เพื่อให้ LED ติด

### **การต่อวงจร**

#### **แบบควบคุมโดยตรง**

```
Arduino Pin → Resistor (220Ω) → LED Segment (a-g)
Common Pin → GND (Common Cathode) หรือ VCC (Common Anode)
```

#### **แบบใช้ Decoder (7447/7448)**

- ส่งข้อมูล 4 บิต (BCD) เข้า Decoder
- Decoder แปลงเป็นสัญญาณ 7 ขาออกมา
- ประหยัดขา GPIO (ใช้แค่ 4 ขา)

### **การแสดงหลายหลัก (Multiplexing)**

```
หลักที่ 1: เปิด → แสดงเลข → ปิด
หลักที่ 2: เปิด → แสดงเลข → ปิด
หลักที่ 3: เปิด → แสดงเลข → ปิด
วนซ้ำเร็วมาก (> 50 Hz) ตาจะมองเห็นเป็นภาพนิ่ง
```

### **ตัวอย่างโค้ด Arduino**

```cpp
// Common Cathode
byte segments[] = {2,3,4,5,6,7,8}; // a-g
byte numbers[10][7] = {
  {1,1,1,1,1,1,0}, // 0
  {0,1,1,0,0,0,0}, // 1
  {1,1,0,1,1,0,1}, // 2
  // ... เพิ่มเติม
};

void displayNumber(int num) {
  for(int i=0; i<7; i++) {
    digitalWrite(segments[i], numbers[num][i]);
  }
}
```

---

## **2. วงจรตรวจสอบแรงดัน (Voltage Sensing)**

### **2.1 Voltage Divider (แบ่งแรงดัน)**

#### **หลักการ**

ใช้ตัวต้านทาน 2 ตัวแบ่งแรงดันให้ต่ำลง เพื่อให้ ADC อ่านได้

#### **สูตร**

```
Vout = Vin × (R2 / (R1 + R2))
```

#### **ตัวอย่าง: วัดแบต 12V ด้วย Arduino (ADC 5V)**

```
R1 = 10kΩ
R2 = 10kΩ
Vout = 12V × (10k / 20k) = 6V (เกิน! ต้องปรับ)

แก้ไข:
R1 = 20kΩ
R2 = 10kΩ
Vout = 12V × (10k / 30k) = 4V (ได้!)
```

#### **โค้ด Arduino**

```cpp
float readVoltage() {
  int raw = analogRead(A0);
  float voltage = (raw / 1023.0) * 5.0; // ADC to Voltage
  float actualVoltage = voltage * 3.0;  // คูณกลับ (R1+R2)/R2
  return actualVoltage;
}
```

### **2.2 Zener Diode Protection**

ใช้ Zener Diode ป้องกันแรงดันเกิน

```
Input → Resistor → ADC Pin
              ↓
         Zener Diode (5.1V) → GND
```

---

## **3. วงจรตรวจสอบกระแส (Current Sensing)**

### **3.1 Shunt Resistor Method**

#### **หลักการ**

ใช้ตัวต้านทานค่าต่ำมาก (0.1Ω) ต่ออนุกรมกับโหลด วัดแรงดันตกคร่อม

#### **สูตร**

```
I = V / R
V = I × R
```

#### **ตัวอย่าง**

```
Shunt Resistor = 0.1Ω
กระแส = 1A
แรงดันตก = 1A × 0.1Ω = 0.1V (100mV)
```

#### **วงจร**

```
VCC → Shunt Resistor (0.1Ω) → Load → GND
       ↓           ↓
      V+          V-  → Differential Amplifier → ADC
```

### **3.2 ACS712 Current Sensor**

#### **คุณสมบัติ**

- วัดกระแส AC/DC ได้
- ช่วงวัด: ±5A, ±20A, ±30A
- แรงดันออก: 2.5V ± (กระแส × Sensitivity)

#### **โค้ด Arduino**

```cpp
float readCurrent() {
  int raw = analogRead(A0);
  float voltage = (raw / 1023.0) * 5.0;
  float current = (voltage - 2.5) / 0.185; // ACS712-5A
  return current;
}
```

---

## **4. วงจร LED Driver**

### **4.1 LED เดี่ยว**

```
GPIO → Resistor → LED → GND

R = (Vcc - Vf) / I
Vcc = 5V, Vf = 2V (LED แดง), I = 20mA
R = (5 - 2) / 0.02 = 150Ω (ใช้ 220Ω)
```

### **4.2 LED หลายดวงอนุกรม**

```
12V → R → LED1 → LED2 → LED3 → GND
R = (12 - 2×3) / 0.02 = 300Ω (ใช้ 330Ω)
```

### **4.3 LED ขนาน (ผิด!)**

```
❌ ห้ามต่อ LED ขนานโดยใช้ Resistor ตัวเดียว
✅ ต้องใช้ Resistor แยกแต่ละดวง
```

---

## **5. วงจร PWM (Pulse Width Modulation)**

### **การใช้งาน**

- ควบคุมความสว่าง LED
- ควบคุมความเร็วมอเตอร์
- สร้างเสียง (Buzzer)

### **ตัวอย่างโค้ด**

```cpp
int ledPin = 9; // PWM Pin

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  for(int i=0; i<=255; i++) {
    analogWrite(ledPin, i); // 0-255
    delay(10);
  }
}
```

---

## **6. วงจร Debounce (กรองสัญญาณปุ่มกด)**

### **ปัญหา**

ปุ่มกดมีการสั่นของสัญญาณ (Bounce) ทำให้อ่านค่าผิด

### **แก้ไขด้วย Hardware**

```
Button → Resistor (10kΩ) → GND
    ↓
Capacitor (0.1µF) → GND
    ↓
GPIO Pin
```

### **แก้ไขด้วย Software**

```cpp
int buttonPin = 2;
int lastState = HIGH;
unsigned long lastDebounceTime = 0;
unsigned long debounceDelay = 50;

void loop() {
  int reading = digitalRead(buttonPin);
  
  if (reading != lastState) {
    lastDebounceTime = millis();
  }
  
  if ((millis() - lastDebounceTime) > debounceDelay) {
    if (reading == LOW) {
      // ปุ่มถูกกดแน่นอน
    }
  }
  
  lastState = reading;
}
```

---

## **ตารางสรุป**

| วงจร                | การใช้งาน  | อุปกรณ์หลัก             |
| ------------------- | --------- | -------------------- |
| **Seven Segment**   | แสดงตัวเลข | LED 7 ดวง, Decoder   |
| **Voltage Divider** | วัดแรงดัน   | Resistor 2 ตัว        |
| **Current Sensing** | วัดกระแส   | Shunt R, ACS712      |
| **LED Driver**      | ควบคุม LED | Resistor, Transistor |
| **PWM**             | ควบคุมกำลัง  | ไม่ต้องใช้อุปกรณ์เพิ่ม      |
| **Debounce**        | กรองสัญญาณ | Capacitor, Software  |

---

> [!TIP]
> **เคล็ดลับ:** ทดลองวงจรบน Breadboard ก่อนเสมอ และใช้ Multimeter ตรวจสอบค่าต่างๆ

---
