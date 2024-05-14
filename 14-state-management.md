# State Management

State Management คือกระบวนการจัดการ state หรือสถานะของข้อมูลใน app เพื่อให้ข้อมูลถูกต้องและอัปเดตพร้อมกันในทุกๆ ส่วนของ UI โดยทั่วไปการทำ State Management ที่ดีจะช่วยให้:

- ข้อมูลถูกแชร์และอัปเดตข้าม widget ได้อย่างมีประสิทธิภาพ
- โค้ดของ UI และตรรกะแยกออกจากกันชัดเจน ง่ายต่อการอ่านและดูแลรักษา
- ลดการเกิด bug ที่เกิดจากความไม่สอดคล้องของข้อมูลใน UI
- ทำให้ app มีขนาดเล็กลงเพราะไม่ต้อง rebuild widget ทั้งหมดเมื่อมีการเปลี่ยนแปลงข้อมูล

Flutter มี approach ในการทำ State Management หลายแบบ เช่น:

1. setState - เป็นวิธีพื้นฐานสุด เหมาะสำหรับ app ขนาดเล็กหรือกรณีที่ state ไม่ได้มีการเปลี่ยนแปลงบ่อย

2. Provider - เป็น state management ที่ออกแบบมาเพื่อแก้ปัญหาของ setState และใช้ InheritedWidget ในการส่งต่อ state ข้าม widget tree

3. Riverpod - พัฒนาต่อยอดมาจาก Provider โดยแก้ปัญหาเรื่อง boilerplate code และเพิ่ม feature อื่นๆ เช่น caching, asynchronous state

4. BLoC (Business Logic Component) - แนวคิดที่แยก business logic ออกจาก presentation layer อย่างชัดเจน state จะถูกควบคุมด้วย stream และ UI จะรับและตอบสนองต่อการเปลี่ยนแปลงของ state ผ่าน stream นั้น

5. MobX - ใช้ observer pattern ร่วมกับ reactive programming ทำให้สามารถสร้าง observable state และเมื่อ state มีการเปลี่ยนแปลง ทุก observer (widget) ที่ขึ้นกับ state นั้นจะถูกอัปเดตโดยอัตโนมัติ

6. Redux - นำแนวคิดจาก Redux ใน React มาปรับใช้กับ Flutter app state จะถูกเก็บใน store และการเปลี่ยนแปลง state ทำได้ผ่านการ dispatch action เท่านั้น

7. GetX - เป็น framework ที่รวม state management, route management และ dependency injection เข้าด้วยกัน มี API ที่ใช้งานง่ายทั้งสำหรับผู้เริ่มต้นและผู้เชี่ยวชาญ

แต่ละวิธีก็มีข้อดีข้อเสียแตกต่างกันไป เหมาะสมกับ app ที่มีขนาดและความซับซ้อนแตกต่างกัน ไม่มีวิธีไหนที่ดีที่สุดสำหรับทุกสถานการณ์ การเลือกใช้ state management ขึ้นอยู่กับปัจจัยหลายอย่าง เช่น ขนาดของ app, ทีมที่พัฒนา, ประสบการณ์ของนักพัฒนา, ข้อจำกัดด้านเวลาและทรัพยากร เป็นต้น

## ตัวอย่างการใช้งาน Provider ใน Flutter

ตัวอย่างการใช้งาน Provider package ใน Flutter app มีดังนี้

1. เพิ่ม provider ใน pubspec.yaml

```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.1.2
```

2. สร้าง model class สำหรับเก็บ state ที่ต้องการแชร์ เช่น `lib/models/counter_model.dart`

```dart
import 'package:flutter/foundation.dart';

class CounterModel extends ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}
```

3. Wrap widget ที่ต้องการให้เข้าถึง state ด้วย `ChangeNotifierProvider` ใน `lib/main.dart`

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'models/counter_model.dart';
import 'screens/home_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => CounterModel(),
      child: MaterialApp(
        title: 'Flutter Provider Demo',
        home: HomeScreen(),
      ),
    );
  }
}
```

4. ใช้ `Provider.of` เพื่อเข้าถึง state ใน widget ที่ต้องการ เช่น `lib/screens/home_screen.dart`

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../models/counter_model.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Flutter Provider Demo'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Consumer<CounterModel>(
              builder: (context, counter, child) => Text(
                '${counter.count}',
                style: Theme.of(context).textTheme.headline4,
              ),
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Provider.of<CounterModel>(context, listen: false).increment();
        },
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
}
```

