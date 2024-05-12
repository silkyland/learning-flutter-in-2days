# Widget

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

จะเห็นว่า lifecycle ของ StatelessWidget นั้นไม่ซับซ้อน เพราะมีเพียงการ build widget ด้วย `build()` โดยไม่ต้องสนใจเรื่องการจัดการ state ภายใน ทำให้เหมาะสำหรับการสร้าง UI components ที่ไม่มีการเปลี่ยนแปลงใดๆ ในตัวเอง

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

### Lifecycle ของ StatefulWidget

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

### Widget Tree

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

## Widget พื้นฐานของ Flutter

Widget พื้นฐานของ Flutter ที่มักจะใช้งานในการพัฒนาแอปพลิเคชันมีดังนี้

## MaterailApp

![material-app.png](/assets/images/7/material-widget.png)

MaterialApp เป็น widget ระดับบนสุดที่ใช้ในการสร้าง application ด้วย Flutter โดยมีหน้าที่หลักในการตั้งค่าและกำหนดรูปแบบให้กับ app ตามแนวทางของ Material Design

คุณสมบัติสำคัญของ MaterialApp ได้แก่:

1. `title` - ชื่อของ app ที่แสดงบน task manager หรือ app switcher
2. `theme` - กำหนด theme ให้กับ app เช่น สี, font, shape ต่างๆ โดยใช้ ThemeData
3. `home` - กำหนดหน้า (screen) แรกที่แสดงเมื่อเปิด app
4. `routes` - กำหนด named routes สำหรับการนำทางไปยังหน้าต่างๆ ภายใน app
5. `initialRoute` - กำหนด route เริ่มต้นสำหรับการนำทาง ถ้าไม่ได้กำหนดจะใช้หน้าจาก `home`
6. `onGenerateRoute` - สร้าง route ในระหว่าง runtime ด้วย RouteSettings
7. `debugShowMaterialGrid`, `showSemanticsDebugger` - แสดงตาราง grid และข้อมูล semantics เพื่อช่วยในการออกแบบ layout
8. `locale`, `localizationsDelegates`, `supportedLocales` - ตั้งค่าที่เกี่ยวข้องกับ localization

ตัวอย่างโครงสร้างพื้นฐานของการใช้งาน MaterialApp:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My Flutter App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home Page'),
      ),
      body: Center(
        child: Text('Hello, World!'),
      ),
    );
  }
}
```

ในตัวอย่างด้านบน MaterialApp ถูกใช้เป็น root widget ที่ครอบ MyHomePage ซึ่งเป็นหน้าหลักของ app โดย MaterialApp จะจัดการเรื่อง theme, title และ home widget ให้

นอกจาก MaterialApp แล้ว Flutter ยังมี CupertinoApp ซึ่งเป็น widget สำหรับสร้าง app ตามแบบ iOS ที่มีโครงสร้างและคุณสมบัติคล้ายกับ MaterialApp

สรุปคือ MaterialApp เป็นจุดเริ่มต้นในการสร้าง app ด้วย Flutter ที่มี design ตามแนวทาง Material ช่วยจัดการเรื่องพื้นฐาน เช่น routing, theming, localization ให้ เราจึงสามารถโฟกัสไปที่การออกแบบ UI ที่น่าสนใจและใช้งานได้จริงได้อย่างเต็มที่

## CupertinoApp

![CupertinoApp](/assets/images/7/cupertino-widget.png)

CupertinoApp เป็น widget ของ Flutter ที่ใช้สร้าง application ตามแบบ iOS ซึ่งมีลักษณะคล้ายกับ MaterialApp ที่ใช้สำหรับสร้าง app แบบ Android โดย CupertinoApp จะมี widget และ component ต่างๆ ที่ออกแบบมาให้เข้ากับ design language ของ Apple

คุณสมบัติหลักของ CupertinoApp ได้แก่:

1. `home` - กำหนดหน้าแรกของ app
2. `theme` - กำหนด theme ของ app ด้วย CupertinoThemeData เช่น สี, font ต่างๆ
3. `routes` - กำหนด named routes สำหรับการนำทางระหว่างหน้า
4. `initialRoute` - กำหนด route เริ่มต้น ถ้าไม่ได้ระบุจะใช้หน้าจาก `home`
5. `onGenerateRoute` - สร้าง route ขณะ runtime โดยใช้ RouteSettings
6. `localizationsDelegates`, `supportedLocales`, `locale` - ตั้งค่าเกี่ยวกับ localization
7. `debugShowCheckedModeBanner` - ควบคุมการแสดง "debug" banner ที่มุมขวาบน

ตัวอย่างโครงสร้างพื้นฐานของ CupertinoApp:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      title: 'My Cupertino App',
      theme: CupertinoThemeData(
        primaryColor: CupertinoColors.activeBlue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Home Page'),
      ),
      child: Center(
        child: Text('Hello, World!'),
      ),
    );
  }
}
```

