---
description: วิธีอัปโหลด MkDocs Documentation ขึ้น GitHub และ Deploy GitHub Pages
---

# วิธีอัปโหลด MkDocs ขึ้น GitHub

## ขั้นตอนที่ 1: เตรียม Git Repository

```bash
cd /media/devg/Micro-SV7/GitHub/GhostMicro/micro-electronic

# ตรวจสอบสถานะ
git status

# เพิ่มไฟล์ทั้งหมด
git add .

# Commit
git commit -m "Add comprehensive electronics documentation"
```

## ขั้นตอนที่ 2: Push ขึ้น GitHub

```bash
# ถ้ายังไม่มี remote
git remote add origin https://github.com/YOUR_USERNAME/micro-electronic.git

# Push
git push -u origin main
```

## ขั้นตอนที่ 3: ติดตั้ง GitHub Actions สำหรับ Auto Deploy

สร้างไฟล์ `.github/workflows/deploy-docs.yml`:

```yaml
name: Deploy MkDocs to GitHub Pages

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.x
      
      - name: Install dependencies
        run: |
          pip install mkdocs-material
      
      - name: Deploy to GitHub Pages
        run: mkdocs gh-deploy --force
```

## ขั้นตอนที่ 4: เปิดใช้งาน GitHub Pages

1. ไปที่ GitHub Repository
2. Settings → Pages
3. Source: เลือก `gh-pages` branch
4. Save

## ขั้นตอนที่ 5: ตรวจสอบ

เว็บไซต์จะอยู่ที่:
```
https://YOUR_USERNAME.github.io/micro-electronic/
```

---

## คำสั่งที่ใช้บ่อย

### อัปเดตเอกสาร
```bash
# แก้ไขไฟล์ใน docs/
git add .
git commit -m "Update documentation"
git push
```

### ทดสอบ Local
```bash
mkdocs serve
# เปิด http://localhost:8000
```

### Build Manual
```bash
mkdocs build
# ไฟล์จะอยู่ใน site/
```

---

## Troubleshooting

### ถ้า GitHub Actions ไม่ทำงาน
1. ตรวจสอบ Permissions ใน Settings → Actions → General
2. เปิด "Read and write permissions"

### ถ้าหน้าเว็บไม่แสดง
1. ตรวจสอบ branch `gh-pages` ว่ามีไฟล์
2. รอ 2-3 นาที (GitHub ต้องใช้เวลา deploy)

---

> [!TIP]
> **คำแนะนำ:** ใช้ GitHub Actions จะทำให้ทุกครั้งที่ push ขึ้น GitHub เว็บไซต์จะอัปเดตอัตโนมัติ