จากตัวอย่าง เราสร้าง `CounterModel` เพื่อเก็บและจัดการ state ของการนับจำนวน มีการ expose `count` ผ่าน getter และมี method `increment` สำหรับเพิ่มค่า count และเรียก `notifyListeners()` เพื่อแจ้งให้ consumer รู้ว่า state มีการเปลี่ยนแปลง

ในไฟล์ `main.dart` เราครอบ `MaterialApp` ด้วย `ChangeNotifierProvider` พร้อมระบุ `CounterModel` เป็น state ที่ต้องการแชร์

ในไฟล์ `home_screen.dart` เราใช้ `Provider.of<CounterModel>(context)` เพื่อเข้าถึง `CounterModel` และอ่านค่า `count` มาแสดงผลใน `Text` widget และใช้ `Provider.of<CounterModel>(context, listen: false)` เพื่อเรียกใช้ method `increment` เมื่อมีการกดปุ่ม FloatingActionButton

โดยการใช้ `listen: false` จะทำให้ widget ไม่ rebuild เมื่อ state มีการเปลี่ยนแปลง ซึ่งเหมาะสำหรับกรณีที่ต้องการอ่าน state เพียงครั้งเดียวตอน build และไม่ต้องการให้ widget นั้น rebuild เมื่อ state เปลี่ยนแปลง

ส่วนการใช้ `Consumer` widget จะทำให้เราสามารถกำหนดได้ว่าเฉพาะส่วนไหนใน widget ที่ต้องการให้ rebuild เมื่อ state มีการเปลี่ยนแปลง ช่วยเพิ่มประสิทธิภาพโดยไม่ต้อง rebuild ทั้ง widget tree

นี่คือตัวอย่างพื้นฐานของการใช้ Provider ใน Flutter app โดยเราสามารถประยุกต์ใช้ในการแชร์ state ที่ซับซ้อนกว่านี้ รวมถึงใช้คู่กับ package อื่นๆ เช่น http เพื่อจัดการ state ที่ได้จาก API ได้ด้วย

### ตะกร้าสินค้าด้วย Provider

![Shopping Cart](/assets/images/practice/provider.gif)

มาสร้าง Flutter app สำหรับเลือกเครื่องเขียนใส่ตระกร้ากัน โดยจะใช้ Provider package ในการจัดการ state ของรายการสินค้าในตระกร้า

1. สร้างไฟล์ `lib/models/cart_model.dart` สำหรับเก็บ state ของรายการสินค้าในตระกร้า

```dart
import 'package:flutter/foundation.dart';

class CartItem {
  final String id;
  final String name;
  final double price;
  final int quantity;

  CartItem({
    required this.id,
    required this.name,
    required this.price,
    required this.quantity,
  });
}

class CartModel extends ChangeNotifier {
  final List<CartItem> _items = [];

  List<CartItem> get items => _items;

  int get itemCount => _items.length;

  double get totalPrice => _items.fold(0, (sum, item) => sum + item.price * item.quantity);

  void addItem(String productId, String name, double price, int quantity) {
    if (_items.any((item) => item.id == productId)) {
      _items.firstWhere((item) => item.id == productId).quantity += quantity;
    } else {
      _items.add(CartItem(
        id: productId,
        name: name,
        price: price,
        quantity: quantity,
      ));
    }
    notifyListeners();
  }

  void removeItem(String productId) {
    _items.removeWhere((item) => item.id == productId);
    notifyListeners();
  }

  void clear() {
    _items.clear();
    notifyListeners();
  }
}
```

2. สร้างไฟล์ `lib/models/product_model.dart` สำหรับเก็บข้อมูลของเครื่องเขียนแต่ละชนิด

```dart
class Product {
  final String id;
  final String name;
  final double price;

  Product({
    required this.id,
    required this.name,
    required this.price,
  });
}

final List<Product> products = [
  Product(id: '1', name: 'Pencil', price: 5.0),
  Product(id: '2', name: 'Pen', price: 10.0),
  Product(id: '3', name: 'Eraser', price: 3.0),
  Product(id: '4', name: 'Ruler', price: 7.0),
  Product(id: '5', name: 'Marker', price: 15.0),
];
```

