# Raiwa เช็คชื่อแก๊ง

เว็บเช็คชื่อ Airdrop, Mini Supply และงัดร้านของแก๊ง Raiwa พร้อมบันทึกของที่ได้, แต้มสะสม, เบิกกล่อง, ประวัติสมาชิก และปุ่มส่งข้อความไป Discord

- เป็นเว็บไฟล์เดียว (`index.html`) ไม่ต้อง build
- เก็บข้อมูลใน **Firebase Firestore** (แผนฟรี) ทุกคนเห็นข้อมูลชุดเดียวกันแบบเรียลไทม์
- เข้าใช้ด้วย **รหัสแก๊ง** คนที่รู้รหัสเท่านั้นถึงเห็นและแก้ข้อมูลได้

## ไฟล์ในโปรเจกต์

| ไฟล์ | ใช้ทำอะไร |
|---|---|
| `index.html` | หน้าเว็บทั้งหมด |
| `firebase-config.js` | ค่าเชื่อมต่อ Firebase ของแก๊ง (ต้องแก้ครั้งแรก) |
| `firestore.rules` | กฎความปลอดภัยของฐานข้อมูล (คัดลอกไปวางใน Firebase) |
| `netlify.toml` | ตั้งค่า Netlify |
| `logo.png` | โลโก้แก๊ง |

## ขั้นที่ 1: สร้าง Firebase (ครั้งเดียว)

1. เข้า <https://console.firebase.google.com> ล็อกอินด้วย Gmail
2. กด **Create a project** ตั้งชื่อ เช่น `raiwa-checkin` (ปิด Google Analytics ได้)
3. เมนูซ้าย **Build → Firestore Database → Create database**
   - Location: เลือก `asia-southeast1 (Singapore)`
   - เลือก **Start in production mode**
4. ไปแท็บ **Rules** ลบของเดิม แล้ววางเนื้อหาจากไฟล์ `firestore.rules` กด **Publish**
5. กดรูปเฟือง **Project settings** → เลื่อนลงไป **Your apps** → กดไอคอน `</>` (Web) ตั้งชื่อแอป แล้วกด Register
6. จะได้ค่า `firebaseConfig = { apiKey: ..., ... }` คัดลอกค่าทั้งหมดไปใส่ในไฟล์ `firebase-config.js`

> ค่าใน `firebase-config.js` เปิดเผยได้ ไม่ใช่รหัสลับ

## ขั้นที่ 2: ตั้งรหัสแก๊ง

ไม่ต้องตั้งในระบบ แค่คิดรหัสขึ้นมาเอง เป็นตัวอังกฤษหรือตัวเลข อย่างน้อย 6 ตัว (แนะนำ 10 ตัวขึ้นไป เช่น `Raiwa7Blue2026`)

- ทุกคนในแก๊งใส่รหัสเดียวกันตอนเปิดเว็บครั้งแรก เครื่องจะจำไว้
- รหัสที่ต่างกันจะเห็นข้อมูลคนละชุด ห้ามพิมพ์ผิด
- อย่าโพสต์รหัสในที่สาธารณะ ส่งในห้อง Discord ส่วนตัวของแก๊งเท่านั้น

## ขั้นที่ 3: ขึ้น Netlify

1. เข้า <https://app.netlify.com> → **Sign up with GitHub**
2. **Add new site → Import an existing project → GitHub** แล้วเลือก repo นี้
3. Build command: เว้นว่าง / Publish directory: `.` แล้วกด **Deploy**
4. ได้ลิงก์ เช่น `https://xxxx.netlify.app` (เปลี่ยนชื่อได้ที่ **Site configuration → Change site name**)

ต่อจากนี้ ทุกครั้งที่แก้ไฟล์ใน GitHub, Netlify จะอัปเดตเว็บให้อัตโนมัติ

## แก้รายชื่อสมาชิก / เวลา / ร้าน

อยู่ด้านบนของ `<script>` ใน `index.html`

- `MEMBERS` รายชื่อสมาชิก (ลำดับคือ #1, #2, …) **เพิ่มชื่อต่อท้ายได้ แต่อย่าสลับลำดับหรือลบกลางรายการ** เพราะข้อมูลเก่าผูกกับลำดับ
- `AIR` เวลา Airdrop
- `MINI` เวลา Mini Supply
- `SHOPS` รายชื่อร้านและสี

## โควตาฟรีของ Firebase

แผนฟรี (Spark) อ่านได้ 50,000 ครั้ง/วัน เขียนได้ 20,000 ครั้ง/วัน เกินพอสำหรับแก๊ง 15 คน
