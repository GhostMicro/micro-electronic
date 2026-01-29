# ระบบป้องกันวงจร

วงจรป้องกันที่สำคัญเพื่อความปลอดภัยและความทนทานของอุปกรณ์

---

## **1. วงจรกรองกระแสและความถี่**

### **1.1 Decoupling Capacitor (กรองสัญญาณรบกวน)**

#### **หลักการ**

ตัวเก็บประจุต่อขนานกับแหล่งจ่ายไฟ เพื่อกรองสัญญาณรบกวนความถี่สูง

#### **การต่อวงจร**

```
VCC → Decoupling Cap (0.1µF Ceramic) → GND
      ใกล้ขา VCC ของ IC มากที่สุด
```

#### **ค่าที่แนะนำ**

- **0.1µF (100nF) Ceramic:** กรองความถี่สูง (ใช้ทุก IC)
- **10µF Electrolytic:** กรองความถี่ต่ำ (ใช้กับแหล่งจ่ายหลัก)
- **100µF:** สำรองพลังงานชั่วคราว

#### **กฎการใช้งาน**

- ใช้ 0.1µF ทุก IC
- ต่อใกล้ขา VCC และ GND มากที่สุด
- ใช้ทั้ง Ceramic และ Electrolytic ร่วมกัน

### **1.2 LC Filter (Low-Pass Filter)**

#### **หลักการ**

ใช้ Inductor (L) และ Capacitor (C) กรองความถี่สูง

#### **วงจร**

```
Input → Inductor → Output
              ↓
         Capacitor → GND
```

#### **การใช้งาน**

- กรองสัญญาณรบกวนจาก Switching Regulator
- กรองสัญญาณ EMI/RFI
- ป้องกันสัญญาณรบกวนในวงจรเสียง

### **1.3 Ferrite Bead**

#### **หลักการ**

ต้านทานความถี่สูง ปล่อยความถี่ต่ำผ่าน

#### **การใช้งาน**

```
Power Input → Ferrite Bead → IC VCC
```

- กรอง EMI/RFI
- ป้องกันสัญญาณรบกวนในสาย USB
- ใช้กับสาย Power ของ IC ที่ละเอียด

---

## **2. ระบบป้องกันไฟย้อน (Reverse Polarity Protection)**

### **2.1 ใช้ Diode**

#### **วงจร**

```
Input (+) → Diode (1N4007) → Output (+)
Input (-) ────────────────→ Output (-)
```

#### **ข้อดี**

- ง่าย ราคาถูก
- ป้องกันได้ 100%

#### **ข้อเสีย**

- แรงดันตก 0.7V (Diode ธรรมดา)
- แรงดันตก 0.3V (Schottky Diode)
- สูญเสียพลังงาน

### **2.2 ใช้ P-Channel MOSFET**

#### **วงจร**

```
Input (+) → Source (MOSFET) → Drain → Output (+)
            Gate ← Resistor (10kΩ) → Input (-)
Input (-) ──────────────────────────→ Output (-)
```

#### **ข้อดี**

- แรงดันตกต่ำมาก (< 0.1V)
- ไม่สูญเสียพลังงาน
- เหมาะกับกระแสสูง

#### **ข้อเสีย**

- ซับซ้อนกว่า
- ราคาแพงกว่า

### **2.3 ใช้ Fuse + Diode**

#### **วงจร**

```
Input (+) → Fuse → Load → Output
Input (-) ────────────────→ Output
     ↓
Diode (ย้อนกลับ) → Fuse
```

เมื่อต่อผิดขั้ว Diode จะนำไฟ → Fuse ขาด

---

## **3. วงจรฟิวส์อิเล็กทรอนิกส์ (Electronic Fuse)**

### **3.1 ใช้ MOSFET + Current Sensing**

#### **หลักการ**

ตรวจจับกระแสเกิน → ตัด MOSFET ทันที

#### **วงจร**

```
Input → MOSFET → Shunt R → Load → GND
        ↑
    Control Circuit
        ↑
    Current Sense
```

#### **ข้อดี**

- ตัดเร็วมาก (µs)
- Reset ได้ (ไม่ต้องเปลี่ยน)
- ปรับค่ากระแสได้

### **3.2 ใช้ IC (เช่น LTC4365)**

#### **คุณสมบัติ**

