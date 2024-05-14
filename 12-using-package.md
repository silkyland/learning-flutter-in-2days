# Package

** package ** คือชุดของโค้ดหรือไลบรารี่ที่ถูกเขียนขึ้นมาเพื่อแก้ปัญหาหรือเพิ่มฟีเจอร์บางอย่างใน Flutter app โดยจะมีการจัดเก็บและเผยแพร่ package เหล่านี้ไว้ในรูปแบบที่ใช้งานง่ายและสะดวก
package จะประกอบด้วยโค้ด, asset, ไลบรารี่, หรือแม้แต่ plugin ที่ถูกห่อหุ้มและนำมาใช้งานได้ง่ายผ่านระบบ package management ของ Flutter โดยผู้พัฒนา package จะเผยแพร่ package ของตัวเองผ่านเว็บไซต์ pub.dev ซึ่งจะมีการดูแลเรื่องคุณภาพและความปลอดภัยในระดับหนึ่ง
การใช้ package ใน Flutter นั้นช่วยให้การพัฒนา app ทำได้รวดเร็วและมีประสิทธิภาพมากขึ้น โดยผู้พัฒนาไม่จำเป็นต้องเขียนโค้ดทุกอย่างขึ้นมาใหม่ตั้งแต่เริ่มต้น แต่สามารถนำ package ที่มีอยู่แล้วมาใช้และต่อยอดได้ทันที โดย package จะครอบคลุมในหลากหลายด้าน เช่น:

Widget และ UI components เช่น button, text field, loading spinner ต่างๆ
ระบบ state management เช่น provider, bloc, riverpod
การทำงานกับ API และ HTTP request
พวก utility สำหรับจัดการวันที่ เวลา สกุลเงิน รูปภาพ ฯลฯ
ระบบ authentication และการเชื่อมต่อกับบริการต่างๆ
พวก plugin สำหรับเชื่อมต่อกับ native platform เช่น กล้อง, location, sensor
ฯลฯ

## Pub.dev