ในตัวอย่างข้างต้น เราใช้ CupertinoApp เป็น root widget และกำหนด theme ด้วย CupertinoThemeData โดยหน้าหลักจะเป็น MyHomePage ที่ใช้ CupertinoPageScaffold และ CupertinoNavigationBar เป็นองค์ประกอบหลัก ซึ่งจะให้ look and feel เหมือนกับ app บน iOS

การใช้ CupertinoApp ร่วมกับ widget อื่นๆ เช่น CupertinoTabScaffold, CupertinoTextField, CupertinoButton, CupertinoDatePicker จะช่วยให้เราสร้าง app ที่มีหน้าตาและ interaction ตามมาตรฐานของ iOS ได้อย่างสมบูรณ์แบบ

อย่างไรก็ตาม ในการพัฒนา app ด้วย Flutter เราสามารถใช้ widget จากทั้ง Material และ Cupertino ร่วมกันได้ เพื่อให้สามารถปรับแต่ง design ของ app ได้ตามความต้องการ และรองรับผู้ใช้งานบนแพลตฟอร์มที่หลากหลายมากขึ้น

## Scaffold

Scaffold เป็น widget หลักที่ใช้สร้าง layout ของหน้า (screen) ใน Flutter โดยมีโครงสร้างพื้นฐานประกอบด้วยส่วนต่างๆ ที่จำเป็น เช่น app bar, body, bottom navigation bar, floating action button, drawer ฯลฯ

ส่วนประกอบหลักของ Scaffold ได้แก่:

1. `appBar` - แถบด้านบนของหน้าจอ ใช้วาง title, action buttons, menu เป็นต้น
2. `body` - ส่วนเนื้อหาหลักของหน้า วาง widget ที่แสดงข้อมูลหรือ UI ต่างๆ
3. `bottomNavigationBar` - แถบด้านล่างสำหรับสร้างเมนูหรือปุ่มนำทาง
4. `floatingActionButton` - ปุ่มลอยที่มักอยู่มุมขวาล่าง ใช้สำหรับ action หลักของหน้านั้นๆ
5. `drawer` - ลิ้นชักด้านข้างที่เลื่อนออกมาจากทางซ้ายของหน้าจอ ใช้วางเมนูหรือตัวเลือกเพิ่มเติม
6. `backgroundColor`, `backgroundImage` - กำหนดสีหรือรูปภาพพื้นหลังให้กับ Scaffold
7. `bottomSheet`, `drawerScrimColor`, `persistentFooterButtons` ฯลฯ

ตัวอย่างการใช้งาน Scaffold เบื้องต้น:

```dart
Scaffold(
  appBar: AppBar(
    title: Text('My App'),
  ),
  body: Center(
    child: Text('Hello, World!'),
  ),
  floatingActionButton: FloatingActionButton(
    onPressed: () {},
    child: Icon(Icons.add),
  ),
  bottomNavigationBar: BottomNavigationBar(
    items: [
      BottomNavigationBarItem(
        icon: Icon(Icons.home),
        label: 'Home',
      ),
      BottomNavigationBarItem(
        icon: Icon(Icons.settings),
        label: 'Settings',
      ),
    ],
  ),
)
```

Scaffold มีประโยชน์ในการจัดวางโครงสร้างพื้นฐานของหน้า UI ตามรูปแบบของ Material Design ช่วยให้สร้าง app ที่มีหน้าตาสวยงาม เป็นมาตรฐาน และใช้งานง่าย โดยเราสามารถกำหนดส่วนประกอบต่างๆ ผ่าน properties ของ Scaffold ได้อย่างยืดหยุ่น

## AppBar

![AppBar](./assets/images/7/appbar.png)

