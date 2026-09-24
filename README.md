# 📐 Maths Helper (`mth` & `slv`)

เครื่องมือคำนวณและแก้สมการสไตล์ Excel & วิศวกรรม ติดตั้งง่ายในบรรทัดเดียว ไม่ต้องพึ่งพาระบบหรือเซิร์ฟเวอร์ใดๆ (Standalone 100%)

---

## ⚡ ติดตั้งง่ายใน 1 บรรทัด (One-Liner Install)

### 🪟 สำหรับผู้ใช้ Windows (PowerShell)
เปิด **PowerShell** หรือ **Windows Terminal** แล้วคัดลอกคำสั่งนี้ไปวาง:

```powershell
irm https://raw.githubusercontent.com/joece035/maths-helper/main/install.ps1 | iex
```

---

### 🐧 🍎 สำหรับ Linux / macOS / WSL / Git Bash / Termux (Bash/Zsh)
เปิด **Terminal** แล้วคัดลอกคำสั่งนี้ไปวาง:

```bash
curl -fsSL https://raw.githubusercontent.com/joece035/maths-helper/main/install.sh | bash
```

> **หมายเหตุ:** ติดตั้งเสร็จแล้ว สามารถพิมพ์ `mth` หรือ `slv` ใช้งานได้ทันทีในหน้าต่าง Terminal ถัดไป!

---

## 🎯 ฟังก์ชันหลัก

### 1. `mth` — เครื่องคิดเลขสไตล์ Excel (Human-friendly)
*(มีชื่อเรียกแทน: `calc`, `math`)*

รองรับสูตรแบบ Excel ทั้งหมด ไม่ต้องพิมพ์ไวยากรณ์คอมพิวเตอร์ให้ปวดหัว:

| รูปแบบการใช้งาน | ตัวอย่างคำสั่ง | ผลลัพธ์ | คำอธิบาย |
| :--- | :--- | :--- | :--- |
| **คำนวณทั่วไป** | `mth 10/3` | `3.33` | ทศนิยม 2 ตำแหน่ง (default) |
| **พีทาโกรัส / รากที่สอง** | `mth "sqrt(3^2 + 4^2)"` | `5.00` | รองรับ `^` หรือ `**` |
| **ฟังก์ชัน Excel SUM** | `mth "SUM(10, 20, 30)"` | `60` | ใส่คอมม่าเหมือน Excel |
| **ฟังก์ชัน Excel AVG** | `mth "AVG(10, 20, 30)"` | `20.00` | หาค่าเฉลี่ย |
| **น้ำหนักเหล็กเส้น (ตัวอย่างโยธา)** | `mth "pi() * (0.016/2)^2 * 7850"` | `1.58` | กก./เมตร สำหรับเหล็ก DB16 |
| **กำหนดทศนิยม & ปัดเศษ** | `mth 10/3 4` | `3.3333` | ปัดตามหลักคณิตศาสตร์ 4 ตำแหน่ง |
| **ปัดขึ้น (ROUNDUP)** | `mth 10/3 0 u` | `4` | `u` = roundup (ปัดขึ้นเสมอ) |
| **ปัดลง (ROUNDDOWN)** | `mth 10/3 0 d` | `3` | `d` = rounddown (ปัดลงเสมอ) |
| **เงื่อนไข IF** | `mth 'if(100 > 50, "PASS", "FAIL")'` | `PASS` | Excel IF condition |

---

### 2. `slv` — โปรแกรมแก้สมการพีชคณิต (Algebraic Solver)
*(มีชื่อเรียกแทน: `solve`)*

แก้สมการหาค่าตัวแปรได้ทั้งแบบติดตัวแปร (Symbolic) และแบบใส่ค่าตัวเลข (Numeric):

```bash
# สมการเชิงเส้นตัวแปรเดียว
slv "2x + 10 = 30"
# ผลลัพธ์: x = 10

# สมการ 2 ตัวแปร โดยกำหนดค่าตัวแปรหนึ่ง
slv "x = 2x + y" "y = 2"
# ผลลัพธ์: x = -2,  y = 2

# ตรีโกณมิติแบบองศา (Degree mode: --deg หรือ -d)
slv --deg "h = a * sin(b)" "a = 10" "b = 30"
# ผลลัพธ์: h = 5,  a = 10,  b = 30   (เพราะ sin(30°) = 0.5)

# ตัวอย่างงานวิศวกรรม: หา Reaction คานช่วงเดี่ยว (Ra + Rb = W)
slv "Ra + Rb = 100" "Ra = 40"
# ผลลัพธ์: Rb = 60,  Ra = 40

# ปิทาโกรัสหาด้านตรงข้ามมุมฉาก c
slv "a^2 + b^2 = c^2" "a = 3" "b = 4"
# ผลลัพธ์: c = 5,  a = 3,  b = 4  (เลือกคำตอบบวกให้อัตโนมัติ)
```

---

## 🛠️ ความต้องการของระบบ (Requirements)

- **`mth`**:
  - บน Linux/macOS/WSL/Git Bash: ใช้เพียง `awk` และ `bash` (มีติดมากับทุกระบบอยู่แล้ว ไม่ต้องลงอะไรเพิ่ม)
  - บน Windows PowerShell: รองรับการทำงานร่วมกับ Python 3 (หรือรันสูตรเลขพื้นฐานได้ทันที)
- **`slv`**:
  - ต้องการ **Python 3** และไลบรารี `sympy` (สคริปต์ตัวติดตั้งจะตรวจเช็คและติดตั้งให้แบบอัตโนมัติ)

---

## 🗑️ วิธีการถอนการติดตั้ง (Uninstall)

- **Linux / macOS / WSL / Git Bash**:
  ```bash
  rm -rf ~/.maths-helper ~/.local/bin/mth ~/.local/bin/slv ~/.local/bin/calc ~/.local/bin/solve
  ```
  *(จากนั้นลบบรรทัด `maths-helper` ใน `~/.bashrc` หรือ `~/.zshrc` ออก)*

- **Windows PowerShell**:
  ```powershell
  Remove-Item -Recurse -Force "$HOME\.maths-helper"
  ```
  *(จากนั้นเปิด `$PROFILE` ลบบรรทัด `maths-helper` ออก)*

---

## 📄 License
MIT License © 2026 joece035
