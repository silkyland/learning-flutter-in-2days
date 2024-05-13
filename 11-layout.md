# Layout

การวาง Layout ใน Flutter คือการจัดวางองค์ประกอบต่างๆ ของ UI เช่น Widgets ลงบนหน้าจอแอปพลิเคชัน Flutter ใช้ระบบ Layout ที่ยืดหยุ่นและมีประสิทธิภาพในการสร้าง UI ที่สวยงามและรองรับขนาดหน้าจอที่หลากหลาย

เราทราบว่า Everything is a Widget - ใน Flutter ทุกอย่างคือ Widget ตั้งแต่ปุ่ม ข้อความ รูปภาพ หรือแม้แต่ไอคอน หรือ แม้แต่ widget ที่เรามองไม่เห็นเช่น rows, columns, flex, grid, และอื่นๆ ก็ล้วนแต่เป็น Widget ทั้งนั้น

เราสามารถสร้าง Layout ได้โดยการประกอบ Widget เข้าด้วยกันเพื่อสร้าง Widget ที่ซับซ้อนยิ่งขึ้น ยกตัวอย่างเช่น ภาพหน้าจอแรกด้านล่างนี้แสดง ไอคอน 3 อันที่มีป้ายกำกับอยู่ใต้แต่ละไอคอน:

