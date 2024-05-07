# Flutter

## โครงสร้าง Folder ของ Flutter

หลังจากการสร้าง Project ของ Flutter ใหม่ Flutter จะทำการสร้างโครงสร้างไฟล์เหล่านี้ให้เราอย่างอัตโนมัติ:

```
flutter_app/
├── android/
├── ios/
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
├── test/
├── assets/
│   ├── images/
│   └── fonts/
├── pubspec.yaml
└── README.md
```

1. `android/` และ `ios/`: โฟลเดอร์สำหรับไฟล์เฉพาะของ Android และ iOS เมื่อต้องการสร้าง native code หรือกำหนดค่าเฉพาะแพลตฟอร์ม
2. `lib/`: โฟลเดอร์หลักที่เก็บโค้ด Dart ทั้งหมดสำหรับแอป Flutter
   - `main.dart`: จุดเริ่มต้นของแอปพลิเคชัน กำหนด Root Widget และเรียกหน้าจอหลัก
   - `screens/`: เก็บไฟล์ต่างๆ ที่แสดง UI ของแต่ละหน้าจอในแอป เช่น HomeScreen, DetailScreen
   - `widgets/`: เก็บวิดเจ็ตที่ใช้ซ้ำในแอป เช่น ปุ่ม, ข้อความ เพื่อให้ใช้งานได้สะดวกมากขึ้น
   - `models/`: เก็บคลาสโมเดลต่างๆ ที่ใช้ในแอป เช่น User model
   - `services/`: เก็บไฟล์ที่เกี่ยวข้องกับเซอร์วิส เช่น การเรียก API
   - `utils/`: เก็บไฟล์ helpers หรือ constants ที่ใช้ทั่วแอป
3. `test/`: โฟลเดอร์สำหรับเขียน unit tests, widget tests และ integration tests
4. `assets/`: โฟลเดอร์เก็บไฟล์แอสเซท เช่น รูปภาพ, ไอคอน, ฟอนต์ ที่ใช้ในแอป
5. `pubspec.yaml`: ไฟล์กำหนดการตั้งค่าของโปรเจ็กต์ Flutter เช่น ชื่อ, เวอร์ชัน, ไลบรารี่ที่ใช้, assets ต่างๆ เช่น fonts, images เป็นต้น
6. `README.md`: ไฟล์สำหรับใส่คำอธิบายหรือเอกสารประกอบโปรเจ็กต์

## Widget

_"Everything is Widget"_ - ใน Flutter เกือบทุกอย่างเป็น Widget ที่นำมาประกอบกันเป็นส่วนให้แสดงผลบนหน้าจอ เช่น โครงสร้าง, ปุ่ม, ข้อความ, รูปภาพ, ไอคอน และอื่นๆ Widget เป็นส่วนประกอบพื้นฐานในการสร้าง UI ของแอป Flutter

**ประเภทของ Widget**

1. Stateless Widget: เป็น widget ที่ไม่มีการเปลี่ยนแปลงสถานะภายใน (immutable) เหมาะสำหรับการแสดงผลคงที่ ไม่ขึ้นกับข้อมูลที่เปลี่ยนแปลง
2. Stateful Widget: เป็น widget ที่มีการเปลี่ยนแปลงสถานะภายใน (mutable) เหมาะสำหรับการแสดงผลที่ขึ้นกับข้อมูลที่เปลี่ยนแปลงไป เช่น ข้อมูลจากผู้ใช้หรือ API

### Stateless Widget

**StatelessWidget** คือ Widget ที่ไม่มีการจัดการ state ภายใน (immutable state) นั่นคือ properties และลักษณะที่แสดงผลของ widget จะถูกกำหนดตั้งแต่ตอนสร้าง และจะคงที่ไม่เปลี่ยนแปลงตลอดช่วงเวลาที่ widget ถูกแสดงผลบนหน้าจอ

StatelessWidget เหมาะสำหรับ UI components ที่ไม่ซับซ้อน ไม่มีการเปลี่ยนแปลงข้อมูลหรือ state จากภายใน เช่น:

- ข้อความ, ไอคอน, รูปภาพ ที่แสดงแบบคงที่
- ปุ่มที่มี label และ icon คงที่
- การจัดวาง (layout) widgets แบบคงที่ เช่น Row, Column, Container
- Custom widgets ที่ combine widgets พื้นฐานต่างๆ เป็น component แบบคงที่

