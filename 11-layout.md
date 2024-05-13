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
