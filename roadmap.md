

# fri8nd— Version 1 Development Plan

Scope: **Local file organizer agent only** (ตาม Roadmap v1 ในเอกสาร Product Plan — ไม่แตะ OCR/Gemini/Knowledge Engine ในเฟสนี้)

Goal: เฝ้าโฟลเดอร์ที่กำหนด (เริ่มจาก `Downloads`) แล้วให้ AI ช่วยตั้งชื่อไฟล์ใหม่ สร้างโฟลเดอร์ และย้ายไฟล์อัตโนมัติ

---

## Phase 0 — Foundation & Setup

- [ ] ตัดสินใจ desktop shell: Electron vs Tauri (Tauri เบากว่า, resource ต่ำกว่า, เหมาะกับ background agent ที่ต้องรันตลอดเวลา — แนะนำเริ่มจาก Tauri ถ้าไม่ติดปัญหาเรื่อง native module)
- [ ] Scaffold โปรเจกต์: desktop shell + Node.js background process
- [ ] ตั้งค่า SQLite เป็น local database (เก็บ file index, log การจัดการไฟล์)
- [ ] ตั้งค่า auto-start เมื่อเปิดเครื่อง (login item / background service)
- [ ] Repo structure เบื้องต้น (`/agent`, `/app`, `/db`, `/docs`)

---

## Phase 1 — File Watcher

- [ ] เลือก library เฝ้าดูโฟลเดอร์ (เช่น `chokidar` สำหรับ Node.js)
- [ ] Watch โฟลเดอร์ `Downloads` เป็นจุดเริ่มต้น (hardcode ก่อน, ทำ config ทีหลัง)
- [ ] Detect event: ไฟล์ใหม่ถูกสร้าง / ไฟล์ถูกแก้ไข
- [ ] Debounce การอ่านไฟล์ (กันเคสไฟล์ยัง download ไม่เสร็จ)
- [ ] Log ไฟล์ที่ตรวจพบลง SQLite (path, ชื่อเดิม, timestamp, สถานะ)

---

## Phase 2 — File Analysis (Basic, ไม่ใช้ AI ก่อน)

- [ ] อ่าน file metadata พื้นฐาน: นามสกุลไฟล์, ขนาด, วันที่สร้าง
- [ ] ตรวจจับไฟล์ซ้ำ (hash-based, เช่น SHA-256) เป็น rule-based ก่อน ยังไม่ต้องใช้ AI
- [ ] จัดกลุ่มไฟล์เบื้องต้นตามนามสกุล (image / document / archive / installer ฯลฯ)

---

## Phase 3 — AI-Assisted Naming & Categorization

- [ ] เชื่อม AI API (BYOK: Gemini / OpenAI / Claude ตาม key ที่ผู้ใช้ใส่)
- [ ] Prompt design: ส่งชื่อไฟล์เดิม + metadata (+ เนื้อหาบางส่วนถ้าเป็น text/PDF) → ให้ AI แนะนำชื่อใหม่ + หมวดหมู่
- [ ] Rule engine: ผู้ใช้กำหนด mapping เอง ได้ (เช่น .pdf ใบเสร็จ → โฟลเดอร์ Receipts)
- [ ] AI แนะนำ แต่ยังไม่ auto-apply — ให้ผู้ใช้ confirm ก่อนในเฟสนี้ (Human Controlled ตาม philosophy)

---

## Phase 4 — Auto Organize

- [ ] สร้างโฟลเดอร์ใหม่อัตโนมัติตามหมวดหมู่ที่ AI แนะนำ (หลังผ่านการ confirm)
- [ ] ย้ายไฟล์ + rename ตาม pattern ที่ตั้งไว้
- [ ] เก็บ undo log (ย้อนกลับได้ถ้าจัดผิด)
- [ ] Setting: เปิด/ปิด auto-apply โดยไม่ต้อง confirm ทีละไฟล์ (สำหรับ user ที่มั่นใจ)

---

## Phase 5 — Minimal Desktop UI

- [ ] Dashboard พื้นฐาน: แสดง log ไฟล์ที่ถูกจัดการล่าสุด
- [ ] หน้า Settings: เลือกโฟลเดอร์ที่ต้องการเฝ้าดู, ใส่ API Key (BYOK), เปิด/ปิด auto-apply
- [ ] ปุ่ม pause/resume agent

---

## Not in Scope (v1) — เก็บไว้ future phase

- OCR / อ่านเนื้อหาเอกสารเชิงลึก
- Export เข้า Obsidian
- Natural language search
- Knowledge Graph
- Multi-device sync

---

## Reference

- ต่อยอด prompt/logic จาก [MDflow](https://github.com/sjsiwat/MDflow) เมื่อถึง phase OCR/Knowledge Engine ในอนาคต (ไม่ต้องออกแบบ prompt ใหม่จากศูนย์)