ข้อดีของ StatelessWidget คือมีโครงสร้างที่เรียบง่าย เขียนโค้ดน้อย และมีประสิทธิภาพในการ render สูง เพราะไม่ต้องมีการจัดการ state ภายใน ทำให้เหมาะกับ UI ส่วนที่ไม่ซับซ้อนและแสดงผลคงที่

ในการสร้าง StatelessWidget เราจะสร้าง class ที่ extends จาก `StatelessWidget` และ implement เมธอด `build()` ซึ่งทำหน้าที่คืนค่า widget ที่ต้องการให้แสดงผล โดย widget ที่คืนมักจะเป็นการ combine widgets พื้นฐานต่างๆ ผ่านการจัดวางใน layout widgets เช่น Row, Column, Stack เป็นต้น

ตัวอย่างโค้ดการสร้าง StatelessWidget:

```dart
class MyCard extends StatelessWidget {
  final String title;
  final String subtitle;

  const MyCard({required this.title, required this.subtitle});

  @override
  Widget build(BuildContext context) {
    return Card(
      child: Padding(
        padding: EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(title, style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold)),
            SizedBox(height: 8),
            Text(subtitle, style: TextStyle(fontSize: 18)),
          ],
        ),
      ),
    );
  }
}
```

ในตัวอย่างนี้ เราสร้าง MyCard widget ที่แสดงข้อความ title และ subtitle ภายใน Card โดยจัดวางด้วย Column และกำหนดลักษณะตัวอักษรผ่าน TextStyle

การใช้งาน MyCard widget สามารถทำได้โดย:

```dart
MyCard(
  title: 'Flutter is awesome',
  subtitle: 'A powerful and flexible UI framework',
)
```

ซึ่ง MyCard จะแสดงผลเป็น Card ที่ประกอบด้วยข้อความและจัดรูปแบบตามที่กำหนดใน `build()` method โดยไม่มีการเปลี่ยนแปลง state ภายในตัว widget เอง

### Lifecycle ของ StatelessWidget

Lifecycle ของ StatelessWidget นั้นค่อนข้างเรียบง่าย เนื่องจากมันไม่มีการจัดการ state ภายใน ดังนั้นจึงไม่จำเป็นต้องมีเมธอดพิเศษต่างๆ ที่เกี่ยวข้องกับการจัดการ state

Lifecycle หลักๆ ของ StatelessWidget ประกอบด้วย:

1. **Constructor**
   - เมื่อสร้าง instance ของ StatelessWidget constructor จะถูกเรียกเพื่อกำหนดค่า properties ต่างๆ ให้กับ widget
   - ใน constructor เราสามารถรับ parameter ที่จำเป็นสำหรับการสร้าง widget ได้ เช่น ข้อความ สี ขนาด ฯลฯ
2. **build()**
   - หลังจากสร้าง instance แล้ว Flutter framework จะเรียกเมธอด `build()` เพื่อสร้าง widget tree ตาม logic ที่เขียนไว้
   - ภายใน `build()` เราจะกำหนด widget ย่อยๆ ที่ประกอบกันเป็น widget หลัก โดยอาจมีการกำหนดค่าต่างๆ ผ่าน properties ของ sub-widgets เหล่านั้น
   - เมธอด `build()` จะถูกเรียกซ้ำเมื่อ parent widget มีการเปลี่ยนแปลงและต้องการ rebuild child widgets ใหม่
3. **Destroyed**
   - เมื่อ StatelessWidget ถูกลบออกจาก widget tree หรือถูกแทนที่ด้วย widget อื่น instance ของมันจะถูกกำจัดออกจากหน่วยความจำโดยอัตโนมัติ
   - ไม่จำเป็นต้องมีการเคลียร์หรือจัดการ resource ใดๆ เพิ่มเติม เนื่องจาก StatelessWidget ไม่มีการจัดการ state ใดๆ ด้วยตัวเอง

ตัวอย่างโค้ดแสดง lifecycle ของ StatelessWidget อย่างง่าย:

```dart
class MyWidget extends StatelessWidget {
  final String text;

  MyWidget({required this.text}) {
    print('Constructor called');
  }

  @override
  Widget build(BuildContext context) {
    print('Build called');
    return Text(text);
  }
}
```

เมื่อใช้งาน `MyWidget` ในโค้ด จะมีการพิมพ์ข้อความตาม lifecycle ดังนี้:

```
Constructor called
Build called
```

