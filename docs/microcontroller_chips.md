# ตระกูลชิป Microcontroller: ATmega, ESP, STM32

คู่มือเปรียบเทียบชิปไมโครคอนโทรลเลอร์ยอดนิยม พร้อมความสามารถและการใช้งาน

---

## **1. ตระกูล ATmega (Atmel/Microchip)**

### **ATmega328P**

#### **คุณสมบัติ**

- **สถาปัตยกรรม:** 8-bit AVR
- **ความเร็ว:** 16 MHz
- **Flash:** 32 KB
- **RAM:** 2 KB
- **EEPROM:** 1 KB
- **GPIO:** 23 ขา
- **ADC:** 6 ช่อง (10-bit)
- **PWM:** 6 ช่อง
- **แรงดัน:** 1.8-5.5V

#### **ความสามารถพิเศษ**

- ประหยัดพลังงาน (Sleep Mode)
- มี Watchdog Timer
- มี Brown-out Detection

#### **การใช้งาน**

- **Arduino Uno, Nano:** โปรเจกต์ทั่วไป
- **ระบบควบคุมแสงไฟ:** เปิด-ปิดไฟอัตโนมัติ
- **เซนเซอร์อุณหภูมิ:** DHT22, DS18B20
- **Motor Controller:** ควบคุมมอเตอร์ DC

---

### **ATmega2560**

#### **คุณสมบัติ**

- **ความเร็ว:** 16 MHz
- **Flash:** 256 KB
- **RAM:** 8 KB
- **EEPROM:** 4 KB
- **GPIO:** 86 ขา
- **ADC:** 16 ช่อง (10-bit)
- **PWM:** 15 ช่อง
- **UART:** 4 พอร์ต

#### **ความสามารถพิเศษ**

- GPIO เยอะมาก (86 ขา)
- UART หลายพอร์ต
- Memory เยอะกว่า 328P

#### **การใช้งาน**

- **Arduino Mega:** โปรเจกต์ใหญ่
- **3D Printer:** RAMPS 1.4
- **CNC Machine:** ควบคุม Stepper Motor
- **ระบบ Home Automation:** ควบคุมหลายอุปกรณ์

---

### **ATmega32U4**

#### **คุณสมบัติ**

- **ความเร็ว:** 16 MHz
- **Flash:** 32 KB
- **RAM:** 2.5 KB
- **GPIO:** 26 ขา
- **USB:** Native USB (HID)

#### **ความสามารถพิเศษ**

- **USB ในตัว** (ไม่ต้องใช้ชิปแปลง)
- ทำ USB Keyboard/Mouse ได้

#### **การใช้งาน**

- **Arduino Leonardo, Pro Micro:** USB Projects
- **Custom Keyboard:** DIY Mechanical Keyboard
- **USB Game Controller:** Joystick, Racing Wheel
- **USB HID Device:** Barcode Scanner

---

## **2. ตระกูล ESP (Espressif)**

### **ESP8266**

#### **คุณสมบัติ**

- **สถาปัตยกรรม:** 32-bit Xtensa
- **ความเร็ว:** 80/160 MHz
- **Flash:** 512 KB - 4 MB (External)
- **RAM:** 80 KB
- **GPIO:** 17 ขา
- **ADC:** 1 ช่อง (10-bit)
- **WiFi:** 802.11 b/g/n (2.4 GHz)

#### **ความสามารถพิเศษ**

- **WiFi ในตัว**
- ราคาถูกมาก (~30 บาท)
- Deep Sleep (20 µA)

#### **การใช้งาน**

- **NodeMCU, Wemos D1 Mini:** IoT Projects
- **Smart Plug:** เปิด-ปิดปลั๊กผ่าน WiFi
- **Weather Station:** ส่งข้อมูลอากาศขึ้น Cloud
- **WiFi Relay:** ควบคุม Relay ผ่าน WiFi

---

### **ESP32**

#### **คุณสมบัติ**

- **สถาปัตยกรรม:** 32-bit Xtensa Dual-Core
- **ความเร็ว:** 240 MHz (2 cores)
- **Flash:** 4 MB - 16 MB (External)
- **RAM:** 520 KB
- **GPIO:** 34 ขา
- **ADC:** 18 ช่อง (12-bit)
- **DAC:** 2 ช่อง
- **WiFi:** 802.11 b/g/n (2.4 GHz)
- **Bluetooth:** Classic + BLE 4.2

#### **ความสามารถพิเศษ**

- **Dual-Core** (ทำงาน 2 อย่างพร้อมกัน)
- **WiFi + Bluetooth**
- **Touch Sensor:** 10 ขา
- **Hall Sensor:** ตรวจจับแม่เหล็ก
- Deep Sleep (10 µA)

#### **การใช้งาน**

- **ESP32 DevKit:** IoT, Smart Home
- **ESP32-CAM:** กล้องวงจรปิด WiFi
- **Smart Speaker:** Voice Control
- **Bluetooth Audio:** ลำโพง Bluetooth
- **GPS Tracker:** WiFi + GPS
- **Drone Controller:** รับสัญญาณ I-BUS/S-BUS

---

### **ESP32-S2**

#### **คุณสมบัติ**

- **Core:** Single-Core (240 MHz)
- **WiFi:** 802.11 b/g/n
- **Bluetooth:** ไม่มี
- **USB:** Native USB (OTG)
- **GPIO:** 43 ขา

#### **ความสามารถพิเศษ**

- **USB ในตัว** (ไม่ต้องใช้ชิปแปลง)
- GPIO เยอะกว่า ESP32

#### **การใช้งาน**

- **USB Device:** Keyboard, Mouse
- **IoT ที่ไม่ต้องการ Bluetooth**

---

### **ESP32-C3**

