# ประเภทการสื่อสารและความเร็วในการสื่อสาร

ในโลกของไมโครคอนโทรลเลอร์และ IoT มีโปรโตคอลการสื่อสารหลายแบบ แต่ละแบบมีจุดเด่นและความเหมาะสมต่างกัน

---

## **1. UART (Universal Asynchronous Receiver-Transmitter)**

### **ลักษณะ**

- **แบบ:** Asynchronous (ไม่มีสัญญาณนาฬิการ่วม)
- **จำนวนสาย:** 2 สาย (TX, RX) + GND
- **ทิศทาง:** Full-Duplex (ส่ง-รับพร้อมกันได้)
- **จำนวนอุปกรณ์:** 1 ต่อ 1 (Point-to-Point)

### **ความเร็ว (Baud Rate)**

- **9600 bps:** GPS, เซนเซอร์ทั่วไป
- **115200 bps:** Arduino, ESP32 (ยอดนิยม)
- **921600 bps:** ESP32 Flash Download

### **การใช้งาน**

- Arduino ↔ คอมพิวเตอร์ (Serial Monitor)
- ESP32 ↔ GPS Module
- Bluetooth Module (HC-05, HC-06)

---

## **2. I2C (Inter-Integrated Circuit)**

### **ลักษณะ**

- **แบบ:** Synchronous (มีสัญญาณนาฬิกา)
- **จำนวนสาย:** 2 สาย (SDA, SCL) + GND
- **จำนวนอุปกรณ์:** หลายตัว (ใช้ Address แยก)

### **ความเร็ว**

- **100 Kbps:** Standard Mode - เซนเซอร์ทั่วไป
- **400 Kbps:** Fast Mode - OLED, RTC (ยอดนิยม)
- **1 Mbps:** Fast Mode Plus

### **การใช้งาน**

- OLED Display (SSD1306)
- RTC (DS3231, DS1307)
- เซนเซอร์ (BMP280, MPU6050, AHT20)

---

## **3. SPI (Serial Peripheral Interface)**

### **ลักษณะ**

- **แบบ:** Synchronous
- **จำนวนสาย:** 4 สาย (MOSI, MISO, SCK, CS) + GND
- **ทิศทาง:** Full-Duplex

### **ความเร็ว**

- **1-10 MHz:** เซนเซอร์, SD Card
- **10-20 MHz:** TFT Display
- **20-80 MHz:** ESP32 Flash Memory

### **การใช้งาน**

- SD Card Module
- TFT Display (ILI9341, ST7735)
- NRF24L01 (Wireless Module)

---

## **4. I-BUS (FlySky)**

### **ลักษณะ**

- **แบบ:** Serial Protocol (UART-based)
- **จำนวนสาย:** 1 สาย (Signal) + GND + VCC
- **ทิศทาง:** One-way (Receiver → Flight Controller)
- **จำนวนช่อง:** 6-14 ช่อง

### **ความเร็ว**

- **115200 Baud**
- **อัพเดท:** 7 ms (ประมาณ 143 Hz)

### **ข้อดี**

- ใช้สายเดียว ประหยัดขา GPIO
- ส่งข้อมูลดิจิทัล แม่นยำกว่า PWM
- รองรับหลายช่อง (6-14 ช่อง)
- ราคาถูก (รีโมท FlySky FS-i6, FS-i6X)

### **การใช้งาน**

- โดรน DIY
- เครื่องบิน RC
- รถ RC ที่ต้องการหลายช่อง

---

## **5. S-BUS (Futaba)**

### **ลักษณะ**

- **แบบ:** Serial Protocol (Inverted UART)
- **จำนวนสาย:** 1 สาย (Signal) + GND + VCC
- **ทิศทาง:** One-way (Receiver → Flight Controller)
- **จำนวนช่อง:** 16 ช่อง

### **ความเร็ว**

- **100000 Baud** (Inverted UART)
- **อัพเดท:** 7-14 ms (ประมาณ 70-143 Hz)

### **ข้อดี**

- รองรับ 16 ช่อง
- ความละเอียดสูง (11-bit per channel)
- มาตรฐานอุตสาหกรรม RC

### **ข้อเสีย**

- **Inverted Signal** ต้องใช้วงจรกลับสัญญาณ
- ราคาแพงกว่า I-BUS

### **การใช้งาน**

- โดรนแข่ง (Racing Drone)
- เครื่องบิน RC ขนาดใหญ่
- ระบบควบคุมที่ต้องการหลายช่อง

### **การแก้ปัญหา Inverted Signal**

```cpp
// ESP32 - Software Invert
Serial2.begin(100000, SERIAL_8E2, RXD2, TXD2, true); // true = inverted
```

---

## **ตารางสรุปเปรียบเทียบ**

| โปรโตคอล  | ความเร็ว       | จำนวนสาย | การใช้งาน           |
| --------- | ------------- | ------- | ------------------ |
| **UART**  | 9.6K-921K bps | 2       | GPS, Debug         |
| **I2C**   | 100K-1M bps   | 2       | OLED, RTC, เซนเซอร์ |
| **SPI**   | 1-80 MHz      | 4+      | SD Card, Display   |
| **I-BUS** | 115200 baud   | 1       | RC FlySky (โดรน)   |
| **S-BUS** | 100000 baud   | 1       | RC Futaba (โดรน)   |

---

> [!TIP]
> **เคล็ดลับ:** สำหรับโดรน DIY แนะนำใช้ **I-BUS** (ถูกกว่า) หรือ **S-BUS** (แม่นยำกว่า) แทน PWM เพราะใช้สายเดียวและรองรับหลายช่อง

---