![Package](https://pub.dev/static/hash-g6of4ff8/img/pub-dev-logo.svg)

pub.dev - เป็นเว็บไซต์หลักที่รวบรวม package ทั้งหมดของ Dart และ Flutter โดยเป็นแหล่งอย่างเป็นทางการที่ควรเช็คเป็นอันดับแรก เพราะ package ที่อยู่บน pub.dev จะผ่านการตรวจสอบคุณภาพในระดับหนึ่งแล้ว สามารถค้นหา package ที่ต้องการ ดูรายละเอียด เวอร์ชัน ตัวอย่างการใช้งาน และเพิ่มเข้าไปในโปรเจ็กต์ของเราได้เลย

Link - [pub.dev](https://pub.dev/)

## การใช้ package ใน Flutter

- Package คือชุดของโค้ดที่ถูกเขียนขึ้นมาและเผยแพร่โดยนักพัฒนาอื่นๆ เพื่อช่วยให้การพัฒนา app ใน Flutter ทำได้ง่ายและรวดเร็วขึ้น
- Flutter มี package หลายพันตัวที่พร้อมให้ใช้งานใน pub.dev ซึ่งเป็นที่รวบรวม package อย่างเป็นทางการของ Flutter
- เราสามารถเพิ่ม package ที่ต้องการใช้ลงใน pubspec.yaml ซึ่งเป็นไฟล์ที่ใช้จัดการ dependencies ของแอปเรา เช่น:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.5
```

- จากนั้นรัน flutter pub get เพื่อดาวน์โหลด package ที่ระบุไว้และอัปเดตไฟล์ pubspec.lock
- ในโค้ด เราสามารถ import package ที่ต้องการใช้ได้ด้วยคำสั่ง import เช่น:

```dart
import 'package:http/http.dart' as http;
```

- จากนั้นก็สามารถเรียกใช้งาน API หรือ widget ที่ package นั้นๆ มีให้ได้เลย ตัวอย่างการใช้งาน package http สำหรับเรียกใช้งาน API ด้วย http request ได้ดังนี้:

```dart
http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts'));
```

- การใช้ package ช่วยให้เราไม่ต้องเขียนโค้ดบางอย่างซ้ำๆ เอง ทำให้พัฒนาแอปได้เร็วขึ้นมาก
- อย่างไรก็ตาม ต้องใช้ package ด้วยความระมัดระวังและเลือก package ที่น่าเชื่อถือจากผู้พัฒนา ตรวจสอบจำนวน likes, pub points, changelog และอัปเดตล่าสุด เพื่อให้มั่นใจว่าเป็น package ที่ดี
- การใช้ package ถือเป็นส่วนสำคัญในการพัฒนาแอปด้วย Flutter ที่ช่วยประหยัดเวลาและทำให้พัฒนาแอปได้ง่ายขึ้น

สรุปแล้ว package เป็นเครื่องมือที่มีประโยชน์มากสำหรับการพัฒนา Flutter app โดยเฉพาะอย่างยิ่งสำหรับนักพัฒนามือใหม่ที่สามารถเริ่มใช้ประโยชน์จาก package ได้ทันทีโดยไม่ต้องเขียนโค้ดทุกอย่างตั้งแต่ต้น อย่างไรก็ตาม การเลือกใช้ package ก็ต้องทำด้วยความระมัดระวังเพื่อให้แน่ใจว่า package ที่ใช้มีคุณภาพและเหมาะสมสำหรับแอปของเรา

## Practice

ให้ผู้เข้าร่วมอบรม ติดตั้งและใช้งาน package `card_swiper` โดย `card_swiper` เป็น package ที่ช่วยให้เราสร้าง `image slider` หรือ `carousel` ได้อย่างสวยงามและใช้งานง่าย

![Card Swiper](/assets/images/practice/package.png)

ติดตั้ง package `card_swiper` โดยเพิ่ม dependencies ในไฟล์ `pubspec.yaml` ดังนี้:

- [Card Swiper Package ](https://pub.dev/packages/card_swiper)

```yaml
dependencies:
  flutter:
    sdk: flutter
  card_swiper: ^3.0.1
```

มาทำแบบฝึกหัดในการติดตั้งและใช้งาน package card_swiper โดย card_swiper เป็น package ที่ช่วยให้เราสร้าง image slider หรือ carousel ได้อย่างสวยงามและใช้งานง่าย

ขั้นตอนมีดังนี้:

1. เปิด terminal และ navigate ไปยังโฟลเดอร์โปรเจ็กต์ Flutter
2. เปิดไฟล์ pubspec.yaml
3. ภายใต้ dependencies: ให้เพิ่มบรรทัดใหม่และพิมพ์:

```yaml
card_swiper: ^2.0.4
```

4. กลับมาที่ terminal และรันคำสั่ง:

```
flutter pub get
```

5. สร้างไฟล์ใหม่ชื่อ image_slider_page.dart ในโฟลเดอร์ lib

6. เปิดไฟล์ image_slider_page.dart และเขียนโค้ดดังนี้:

```dart
import 'package:flutter/material.dart';
import 'package:card_swiper/card_swiper.dart';

class ImageSliderPage extends StatelessWidget {
  final List<String> imageUrls = [
    'https://source.unsplash.com/random/?cat',
    'https://source.unsplash.com/random/?bird',
    'https://source.unsplash.com/random/?sky,building',
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Slider'),
      ),
      body: Container(
        padding: EdgeInsets.all(16),
        child: Swiper(
          itemBuilder: (BuildContext context, int index) {
            return Image.network(
              imageUrls[index],
              fit: BoxFit.cover,
            );
          },
          itemCount: imageUrls.length,
          viewportFraction: 0.8,
          scale: 0.9,
        ),
      ),
    );
  }
}
```

7. ในไฟล์ main.dart ให้เรียกใช้งาน ImageSliderPage ดังนี้:

```dart
import 'package:flutter/material.dart';
import 'image_slider_page.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Image Slider Demo',
      home: ImageSliderPage(),
    );
  }
}
```

8. รันแอปด้วยคำสั่ง flutter run บน terminal

เมื่อเสร็จแล้ว คุณจะได้ image slider ที่สามารถ swipe ได้อย่างสวยงามโดยใช้ package card_swiper โดยเราใช้รูปภาพจาก URL ในตัวอย่างนี้ แต่คุณสามารถใช้รูปภาพ Asset หรือจากแหล่งอื่นๆ ได้เช่นกัน

## โจทย์

โจทย์: ให้ติดตั้งและใช้งาน package google_fonts เพื่อเปลี่ยนฟอนต์ในแอป Flutter

ขั้นตอน:

1. ศึกษาวิธีการติดตั้งและใช้งาน package google_fonts จากเว็บไซต์ https://pub.dev/packages/google_fonts
2. ติดตั้ง package ตามขั้นตอนที่ระบุโดยการเพิ่ม dependency ใน pubspec.yaml และรัน flutter pub get
3. เลือกฟอนต์ที่ต้องการใช้งานจากเว็บไซต์ https://fonts.google.com/ อย่างน้อย 2 ฟอนต์
4. สร้างไฟล์ใหม่ชื่อ google_fonts_demo.dart ในโฟลเดอร์ lib
5. เขียนโค้ดเพื่อแสดง Text widget ที่ใช้ฟอนต์จาก package google_fonts โดยใช้ฟอนต์ที่เลือกไว้ในข้อ 3
6. แสดงข้อความ "Hello, World!" ด้วยฟอนต์แรก และข้อความ "สวัสดีชาวโลก" ด้วยฟอนต์ที่สอง โดยจัดให้อยู่กึ่งกลางหน้าจอ
7. ปรับขนาดฟอนต์ให้เหมาะสม เช่น 24 สำหรับข้อความภาษาอังกฤษ และ 28 สำหรับข้อความภาษาไทย
8. เรียกใช้ GoogleFontsDemo ใน main.dart เพื่อแสดงผลการทำงาน
9. รันแอปและดูผลลัพธ์

ส่งงานโดยการ commit โค้ดที่เขียนไว้และ push ขึ้น branch ของตัวเอง บน GitHub แล้วส่งลิ้งค์ไปยังอีเมล์ของผู้สอน
