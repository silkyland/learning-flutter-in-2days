## Theme in Flutter

เรื่อง Theme ใน Flutter เป็นเรื่องสำคัญที่ช่วยให้แอปพลิเคชันของเรามีรูปลักษณ์ที่สวยงาม สอดคล้องกัน และเป็นมืออาชีพ โดย Flutter ให้ความยืดหยุ่นในการกำหนด Theme ของแอปพลิเคชันได้อย่างง่ายดาย ต่อไปนี้เป็นเนื้อหาสำคัญเกี่ยวกับ Theme ใน Flutter:

1. **ThemeData**: `ThemeData` เป็น class หลักที่ใช้ในการกำหนด Theme ของแอปพลิเคชัน โดยจะประกอบไปด้วยการกำหนดค่าต่างๆ เช่น สี, ฟอนต์, รูปร่าง, และอื่นๆ ที่จะถูกใช้ในแอปพลิเคชัน

2. **Colors**: Flutter มีชุดสีพื้นฐานที่เรียกว่า Material Color Palette ซึ่งประกอบด้วยสีหลักและสีเฉดต่างๆ เราสามารถใช้สีเหล่านี้ในการกำหนด Theme หรือสร้างชุดสีของเราเองได้

3. **Typography**: Flutter มีชุดฟอนต์พื้นฐานที่เรียกว่า Material Typography ซึ่งประกอบด้วยขนาดและรูปแบบของข้อความต่างๆ เช่น Headline, Title, Subtitle, Body Text เป็นต้น เราสามารถใช้ Typography เหล่านี้หรือกำหนดฟอนต์เองได้

4. **Theme Widgets**: Flutter มี Widgets หลายตัวที่ใช้ในการกำหนด Theme เช่น `Theme`, `MaterialApp`, `ThemeData.light()`, `ThemeData.dark()` เป็นต้น ซึ่งช่วยให้สามารถกำหนด Theme ได้อย่างง่ายดายและยืดหยุ่น

5. **Custom Themes**: นอกจากการใช้ Theme พื้นฐานแล้ว เรายังสามารถสร้าง Custom Theme ของเราเองได้ โดยการกำหนดค่าต่างๆ ใน `ThemeData` ตามที่เราต้องการ ซึ่งช่วยให้แอปพลิเคชันของเรามีเอกลักษณ์เฉพาะตัว

6. **Theme Switching**: Flutter ยังรองรับการสลับ Theme ได้อย่างง่ายดาย เช่น การสลับระหว่าง Light Theme และ Dark Theme ซึ่งช่วยให้ผู้ใช้สามารถปรับแต่งหน้าตาของแอปพลิเคชันได้ตามความต้องการ

7. **Theme Inheritance**: ใน Flutter, Theme สามารถสืบทอดและแก้ไขค่าได้ เช่น เราสามารถกำหนด Theme หลักใน `MaterialApp` และสามารถแก้ไขค่าบางส่วนใน Widgets ลูกได้ ซึ่งช่วยให้การจัดการ Theme ในแอปพลิเคชันเป็นเรื่องง่าย

การใช้ Theme ใน Flutter ช่วยให้แอปพลิเคชันของเรามีความสอดคล้องและเป็นมืออาชีพ ซึ่งส่งผลต่อประสบการณ์ของผู้ใช้และความน่าเชื่อถือของแอปพลิเคชัน

### ตัวอย่างการตั้งค่่า Theme ให้กับ Application

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My App',
      theme: ThemeData(
        // กำหนดชุดสีหลักของแอปพลิเคชัน
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.blue),

        // กำหนดฟอนต์หลักของแอปพลิเคชัน
        fontFamily: 'Roboto',

        // กำหนดรูปแบบของ Typography
        textTheme: TextTheme(
          displayLarge: TextStyle(fontSize: 48, fontWeight: FontWeight.bold),
          displayMedium: TextStyle(fontSize: 36),
          bodyLarge: TextStyle(fontSize: 18),
          bodyMedium: TextStyle(fontSize: 16),
        ),

        // กำหนดรูปแบบของปุ่ม
        elevatedButtonTheme: ElevatedButtonThemeData(
          style: ElevatedButton.styleFrom(
            textStyle: TextStyle(fontSize: 18),
            padding: EdgeInsets.symmetric(vertical: 16, horizontal: 32),
            shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(24)),
          ),
        ),

        // กำหนดรูปแบบของ AppBar
        appBarTheme: AppBarTheme(
          backgroundColor: Colors.blue,
          foregroundColor: Colors.white,
          titleTextStyle: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
        ),

        // กำหนดรูปแบบของ Card
        cardTheme: CardTheme(
          color: Colors.white,
          elevation: 4,
          shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16)),
        ),

        // ใช้ Material 3
        useMaterial3: true,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Welcome to My App',
              style: Theme.of(context).textTheme.displayMedium,
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {},
              child: Text('Get Started'),
            ),
            SizedBox(height: 20),
            Card(
              child: Padding(
                padding: EdgeInsets.all(16),
                child: Text(
                  'This is a sample card',
                  style: Theme.of(context).textTheme.bodyLarge,
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

#### ตัวอย่างผลลัพธ์การตั้งค่า Theme ให้กับ Application

![ผลการตั้งค่า Theme](/assets/images/8/theme.png)