โดย constructor จะถูกเรียกตอนสร้าง instance ของ `MyWidget` และ `build()` จะถูกเรียกตามมาเพื่อสร้าง widget ย่อยตามที่กำหนดไว้

จะเห็นว่า lifecycle ของ StatelessWidget นั้นไม่ซับซ้อน เพราะมีเพียงการ build widget ด้วย `build()` โดยไม่ต้องสนใจเรื่องการจัดการ state ภายใน ทำให้เหมาะสำหรับการสร้าง UI components ที่ไม่มีการเปลี่ยนแปลงใดๆ ในตัวเองครับ

### StatefulWidget

**StatefulWidget** คือ Widget ที่มีการจัดการ state ภายใน (mutable state) ซึ่ง state นี้สามารถเปลี่ยนแปลงค่าได้ตลอดช่วงเวลาที่ widget ถูกแสดงผลบนหน้าจอ เมื่อ state มีการเปลี่ยนแปลง Flutter framework จะทำการ rebuild widget ใหม่โดยอัตโนมัติเพื่ออัปเดตหน้าตาให้สอดคล้องกับ state ล่าสุด

StatefulWidget เหมาะสำหรับ UI ที่มีการเปลี่ยนแปลง state ไม่ว่าจากการโต้ตอบของผู้ใช้ (user interaction) หรือจากการทำงานภายใน เช่น:

- ฟอร์มที่มี input fields ต่างๆ ที่ผู้ใช้สามารถแก้ไขข้อมูลได้
- ปุ่มที่เปลี่ยนสถานะ เช่น ปุ่มที่กดแล้วเปลี่ยนข้อความจาก "Follow" เป็น "Unfollow"
- วิดเจ็ตที่แสดงข้อมูลแบบเรียลไทม์ เช่น นาฬิกา หรือ live feed
- วิดเจ็ตที่มีการเล่นแอนิเมชันต่างๆ

ในการสร้าง StatefulWidget จะแบ่งเป็น 2 ส่วนหลักๆ คือ:

1. Class ที่ extends StatefulWidget ซึ่งเป็นส่วนของ widget ที่ immutable
2. Class ที่ extends State ซึ่งเป็นส่วนของ state ที่ mutable

ใน State class จะประกอบด้วย:

- ตัวแปรต่างๆ ที่เป็น state ของ widget
- เมธอด `initState()` ที่ใช้ตอนสร้าง State ครั้งแรก เช่น กำหนดค่าเริ่มต้นให้กับตัวแปร
- เมธอด `build()` ที่คืนค่า widget ตาม state ปัจจุบัน (เหมือนใน StatelessWidget)
- เมธอด `setState()` ที่ใช้เมื่อต้องการเปลี่ยนแปลง state และสั่งให้ Flutter rebuild widget

ตัวอย่างโค้ดการสร้าง StatefulWidget:

```dart
class Counter extends StatefulWidget {
  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _count = 0;

  void _incrementCount() {
    setState(() {
      _count++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text('Count: $_count'),
        ElevatedButton(
          onPressed: _incrementCount,
          child: Text('Increment'),
        ),
      ],
    );
  }
}
```

ในตัวอย่างนี้ เราสร้าง Counter widget ที่แสดงค่า count ปัจจุบัน และมีปุ่ม Increment เพื่อเพิ่มค่า count

- ใน `_CounterState` เรามีตัวแปร `_count` เป็น state ส่วน `_incrementCount()` คือฟังก์ชันที่เรียกเมื่อกดปุ่ม ซึ่งจะใช้ `setState()` ในการเพิ่มค่า `_count` และสั่ง rebuild widget
- ใน `build()` จะคืนค่าเป็น Column ที่มี Text แสดงค่า count และปุ่ม Increment ที่เรียก `_incrementCount` เมื่อถูกกด

การใช้งาน Counter widget สามารถทำได้โดย:

```dart
Counter()
```

ซึ่ง Counter จะแสดงเป็นข้อความ "Count: 0" และปุ่ม Increment ที่สามารถกดเพื่อเพิ่มค่า count ได้ โดยทุกครั้งที่กดปุ่ม widget จะถูกสร้างใหม่และอัปเดตข้อความให้แสดงค่า count ล่าสุด

### Lifecycle ของ StatelessWidget

![flutter stateful lifecycle](/assets/images/lifecycle.png)