AppBar เป็น widget ใน Flutter ที่ใช้แสดงแถบด้านบนของแอปพลิเคชัน (top app bar) ซึ่งมักจะประกอบด้วยชื่อหน้าจอ ไอคอน และตัวเลือกต่างๆ ที่เกี่ยวข้องกับหน้านั้นๆ AppBar มีหน้าที่หลักในการนำทาง ให้ข้อมูล และจัดการ action ต่างๆ ภายในแอป

คุณสมบัติสำคัญของ AppBar ได้แก่:

1. `title` - กำหนดข้อความหรือ widget ที่แสดงเป็นชื่อของ AppBar
2. `leading` - กำหนด widget ที่แสดงด้านซ้ายของ title เช่น ปุ่มย้อนกลับ
3. `actions` - กำหนด widget ที่แสดงด้านขวาของ title เช่น ปุ่ม menu, search, settings เป็นต้น
4. `bottom` - กำหนด widget ที่แสดงด้านล่างของ AppBar เช่น TabBar, SearchBar เป็นต้น
5. `backgroundColor` - กำหนดสีพื้นหลังของ AppBar
6. `elevation` - กำหนดระดับเงาของ AppBar
7. `iconTheme`, `actionsIconTheme`, `textTheme` - กำหนด theme ให้กับไอคอนและข้อความใน AppBar
8. `centerTitle` - กำหนดว่าต้องการให้ title อยู่ตรงกลางหรือไม่ (ค่าเริ่มต้นเป็น false)

ตัวอย่างการใช้งาน AppBar:

```dart
Scaffold(
  appBar: AppBar(
    title: Text('My App'),
    leading: IconButton(
      icon: Icon(Icons.menu),
      onPressed: () {
        // open drawer
      },
    ),
    actions: [
      IconButton(
        icon: Icon(Icons.search),
        onPressed: () {
          // perform search
        },
      ),
      IconButton(
        icon: Icon(Icons.settings),
        onPressed: () {
          // open settings
        },
      ),
    ],
    backgroundColor: Colors.blue,
    elevation: 4,
    centerTitle: true,
  ),
  body: Center(
    child: Text('Hello, World!'),
  ),
)
```

ในตัวอย่างด้านบน เราสร้าง AppBar ที่มีองค์ประกอบดังนี้:

- title แสดงข้อความ "My App"
- leading มีปุ่ม menu สำหรับเปิด drawer
- actions ประกอบด้วยปุ่ม search และ settings
- สีพื้นหลังเป็นสีน้ำเงิน
- มีเงาระดับ 4
- จัดชื่อ title ให้อยู่ตรงกลาง

AppBar เป็น widget ที่มีความยืดหยุ่นสูง สามารถปรับแต่งให้เข้ากับธีมและรูปแบบของแอปได้หลากหลาย ช่วยให้ UI ของแอปดูสวยงามและใช้งานได้อย่างมีประสิทธิภาพ ตอบโจทย์ความต้องการของผู้ใช้ได้เป็นอย่างดี

## Container

![Container](./assets/images/7/container.png)

Container เป็น widget อเนกประสงค์ที่ใช้ในการสร้างกล่องหรือภาชนะสำหรับบรรจุ widget อื่นๆ โดยมีความสามารถในการกำหนดขนาด, สี, ระยะขอบ, การจัดวาง และการตกแต่งต่างๆ ให้กับ child widget ที่อยู่ภายใน

คุณสมบัติหลักๆ ของ Container ได้แก่:

1. `child` - กำหนด widget ที่อยู่ภายใน Container (optional)
2. `alignment` - กำหนดการจัดวาง child widget ภายใน Container
3. `padding` - กำหนดระยะห่างระหว่าง child widget กับขอบของ Container
4. `color` - กำหนดสีพื้นหลังของ Container
5. `decoration` - กำหนดการตกแต่ง Container ด้วย BoxDecoration เช่น สี, รูปภาพ, border, gradient เป็นต้น
6. `foregroundDecoration` - กำหนด decoration ที่แสดงทับหน้า child widget
7. `width`, `height` - กำหนดขนาดความกว้างและความสูงของ Container
8. `constraints` - กำหนดขนาดขั้นต่ำและขั้นสูงของ Container ด้วย BoxConstraints
9. `margin` - กำหนดระยะห่างระหว่าง Container กับ widget ภายนอก
10. `transform` - ใช้ Matrix4 ในการแปลง Container เช่น scale, rotate, translate เป็นต้น

ตัวอย่างการใช้งาน Container:

