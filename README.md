# แอป Android — ระบบบริหารจัดการโรงเรียน

แอปนี้เปิดระบบบริหารจัดการโรงเรียน (Cloudflare Pages) แบบเต็มจอด้วย **Trusted Web Activity** ของ Google
เมื่อแก้ระบบบนเว็บ แอปได้ของใหม่ทันที ไม่ต้องสร้างแอปใหม่

## ดาวน์โหลดแอป
ไปที่แท็บ **Releases** (ด้านขวาของหน้านี้) → เลือกเวอร์ชันล่าสุด → ดาวน์โหลด `school-app-x.y.apk`
ส่งไฟล์ให้บุคลากรทาง LINE / Google Drive → เปิดบนมือถือ → อนุญาต "ติดตั้งแอปที่ไม่รู้จัก" → ติดตั้ง

ไฟล์ `.aab` ใช้อัปโหลดขึ้น Google Play Console

## เปลี่ยนลิงก์ ชื่อแอป หรือสี
แก้ไฟล์ [`app.properties`](app.properties) บนหน้าเว็บ GitHub (ปุ่มดินสอ) → Commit changes
GitHub Actions จะสร้างแอปเวอร์ชันใหม่ให้อัตโนมัติภายในประมาณ 5 นาที (ดูความคืบหน้าที่แท็บ **Actions**)

| ค่า | ความหมาย |
| --- | --- |
| `siteUrl` | ลิงก์ระบบของโรงเรียน (https) |
| `packageId` | ชื่อแพ็กเกจของแอป — **ห้ามเปลี่ยนหลังแจกแอปแล้ว** |
| `appName` / `launcherName` | ชื่อแอป / ชื่อใต้ไอคอน |
| `themeColor` / `backgroundColor` | สีแถบด้านบน / สีหน้าเปิดแอป |

## ให้แอปเปิดเต็มจอ (ไม่มีแถบที่อยู่เว็บ)
เข้าระบบด้วยผู้ดูแลระบบ → **ตั้งค่าระบบ → แอป Android** → กรอก Package ID และ SHA-256
(ค่าทั้งสองแสดงในหน้าสรุปของงาน build ล่าสุดในแท็บ Actions และในหน้า Release)

ถ้าส่งขึ้น Google Play: คัดลอก SHA-256 ของ "App signing key certificate" จาก Play Console → App integrity
แล้วเพิ่มเป็นบรรทัดที่ 2 ในช่อง SHA-256

## กุญแจเซ็นแอป
กุญแจเก็บใน **Settings → Secrets and variables → Actions** ของ repository นี้
(`ANDROID_KEYSTORE_BASE64`, `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS`, `ANDROID_KEY_PASSWORD`)
ห้ามลบ — ถ้าเปลี่ยนกุญแจ มือถือที่ติดตั้งแอปไว้แล้วจะอัปเดตไม่ได้ และต้องแก้ SHA-256 ในระบบ