**Lifecycle ของ StatefulWidget** ประกอบด้วยเหตุการณ์และเมธอดต่างๆ ที่ถูกเรียกโดย Flutter framework ตั้งแต่การสร้าง widget จนถึงการทำลายทิ้ง ซึ่งเราสามารถ override เมธอดเหล่านี้เพื่อเพิ่ม logic การทำงานในช่วงเวลาต่างๆ ได้

1. **createState()**
   - เมื่อสร้าง instance ของ StatefulWidget เมธอด `createState()` จะถูกเรียกเพื่อสร้าง instance ของ State object ที่เชื่อมโยงกับ widget นั้น
   - ใน `createState()` เราต้อง return instance ของ State class ที่เราสร้างขึ้นมา
2. **initState()**
   - หลังจากสร้าง State object แล้ว เมธอด `initState()` จะถูกเรียกเพียงครั้งเดียวเพื่อเริ่มต้นค่า state ต่างๆ ของ widget
   - เราสามารถใช้ `initState()` ในการกำหนดค่าเริ่มต้นให้กับตัวแปร เรียก API เพื่อดึงข้อมูล หรือเริ่มต้น listener ต่างๆ ได้
   - ต้องเรียก `super.initState()` ก่อนเสมอเมื่อ override `initState()`
3. **didChangeDependencies()**
   - หลังจาก `initState()` ทำงานเสร็จ เมธอด `didChangeDependencies()` จะถูกเรียกทันที
   - เมธอดนี้จะถูกเรียกซ้ำเมื่อมีการเปลี่ยนแปลง dependencies ของ widget เช่น เมื่อ InheritedWidget มีการเปลี่ยนแปลง
   - เราสามารถใช้ `didChangeDependencies()` ในการอัปเดตค่า state ที่ขึ้นกับ dependencies ได้
4. **build()**
   - เมื่อ State object พร้อมใช้งานแล้ว Flutter framework จะเรียกเมธอด `build()` เพื่อสร้าง widget tree ตาม state ปัจจุบัน
   - `build()` จะถูกเรียกซ้ำเมื่อมีการเปลี่ยนแปลง state ผ่านเมธอด `setState()` หรือเมื่อต้องมีการ rebuild widget ใหม่
5. **didUpdateWidget()**
   - เมื่อ StatefulWidget มีการเปลี่ยนแปลง configuration (เช่น properties ของมัน) `didUpdateWidget()` จะถูกเรียกที่ State object เดิม
   - เราสามารถเปรียบเทียบ widget เก่ากับใหม่ และอัปเดต state ตามการเปลี่ยนแปลงได้ใน `didUpdateWidget()`
6. **setState()**
   - เมื่อต้องการเปลี่ยนแปลง state ภายใน StatefulWidget ให้เรียกเมธอด `setState()` พร้อมด้วย callback ที่อัปเดตค่า state
   - หลังจาก `setState()` ทำงานเสร็จ Flutter framework จะเรียก `build()` อีกครั้งเพื่ออัปเดต UI ให้สอดคล้องกับ state ใหม่
7. **deactivate()**
   - เมื่อ State object ถูกลบออกจาก widget tree ชั่วคราว (เช่นเมื่อมีการเปลี่ยนหน้า) `deactivate()` จะถูกเรียก
   - เราสามารถใช้ `deactivate()` เพื่อจัดการ resources หรือยกเลิก listeners ที่ไม่จำเป็นชั่วคราวได้
8. **dispose()**
   - ก่อนที่ State object จะถูกลบออกจากหน่วยความจำอย่างถาวร (เช่นเมื่อปิดหน้าจอ) `dispose()` จะถูกเรียก
   - เราต้องใช้ `dispose()` ในการเคลียร์ resources ต่างๆ เช่นปิด streams ยกเลิก timers หรือ listeners เพื่อป้องกัน memory leaks
   - ต้องเรียก `super.dispose()` เสมอเมื่อ override `dispose()`