#### **คุณสมบัติ**

- **สถาปัตยกรรม:** 32-bit RISC-V
- **ความเร็ว:** 160 MHz
- **WiFi + BLE 5.0**
- **ราคา:** ถูกกว่า ESP32

#### **ความสามารถพิเศษ**

- **RISC-V** (ไม่ใช่ Xtensa)
- **BLE 5.0** (ใหม่กว่า ESP32)
- ราคาถูก

#### **การใช้งาน**

- **IoT ราคาถูก**
- **BLE Beacon**
- **Smart Sensor**

---

## **3. ตระกูล STM32 (STMicroelectronics)**

### **STM32F103C8T6 (Blue Pill)**

#### **คุณสมบัติ**

- **สถาปัตยกรรม:** 32-bit ARM Cortex-M3
- **ความเร็ว:** 72 MHz
- **Flash:** 64 KB (บางรุ่น 128 KB)
- **RAM:** 20 KB
- **GPIO:** 37 ขา
- **ADC:** 10 ช่อง (12-bit)
- **Timer:** 7 ตัว
- **UART:** 3 พอร์ต
- **SPI:** 2 พอร์ต
- **I2C:** 2 พอร์ต
- **CAN:** 1 พอร์ต

#### **ความสามารถพิเศษ**

- **CAN Bus** (ใช้ในรถยนต์)
- **DMA** (Direct Memory Access)
- ราคาถูก (~50 บาท)

#### **การใช้งาน**

- **Blue Pill Board:** โปรเจกต์ทั่วไป
- **CAN Bus Reader:** อ่านข้อมูลรถยนต์ (OBD-II)
- **Drone Flight Controller:** ควบคุมโดรน
- **Fast Data Logger:** บันทึกข้อมูลความเร็วสูง

---

### **STM32F401CCU6 (Black Pill)**

#### **คุณสมบัติ**

- **สถาปัตยกรรม:** ARM Cortex-M4
- **ความเร็ว:** 84 MHz
- **Flash:** 256 KB
- **RAM:** 64 KB
- **FPU:** มี (Floating Point Unit)

#### **ความสามารถพิเศษ**

- **FPU** (คำนวณทศนิยมเร็ว)
- Memory เยอะกว่า Blue Pill

#### **การใช้งาน**

- **DSP (Digital Signal Processing)**
- **Audio Processing**
- **Fast Control System**

---

### **STM32F407VGT6**

#### **คุณสมบัติ**

- **ความเร็ว:** 168 MHz
- **Flash:** 1 MB
- **RAM:** 192 KB
- **GPIO:** 82 ขา
- **ADC:** 16 ช่อง (12-bit)
- **DAC:** 2 ช่อง
- **FPU:** มี

#### **ความสามารถพิเศษ**

- **ความเร็วสูงมาก** (168 MHz)
- Memory เยอะมาก
- GPIO เยอะ

#### **การใช้งาน**

- **Industrial Control**
- **Motor Control (FOC)**
- **High-Speed Data Acquisition**
- **Audio/Video Processing**

---

### **STM32H743**

#### **คุณสมบัติ**

- **สถาปัตยกรรม:** ARM Cortex-M7
- **ความเร็ว:** 480 MHz
- **Flash:** 2 MB
- **RAM:** 1 MB
- **FPU + DSP**

#### **ความสามารถพิเศษ**

- **เร็วที่สุดใน STM32**
- Memory มหาศาล

#### **การใช้งาน**

- **High-Performance Computing**
- **AI/ML on Edge**
- **Advanced Motor Control**

---

## **ตารางเปรียบเทียบตระกูลชิป**

| ชิป             | สถาปัตยกรรม  | ความเร็ว | RAM    | WiFi/BT | ราคา  | เหมาะกับ   |
| -------------- | ----------- | ------- | ------ | ------- | ----- | --------- |
| **ATmega328P** | 8-bit AVR   | 16 MHz  | 2 KB   | ไม่มี     | ~30฿  | ผู้เริ่มต้น    |
| **ATmega2560** | 8-bit AVR   | 16 MHz  | 8 KB   | ไม่มี     | ~150฿ | GPIO เยอะ |
| **ESP8266**    | 32-bit      | 160 MHz | 80 KB  | WiFi    | ~30฿  | IoT ถูก    |
| **ESP32**      | 32-bit Dual | 240 MHz | 520 KB | WiFi+BT | ~100฿ | IoT ครบ   |
| **STM32F103**  | ARM M3      | 72 MHz  | 20 KB  | ไม่มี     | ~50฿  | CAN Bus   |
| **STM32F407**  | ARM M4      | 168 MHz | 192 KB | ไม่มี     | ~300฿ | อุตสาหกรรม |

---

## **เคล็ดลับการเลือกชิป**

### **ผู้เริ่มต้น**
- **ATmega328P** (Arduino Uno) - ง่ายที่สุด

### **IoT / Smart Home**
- **ESP32** - WiFi + Bluetooth ครบ
- **ESP8266** - ถูกกว่า แต่ไม่มี Bluetooth

### **ความเร็วสูง / อุตสาหกรรม**
- **STM32F407** - เร็ว มี FPU
- **STM32H743** - เร็วที่สุด

### **CAN Bus / รถยนต์**
- **STM32F103** - มี CAN Bus ในตัว

### **GPIO เยอะ**
- **ATmega2560** (86 ขา)
- **STM32F407** (82 ขา)

---

> [!TIP]
> **คำแนะนำ:** เริ่มจาก ATmega328P (Arduino) เพื่อเรียนรู้ จากนั้นเปลี่ยนไป ESP32 เมื่อต้องการ WiFi หรือ STM32 เมื่อต้องการความเร็วสูง

---