- Overvoltage Protection
- Undervoltage Protection
- Reverse Polarity Protection
- Overcurrent Protection

---

## **4. ป้องกันแรงดันเกิน (Overvoltage Protection)**

### **4.1 Zener Diode Clamp**

#### **วงจร**

```
Input → Resistor → Output
            ↓
       Zener Diode → GND
```

#### **การทำงาน**

- แรงดันปกติ: Zener ไม่นำไฟ
- แรงดันเกิน: Zener นำไฟ → ลัดวงจรผ่าน Resistor

#### **ตัวอย่าง**

```
Zener 5.1V ป้องกัน GPIO (5V)
Input 12V → R (1kΩ) → GPIO
                ↓
           Zener 5.1V → GND
```

### **4.2 TVS Diode (Transient Voltage Suppressor)**

#### **คุณสมบัติ**

- ตอบสนองเร็วมาก (ps)
- ป้องกัน ESD, Lightning
- ใช้กับสาย I/O, Power

#### **การใช้งาน**

```
Signal Line → TVS Diode → GND
```

---

## **5. ป้องกันกระแสเกิน (Overcurrent Protection)**

### **5.1 Fuse (ฟิวส์)**

#### **ประเภท**

- **Fast-Blow:** ขาดเร็ว (วงจรดิจิทัล)
- **Slow-Blow:** ขาดช้า (มอเตอร์, หม้อแปลง)
- **Resettable Fuse (PTC):** Reset ได้เอง

#### **การเลือกใช้**

```
Fuse Rating = Load Current × 1.25
```

### **5.2 Current Limiting Resistor**

#### **วงจร**

```
Input → Resistor → Load
```

#### **การคำนวณ**

```
R = (Vin - Vload) / Imax
```

---

## **6. ป้องกันการช็อตลัดวงจร**

### **6.1 Circuit Breaker (เบรกเกอร์)**

#### **การทำงาน**

- ตรวจจับกระแสเกิน
- ตัดวงจรอัตโนมัติ
- Reset ได้ (กดปุ่ม)

### **6.2 Isolation (แยกวงจร)**

#### **วิธีการ**

- **Optocoupler:** แยกด้วยแสง
- **Relay:** แยกด้วยแม่เหล็กไฟฟ้า
- **Transformer:** แยกด้วยสนามแม่เหล็ก

#### **ประโยชน์**

- ป้องกันกระแสรั่วไหล
- ป้องกันไฟกระชาก
- ป้องกันไฟช็อต

---

## **7. ป้องกัน ESD (Electrostatic Discharge)**

### **7.1 ESD Diode**

```
Signal → ESD Diode Array → IC Pin
```

### **7.2 RC Filter**

```
Signal → Resistor (1kΩ) → IC Pin
              ↓
         Capacitor (100pF) → GND
```

---

## **ตารางสรุป**

| ระบบป้องกัน     | อุปกรณ์                | การใช้งาน          |
| ------------- | -------------------- | ----------------- |
| **กรองสัญญาณ** | Capacitor, LC Filter | กรอง EMI/RFI      |
| **ไฟย้อน**     | Diode, MOSFET        | ป้องกันต่อผิดขั้ว       |
| **แรงดันเกิน**  | Zener, TVS           | ป้องกัน Overvoltage |
| **กระแสเกิน**  | Fuse, PTC            | ป้องกัน Overcurrent |
| **ช็อตลัดวงจร** | Circuit Breaker      | ตัดวงจรอัตโนมัติ      |
| **ESD**       | ESD Diode, RC        | ป้องกันไฟฟ้าสถิต      |

---

## **แนวทางปฏิบัติที่ดี**

1. **ใช้ Decoupling Cap ทุก IC** (0.1µF)
2. **ป้องกันไฟย้อนเสมอ** (Diode หรือ MOSFET)
3. **ใช้ Fuse กับแหล่งจ่ายไฟหลัก**
4. **แยกวงจรด้วย Optocoupler** (ถ้าต่อกับ AC)
5. **ใช้ TVS Diode กับสาย I/O ภายนอก**

---

> [!WARNING]
> **ข้อควรระวัง:** ระบบป้องกันไม่ได้ทำให้วงจรปลอดภัย 100% แต่ช่วยลดความเสี่ยงและความเสียหายเมื่อเกิดปัญหา

---
