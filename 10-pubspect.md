# pubspec.yaml

pubspec.yaml เป็นไฟล์ configuration หลักของโปรเจ็กต์ Flutter ที่ใช้ในการระบุข้อมูลเกี่ยวกับแอปพลิเคชัน, dependencies, assets และการตั้งค่าต่างๆ ไฟล์นี้อยู่ในโฟลเดอร์ root ของโปรเจ็กต์ และใช้รูปแบบ YAML (Yet Another Markup Language) ในการเขียน

ส่วนประกอบหลักของไฟล์ pubspec.yaml มีดังนี้:

1. name: ชื่อของแอปพลิเคชัน
   ```yaml
   name: my_app
   ```

2. description: คำอธิบายสั้นๆ เกี่ยวกับแอปพลิเคชัน
   ```yaml
   description: A new Flutter project.
   ```

3. version: เลขเวอร์ชันของแอปพลิเคชัน
   ```yaml
   version: 1.0.0+1
   ```

4. environment: ระบุเวอร์ชันของ Flutter SDK และ Dart SDK ที่ใช้ในโปรเจ็กต์
   ```yaml
   environment:
     sdk: ">=2.12.0 <3.0.0"
   ```

5. dependencies: ระบุ package หรือ library ภายนอกที่ใช้ในโปรเจ็กต์ พร้อมทั้งเวอร์ชันที่ต้องการ
   ```yaml
   dependencies:
     flutter:
       sdk: flutter
     http: ^0.13.0
     provider: ^6.0.0
   ```

6. dev_dependencies: ระบุ package ที่ใช้เฉพาะในขั้นตอนการพัฒนา เช่น testing, linting เป็นต้น
   ```yaml
   dev_dependencies:
     flutter_test:
       sdk: flutter
     mockito: ^5.0.0
   ```

7. flutter: ใช้ในการตั้งค่าเกี่ยวกับ Flutter เช่น assets, fonts, และ plugin ต่างๆ
   ```yaml
   flutter:
     uses-material-design: true
     assets:
       - images/
     fonts:
       - family: Raleway
         fonts:
           - asset: fonts/Raleway-Regular.ttf
           - asset: fonts/Raleway-Italic.ttf
             style: italic
   ```

นอกจากนี้ยังมีส่วนอื่นๆ ที่สามารถใส่ในไฟล์ pubspec.yaml ได้อีก เช่น:
- publish_to: ระบุ repository ที่ใช้ในการเผยแพร่ package
- author หรือ authors: ระบุชื่อผู้พัฒนาแอปพลิเคชัน
- homepage: URL ของเว็บไซต์หรือเพจที่ให้ข้อมูลเกี่ยวกับแอปพลิเคชัน
- issue_tracker: URL ของระบบติดตามปัญหาหรือบั๊กของแอปพลิเคชัน
- documentation: URL ของเอกสารประกอบแอปพลิเคชัน

การตั้งค่าต่างๆ ในไฟล์ pubspec.yaml มีผลต่อการทำงานและการคอมไพล์ของแอปพลิเคชัน ดังนั้นจึงควรใส่ใจและตรวจสอบให้แน่ใจว่าได้กำหนดค่าที่ถูกต้องและเหมาะสมกับความต้องการของโปรเจ็กต์ รวมถึงควรมีการอัปเดตไฟล์ pubspec.yaml เป็นระยะๆ เมื่อมีการเพิ่ม ลบ หรือเปลี่ยนแปลง dependencies หรือส่วนอื่นๆ ในโปรเจ็กต์ เพื่อให้แอปพลิเคชันสามารถทำงานได้อย่างถูกต้องและมีเสถียรภาพ

## Increment version

ในการ increment version ของแอปพลิเคชัน Flutter ใน pubspec.yaml เราสามารถทำได้ตามรูปแบบของเลขเวอร์ชันที่นิยมใช้ เช่น Semantic Versioning (SemVer) ซึ่งประกอบด้วย 3 ส่วนหลักคือ MAJOR.MINOR.PATCH โดยมีความหมายดังนี้

- MAJOR: เพิ่มขึ้นเมื่อมีการเปลี่ยนแปลงที่ไม่เข้ากันกับเวอร์ชันเก่า (breaking changes)
- MINOR: เพิ่มขึ้นเมื่อมีการเพิ่มฟีเจอร์ใหม่ที่ยังคงใช้งานร่วมกับเวอร์ชันเก่าได้
- PATCH: เพิ่มขึ้นเมื่อมีการแก้ไขบั๊กหรือปรับปรุงเล็กน้อยที่ไม่กระทบกับฟีเจอร์เดิม

นอกจากนี้ เรายังสามารถใส่ metadata เพิ่มเติมต่อท้ายเลขเวอร์ชันได้อีก เช่น pre-release identifier (+1, +2) หรือ build metadata (b1, b2) เป็นต้น

ตัวอย่างการ increment version ใน pubspec.yaml:

```yaml
version: 1.0.0    # เวอร์ชันเริ่มต้น

version: 1.0.1    # increment PATCH เมื่อมีการแก้ไขบั๊ก

version: 1.1.0    # increment MINOR เมื่อเพิ่มฟีเจอร์ใหม่

version: 2.0.0    # increment MAJOR เมื่อมีการเปลี่ยนแปลงใหญ่ที่ไม่เข้ากับเวอร์ชันเก่า

version: 1.0.0+1  # เพิ่ม build metadata

version: 1.0.0-beta+1  # ระบุเป็น pre-release version
```

เมื่อเรา increment version ใน pubspec.yaml แล้ว ควรอย่าลืม:
- Update changelog หรือ release notes เพื่อให้ผู้ใช้ทราบถึงการเปลี่ยนแปลงในเวอร์ชันใหม่
- Commit และ tag โค้ดในระบบ version control ด้วยหมายเลขเวอร์ชันใหม่
- สร้างไฟล์ build ใหม่ (apk, ipa) สำหรับเวอร์ชันล่าสุด
- อัปโหลดไฟล์ build และข้อมูลเวอร์ชันใหม่ขึ้น app store หรือแพลตฟอร์มที่ใช้งาน

การ increment version อย่างเหมาะสมและสม่ำเสมอจะช่วยให้ผู้ใช้และนักพัฒนาอื่นๆ สามารถติดตามความคืบหน้าและการเปลี่ยนแปลงของแอปพลิเคชันได้ง่ายขึ้น รวมถึงช่วยให้การบริหารจัดการและแก้ไขปัญหาในแต่ละเวอร์ชันทำได้อย่างมีประสิทธิภาพมากขึ้นอีกด้วย
