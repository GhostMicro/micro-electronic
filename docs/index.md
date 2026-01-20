# ยินดีต้อนรับสู่พื้นฐานอิเล็กทรอนิกส์

แหล่งรวบรวมความรู้และเอกสารอ้างอิงสำหรับผู้เริ่มต้นและผู้สนใจด้านอิเล็กทรอนิกส์ ไมโครคอนโทรลเลอร์ และ IoT

---

## **📚 เนื้อหาหลัก**

### **พื้นฐานอิเล็กทรอนิกส์**
- [อุปกรณ์พื้นฐาน](basic_components.md) - Resistor, Capacitor, Diode, Transistor
- [ทฤษฎีไฟฟ้า](basic_theory.md) - กฎของโอห์ม, กำลังไฟฟ้า, AC/DC
- [คู่มือใช้งาน](practical_guide.md) - Breadboard, Multimeter, เครื่องมือพื้นฐาน
- [วงจรพื้นฐาน](basic_circuits.md) - Seven Segment, วัดแรงดัน/กระแส, LED Driver
- [ระบบป้องกัน](circuit_protection.md) - กรองสัญญาณ, ป้องกันไฟย้อน, Fuse

### **แหล่งจ่ายไฟและพลังงาน**
- [แหล่งจ่ายไฟ](power_sources.md) - ภาพรวมแหล่งจ่ายไฟ
- [Li-ion 18650](power_sources_li-ion.md) - แบตเตอรี่ Li-ion
- [Li-Po](power_sources_li-po.md) - แบตเตอรี่ Li-Po
- [BMS](power_sources_bms.md) - ระบบจัดการแบตเตอรี่
- [การดูแลรักษา](power_sources_maintenance.md) - การดูแลแบตเตอรี่

### **วงจรและการต่อวงจร**
- [การต่อวงจรอนุกรมและขนาน](circuit_series_parallel.md)
- [Pull-Up และ Pull-Down](pull_up_pull_down.md)
- [Inverter และ Converter](inverter_converter.md)

### **การสื่อสาร**
- [โปรโตคอลการสื่อสาร](communication_protocols.md) - UART, I2C, SPI, I-BUS, S-BUS
- [สัญญาณไร้สาย](wireless_communication.md) - WiFi, Bluetooth, LoRa, GSM
- [GPS Modules](gps_modules.md) - โมดูล GPS และการใช้งาน

### **ไมโครคอนโทรลเลอร์**
- [ตระกูลชิป](microcontroller_chips.md) - ATmega, ESP, STM32
- [การประยุกต์ใช้](microcontroller_applications.md) - โปรเจกต์ต่างๆ
- [DIY Modules](diy_modules.md) - โมดูลยอดนิยม

### **Software และเครื่องมือ**
- [IDE สำหรับเขียนโค้ด](software_ide.md) - Arduino IDE, PlatformIO, VS Code
- [ออกแบบวงจร](software_hardware_design.md) - Fritzing, KiCad, EasyEDA
- [เครื่องมือขั้นสูง](software_advanced_tools.md) - ROS, OpenCV, Node-RED, QGroundControl

### **มาตรฐานและอุตสาหกรรม**
- [มาตรฐานอุตสาหกรรม](industrial_standards.md) - USB, WiFi, IP Rating, RoHS

---

## **🎯 เริ่มต้นอย่างไร?**

### **สำหรับผู้เริ่มต้น**
1. อ่าน [ทฤษฎีไฟฟ้า](basic_theory.md) เพื่อเข้าใจพื้นฐาน
2. ศึกษา [อุปกรณ์พื้นฐาน](basic_components.md)
3. ทดลองใช้ [Breadboard](practical_guide.md)
4. เริ่มต้นด้วย [Arduino IDE](software_ide.md)

### **สำหรับ IoT / Smart Home**
1. เลือก [ESP32](microcontroller_chips.md#esp32)
2. ศึกษา [WiFi และ Bluetooth](wireless_communication.md)
3. ใช้ [Node-RED](software_advanced_tools.md#node-red) สร้าง Dashboard

### **สำหรับโดรน / RC**
1. ศึกษา [I-BUS/S-BUS](communication_protocols.md)
2. ใช้ [ArduPilot](software_advanced_tools.md#ardupilot)
3. ควบคุมด้วย [QGroundControl](software_advanced_tools.md#qgroundcontrol)

---

## **⚡ ข้อควรระวัง**

> [!WARNING]
> - ใช้แบตเตอรี่ Li-ion/Li-Po ต้องระวัง อ่าน [การดูแลรักษา](power_sources_maintenance.md)
> - ต่อวงจรให้ถูกต้อง ศึกษา [Pull-Up/Pull-Down](pull_up_pull_down.md)
> - ปฏิบัติตาม [มาตรฐานความปลอดภัย](industrial_standards.md)

---

## **📖 เอกสารนี้เหมาะกับ**

- ผู้เริ่มต้นที่สนใจอิเล็กทรอนิกส์
- นักศึกษาวิศวกรรม
- Maker และ DIY Enthusiast
- ผู้พัฒนา IoT และ Smart Home
- ผู้สนใจโดรนและหุ่นยนต์

---

> [!NOTE]
> เอกสารนี้อัปเดตอย่างต่อเนื่อง หากพบข้อผิดพลาดหรือต้องการเพิ่มเติมเนื้อหา สามารถแจ้งได้

---