![layout](https://docs.flutter.dev/assets/images/docs/ui/layout/lakes-icons.png)
![layout](https://docs.flutter.dev/assets/images/docs/ui/layout/lakes-icons-visual.png)

ภาพหน้าจอที่สองแสดงการจัดวางแบบ Visual โดยแสดง Row (แถว) ที่ประกอบด้วย 3 Column (คอลัมน์) ซึ่งแต่ละคอลัมน์มีไอคอนและป้ายกำกับ (Label)

ต่อไปนี้คือการแสดงผล Diagram ของ Widget Tree ในการจัดวาง Layout จาก widget ด้านบน

![alt text](/assets/images/11/wiget-tree.png)

## การสร้าง Multiple Widgets กับ Layout โดยใช้รูปแบบ Vertical (แนวตั้ง) และ Horizontal (แนวนอน)

สำหรับการสร้าง Multiple Widgets ใน Layout โดยใช้รูปแบบ Vertical (แนวตั้ง) และ Horizontal (แนวนอน) สามารถทำได้ดังนี้
Column และ Row ใน Flutter เป็น widgets ที่ใช้ในการจัดวาง widgets แบบ linear หรือเรียงต่อกัน โดยมีรายละเอียดดังนี้

### Column

- เป็น widget ที่ใช้ในการจัดเรียง children widgets แบบแนวตั้ง (vertical)
- children widgets จะถูกวางซ้อนกันจากบนลงล่าง
- สามารถกำหนด properties ของ Column เพื่อควบคุมลักษณะการแสดงผล เช่น
  - mainAxisAlignment: กำหนดการจัดวาง children ในแนวตั้ง เช่น center, start, end, spaceBetween เป็นต้น
  - crossAxisAlignment: กำหนดการจัดวาง children ในแนวนอน เช่น center, start, end, stretch เป็นต้น
  - mainAxisSize: กำหนดขนาดของ Column ในแนวตั้ง สามารถเป็น min หรือ max

ตัวอย่างการใช้ Column:

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  crossAxisAlignment: CrossAxisAlignment.start,
  children: [
    Text('Item 1'),
    Text('Item 2'),
    Text('Item 3'),
  ],
)
```

### Row

- เป็น widget ที่ใช้ในการจัดเรียง children widgets แบบแนวนอน (horizontal)
- children widgets จะถูกวางเรียงกันจากซ้ายไปขวา
- สามารถกำหนด properties ของ Row เพื่อควบคุมลักษณะการแสดงผล เช่น
  - mainAxisAlignment: กำหนดการจัดวาง children ในแนวนอน เช่น center, start, end, spaceBetween เป็นต้น
  - crossAxisAlignment: กำหนดการจัดวาง children ในแนวตั้ง เช่น center, start, end, stretch เป็นต้น
  - mainAxisSize: กำหนดขนาดของ Row ในแนวนอน สามารถเป็น min หรือ max

ตัวอย่างการใช้ Row:

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    Icon(Icons.add),
    Text('Add'),
    Icon(Icons.remove),
  ],
)
```

Column และ Row เป็น widgets ที่ใช้งานบ่อยมากในการสร้าง layout ใน Flutter เพราะช่วยให้สามารถจัดวาง widgets ได้ง่ายและยืดหยุ่น สามารถนำไปประยุกต์ใช้ในการสร้าง UI ที่หลากหลายได้

เรามาลองวิเคราะห์การจัดเรียง Column และ Row ใน Flutter จากรูปตัวอย่างด้านล่าง

![alt text](/assets/images/11/layout-example.png)

การจัดเรียงองค์ประกอบของ Layout ให้มองจากภาพใหญ่ก่อน แล้วค่อยๆ ซอยย่อยลงไปทีละขั้นตอน ดังนี้

1.  จากรูปด้านบนหากมองดูด้านนอกสุด เราจะเริ่มต้นที่ `Row` widget ก่อน นั่นคือ โดยแบ่ง Layout ออกเป็น 2 ส่วน คือฝั่งซ้ายที่เป็นรายละเอียด และ ฝั่งขวาที่เป็นรูปภาพ

    ```dart
    Row(
    children: [
        // 1. [Widget รายละเอียด]  <-- ด้านซ้ายมือ
        Column(
          children: [
               ....
          ],
        ),
        // 2. [Widget รูปภาพ]  <-- ด้านขวามือ
        Image.asset(
         ...
        ),
    ],
    )
    ```

2.  จากนั้นเราจะแยกส่วนของ `Widget รายละเอียด` ออกมา ดูจากรูปภาพ

    ![alt text](/assets/images/11/column.png)

    ซึ่งประกอบด้วย `Column` ประกอบด้วย `children` 4 องค์ประกอบ คือ

    - ชื่อเมนูอาหาร (Text)

    - รายละเอียดเมนูอาหาร (Text)

    - เป็น Rating และ Review ที่ถูกจัดเรียงแนวนอน (Row)

      - Rating อาหารที่จัดเรียงรูปดาวแนวนอน (Row)

        - รูปดาว (Icon)
        - คะแนน Review (Text)

    - รายการแบบแนวนอนแสดงรายละเอียดการเตรียมอาหาร (Row)

      - การเตรียมอาหาร (Column)

        - รูปไอคอน (Icon)
        - ข้อความ PREP: (Text)
        - ข้อความ 25 min (Text)

      - ระยะเวลาในการปรุง (Column)

        - รูปไอคอน (Icon)
        - ข้อความ COOK: (Text)
        - ข้อความ 1 hr (Text)

      - ปริมาณที่เหมาะต่อหัว (Column)

        - รูปไอคอน (Icon)
        - ข้อความ Feed: (Text)
        - ข้อความ 4 - 6 (Text)

    ดังนั้นเราสามารถเขียนโค้ดดังนี้

    ```dart
    Column(
    crossAxisAlignment: CrossAxisAlignment.start,
        children: [
            Text(
                'Strawberry Pavlova',
                style: TextStyle(
                    fontSize: 20,
                    fontWeight: FontWeight.bold,
                ),
            ),
            SizedBox(height: 10),
            Text(
                'Pavlova is a meringue-based dessert named after the Russian ballerina Anna Pavlova. Pavlova features a crisp crust and soft, light inside, topped with fruit and whipped cream.',
                style: TextStyle(fontSize: 16),
            ),
            SizedBox(height: 20),
            Row(
                children: [
                    Row(
                        children: [
                            Icon(Icons.star, color: Colors.yellow),
                            Icon(Icons.star, color: Colors.yellow),
                            Icon(Icons.star, color: Colors.yellow),
                            Icon(Icons.star, color: Colors.yellow),
                            Icon(Icons.star, color: Colors.yellow),
                        ],
                    ),
                    SizedBox(width: 10),
                    Text('170 Reviews'),
                ],
            ),
            SizedBox(height: 20),
            Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [
                    Column(
                        children: [
                            Icon(Icons.kitchen, color: Colors.green),
                            Text('PREP:'),
                            Text('25 min'),
                        ],
                    ),
                    Column(
                        children: [
                            Icon(Icons.timer, color: Colors.green),
                            Text('COOK:'),
                            Text('1 hr'),
                        ],
                    ),
                    Column(
                        children: [
                            Icon(Icons.restaurant, color: Colors.green),
                            Text('FEEDS:'),
                            Text('4-6'),
                        ],
                    ),
                ],
            ),
        ],
    );
    ```

3.  สุดท้ายเราจะเขียนโค้ดสำหรับ `Widget รูปภาพ` ดังนี้

    ```dart
    Image.asset(
        'assets/images/pavlova.jpg',
        width: 200,
        height: 200,
        fit: BoxFit.cover,
    ),
    ```

4.  รวมโค้ดทั้งหมดเข้าด้วยกัน และตกแต่ง style ให้สวยงาม

    ```dart
    Row(
          crossAxisAlignment: CrossAxisAlignment.start,
          mainAxisAlignment: MainAxisAlignment.start,
          children: [
            Container(
              width: 170,
              padding: const EdgeInsets.all(8.0),
              child: const Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Align(
                    alignment: Alignment.center,
                    child: Text(
                      'Strawberry Pavlova',
                      textAlign: TextAlign.center,
                      style: TextStyle(
                        fontSize: 14,
                        fontWeight: FontWeight.bold,
                      ),
                    ),
                  ),
                  SizedBox(height: 10),
                  Text(
                    'Pavlova is a meringue-based dessert named after the Russian ballerina Anna Pavlova. Pavlova features a crisp crust and soft, light inside, topped with fruit and whipped cream.',
                    style: TextStyle(fontSize: 10),
                  ),
                  SizedBox(height: 10),
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                    children: [
                      Row(
                        children: [
                          Icon(Icons.star, color: Colors.yellow, size: 10),
                          Icon(Icons.star, color: Colors.yellow, size: 10),
                          Icon(Icons.star, color: Colors.yellow, size: 10),
                          Icon(Icons.star, color: Colors.yellow, size: 10),
                          Icon(Icons.star, color: Colors.yellow, size: 10),
                        ],
                      ),
                      SizedBox(width: 10),
                      Text('170 Reviews', style: TextStyle(fontSize: 10)),
                    ],
                  ),
                  SizedBox(height: 10),
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      Column(
                        children: [
                          Icon(Icons.kitchen, color: Colors.green, size: 14),
                          Text('PREP:', style: TextStyle(fontSize: 10)),
                          Text('25 min', style: TextStyle(fontSize: 10)),
                        ],
                      ),
                      Column(
                        children: [
                          Icon(Icons.timer, color: Colors.green, size: 14),
                          Text('COOK:', style: TextStyle(fontSize: 10)),
                          Text('1 hr', style: TextStyle(fontSize: 10)),
                        ],
                      ),
                      Column(
                        children: [
                          Icon(Icons.restaurant, color: Colors.green, size: 14),
                          Text('FEEDS:', style: TextStyle(fontSize: 10)),
                          Text('4-6', style: TextStyle(fontSize: 10)),
                        ],
                      ),
                    ],
                  ),
                ],
              ),
            ),
            Expanded(
              child: Image.network(
                'https://images.unsplash.com/photo-1685156328658-da6116852b4c?q=80&w=1469&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
                width: 200,
                height: 200,
                fit: BoxFit.cover,
              ),
            ),
          ],
        )
    ```

    ผลลัพธ์ที่ได้คือ

    ![alt text](/assets/images/11/example-completed.png)

## การจัดวาง Layout ของ Column และ Row ใน Flutter

ในการพัฒนาแอปพลิเคชันด้วย Flutter นักพัฒนาสามารถควบคุมการจัดวาง Layout ของ Widget ต่างๆ ได้อย่างยืดหยุ่น โดยเฉพาะอย่างยิ่งการจัดวาง Widget ใน Column และ Row ซึ่งเป็น Widget พื้นฐานที่ใช้ในการจัดเรียง Widget แนวตั้งและแนวนอน ตามลำดับ

ในการกำหนดการจัดวาง Layout ของ Column และ Row เราสามารถใช้ `mainAxisAlignment` และ `crossAxisAlignment` ซึ่งเป็น properties ที่ใช้ในการกำหนดการจัดวางตำแหน่งของ children Widget ในแนวแกนหลัก (main axis) และแนวแกนรอง (cross axis) ของ Column หรือ Row นั้นๆ

![alt text](/assets/images/11/alignment-row-column.png)

![alt text](/assets/images/11/alignment-column.png)

โดย `mainAxisAlignment` จะใช้ในการกำหนดการจัดวางของ children ในแนวแกนหลัก ซึ่งก็คือแนวตั้งสำหรับ Column และแนวนอนสำหรับ Row ซึ่งมีค่าที่สามารถกำหนดได้ ดังนี้

- `MainAxisAlignment.start`: จัดวาง children ชิดไปทางจุดเริ่มต้นของแกนหลัก
- `MainAxisAlignment.center`: จัดวาง children ไว้ตรงกลางของแกนหลัก
- `MainAxisAlignment.end`: จัดวาง children ชิดไปทางจุดสิ้นสุดของแกนหลัก
- `MainAxisAlignment.spaceBetween`: กระจาย children ให้มีระยะห่างเท่าๆกันตลอดความยาวของแกนหลัก โดย children ตัวแรกและตัวท้ายจะชิดขอบ
- `MainAxisAlignment.spaceAround`: กระจาย children ให้มีระยะห่างเท่าๆกันตลอดความยาวของแกนหลัก โดย children แต่ละตัวจะมีระยะห่างพอๆกันทั้งด้านหน้าและด้านหลัง
- `MainAxisAlignment.spaceEvenly`: กระจาย children และช่องว่างให้มีระยะห่างเท่ากันหมดตลอดความยาวแกนหลัก

ในทำนองเดียวกัน `crossAxisAlignment` จะใช้ในการกำหนดการจัดวางของ children ในแนวแกนรอง ซึ่งเป็นแนวตั้งฉากกับแกนหลัก คือ แนวนอนสำหรับ Column และแนวตั้งสำหรับ Row ซึ่งมีค่าที่กำหนดได้ ได้แก่

- `CrossAxisAlignment.start`: จัดวาง children ชิดไปทางจุดเริ่มต้นของแกนรอง
- `CrossAxisAlignment.center`: จัดวาง children ไว้ตรงกลางของแกนรอง
- `CrossAxisAlignment.end`: จัดวาง children ชิดไปทางจุดสิ้นสุดของแกนรอง
- `CrossAxisAlignment.stretch`: ยืด children ให้มีขนาดเต็มความกว้างของ Column หรือความสูงของ Row
- `CrossAxisAlignment.baseline`: จัดวาง children ตามเส้น baseline โดยปกติจะใช้กับ Text Widget

นอกจากนี้ เรายังสามารถใช้ `VerticalDirection` และ `TextDirection` เพื่อกำหนดทิศทางการจัดเรียง children ใน Column และการจัดเรียง Text ภายใน Row ได้อีกด้วย

การกำหนดการจัดวาง Layout ของ Column และ Row อย่างเหมาะสม จะช่วยให้การออกแบบ UI มีความยืดหยุ่นและรองรับความหลากหลายของขนาดหน้าจอได้ดียิ่งขึ้น ทำให้แอปพลิเคชันมีความสวยงามและใช้งานได้อย่างเป็นมิตรกับผู้ใช้มากขึ้น

## Stack Widget

![alt text](https://docs.flutter.dev/assets/images/docs/ui/layout/stack.png)

Stack เป็น Widget ที่ใช้ในการวาง Widget ซ้อนกันเป็นชั้นๆ โดย Widget ที่อยู่ด้านบนจะทับ Widget ที่อยู่ด้านล่าง ซึ่งตำแหน่งของ Widget เหล่านี้จะถูกกำหนดโดยใช้ `alignment` property ของ Stack

นอกจากนี้ Stack ยังมี `positioned` ที่ช่วยให้เราสามารถกำหนดตำแหน่งของ Widget ภายใน Stack ได้อย่างอิสระ โดยสามารถกำหนด top, bottom, left และ right เพื่อระบุระยะห่างจากขอบของ Stack

ตัวอย่างการใช้งาน Stack และ Positioned:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Stack Example'),
        ),
        body: Center(
          child: Stack(
            alignment: Alignment.center,
            children: <Widget>[
              Container(
                width: 200,
                height: 200,
                color: Colors.red,
              ),
              Positioned(
                top: 20,
                left: 20,
                child: Container(
                  width: 100,
                  height: 100,
                  color: Colors.blue,
                ),
              ),
              Positioned(
                bottom: 20,
                right: 20,
                child: Container(
                  width: 100,
                  height: 100,
                  color: Colors.green,
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

ในตัวอย่างนี้ เราสร้าง Stack ที่มี Container สีแดงขนาด 200x200 เป็น children ตัวแรก จากนั้นเราใช้ Positioned เพื่อวาง Container สีน้ำเงินขนาด 100x100 ไว้มุมบนซ้าย โดยกำหนดระยะห่างจากด้านบนและซ้ายของ Stack 20 pixels และใช้ Positioned อีกครั้งเพื่อวาง Container สีเขียวขนาด 100x100 ไว้มุมล่างขวา โดยกำหนดระยะห่างจากด้านล่างและขวาของ Stack 20 pixels

ผลลัพธ์ที่ได้คือ

![alt text](/assets/images/11/stack.png)

เมื่อ run โค้ดนี้ คุณจะเห็น Container สีแดงวางอยู่ตรงกลาง ซึ่งมี Container สีน้ำเงินซ้อนทับอยู่ที่มุมบนซ้าย และ Container สีเขียวซ้อนทับอยู่ที่มุมล่างขวา ซึ่งแสดงให้เห็นถึงการทำงานของ Stack และ Positioned ในการจัดวาง Widget แบบซ้อนทับกัน

Stack เป็น Widget ที่มีประโยชน์มากในการสร้าง UI ที่ซับซ้อน เช่น การวางรูปภาพหรือ Widget อื่นๆ ซ้อนทับกัน หรือการสร้างเอฟเฟกต์พิเศษต่างๆ ในแอปพลิเคชัน Flutter

# Card Widget

![alt text](https://docs.flutter.dev/assets/images/docs/ui/layout/card-flutter-gallery.png)

Card เป็น Widget ที่ใช้ในการแสดงข้อมูลในรูปแบบของการ์ด โดยมีลักษณะเป็นกล่องสี่เหลี่ยมที่มีเงาและขอบมน ซึ่งสามารถใส่ข้อความ รูปภาพ หรือ Widget อื่นๆ ลงไปได้ โดยปกติ Card มักถูกใช้ในการแสดงข้อมูลที่เป็นส่วนย่อยหรือเป็นหมวดหมู่ เพื่อให้ UI มีความสวยงามและเป็นระเบียบมากขึ้น

ตัวอย่างการใช้งาน Card:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Card Example'),
        ),
        body: Center(
          child: Card(
            elevation: 5,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(10),
            ),
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: <Widget>[
                ListTile(
                  leading: Icon(Icons.album),
                  title: Text('The Enchanted Nightingale'),
                  subtitle: Text('Music by Julie Gable. Lyrics by Sidney Stein.'),
                ),
                ButtonBar(
                  children: <Widget>[
                    TextButton(
                      child: const Text('BUY TICKETS'),
                      onPressed: () {/* ... */},
                    ),
                    TextButton(
                      child: const Text('LISTEN'),
                      onPressed: () {/* ... */},
                    ),
                  ],
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

ในตัวอย่างนี้ เราสร้าง Card ที่มีเงาและขอบมนโดยใช้ `elevation` และ `shape` properties จากนั้นภายใน Card เราใส่ Column ที่มี ListTile และ ButtonBar เป็น children

โดย ListTile จะแสดงไอคอน ข้อความหัวเรื่อง และข้อความรายละเอียด ส่วน ButtonBar จะแสดงปุ่ม 'BUY TICKETS' และ 'LISTEN' ซึ่งสามารถกำหนด callback function เพื่อตอบสนองต่อการกดปุ่มได้

เมื่อ run โค้ดนี้ คุณจะเห็น Card ที่มีข้อมูลของอัลบั้มเพลงแสดงอยู่ตรงกลางของหน้าจอ ซึ่งประกอบไปด้วยไอคอน ชื่ออัลบั้ม ชื่อศิลปิน และปุ่มสำหรับซื้อตั๋วและฟังเพลง

ตัวอย่างผลลัพธ์ที่ได้:

![alt text](/assets/images/11/card.png)

Card เป็น Widget ที่นิยมใช้กันอย่างแพร่หลายใน Material Design เนื่องจากช่วยให้ UI มีความสวยงาม เป็นระเบียบ และง่ายต่อการอ่านข้อมูล นอกจากนี้ ยังสามารถกำหนดสีพื้นหลัง ขนาด ความโค้งมนของขอบ และ Elevation ได้ตามต้องการอีกด้วย

## ListTile Widget

ListTile เป็น Widget ที่ใช้ในการแสดงแถวของข้อมูลในรูปแบบของรายการ (List) โดยปกติจะประกอบไปด้วยไอคอนหรือรูปภาพ ข้อความหัวเรื่อง (title) และข้อความรายละเอียด (subtitle) ซึ่ง ListTile มักถูกใช้ร่วมกับ ListView หรือ Column เพื่อแสดงรายการข้อมูลแบบเรียงลำดับ

ListTile มีส่วนประกอบหลักๆ ดังนี้

- `leading`: วิดเจ็ตที่แสดงด้านซ้ายของ ListTile เช่น ไอคอนหรือรูปภาพ
- `title`: ข้อความหัวเรื่องของ ListTile
- `subtitle`: ข้อความรายละเอียดของ ListTile
- `trailing`: วิดเจ็ตที่แสดงด้านขวาของ ListTile เช่น ไอคอนหรือปุ่ม
- `onTap`: callback function ที่จะถูกเรียกเมื่อผู้ใช้แตะบน ListTile

ตัวอย่างการใช้งาน ListTile:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text('ListTile Example'),
        ),
        body: ListView(
          children: <Widget>[
            ListTile(
              leading: const Icon(Icons.map),
              title: const Text('Map'),
              subtitle: const Text('Google Map'),
              onTap: () {
                // ทำอะไรบางอย่างเมื่อ ListTile ถูกแตะ
              },
            ),
            ListTile(
              leading: const Icon(Icons.photo_album),
              title: const Text('Album'),
              subtitle: const Text('image gallery'),
              onTap: () {
                // ทำอะไรบางอย่างเมื่อ ListTile ถูกแตะ
              },
            ),
            ListTile(
              leading: const Icon(Icons.phone),
              title: const Text('Phone'),
              subtitle: const Text('Call'),
              onTap: () {
                // ทำอะไรบางอย่างเมื่อ ListTile ถูกแตะ
              },
            ),
            ListTile(
              leading: const Icon(Icons.contacts),
              title: const Text('Contacts'),
              subtitle: const Text('Contact list'),
              onTap: () {
                // ทำอะไรบางอย่างเมื่อ ListTile ถูกแตะ
              },
            ),
            ListTile(
              leading: const Icon(Icons.settings),
              title: const Text('Settings'),
              subtitle: const Text('App settings'),
              onTap: () {
                // ทำอะไรบางอย่างเมื่อ ListTile ถูกแตะ
              },
            ),
          ],
        ),
      ),
    );
  }
}

```

ในตัวอย่างนี้ เราสร้าง ListView ที่มี ListTile หลายๆ อันเป็น children โดยแต่ละ ListTile จะมีไอคอนที่แตกต่างกันและข้อความหัวเรื่องที่ต่างกัน และเมื่อผู้ใช้แตะบน ListTile แต่ละอัน ก็จะเรียก callback function ที่กำหนดไว้ใน `onTap` (ในตัวอย่างนี้ ยังไม่ได้กำหนด callback function ไว้)

เมื่อ run โค้ดนี้ คุณจะเห็นหน้าจอที่มีรายการ ListTile หลายๆ อัน ซึ่งสามารถเลื่อนขึ้นลงเพื่อดูรายการทั้งหมดได้ และเมื่อแตะบน ListTile แต่ละอัน ก็จะสามารถตอบสนองต่อการกระทำนั้นได้ตามที่กำหนดใน callback function

ผลลัพธ์ที่ได้คือ:

![alt text](/assets/images/11/listtile.png)

ListTile เป็น Widget ที่มีประโยชน์มากในการสร้าง UI ที่เป็นรายการข้อมูล เนื่องจากช่วยให้สามารถจัดรูปแบบและแสดงข้อมูลได้อย่างเป็นระเบียบ อีกทั้งยังสามารถกำหนดการตอบสนองต่อการกระทำของผู้ใช้ได้อย่างง่ายดายอีกด้วย

## สร้าง Layout จาก Design

<img src="https://docs.flutter.dev/assets/images/docs/ui/layout/layout-demo-app.png" width="500">

### วาดแผนผังเค้าโครง

1. ลองออกแบบในความคิดว่าองค์ประกอบของ Layout หลักๆ คืออะไรบ้าง และจะวางอย่างไร

   <img src='https://docs.flutter.dev/assets/images/docs/ui/layout/layout-sketch-intro.svg' width='500'>

2. ในแต่ละ Row หรือ Column จะมีองค์ประกอบอะไรบ้าง

   ![alt text](/assets/images/11/inside-row-column.png)

### การเขียนโค้ด

1.  สร้าง project ใหม่ แล้วแทนที่ Code ใน `main.dart` ด้วยโค้ดด้านล่าง

    ```dart
    import 'package:flutter/material.dart';

    void main() => runApp(const MyApp());

    class MyApp extends StatelessWidget {
      const MyApp({super.key});

      @override
      Widget build(BuildContext context) {
        const String appTitle = 'Flutter layout demo';
        return MaterialApp(
          title: appTitle,
          home: Scaffold(
            appBar: AppBar(
              title: const Text(appTitle),
            ),
            body: const Center(
              child: Text('Hello World'),
            ),
          ),
        );
      }
    }
    ```

2.  สร้างไฟล์ `title_section.dart` ใน folder `lib/sections` เพิ่ม `TitleSection` widget ที่จะใช้ในการแสดงข้อมูลหัวเรื่อง

     <img src="https://docs.flutter.dev/assets/images/docs/ui/layout/layout-sketch-title-block-unlabeled.svg" width="500">

```dart
class TitleSection extends StatelessWidget {
    const TitleSection({
      super.key,
      required this.name,
      required this.location,
    });

    final String name;
    final String location;

    @override
    Widget build(BuildContext context) {
      return Padding(
        padding: const EdgeInsets.all(32),
        child: Row(
          children: [
            Expanded(
              /*1*/
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  /*2*/
                  Padding(
                    padding: const EdgeInsets.only(bottom: 8),
                    child: Text(
                      name,
                      style: const TextStyle(
                        fontWeight: FontWeight.bold,
                      ),
                    ),
                  ),
                  Text(
                    location,
                    style: TextStyle(
                      color: Colors.grey[500],
                    ),
                  ),
                ],
              ),
            ),
            /*3*/
            Icon(
              Icons.star,
              color: Colors.red[500],
            ),
            const Text('41'),
          ],
        ),
      );
    }
  }
```

3.เปลี่ยน `body` ใน `MyApp` ให้เป็น `SingleChildScrollView` และเพิ่ม `TitleSection` ลงไป

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    const String appTitle = 'Flutter layout demo';
    return MaterialApp(
      title: appTitle,
      home: Scaffold(
        appBar: AppBar(
          title: const Text(appTitle),
        ),
        body: SingleChildScrollView(
          child: Column(
            children: const [
              TitleSection(
                name: 'Oeschinen Lake Campground',
                location: 'Kandersteg, Switzerland',
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

4. สร้างไฟล์ `button_section.dart` ใน folder `lib/sections` เพิ่ม `ButtonSection` widget ที่จะใช้ในการแสดงปุ่ม

```dart
class ButtonSection extends StatelessWidget {
  const ButtonSection({super.key});

  @override
  Widget build(BuildContext context) {
    final Color color = Theme.of(context).primaryColor;
    return SizedBox(
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: [
          ButtonWithText(
            color: color,
            icon: Icons.call,
            label: 'CALL',
          ),
          ButtonWithText(
            color: color,
            icon: Icons.near_me,
            label: 'ROUTE',
          ),
          ButtonWithText(
            color: color,
            icon: Icons.share,
            label: 'SHARE',
          ),
        ],
      ),
    );
  }
}

class ButtonWithText extends StatelessWidget {
  const ButtonWithText({
    super.key,
    required this.color,
    required this.icon,
    required this.label,
  });

  final Color color;
  final IconData icon;
  final String label;

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Icon(icon, color: color),
        Padding(
          padding: const EdgeInsets.only(top: 8),
          child: Text(
            label,
            style: TextStyle(
              fontSize: 12,
              fontWeight: FontWeight.w400,
              color: color,
            ),
          ),
        ),
      ],
    )
  }
}
```

5. แก้ไข `body` ใน `MyApp` ให้เพิ่ม `ButtonSection` ลงไป

```dart
...
body: SingleChildScrollView(
  child: Column(
    children: const [
      TitleSection(
        name: 'Oeschinen Lake Campground',
        location: 'Kandersteg, Switzerland',
      ),
      ButtonSection(), // Add this line
  ),
),
...
```

6. สร้างไฟล์ `text_section.dart` ใน folder `lib/sections` เพิ่ม `TextSection` widget ที่จะใช้ในการแสดงข้อความ

```dart

class TextSection extends StatelessWidget {
  const TextSection({
    super.key,
    required this.description,
  });

  final String description;

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(32),
      child: Text(
        description,
        softWrap: true,
      ),
    );
  }
}
```

7. แก้ไข `body` ใน `MyApp` ให้เพิ่ม `TextSection` ลงไป

```dart
...
body: SingleChildScrollView(
  child: Column(
    children: const [
      TitleSection(
        name: 'Oeschinen Lake Campground',
        location: 'Kandersteg, Switzerland',
      ),
      ButtonSection(),
      TextSection(
        description: 'Lake Oeschinen lies at the foot of the Blüemlisalp in the Bernese '
            'Alps. Situated 1,578 meters above sea level, it is one of the larger Alpine '
            'lakes. A gondola ride from Kandersteg, followed by a half-hour walk through '
            'pastures and pine forest, leads you to the lake, which warms to 20 degrees '
            'Celsius in the summer. Activities enjoyed here include rowing, and riding '
            'the summer toboggan run.',
      ),
    ],
  ),
),
...
```

8. สร้างไฟล์ `image_section.dart` ใน folder `lib/sections` เพิ่ม `ImageSection` widget ที่จะใช้ในการแสดงรูปภาพ

```dart
class ImageSection extends StatelessWidget {
  const ImageSection({super.key});

  @override
  Widget build(BuildContext context) {
    return Image.asset(
      'assets/images/lake.jpg',
      width: 600,
      height: 240,
      fit: BoxFit.cover,
    );
  }
}
```

- สร้างโฟลเดอร์ `assets/images` และเพิ่มรูปภาพ `lake.jpg` ลงไป ดาวน์โหลดได้ [ที่นี่](https://raw.githubusercontent.com/flutter/website/main/examples/layout/lakes/step5/images/lake.jpg)

  <img src="https://raw.githubusercontent.com/flutter/website/main/examples/layout/lakes/step5/images/lake.jpg" width="500">

- แก้ไข `pubspec.yaml` เพิ่ม path ของรูปภาพ

  ```yaml
  flutter:
    assets:
      - assets/images/lake.jpg
  ```

9. ทำการ Run โค้ด และตรวจสอบผลลัพธ์
