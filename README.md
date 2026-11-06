# ระบบขอเวชระเบียน (Medical Records Requests)

ลูกค้าสแกน QR ของสาขา → กรอกใบคำร้องและเซ็นชื่อบนมือถือ → เจ้าหน้าที่ติดตามงานจนส่งมอบ → พิมพ์ใบคำร้อง A4 เก็บเข้าแฟ้ม
โครงสร้างเดียวกับระบบแจ้งเหตุและระบบความคิดเห็น: GitHub Pages + Google Apps Script + Google Sheets

| ไฟล์ | ใช้ทำอะไร |
|---|---|
| `Code.gs` | โค้ดฝั่งเซิร์ฟเวอร์ วางใน Apps Script ของชีต Medical Records Requests |
| `index.html` | หน้าลูกค้า (เปิดจาก QR `?b=MA` / `?b=K3` / `?b=K4`) |
| `admin.html` | หน้าเจ้าหน้าที่ |
| `config.js` | ใส่ลิงก์เว็บแอป Apps Script (ลงท้าย /exec) |
| `manifest.webmanifest`, `*.png` | ไอคอน และติดตั้งเป็นแอปบนมือถือ |

## ติดตั้ง
1. เปิดชีต **Medical Records Requests** → ส่วนขยาย → Apps Script → ลบโค้ดเดิม วาง `Code.gs` ทั้งไฟล์ → บันทึก
2. เลือกฟังก์ชัน `setup` → เรียกใช้ → อนุญาตสิทธิ์
3. การทำให้ใช้งานได้ → รายการใหม่ → เว็บแอป · เรียกใช้ในฐานะ **ฉัน** · ผู้มีสิทธิ์เข้าถึง **ทุกคน** → คัดลอกลิงก์ /exec
4. GitHub สร้าง repo `records` (Public) → อัปโหลดไฟล์ทั้งหมดในโฟลเดอร์นี้ → Settings → Pages → Branch main → Save
5. แก้ `config.js` ใน GitHub ให้เป็น `window.APP_API_URL = "ลิงก์ /exec";`
6. เปิด `https://larepong-create.github.io/records/admin.html` เข้าระบบ `admin` / `admin1234` แล้วเปลี่ยนรหัสผ่านทันที

## LINE (บอท Muang Ake Records)
1. หน้าตั้งค่า → วาง Channel access token → บันทึก
2. LINE Developers → channel Muang Ake Records → Messaging API → Webhook URL = ลิงก์ /exec → Update → เปิด Use webhook
3. เชิญบอทเข้ากลุ่มที่ต้องการรับแจ้งเตือน ระบบจะบันทึกกลุ่มให้อัตโนมัติ (หรือพิมพ์ `ตั้งกลุ่มเวชระเบียน` ในกลุ่ม)
4. กด "ส่งข้อความทดสอบ"

## บทบาทผู้ใช้
- ผู้ดูแลระบบ: ทุกอย่าง รวมถึงตั้งค่าและผู้ใช้
- เวชระเบียน / ผู้บริหาร: เห็นและดำเนินการทุกสาขา
- เจ้าหน้าที่สาขา: เห็นคำขอของสาขาตัวเอง และคำขอที่ลูกค้าจะมารับที่สาขาตัวเอง

ข้อมูลอยู่ในชีต `MR_Requests` (1 แถว = 1 คำขอ) · ผู้ใช้ `MR_Users` · การตั้งค่า `MR_Settings`
