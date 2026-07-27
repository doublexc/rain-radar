จัดให้ครับ! นี่คือโครงสร้างไฟล์ `README.md` แบบครบถ้วน ชัดเจน พร้อมระบุรายละเอียดฟีเจอร์ หลักการทำงาน และเทคนิคการรับมือกับข้อมูลเรดาร์ สามารถก๊อปปี้ไปวางใน Repository บน GitHub ได้เลยครับ

---

```markdown
# 🌧️ ฝนมาหรือยัง? (Is Rain Coming?)

เว็บแอปพลิเคชันประเมินโอกาสและเวลาที่ฝนจะตกถึงตำแหน่งของคุณแบบเรียลไทม์ โดยประมวลผลจากภาพเรดาร์ตรวจจับฝนแอนิเมชัน (GIF) ของกรมอุตุนิยมวิทยา / กทม. ออกแบบมาให้รันเป็น **Static Web (GitHub Pages)** ได้ 100% โดยไม่ต้องเปิดเซิร์ฟเวอร์ Backend

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

---

## ✨ จุดเด่นของแอปพลิเคชัน (Features)

* 📱 **Mobile-First UX/UI:** ออกแบบเพื่อการใช้งานบนมือถือเป็นหลัก ทำงานแบบ Step-by-Step Wizard (6 ขั้นตอน) เข้าใจง่าย ไม่ซับซ้อน
* 📡 **Real-time Radar Fetcher:** ดึงภาพเรดาร์ล่าสุดจากกรมอุตุนิยมวิทยาอัตโนมัติ พร้อมระบบ **Auto-Fallback** (สลับสถานีหนองแขม ↔ หนองจอก อัตโนมัติเมื่อสถานีใดสถานีหนึ่งปิดปรับปรุง)
* 🛡️ **Network Resiliency:** มีระบบ Proxy Fallback และปุ่มอัปโหลดไฟล์ GIF จากเครื่องสำรองไว้ หากเซิร์ฟเวอร์หลักมีปัญหา
* 🎨 **Interactive Canvas Overlay:** ใช้เทคนิคซ้อน Layer `<canvas>` แบบโปร่งใสทับภาพ GIF แอนิเมชัน ทำให้วาดเวกเตอร์และมาร์กเกอร์ทับภาพเคลื่อนไหวได้ไหลลื่น
* 🧮 **Vector Math Calculation:** ประมวลผลความเร็วเคลื่อนตัวของฝน ($px/min$) และคำนวณทิศทางเทียบกับตำแหน่งผู้ใช้ด้วย **Dot Product Alignment** ร่วมกับ Heuristic Scoring Model

---

## 🛠️ ขั้นตอนการประเมิน (Workflow)

1. **โหลดภาพเรดาร์:** ดึงภาพ GIF เคลื่อนไหวล่าสุด (11 เฟรม ย้อนหลังประมาณ 50 นาที)
2. **ระบุจุดผู้ใช้ (📍):** แตะบนแผนที่เพื่อปักหมุดตำแหน่งของคุณ
3. **ระบุทิศทางฝน (↗️):** ลากลูกศรบนภาพเพื่อระบุทิศทางกลุ่มเมฆฝน
4. **ติดตามตำแหน่งฝน (A → B):** แตะจุดฝนในเฟรมเก่า (จุด A) และเฟรมปัจจุบัน (จุด B) เพื่อหาความเร็วเคลื่อนตัว
5. **ระบุความแรง:** เลือกสีหลักของกลุ่มฝน (เขียว = เบา, เหลือง = ปานกลาง, แดง = หนัก)
6. **แสดงผลลัพธ์:** ประมวลผลเปรียบเทียบออกมาเป็น **% โอกาสที่ฝนจะตกถึงคุณ** และ **เวลาคาดการณ์ (นาที)**

---

## 🏗️ แหล่งข้อมูลภาพเรดาร์ (Radar Sources & Fallback)

ระบบจะพยายามดึงข้อมูลเรียลไทม์เรียงตามลำดับความสดใหม่ดังนี้:

1. **กรมอุตุนิยมวิทยา (สถานีหนองแขม):** `pic_bmankLoop.gif` *(หลัก)*
2. **กรมอุตุนิยมวิทยา (สถานีหนองจอก):** `pic_bmanjLoop.gif` *(สำรอง 1)*
3. **สำนักการระบายน้ำ กทม.:** `nkradar.gif` *(สำรอง 2)*
4. **Local File Upload:** ปุ่มอัปโหลดไฟล์ GIF จากเครื่องผู้ใช้ *(กรณีเซิร์ฟเวอร์ภายนอกล่มทั้งหมด)*

---

## 🚀 วิธีนำไปใช้งาน (Deployment)

เนื่องจากโปรเจกต์นี้เป็น Vanilla HTML/CSS/JavaScript เพียงไฟล์เดียว ไม่ต้องมีขั้นตอน Build Process:

1. **Clone Repository:**
   ```bash
   git clone [https://github.com/YOUR_USERNAME/rain-radar.git](https://github.com/YOUR_USERNAME/rain-radar.git)
   cd rain-radar

```

2. **เปิดใช้งานบน Local:**
เปิดไฟล์ `index.html` ผ่าน Web Browser ได้ทันที
3. **Deploy ขึ้น GitHub Pages:**
* ไปที่ Repository **Settings** > **Pages**
* เลือก Source เป็น `main` branch / `root` folder
* กด **Save** ระบบจะสร้าง URL เว็บพร้อมใช้งานให้อัตโนมัติ



---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

```

```
