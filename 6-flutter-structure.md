# Flutter

## โครงสร้าง Folder ของ Flutter

หลังจากการสร้าง Project ของ Flutter ใหม่ Flutter จะทำการสร้างโครงสร้างไฟล์เหล่านี้ให้เราอย่างอัตโนมัติ:

```
flutter_app/
├── android/
├── ios/
├── build/
├── lib/
│   ├── main.dart
│   ├── screens/
│   │   ├── home_screen.dart
│   │   └── detail_screen.dart
│   ├── widgets/
│   │   ├── custom_button.dart
│   │   └── custom_text.dart
│   ├── models/
│   │   └── user.dart
│   ├── services/
│   │   └── api_service.dart
│   ├── utils/
│   │   ├── constants.dart
│   │   └── helpers.dart
│   └── emoji/
│       └── emoji_list.dart
├── linux/
├── macos/
├── test/
├── web/
├── windows/
├── .gitignore
├── .metadata
├── analysis_options.yaml
├── assets/
│   ├── images/
│   └── fonts/
├── pubspec.yaml
└── README.md
```

1. `android/` และ `ios/`: โฟลเดอร์สำหรับไฟล์เฉพาะของ Android และ iOS เมื่อต้องการสร้าง native code หรือกำหนดค่าเฉพาะแพลตฟอร์ม

2. `build/`: โฟลเดอร์ที่เก็บไฟล์ build ของแอปพลิเคชัน เมื่อทำการคอมไพล์และสร้างแอปพลิเคชัน

3. `lib/`: โฟลเดอร์หลักที่เก็บโค้ด Dart ทั้งหมดสำหรับแอป Flutter

   - `main.dart`: จุดเริ่มต้นของแอปพลิเคชัน กำหนด Root Widget และเรียกหน้าจอหลัก
   - `screens/`: เก็บไฟล์ต่างๆ ที่แสดง UI ของแต่ละหน้าจอในแอป เช่น HomeScreen, DetailScreen
   - `widgets/`: เก็บวิดเจ็ตที่ใช้ซ้ำในแอป เช่น ปุ่ม, ข้อความ เพื่อให้ใช้งานได้สะดวกมากขึ้น
   - `models/`: เก็บคลาสโมเดลต่างๆ ที่ใช้ในแอป เช่น User model
   - `services/`: เก็บไฟล์ที่เกี่ยวข้องกับเซอร์วิส เช่น การเรียก API
   - `utils/`: เก็บไฟล์ helpers หรือ constants ที่ใช้ทั่วแอป
   - `emoji/`: โฟลเดอร์ที่เก็บไฟล์ที่เกี่ยวข้องกับการจัดการ Emoji ในแอปพลิเคชัน

4. `linux/`, `macos/`, `windows/` และ `web/`: โฟลเดอร์สำหรับแพลตฟอร์มอื่นๆ ที่ Flutter รองรับ เช่น Linux, macOS, Windows และ Web

5. `test/`: โฟลเดอร์สำหรับเขียน unit tests, widget tests และ integration tests

6. `.gitignore`: ไฟล์ที่ระบุว่าไฟล์หรือโฟลเดอร์ใดที่ไม่ต้องการให้ Git ติดตาม

7. `.metadata`: ไฟล์เมตาดาต้าของโปรเจ็กต์ที่ Flutter ใช้ในการติดตามข้อมูลบางอย่าง

8. `analysis_options.yaml`: ไฟล์กำหนดค่าสำหรับการวิเคราะห์โค้ด Dart เช่น กฎในการตรวจสอบโค้ด, ระดับความรุนแรงของ Linter เป็นต้น

9. `assets/`: โฟลเดอร์เก็บไฟล์แอสเซท เช่น รูปภาพ, ไอคอน, ฟอนต์ ที่ใช้ในแอป

   - `images/`: โฟลเดอร์สำหรับเก็บไฟล์รูปภาพ
   - `fonts/`: โฟลเดอร์สำหรับเก็บไฟล์ฟอนต์

10. `pubspec.yaml`: ไฟล์กำหนดการตั้งค่าของโปรเจ็กต์ Flutter เช่น ชื่อ, เวอร์ชัน, ไลบรารี่ที่ใช้, assets ต่างๆ เช่น fonts, images เป็นต้น

11. `README.md`: ไฟล์สำหรับใส่คำอธิบายหรือเอกสารประกอบโปรเจ็กต์