ตัวอย่างโค้ดเบื้องต้นของ StatefulWidget lifecycle:

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  int _counter = 0;

  @override
  void initState() {
    super.initState();
    print('initState() called');
  }

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    print('didChangeDependencies() called');
  }

  @override
  void didUpdateWidget(covariant MyWidget oldWidget) {
    super.didUpdateWidget(oldWidget);
    print('didUpdateWidget() called');
  }

  @override
  void deactivate() {
    super.deactivate();
    print('deactivate() called');
  }

  @override
  void dispose() {
    super.dispose();
    print('dispose() called');
  }

  void _incrementCounter() {
    setState(() {
      _counter++;
      print('setState() called');
    });
  }

  @override
  Widget build(BuildContext context) {
    print('build() called');
    return Column(
      children: [
        Text('Count: $_counter'),
        ElevatedButton(
          onPressed: _incrementCounter,
          child: Text('Increment'),
        ),
      ],
    );
  }
}
```

เมื่อเราใช้ widget `MyWidget` ในแอป Flutter ผลลัพธ์ของ lifecycle methods ที่ถูกเรียกและลำดับของมันจะเป็นดังนี้:

1. เมื่อสร้าง `MyWidget` ครั้งแรก:

   ```
   initState() called
   didChangeDependencies() called
   build() called
   ```

2. เมื่อกดปุ่ม "Increment":

   ```
   setState() called
   build() called
   ```

3. เมื่อมีการอัปเดต parent widget ที่ครอบ `MyWidget` อยู่ (เช่นเมื่อ rebuild จาก `setState()` ของ parent):

   ```
   didUpdateWidget() called
   build() called
   ```

4. เมื่อ `MyWidget` ถูกลบออกจาก widget tree ชั่วคราว (เช่นเมื่อเปลี่ยนไปแสดง route อื่น):

   ```
   deactivate() called
   ```

5. เมื่อกลับมาแสดง `MyWidget` อีกครั้งหลังจาก deactivate:

   ```
   build() called
   ```

6. เมื่อลบ `MyWidget` ออกจาก widget tree อย่างถาวร (เช่นเมื่อปิดหน้าจอหรือ pop route ออก):
   ```
   deactivate() called
   dispose() called
   ```

โดยสังเกตว่า:

- `initState()`, `didChangeDependencies()` และ `dispose()` จะถูกเรียกเพียงครั้งเดียวตลอด lifecycle ของ widget
- `didUpdateWidget()` จะถูกเรียกเมื่อมีการเปลี่ยนแปลงบาง properties ของ widget จาก parent (เช่นเมื่อ parent rebuild)
- `build()` จะถูกเรียกหลังจากเมธอดต่างๆ ที่เกี่ยวข้องกับการเปลี่ยนแปลง state หรือ configuration ของ widget เพื่ออัปเดต UI ให้สอดคล้องกับ state ล่าสุด
- `deactivate()` อาจถูกเรียกหลายครั้งหากมีการซ่อนและแสดง widget บ่อยๆ แต่ `dispose()` จะเรียกเพียงครั้งเดียวตอนลบ widget ทิ้งเท่านั้น

อย่างไรก็ตาม ผลลัพธ์ที่แท้จริงอาจแตกต่างกันไปบ้างขึ้นอยู่กับว่า `MyWidget` ถูกใช้งานร่วมกับ widget อื่นๆ อย่างไร และมีการจัดการ state ของแอปเป็นอย่างไร แต่ลำดับพื้นฐานของ lifecycle ก็จะเป็นไปตามที่กล่าวไว้ข้างต้น

**Widget Tree**

Widget Tree คือการนำ Widget มาซ้อนกันเป็นแบบแผนผังต้นไม้ โดย widget ที่บรรจุ widget อื่น ๆ เรียกว่า "parent widget" และ widget ที่อยู่ใน widget อื่น ๆ เรียกว่า "child widget"

ตัวอย่างโครงสร้าง Widget Tree เบื้องต้น:

```
MaterialApp
  ├── Scaffold
  │   ├── AppBar
  │   └── Center
  │       └── Text
  └── FloatingActionButton
