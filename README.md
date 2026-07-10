# Fri8nd

Local-first AI agent ที่ช่วยจัดระเบียบไฟล์ในเครื่องอัตโนมัติ — ตั้งชื่อไฟล์ใหม่ จัดหมวดหมู่ และย้ายไฟล์ให้ โดยไม่ต้องอัปโหลดข้อมูลขึ้น cloud

> สถานะ: **Concept / Early Development** — เริ่มจาก Version 1 (file organizer) ก่อน

---

## แนวคิด

โฟลเดอร์ Downloads ในเครื่องส่วนใหญ่มักรกไปด้วยไฟล์ที่ตั้งชื่อไม่สื่อความหมายและไม่ได้จัดหมวดหมู่ Johny AI เฝ้าดูโฟลเดอร์ที่กำหนด วิเคราะห์ไฟล์ใหม่ที่เข้ามา แล้วช่วยแนะนำชื่อไฟล์และตำแหน่งจัดเก็บที่เหมาะสม โดยผู้ใช้เป็นคนตัดสินใจสุดท้ายว่าจะยอมรับหรือไม่ (ไม่ auto-apply โดยไม่ถาม)

## Philosophy

- **Local First** — ข้อมูลอยู่ในเครื่องผู้ใช้ ไม่บังคับใช้ cloud
- **Privacy First** — ไม่ส่งข้อมูลออกไปโดยไม่จำเป็น
- **AI Assisted** — AI ช่วยแนะนำ ไม่ใช่ตัดสินใจแทนทั้งหมด
- **Human Controlled** — ผู้ใช้ confirm การเปลี่ยนแปลงสำคัญเสมอ

## Scope ปัจจุบัน (v1)

- เฝ้าดูโฟลเดอร์ที่กำหนด (เริ่มจาก Downloads)
- ตรวจจับไฟล์ใหม่ / ไฟล์ซ้ำ
- แนะนำชื่อไฟล์ใหม่และหมวดหมู่ด้วย AI (BYOK: Gemini / OpenAI / Claude)
- สร้างโฟลเดอร์และย้ายไฟล์อัตโนมัติ (หลัง confirm)

ดูรายละเอียด task/phase ทั้งหมดได้ที่ [`johny-ai-v1-plan.md`](./johny-ai-v1-plan.md)

## Tech Stack

- Desktop shell: Electron หรือ Tauri
- Background agent: Node.js
- Database: SQLite
- AI: BYOK (Bring Your Own API Key)

## Not in Scope (v1)

OCR, Obsidian export, natural language search, knowledge graph — วางแผนไว้ใน phase ถัดๆ ไป

## License

TBD