3. สร้างไฟล์ `lib/main.dart` สำหรับ setup Provider และเรียกหน้า ProductListScreen

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'models/cart_model.dart';
import 'screens/product_list_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => CartModel(),
      child: MaterialApp(
        title: 'Shopping Cart Demo',
        home: ProductListScreen(),
      ),
    );
  }
}
```

4. สร้างไฟล์ `lib/screens/product_list_screen.dart` สำหรับแสดงรายการเครื่องเขียน

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../models/cart_model.dart';
import '../models/product_model.dart';
import 'cart_screen.dart';

class ProductListScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Stationery'),
        actions: [
          IconButton(
            icon: Icon(Icons.shopping_cart),
            onPressed: () {
              Navigator.push(
                context,
                MaterialPageRoute(builder: (context) => CartScreen()),
              );
            },
          ),
        ],
      ),
      body: ListView.builder(
        itemCount: products.length,
        itemBuilder: (context, index) {
          final product = products[index];
          return ListTile(
            title: Text(product.name),
            subtitle: Text('\$${product.price}'),
            trailing: IconButton(
              icon: Icon(Icons.add_shopping_cart),
              onPressed: () {
                Provider.of<CartModel>(context, listen: false).addItem(
                  product.id,
                  product.name,
                  product.price,
                  1,
                );
                ScaffoldMessenger.of(context).showSnackBar(
                  SnackBar(content: Text('Added to cart')),
                );
              },
            ),
          );
        },
      ),
    );
  }
}
```

5. สร้างไฟล์ `lib/screens/cart_screen.dart` สำหรับแสดงรายการสินค้าในตระกร้า

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../models/cart_model.dart';

class CartScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Shopping Cart'),
      ),
      body: Consumer<CartModel>(
        builder: (context, cart, child) {
          if (cart.itemCount == 0) {
            return Center(child: Text('Your cart is empty'));
          }
          return ListView.builder(
            itemCount: cart.itemCount,
            itemBuilder: (context, index) {
              final item = cart.items[index];
              return ListTile(
                title: Text(item.name),
                subtitle: Text('Quantity: ${item.quantity}'),
                trailing: Text('\$${item.price * item.quantity}'),
              );
            },
          );
        },
      ),
      bottomNavigationBar: Consumer<CartModel>(
        builder: (context, cart, child) {
          return Container(
            padding: EdgeInsets.all(16),
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                Text(
                  'Total: \$${cart.totalPrice.toStringAsFixed(2)}',
                  style: TextStyle(fontSize: 20),
                ),
                ElevatedButton(
                  onPressed: () {
                    ScaffoldMessenger.of(context).showSnackBar(
                      SnackBar(content: Text('Buying not supported yet.')),
                    );
                  },
                  child: Text('BUY'),
                ),
              ],
            ),
          );
        },
      ),
    );
  }
}
```

เท่านี้เราก็ได้ app ที่สามารถเลือกเครื่องเขียนจาก ProductListScreen ใส่ตระกร้า แล้วไปดูรายการสินค้าในตระกร้าที่ CartScreen ได้แล้ว โดยเราใช้ Provider ในการแชร์ state ของ CartModel ระหว่าง 2 screen นี้

โดยใน CartModel เรามี field `_items` สำหรับเก็บรายการสินค้าในตระกร้า มี method `addItem` สำหรับเพิ่มสินค้า `removeItem` สำหรับลบสินค้า และ `clear` สำหรับล้างตระกร้า รวมถึงมี getter สำหรับอ่านจำนวนและราคารวมของสินค้าด้วย

เวลาเพิ่มสินค้าลงตระกร้าจาก ProductListScreen เราก็เรียก `Provider.of<CartModel>(context, listen: false).addItem()` เพื่อเพิ่มสินค้าลงใน `_items` และใช้ `listen: false` เพื่อไม่ต้อง rebuild

ส่วนใน CartScreen เราใช้ Consumer เพื่อรับ `CartModel` มาแสดงผลจำนวนและราคารวมของสินค้าในตระกร้าได้แบบ real-time เมื่อมีการเปลี่ยนแปลง เช่น เพิ่มหรือลบสินค้า

สามารถดูตัวอย่างที่สมบูรณ์ได้จาก [https://github.com/silkyland/flutter_example_provider_example](https://github.com/silkyland/flutter_example_provider_example)