```

ในตัวอย่างนี้ `MaterialApp` เป็น root widget ที่ครอบ `Scaffold` ซึ่งเป็น parent widget ของ `AppBar`, `Center` และ `FloatingActionButton` ส่วน `Text` เป็น child widget ของ `Center`

การสร้าง Widget Tree ที่มีประสิทธิภาพ ควรแบ่งเป็น widget ย่อยๆ ตามหน้าที่และความรับผิดชอบ ไม่ควรรวมโค้ดไว้ที่ widget เดียวจนเกินไป เพื่อให้อ่านเข้าใจง่ายและสามารถนำ widget ไปใช้ซ้ำได้

**Widget พื้นฐานของ Flutter**

Widget พื้นฐานของ Flutter ที่มักจะใช้งานในการพัฒนาแอปพลิเคชันมีดังนี้

- **Text**: ใช้สำหรับแสดงผลข้อความ โดยสามารถกำหนดรูปแบบ เช่น สี ขนาด ฟอนต์ การจัดวาง ฯลฯ ได้ผ่าน `TextStyle`

- **Row** และ **Column**: เป็น Widget ที่ใช้จัดวาง children widgets ในแนวนอน (Row) หรือแนวตั้ง (Column) คล้ายกับ Flexbox ใน CSS โดยสามารถกำหนดการจัดวาง ระยะห่าง ขนาด ของ children ได้ เช่น `MainAxisAlignment` และ `CrossAxisAlignment`

- **Stack**: ใช้สำหรับวาง children widgets ซ้อนทับกันเป็นลำดับชั้น (layer) คล้ายกับ `position: absolute` ใน CSS โดยสามารถระบุตำแหน่งของ children ได้ด้วย `Positioned` widget

- **Container**: เป็น widget ที่ใช้สร้างกล่องสี่เหลี่ยมที่มีพื้นหลัง สีขอบ ระยะขอบ (padding) รัศมีขอบโค้ง (border radius) เงา ฯลฯ ได้ คล้ายกับ `div` ใน HTML นอกจากนี้ยังสามารถกำหนด constraint ขนาดให้ child widget ได้ด้วย

- **ListView**: ใช้แสดงรายการ (list) ของ widgets แบบเลื่อนได้ (scrollable) ในแนวตั้งหรือแนวนอน เหมาะสำหรับแสดงข้อมูลที่มีจำนวนมากหรือไม่แน่นอน สามารถใช้ `ListView.builder()` เพื่อสร้าง list อย่างมีประสิทธิภาพ

- **GridView**: ใช้แสดง widgets ในรูปแบบตาราง (grid) แบบเลื่อนได้ โดยสามารถกำหนดจำนวนคอลัมน์หรือความกว้างของแต่ละช่องได้ผ่าน `GridView.count()` หรือ `GridView.extent()`

- **Expanded**: เป็น widget ที่ใช้ขยายขนาดของ child widget ให้เต็มพื้นที่ว่างใน Row, Column หรือ Flex โดยสามารถกำหนดสัดส่วนการขยายได้ด้วย `flex` factor ช่วยให้จัดวาง widgets ได้ยืดหยุ่นขึ้น

- **Padding** และ **Margin**: ใช้เพิ่มระยะห่างภายใน (padding) หรือภายนอก (margin) ให้กับ widget โดย Padding เป็น widget ที่ครอบ child widget ส่วน Margin สามารถใช้ผ่าน `Container` หรือ `Padding`

- **IconButton** และ **ElevatedButton**: เป็น widget ปุ่มที่มีไอคอนหรือข้อความ ใช้สำหรับรับ user input ผ่านการกด (tap) โดย `IconButton` เน้นแสดงไอคอนเป็นหลัก ส่วน `ElevatedButton` มีลักษณะเป็นปุ่มยกสูง มีข้อความและสามารถกำหนดสีพื้นหลังและเอฟเฟกต์การกดได้

- **Image**: ใช้แสดงรูปภาพจาก asset, network หรือ file โดยสามารถกำหนดขนาด ตำแหน่ง สเกล ฯลฯ ได้ รวมถึงการแสดงรูปแบบเลื่อนได้ (scrollable) ด้วย `Image.network()`, `FadeInImage()` หรืออื่นๆ

- **GestureDetector**: เป็น widget ที่ใช้จับ gesture การสัมผัสของผู้ใช้ เช่น การแตะ (tap), การลาก (drag), การเลื่อน (swipe) ฯลฯ โดยสามารถครอบ widget อื่นๆ และกำหนด callback เมื่อเกิด gesture นั้นๆ

- **Form** และ **TextFormField**: ใช้สร้างฟอร์มสำหรับรับข้อมูลจากผู้ใช้ โดย Form เป็น widget ที่ครอบฟิลด์ต่างๆ เช่น `TextFormField` สำหรับรับข้อมูลข้อความ ซึ่งมีฟีเจอร์ตรวจสอบความถูกต้อง (validation) ของข้อมูลด้วย

นอกจากนี้ Flutter ยังมี widgets อื่นๆ อีกมากมาย เช่น `BottomNavigationBar`, `Drawer`, `Tab`, `DataTable`, `Chart` ฯลฯ ซึ่งสามารถนำมาประกอบกันเพื่อสร้าง UI ของแอปพลิเคชันได้หลากหลายรูปแบบตามต้องการ
