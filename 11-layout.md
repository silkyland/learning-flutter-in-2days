# Layout

การวาง Layout ใน Flutter คือการจัดวางองค์ประกอบต่างๆ ของ UI เช่น Widgets ลงบนหน้าจอแอปพลิเคชัน Flutter ใช้ระบบ Layout ที่ยืดหยุ่นและมีประสิทธิภาพในการสร้าง UI ที่สวยงามและรองรับขนาดหน้าจอที่หลากหลาย

เราทราบว่า Everything is a Widget - ใน Flutter ทุกอย่างคือ Widget ตั้งแต่ปุ่ม ข้อความ รูปภาพ หรือแม้แต่ไอคอน หรือ แม้แต่ widget ที่เรามองไม่เห็นเช่น rows, columns, flex, grid, และอื่นๆ ก็ล้วนแต่เป็น Widget ทั้งนั้น

เราสามารถสร้าง Layout ได้โดยการประกอบ Widget เข้าด้วยกันเพื่อสร้าง Widget ที่ซับซ้อนยิ่งขึ้น ยกตัวอย่างเช่น ภาพหน้าจอแรกด้านล่างนี้แสดง ไอคอน 3 อันที่มีป้ายกำกับอยู่ใต้แต่ละไอคอน:

![layout](https://docs.flutter.dev/assets/images/docs/ui/layout/lakes-icons.png)
![layout](https://docs.flutter.dev/assets/images/docs/ui/layout/lakes-icons-visual.png)

ภาพหน้าจอที่สองแสดงการจัดวางแบบ Visual โดยแสดง Row (แถว) ที่ประกอบด้วย 3 Column (คอลัมน์) ซึ่งแต่ละคอลัมน์มีไอคอนและป้ายกำกับ (Label)

ต่อไปนี้คือการแสดงผล Diagram ของ Widget Tree ในการจัดวาง Layout จาก widget ด้านบน

<div style="background:white; width: 600px; padding: 5px;">

![alt text](https://docs.flutter.dev/assets/images/docs/ui/layout/sample-flutter-layout.png)

</div>