```dart
Container(
  width: 200,
  height: 200,
  color: Colors.blue,
  padding: EdgeInsets.all(16),
  margin: EdgeInsets.all(8),
  alignment: Alignment.center,
  child: Text(
    'Hello, World!',
    style: TextStyle(
      color: Colors.white,
      fontSize: 24,
    ),
  ),
)
```

ในตัวอย่างด้านบน เราสร้าง Container ที่มีขนาด 200x200 พิกเซล มีสีพื้นหลังเป็นสีน้ำเงิน ภายในมี padding โดยรอบ 16 พิกเซล และมี margin ห่างจากขอบนอก 8 พิกเซล โดยจัดวางข้อความ "Hello, World!" ไว้ตรงกลางของ Container

การใช้ Container ร่วมกับคุณสมบัติ `decoration` ช่วยให้เราสามารถสร้างรูปร่างหรือ effect ที่น่าสนใจให้กับ widget ได้ เช่น การสร้าง card ที่มีเงา การสร้าง button ที่มีขอบโค้งมน หรือการสร้าง container ที่มีรูปภาพพื้นหลังแบบ gradient เป็นต้น

Container มีประโยชน์ในการจัดโครงสร้างและจัดวาง widget ต่างๆ บนหน้าจอ รวมถึงการสร้างเลเอาต์ที่มีความยืดหยุ่นและปรับแต่งได้ตามต้องการ ช่วยให้การพัฒนา UI ด้วย Flutter เป็นไปอย่างมีประสิทธิภาพและสวยงามมากยิ่งขึ้น

## SafeArea

SafeArea เป็น widget ใน Flutter ที่ใช้สำหรับกำหนดพื้นที่ปลอดภัย (safe area) ให้กับ child widget เพื่อหลีกเลี่ยงการถูกบดบังโดย system UI ต่างๆ เช่น status bar, notch, rounded corners ฯลฯ ซึ่งช่วยให้ content ของ app แสดงผลได้อย่างเต็มที่และไม่ถูกรบกวน

คุณสมบัติหลักๆ ของ SafeArea ได้แก่:

1. `child` - กำหนด child widget ที่อยู่ภายใน SafeArea
2. `top`, `bottom`, `left`, `right` - กำหนดว่าต้องการให้ SafeArea เว้นระยะห่างจากขอบด้านใด (ค่าเริ่มต้นเป็น true ทุกด้าน)
3. `minimum` - กำหนดระยะห่างขั้นต่ำระหว่าง child widget กับขอบของ safe area ในแต่ละด้าน
4. `maintainBottomViewPadding` - กำหนดว่าต้องการให้ SafeArea คงระยะห่างด้านล่างเพิ่มเติมสำหรับ bottom view (ค่าเริ่มต้นเป็น false)

ตัวอย่างการใช้งาน SafeArea:

```dart
SafeArea(
  child: Scaffold(
    appBar: AppBar(
      title: Text('My App'),
    ),
    body: Center(
      child: Text('Hello, World!'),
    ),
  ),
)
```

ในตัวอย่างข้างต้น เราใช้ SafeArea ครอบ Scaffold เพื่อให้ content ภายใน Scaffold ไม่ถูกบดบังโดย system UI โดย SafeArea จะเว้นระยะห่างจากขอบทุกด้านตามค่าเริ่มต้น

หากต้องการปรับแต่งระยะห่างของ SafeArea เราสามารถกำหนดค่าผ่าน `minimum` ได้ เช่น:

```dart
SafeArea(
  minimum: EdgeInsets.only(top: 32, left: 16, right: 16),
  child: Scaffold(...),
)
```

ในกรณีนี้ SafeArea จะเว้นระยะห่างด้านบน 32 พิกเซล และด้านซ้ายขวาอย่างละ 16 พิกเซล ในขณะที่ด้านล่างจะไม่เว้นระยะเพิ่มเติม

การใช้ SafeArea ช่วยให้ app ของเรามีความเข้ากันได้ดีกับอุปกรณ์ที่หลากหลาย โดยเฉพาะอุปกรณ์ที่มีรูปร่างหน้าจอแตกต่างจากมาตรฐาน เช่น มี notch มีความโค้งมนตามขอบจอ เป็นต้น ทำให้ UI ของ app ดูเป็นมืออาชีพและใช้งานได้อย่างเต็มประสิทธิภาพบนทุกอุปกรณ์
