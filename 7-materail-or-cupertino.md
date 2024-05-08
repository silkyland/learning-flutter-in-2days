## Materail Design Or Cupertino Design

![Mategrail or Cupertino](/assets//images/7/materail_or_cupertino.png)

เมื่อพูดถึงการพัฒนาแอปพลิเคชันด้วย Flutter เรามีตัวเลือกหลักๆ 2 แบบในการออกแบบ UI คือการใช้ MaterialApp หรือ CupertinoApp มาดูความแตกต่างที่สำคัญระหว่างทั้งสองตัวนี้กัน

#### MaterialApp:

- เป็น widget ของ Flutter ที่ใช้สำหรับสร้าง UI ตามแนวทางการออกแบบ Material Design ของ Google
- เหมาะสำหรับแอป Android เพราะมีลักษณะเหมือนกับ native Android apps
- มี widget พื้นฐานต่างๆ เช่น AppBar, Drawer, BottomNavigationBar, FloatingActionButton ให้ใช้งานได้ทันที
- รองรับ theme และ color scheme ที่หลากหลาย ปรับแต่งได้ง่าย
- Navigation ใช้ Navigator 2.0 ที่มีความยืดหยุ่นสูง

#### CupertinoApp:

- เป็น widget สำหรับสร้าง UI ที่มีลักษณะคล้ายกับ native iOS apps ตามแนวทางการออกแบบของ Apple
- เหมาะสำหรับแอป iOS เพราะให้ look and feel เหมือนแอปท้องถิ่นของ iOS
- มี widget ที่จำลองมาจาก UIKit เช่น CupertinoNavigationBar, CupertinoTabBar, CupertinoButton, CupertinoAlertDialog
- รองรับ theme แบบ iOS ที่มีความนุ่มนวล สะอาดตา เรียบง่าย
- Navigation ใช้ CupertinoPageRoute ซึ่งให้ animation แบบ iOS native

สรุปคือ MaterialApp เหมาะสำหรับแอป Android ส่วน CupertinoApp เหมาะกับแอป iOS โดยเฉพาะ อย่างไรก็ตาม Flutter ออกแบบมาให้รองรับการใช้ widget ข้ามแพลตฟอร์มได้ เพื่อความสะดวกในการพัฒนา

เราสามารถเลือกใช้ MaterialApp หรือ CupertinoApp อย่างใดอย่างหนึ่ง หรือผสมผสานทั้งสองแบบในแอปเดียวกันก็ได้ ขึ้นอยู่กับความต้องการและการออกแบบของเรา โดยรวมแล้ว Flutter ให้ความยืดหยุ่นสูงในการสร้าง UI ที่สวยงามและใช้งานได้ดีบนหลากหลายแพลตฟอร์ม

### Materail Design

![Materail Design](/assets//images/7/materail.png)

**Material Design** คือภาษาออกแบบ (design language) ที่พัฒนาโดย Google เพื่อใช้เป็นแนวทางในการออกแบบ UI ของแอปพลิเคชันและเว็บไซต์ โดยเน้นความเรียบง่าย ชัดเจน และสวยงาม ด้วยการจำลองคุณสมบัติของวัสดุในโลกแห่งความเป็นจริง เช่น พื้นผิว แสงเงา การเคลื่อนไหว เป็นต้น

![Materail Design](/assets//images/7/materail_1.png)

ในบริบทของ Flutter, Material Design ถูกนำมาใช้ในรูปแบบของ widgets ต่างๆ ที่ช่วยให้สร้าง UI ได้อย่างรวดเร็วและสอดคล้องกัน บาง widget ที่สำคัญได้แก่:

1. **Scaffold** : เป็น widget หลักที่ใช้จัดวาง layout ของหน้าแอป ประกอบด้วยส่วนต่างๆ เช่น AppBar, body, FloatingActionButton, Drawer เป็นต้น

2. **AppBar**: แถบด้านบนของแอปที่มักใช้แสดงชื่อหน้า ไอคอนต่างๆ หรือเมนูสำคัญ

3. **Drawer**: ช่องเลื่อนด้านข้างของแอปที่ใช้แสดงเมนูหรือตัวเลือกเพิ่มเติม เรียกใช้งานได้จากไอคอนเมนูบน AppBar

4. **BottomNavigationBar**: แถบด้านล่างของแอปที่ใช้สำหรับนำทางระหว่างหน้าหลักๆ ที่ใช้บ่อย

5. **UserAccountDrawerHeader**: ส่วนหัวของ Drawer ที่ใช้แสดงข้อมูลบัญชีผู้ใช้ เช่น ชื่อ รูปโปรไฟล์ อีเมล เป็นต้น

6. **ListTile**: เป็น widget ที่ใช้แสดงข้อมูลแบบรายการ (list item) มักใช้ร่วมกับ ListView โดยมีส่วนประกอบหลักๆ คือ leading (ไอคอนนำหน้า), title (ข้อความหลัก), subtitle (ข้อความรอง) และ trailing (ไอคอนหรือวิดเจ็ตท้ายรายการ)

7. **ListView**: ใช้สร้างรายการข้อมูลที่สามารถเลื่อนได้ (scrollable) โดยรายการแต่ละอันมักสร้างจาก ListTile

โดยรวมแล้ว การใช้ Material Design และ widgets เหล่านี้จะช่วยให้แอปของคุณมีลักษณะสอดคล้องกันทั้งหมด สวยงาม ใช้งานง่าย และคุ้นเคยในสายตาผู้ใช้ โดยเฉพาะอย่างยิ่งบนแพลตฟอร์ม Android แต่ก็สามารถใช้ได้ดีกับ iOS เช่นกัน ทั้งนี้เราสามารถกำหนดธีม สี และลักษณะต่างๆ ของ Material Design ให้เข้ากับแบรนด์ของเราได้อย่างอิสระ
